# OpenClaw Ecosystem Digest 2026-06-25

> Issues: 439 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-25 02:54 UTC

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

# OpenClaw Project Digest — 2026-06-25

---

## 1. Today's Overview

OpenClaw is sustaining an extremely high development velocity. Over the past 24 hours, **439 issues** and **500 pull requests** were updated, with **66 PRs merged or closed** and **2 new releases** published. The project continues to push major infrastructure work (ACP runtime, session lifecycle hardening) alongside rapid channel-specific fixes (Line, Telegram, IRC, MSTeams). The sheer volume of incoming activity — **375 open issues** and **434 open PRs** — indicates a deeply engaged community but also suggests the maintainer team is stretched thin on triage and product decisions. Data reliability and channel parity remain the dominant thematic concerns across today's activity.

---

## 2. Releases

Two releases were published, reflecting ongoing channel operations and reliability improvements:

- **v2026.6.11-beta.1**:
  - **Slack relay mode** for automated channel operations.
  - **Native Mattermost `/oc_queue`** command support.
  - **Per-DM model overrides**, allowing fine-grained control over model routing per conversation.

- **v2026.6.10**:
  - **Automatic fast mode for talks**: short conversational turns automatically trigger fast mode, with bounded fallback for longer runs.
  - **Zai model synthesis routing** made more reliable for the Zai provider path.

Both releases are relatively lightweight and oriented toward channel reliability and operational control rather than breaking changes or major migration notes. Users on previous beta tracks should review the Slack relay and DM override config options.

---

## 3. Project Progress

**66 PRs were merged or closed today**, a strong indicator of active maintenance and feature advancement. Notable merged/closed PRs:

- **#96616** (Closed/Merged): `fix(line): forward FileMessage fileName to media store for audio MIME detection` — solves the audio-detection half of #96163 for LINE file uploads.

**Active high-impact PRs** (representing significant feature or stability work):

| PR | Theme | Status |
|---|---|---|
| [#77127](https://github.com/openclaw/openclaw/pull/77127) | `write` tool **append mode** — directly addresses critical data-loss bug #40001 | Ready for maintainer review |
| [#48940](https://github.com/openclaw/openclaw/pull/48940) | **ACP gateway-owned node-backed runtime** — durable state separation for restart resilience | Needs proof (long-running PR) |
| [#95996](https://github.com/openclaw/openclaw/pull/95996) | Parent session lifecycle fix — keeps yielded parent runs deferred until subagents settle | Needs proof |
| [#95899](https://github.com/openclaw/openclaw/pull/95899) | AI recovery from non-resumable assistant tails — represents core agent stability work | Open, needs proof |
| [#44143](https://github.com/openclaw/openclaw/pull/44143) | Serialize outbound deliveries per channel+recipient — addresses Telegram reply ordering | Waiting on author |
| [#95317](https://github.com/openclaw/openclaw/pull/95317) | Fix #93041 — Codex usage/limit UI regression in Control UI | Ready for maintainer review |
| [#96636](https://github.com/openclaw/openclaw/pull/96636) | Fuzzy edit fix — preserves unrelated lines during `edit` tool text matching | P0, needs proof |

A strong wave of **channel-specific fixes** also landed for Telegram, QQBot, IRC (UTF-16 boundary chunking), and MSTeams (mention escape tags).

---

## 4. Community Hot Topics

The most active discussions this period highlight several core community needs:

### 🏆 [Issue #75](https://github.com/openclaw/openclaw/issues/75): Linux/Windows Clawdbot Apps
**109 comments, 80 👍** | Open since Jan 1, 2026
The single most engaged issue in the project. The community is deeply requesting desktop apps for Linux and Windows. Currently marked as P2 and `needs-product-decision`.

### 🏆 [Issue #88838](https://github.com/openclaw/openclaw/issues/88838): Core session/transcript SQLite migration via accessor seam
**36 comments** | Maintainer-pinned, P1
This is the core infrastructure tracker for moving session storage to a file-backed accessor pattern. Represents critical work for data reliability.

### 🏆 [Issue #12602](https://github.com/openclaw/openclaw/issues/12602): Slack Block Kit support
**13 comments** | P2, created Feb 9
Strong demand for richer, interactive Slack responses (CRM summaries, action confirm, database results). Frequently requested by community.

### 🏆 [Issue #20786](https://github.com/openclaw/openclaw/issues/20786): Telegram Business Bot support
**8 comments, 6 👍** | P2, created Feb 19
Users are asking for Telegram Business-connected personal chat message support (`business_message` / `business_connection` updates).

### 🏆 [Issue #35203](https://github.com/openclaw/openclaw/issues/35203): Multi-Agent Collaboration Enhancement RFC
**8 comments** | Created March 5
A structured RFC for capability profiling, shared blackboard, layered memory, and token cost governance. Represents the community's push toward enterprise-grade multi-agent orchestration.

**Underlying needs driving these threads:**
- **Platform parity** (#75) — macOS/iOS/Android app users asking why desktop Windows/Linux are missing.
- **Core reliability** (#88838) — users are keenly aware of migration and data safety infrastructure.
- **Richer channel integrations** (#12602, #20786) — Slack and Telegram are primary workspaces; users want them fully featured.
- **Multi-agent governance** (#35203) — power users scaling beyond single-agent setups are hitting token and coordination limits.

---

## 5. Bugs & Stability

Today's bug reports and updates are densely packed with **data-loss, crash-loop, and regression** issues.

### 🔴 Critical (P1, Data Loss / Crash Loop)

| Issue | Summary | Impact |
|---|---|---|
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | **Signal daemon `stop()` race condition** on SIGUSR1 restart — orphaned processes, HTTP port contention, send failures | Crash loop, message loss |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) | **Write tool lacks append mode** — isolated cron sessions overwrite shared files | **Silent data loss** (fix PR #77127 open) |
| [#95495](https://github.com/openclaw/openclaw/issues/95495) | **Memory store relocation without migration** in 2026.6.9 — forced full re-embed of 1499 files | **Data loss**, upgrade regression |
| [#94228](https://github.com/openclaw/openclaw/issues/94228) | **Anthropic `thinking` blocks brick long tool-use threads** — invalid signature 400 error on all follow-ups | Session permanently broken |
| [#87109](https://github.com/openclaw/openclaw/issues/87109) | **Gateway heap growth to 1073MB+ at idle** on macOS — silent cron failures under memory pressure | Crash loop, silent failures |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) | **Active Memory + Codex** path causes long latency, hook timeouts, startup aborts, event-loop stalls | Crash loop, message loss |
| [#95833](https://github.com/openclaw/openclaw/issues/95833) | **Subagent `.jsonl.lock` not released** on abort-settle timeout — permanently breaks session | Message loss |

### 🟠 High (P1, Security / Session State / Message Loss)

| Issue | Summary | Impact |
|---|---|---|
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | `exec` tool does **not inherit `skills.entries.*.env`** environment variables | Security (secret injection broken), regression |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) | **Steer mode does not inject messages mid-turn** for main sessions | Message loss, behavioral regression |
| [#31331](https://github.com/openclaw/openclaw/issues/31331) | **Docker + Sandbox `workspaceAccess`** broken — internal vs host path mismatch | Security, session state |
| [#85030](https://github.com/openclaw/openclaw/issues/85030) | **MCP tools not injected into subagent (`sessions_spawn`) sessions** — config ignored | Session state, security |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | **Bootstrap files in `agentDir` silently ignored** — only workspace directory files loaded | Session state |

### 🟡 Regressions / Moderate (P1/P2)

| Issue | Summary |
|---|---|
| [#32473](https://github.com/openclaw/openclaw/issues/32473) | Control UI requires HTTPS/localhost secure context — blocks VPS deployments |
| [#38439](https://github.com/openclaw/openclaw/issues/38439) | Webchat avatar endpoint `/avatar/{agentId}` returns 404 regression |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | Google Vertex `Cannot convert undefined or null to object` crash |
| [#37966](https://github.com/openclaw/openclaw/issues/37966) | `cacheRetention` silently ignored for LiteLLM-proxied Anthropic models |

**Severity Rank:** The crash-loop/data-loss cluster (#22676, #40001, #95495, #94228, #87109) represents the most acute user-facing risk. The progress on #77127 (append mode fix for #40001) is especially critical and likely to be fast-tracked. The memory store relocation issue (#95495) highlights a gap in migration testing for storage paths.

---

## 6. Feature Requests & Roadmap Signals

User demand is concentrated on four pillars:

### Multi-Agent & Governance
- **[#35203](https://github.com/openclaw/openclaw/issues/35203)**: Multi-Agent Collaboration RFC — capability profiling, blackboard, token governance
- **[#22358](https://github.com/openclaw/openclaw/issues/22358)**: Post-subagent completion extension hook for structured trajectory generation
- **[#27445](https://github.com/openclaw/openclaw/issues/27445)**: Sub-agent announce routing — route completion to parent as user trigger for orchestration
- **[#38626](https://github.com/openclaw/openclaw/issues/38626)**: Subagent lifecycle observability + async supervision controls

### Channel Evolution
- **[#12602](https://github.com/openclaw/openclaw/issues/12602)**: Slack Block Kit support for rich messages
- **[#20786](https://github.com/openclaw/openclaw/issues/20786)**: Telegram Business Bot support
- **[#33413](https://github.com/openclaw/openclaw/issues/33413)**: Slack tool-level progress in assistant thread status
- **[#17840](https://github.com/openclaw/openclaw/issues/17840)**: Opt-in reaction-triggered agent turns

### Security & Control
- **[#12678](https://github.com/openclaw/openclaw/issues/12678)**: Capability-based permissions for skills/tools (default-deny)
- **[#39979](https://github.com/openclaw/openclaw/issues/39979)**: Path-scoped RWX permissions for exec and file tools
- **[#33975](https://github.com/openclaw/openclaw/issues/33975)**: Fallback approval mode + model attribution in messages
- **[#7722](https://github.com/openclaw/openclaw/issues/7722)**: Filesystem sandboxing config (`tools.fileAccess`)

### Infrastructure & DevOps
- **[#13616](https://github.com/openclaw/openclaw/issues/13616)**: Backup/restore utility for config, cron, session history
- **[#86881](https://github.com/openclaw/openclaw/issues/86881)**: Gateway-lite mode without AI harness for deterministic deployments
- **[#16670](https://github.com/openclaw/openclaw/issues/16670)**: Mandatory memory/embedding setup step in onboarding wizard
- **[#22438](https://github.com/openclaw/openclaw/issues/22438)**: Tiered bootstrap file loading for progressive context control

**Likeliest Roadmap Items for Next Release:**
- **`write` tool append mode** (#77127 / #40001): This fixes a clear P1 data-loss bug and has active PR momentum. Strong candidate for v2026.6.12+.
- **Tiered bootstrap loading** (#22438): Repeatedly requested for context window optimization; has linked PRs and strong conceptual alignment with token-conscious power users.
- **Subagent lifecycle hooks and observability** (#22358, #38626): The multi-agent orchestration use case is driving a lot of design energy, and these are foundational enablers.

---

## 7. User Feedback Summary

### Pain Points
- **Data loss dominates sentiment**: The memory relocation without migration (#95495) and the `write` tool overwrite behavior (#40001) are the most severe user-facing issues. Users are experiencing silent data loss on upgrade and on multi-session file writes.
- **Environment variable handling**: The `exec` tool not inheriting skill-scoped environment variables (#31583) is a P1 regression that breaks secret injection workflows, a high-friction enterprise use case.
- **Docker ecosystem friction**: Sandbox workspace access (#31331) and Docker-based deployments hitting HTTPS requirements (#32473) are common support themes.
- **Platform parity**: The Linux/Windows desktop request (#75) has gone unanswered for nearly 6 months despite being the most upvoted issue.
- **Silent failures**: The memory-leak-induced cron task failures (#87109) and group-chat sessions stuck in `failed` state (#86827) erode user trust in background operations.

### Satisfaction Signals
- **Active development pace**: Users see 66+ PRs merged daily and two releases in quick succession, which drives confidence.
- **Responsive channel fixes**: Telegram, LINE, IRC, and MSTeans specific bugs are being addressed promptly with focused PRs.
- **Cutting-edge adoption**: Features like A2A `sessions_send`, ACP runtime, Steer mode, and Active Memory are actively being tested and reported on by a sophisticated user base, indicating strong technical engagement.

### Key Use Cases Driving Feedback
- Enterprise deployment automation (env vars, file append, cron reliability)
- Multi-session and multi-agent production workflows (subagent hooks, lifecycle observability)
- Channel-operations teams (Slack Block Kit, Mattermost `/oc_queue`, Telegram Business)
- Power users with large workspaces (tiered bootstrap, memory compaction model overrides)

---

## 8. Backlog Watch

Several **high-profile or high-upside items** remain unaddressed or stuck in maintainer review/product decision limbo:

| Issue | Created | Last Update | Why It Matters | Stuck On |
|---|---|---|---|---|
| [#75](https://github.com/openclaw/openclaw/issues/75) Linux/Windows Desktop Apps | Jan 1 | Jun 25 | 109 comments, 80 👍 — highest community demand issue. | `needs-product-decision` |
| [#12602](https://github.com/openclaw/openclaw/issues/12602) Slack Block Kit | Feb 9 | Jun 24 | Rich Slack interaction is a top-requested integration feature. | `needs-product-decision` |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) Denylist for exec-approvals | Feb 1 | Jun 24 | Complements allowlist; highly requested for security config flexibility. 7 👍 | `needs-maintainer-review`, `needs-security-review` |
| [#13616](https://github.com/openclaw/openclaw/issues/13616) Backup/Restore Utility | Feb 10 | Jun 24 | Standard disaster recovery tooling missing from quite advanced platform. | `needs-security-review` |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) Tiered Bootstrap Loading | Feb 21 | Jun 25 | Solves token waste; strong alignment with power user workflows. | `needs-maintainer-review`, `needs-product-decision` |
| [#35203](https://github.com/openclaw/openclaw/issues/35203) Multi-Agent Collaboration RFC | Mar 5 | Jun 25 | Structured proposal for multi-agent scale-up. | `needs-maintainer-review`, `needs-product-decision` |
| [#86881](https://github.com/openclaw/openclaw/issues/86881) Gateway-lite Mode | May 26 | Jun 24 | Enables serverless/deterministic deployments — strategic pivot potential. | `needs-maintainer-review`, `needs-product-decision` |
| [#16670](https://github.com/openclaw/openclaw/issues/16670) Onboarding + Memory Setup | Feb 15 | Jun 25 | New users missing memory config; basic UX flow priority. | `needs-maintainer-review`, `needs-product-decision` |

**Observation**: There is a clear pattern of high-value items accumulating the label `clawsweeper:needs-product-decision`. With 375 open issues, the project's quality-of-life features and strategic roadmapping appear bottlenecked by decision bandwidth rather than implementation capacity. Community frustration on #75 (unchanged status for 6 months) reflects this tension.

---

## Summary

OpenClaw on 2026-06-25 is a project of **extraordinary community energy and code velocity**, balanced against a **significant triage and decision-making bottleneck**. While the maintainer team is deploying fixes and features at an impressive clip — particularly around channel compatibility and storage infrastructure — the community's most defining requests (desktop apps, Slack Block Kit, formalized multi-agent governance) remain in product-decision limbo. The immediate health signal is positive: data-loss bugs are being actively addressed (#77127), and 66 merged PRs demonstrate ongoing delivery. The medium-term risk is the growing gap between community demand and maintainer capacity for strategic direction-setting.

---
*Data reflects activity aggregated from github.com/openclaw/openclaw for the 24-hour period ending 2026-06-25.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Analysis Date: 2026-06-25**

---

## 1. Ecosystem Overview

The open-source AI agent ecosystem on June 25, 2026, is experiencing a high-velocity "feature war" increasingly undercut by a universal struggle for production reliability and security hardening. A clear city-state model has emerged: OpenClaw operates as the crowded capital with massive breadth but strategic governance bottlenecks, while ZeroClaw and IronClaw build fortified enterprise citadels around WASM and Rust-based infrastructure. The dominant community signals—cost anxiety, data loss fears, and demands for operational control—reveal an ecosystem maturing past the novelty phase into the reliability and trust phase. Projects that prioritize standardization, token efficiency, and security isolation over raw feature accretion are capturing the highest long-term engagement.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Releases | Health Signal |
|---|---|---|---|---|
| **OpenClaw** | 439 (375 open) | 500 (434 open) | 2 (beta, stable) | High velocity, severe triage bottleneck |
| **ZeroClaw** | 47 | 50 | 0 | Intense, productionizing, deep security RFCs |
| **IronClaw** | 19 | 45 (27 open) | 0 | Crisis recovery post-meltdown, active dogfooding |
| **LobsterAI** | 1 | 41 **merged** | 0 | Excellent consolidation sprint |
| **Hermes Agent** | 50 (37 open) | 50 (40 open) | 0 | Cost friction driving major refactoring |
| **NanoBot** | 11 | 41 (29 open) | 0 | Identity crisis vs capacity, regressions |
| **CoPaw (QwenPaw)** | 25 | 50 (43 open) | 0 | Post-2.0 migration stress testing |
| **NanoClaw** | Moderate | 18 | 0 | Security rising, critical CVE merged |
| **PicoClaw** | Moderate | 8 | 0 | Security audit cycle concluded |
| **TinyClaw** | 0 | 1 closed | 0 | Stable plateau, clean backlog |
| **NullClaw / Moltis / ZeptoClaw** | 0 | 0 | 0 | Dormant |

---

## 3. OpenClaw's Position

OpenClaw functions as the **ecosystem's reference implementation** and operates at a scale unmatched by any peer (439 issues vs. next highest 50). Its core advantages include the broadest channel integration matrix (Slack, Mattermost, Telegram, LINE, IRC, MSTeams), the deepest API protocol layer (ACP runtime, A2A `sessions_send`, Active Memory), and the largest contributor base.

**Key differentiators against peers:**
- **ZeroClaw** is explicitly rebuilding foundational choices (deprecating Extism plugins for WASM-first) while OpenClaw must manage backward compatibility at massive scale.
- **IronClaw** is rewriting core infrastructure in Rust; OpenClaw maintains the largest JS/TS agent framework.
- **LobsterAI** merged 41 PRs in a single consolidation sprint; OpenClaw merges 66 daily but maintains 434 open PRs, highlighting a decision ceiling.
- **TinyClaw/NanoBot** optimize for minimalism; OpenClaw optimizes for breadth.

**Primary competitive vulnerability:** Strategic decision paralysis. High-community-value items (desktop apps #75, multi-agent RFC #35203, Slack Block Kit #12602) remain blocked on `needs-product-decision` while P1 fixes ship daily. The community is willing to contribute, but the maintainer team lacks bandwidth for architectural direction-setting.

---

## 4. Shared Technical Focus Areas

**1. Session & Data Integrity (Universal, Highest Priority)**
Every active project is addressing data loss or corruption:
- **OpenClaw**: Write tool append mode (#77127), memory relocation without migration (#95495)
- **NanoClaw**: stale outbound.db journals (#2750), path traversal CVE (#2799)
- **Hermes Agent**: Hindsight data loss (#36216), credential pool corruption (#19566)
- **ZeroClaw**: MCP orphan accumulation (#5903), translation data leak (#8312)
- **CoPaw**: MiniMax media caching bug stripping images (#5505)

**2. Multi-Agent Delegation & Policy Enforcement**
- **ZeroClaw**: Per-sender RBAC (#5982), delegate tool policy intersection (#8285), MCP scoping bypass (#7733)
- **IronClaw**: Tool approval flow entirely broken post-dogfooding (#5192, #5196, #5197)
- **OpenClaw**: Subagent lifecycle hooks (#22358, #38626), parent session lifecycle fix (#95996)
- **Hermes Agent**: Generalized ACP client for orchestrating external agents (#5257)

**3. Token & Cost Optimization**
- **Hermes Agent**: Lazy tool schema loading (#6839), 73% fixed overhead per call (#4379)
- **OpenClaw**: Tiered bootstrap loading (#22438)
- **IronClaw**: Progressive tool disclosure to reduce prompt size (#5149)
- **NanoBot**: Dream cursor prompt bloat (#4481)

**4. Provider Abstraction Instability**
Rapid LLM provider proliferation (OpenAI, Anthropic, GLM, MiniMax, Kimi, OMLX, VolcEngine, OpenRouter) is breaking fragile adapters across all projects. Custom provider function calling is broken in **CoPaw** (#5345), thinking modes fail in **NanoBot** (#4429), and OpenRouter model fallback is missing in **ZeroClaw** (#8138).

**5. Platform Parity & Desktop UX**
- **OpenClaw**: Linux/Windows desktop apps requested for 6 months (#75)
- **CoPaw**: Tauri auto-updater stalled (#4669), Windows 500 errors (#5379)
- **Hermes Agent**: Windows UTF-8 encoding truncation (#52244)
- **TinyClaw**: Windows CLI fix merged today (PR #281)

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | IronClaw | CoPaw | LobsterAI | TinyClaw / NanoBot |
|---|---|---|---|---|---|---|
| **Target User** | Generalist / Channel Ops | Enterprise / Multi-Tenant | Hosted Enterprise | Power Developer (CN/Global) | Cost-Sensitive Enterprise | Mobile / Edge / Hobbyist |
| **Tech Stack** | JS/TS, Feature Matrix | Rust, WASM, OCI Registries | Rust, NEAR AI Hosted | Python, AgentScope | Python, Model Breadth | Minimalist / Golang |
| **Security Model** | env-based, exec controls | RBAC, OIDC, Supply Chain Signing | Tool Approval Gates | Provider Auth | Secret Injection | Container Sandbox |
| **Architecture Risk** | Decision bottleneck | MCP lifecycle complexity | Meltdown recovery | 2.0 migration regressions | Scheduling stagnation | Limited community / Identity |
| **Community Scale** | Very Large (439 issues) | Large (47 issues) | Large (19 issues) | Large (25 issues) | Medium (1 issue, 41 PRs) | Small (0-11 issues) |

**Notable architectural divergence:**
- **ZeroClaw** is the only project investing heavily in WASM component-model plugins and supply chain signing, positioning for regulated deployments.
- **IronClaw** and **PicoClaw** are the only projects with dedicated Rust/Security hardening sprints.
- **LobsterAI** demonstrated the highest **merge throughput** (41 PRs), indicating strong centralized maintainer capacity.
- **NanoBot** and **CoPaw** are most vulnerable to migration frictions (Telegram Web regression, AgentScope 2.0).

---

## 6. Community Momentum & Maturity

**Tier 1: High Velocity / Governance Bottlenecked**
- **OpenClaw**: 66 PRs merged daily but 434 open. Community enthusiasm outpacing maintainer triage capacity.
- **ZeroClaw**: Deep architectural RFCs (WASM, OIDC, supply chain signing) moving fast but require senior maintainer sign-off.
- **CoPaw**: Massive PR/incoming bug volume from 2.0 beta stress test.

**Tier 2: Aggressive Sprint / Consolidation**
- **LobsterAI**: 41 PRs merged in a single day. Highest merge rate in the ecosystem. Consolidating toward a major release.
- **IronClaw**: Recovery mode post-meltdown. 3 mitigation PRs opened in one day. Dogfooding generating high-quality bug reports.
- **NanoBot**: Pushing Codex feature suite despite regressions. Fix PRs submitted within hours of bug reports.

**Tier 3: Security / Foundation Hardening**
- **PicoClaw**: 12 security advisories closed in coordinated batch. Ready for patch release.
- **NanoClaw**: Critical CVE merged. Backlog of security fixes accumulating.

**Tier 4: Stable / Plateau**
- **TinyClaw**: Clean backlog, one cross-platform fix merged. Waiting for next development cycle.

**Tier 5: Inactive**
- **NullClaw, Moltis, ZeptoClaw**: No activity signals either project dormancy or development occurring outside the monitored repository.

---

## 7. Trend Signals for Developers & Technical Decision-Makers

**1. The "Cost Wall" is the Ecosystem's Bottleneck**
The most compelling technical debate is token optimization. With 73% of API overhead being fixed per Hermes' analysis, any project that solves dynamic context costing and lazy tool loading will capture the cost-sensitive power user segment. **Bet on projects that measure and publish token efficiency metrics.**

**2. Security Isolation is the Enterprise Moat**
Open-source projects failing to implement basic IAM (RBAC, audit trails, delegated credential management) are being actively frozen out of regulated environments. ZeroClaw's WASM sandboxing shift and supply chain signing signal the industry direction. **If your use case touches production data, demand multi-tenant security on day one.**

**3. Channel Parity is Unresolved**
Every project is custom-patching distinct channel ecosystems. The lack of standardized channel middleware creates fragmentation and repeated regression risk. **A unified channel abstraction layer (e.g., ACP) remains the single highest-value missing infrastructure component.**

**4. Multi-Agent is a Governance Problem, not an AI Problem**
The bottleneck isn't model intelligence but parent-child policy propagation, token budget governance, and observability of agent swarms. **Invest in operational tooling for agent coordination, not just model capability.**

**5. "Ship Fast, Break Users" is Losing Trust**
NanoBot's Telegram Web regression and CoPaw's 2.0 migration breakages demonstrate community punishment for unstable features. **Surgical stabilization sprints earn more long-term trust than rapid feature expansion.**

**6. Desktop Parity is a Decisive Unmet Need**
OpenClaw's Issue #75 (80 upvotes, 109 comments, 6 months open) is the ecosystem's highest-profile unmet demand. **Any project that solves first-class Windows/Linux desktop experiences with reliable offline capability will capture a wave of frustrated users.**

**7. The Plugin Standardization Race is Open**
ZeroClaw is going WASM, Hermes wants pip, OpenClaw lacks a formal SDK. **Developers should prefer open protocols over platform lock-in, but should prepare for a consolidation around WASM-based sandboxed plugins within 12 months.**

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for June 25, 2026, based on the provided GitHub activity data.

---

## NanoBot Project Digest – 2026-06-25

### 1. Today’s Overview

NanoBot exhibited extremely high development velocity on June 25, with **41 pull requests** and **11 issues** updated in the last 24 hours. Despite this high throughput, no new release was cut; the project remains focused on stabilizing core features and pushing forward the "Codex" initiative for advanced agent orchestration. The team successfully merged or closed **12 PRs** and resolved **3 bugs/issues**, though a significant volume of work remains open (29 PRs, 8 active issues). Community engagement is robust, but a major regression in Telegram Web support and growing friction around the project’s "ultra-lightweight" identity claim are the dominant signals in the ecosystem.

### 2. Releases

**None.** No new versions were tagged or released on June 25. The current track (v0.2.2) is undergoing heavy patch and feature development, suggesting a larger batch release (likely v0.3.0) is being assembled.

### 3. Project Progress

The following items were closed or merged today (based on top activity data):

- **Bug Fixes Closed:**
  - [#4465](https://github.com/HKUDS/nanobot/issues/4465): WebUI `<thinking>` tag rendering leak fixed.
  - [#4499](https://github.com/HKUDS/nanobot/issues/4499): Telegram channel sending empty messages resolved.
  - [#4413](https://github.com/HKUDS/nanobot/issues/4413): Telegram Bot API 10.1 rich messages tracking issue closed (feature delivered).
- **PRs Closed:**
  - [#4505](https://github.com/HKUDS/nanobot/pull/4505): Duplicate fix closed in favor of [#4489](https://github.com/HKUDS/nanobot/pull/4489) (Telegram Web compat).
  - [#4498](https://github.com/HKUDS/nanobot/pull/4498): Invalid upstream sync PR rejected.

Several high-value "Codex" PRs received substantial updates, signaling active review progress:
- [#4424](https://github.com/HKUDS/nanobot/pull/4424): Memory provenance gating for fact archives.
- [#4415](https://github.com/HKUDS/nanobot/pull/4415): Subagent spawn model overrides.
- [#4416](https://github.com/HKUDS/nanobot/pull/4416): Cron job model presets.
- [#4437](https://github.com/HKUDS/nanobot/pull/4437): Heartbeat trigger command.

### 4. Community Hot Topics

The most active discussions revolve around a core identity conflict and a painful feature regression:

- **Identity Crisis ([Issue #660](https://github.com/HKUDS/nanobot/issues/660)):** The highest-reaction and highest-comment thread. Users are challenging the project’s "ultra-lightweight" descriptor due to the obligatory Node.js dependency. This 4-month-old debate is a persistent pivot point for community trust.
- **Telegram Web Regression ([Issue #4488](https://github.com/HKUDS/nanobot/issues/4488), [#4499](https://github.com/HKUDS/nanobot/issues/4499)):** The introduction of Bot API 10.1 "rich messages" broke Telegram Web clients entirely, showing "This message is not supported." This spawned an immediate flood of fixes. The underlying need is clear: **core channel stability must not be sacrificed for new features.**
- **DingTalk Stability ([Issue #4497](https://github.com/HKUDS/nanobot/issues/4497)):** Users are reporting HTTP timeouts and dropped rich text formatting, with a fix PR already submitted. Rapid turnaround on this issue shows a responsive team.

### 5. Bugs & Stability

**Critical**
- **Telegram Web / Rich Messages ([#4488](https://github.com/HKUDS/nanobot/issues/4488), [#4499](https://github.com/HKUDS/nanobot/issues/4499)):** Full rendering failure for web clients. **Fix PRs in active review** ([#4489](https://github.com/HKUDS/nanobot/pull/4489)).
- **MCP Gateway Crash ([PR #4441](https://github.com/HKUDS/nanobot/pull/4441)):** `RuntimeError` on cancel scope exit during server reconnection causes gateway to crash. Fix under review.
- **WebUI Navigation & Streaming Failure ([Issue #4500](https://github.com/HKUDS/nanobot/issues/4500)):** Three distinct regressions: send button on home screen fails, stop button is broken, and streaming locks up on agent restart. Core UX is currently unreliable.

**High**
- **DingTalk Timeout & Data Loss ([Issue #4497](https://github.com/HKUDS/nanobot/issues/4497)):** ConnectTimeout and dropped rich text. **Fix PR in review** ([#4501](https://github.com/HKUDS/nanobot/pull/4501)).
- **MCP Security Leak ([PR #4436](https://github.com/HKUDS/nanobot/pull/4436), [#4452](https://github.com/HKUDS/nanobot/pull/4452)):** `enabledTools` allowlist was not enforced on resources or prompts, creating a supply-chain security bypass.
- **Dream Cursor Prompt Bloat ([PR #4481](https://github.com/HKUDS/nanobot/pull/4481)):** Disabling the Dream feature does not advance the cursor, leading to ever-growing context windows over time.

**Medium**
- **Custom Provider Thinking Mode ([Issue #4429](https://github.com/HKUDS/nanobot/issues/4429), [PR #4482](https://github.com/HKUDS/nanobot/pull/4482)):** VolcEngine/Doubao users cannot enable reasoning. Fix in review.
- **WebUI Voice Transcription Broken ([Issue #4492](https://github.com/HKUDS/nanobot/issues/4492)):** Browser WebM/Opus format is incompatible with Xiaomi MiMo ASR. No fix PR yet.

### 6. Feature Requests & Roadmap Signals

The data strongly implies the next major release is being assembled around the **"Codex"** suite and **infrastructure hardening**:

- **Codex (Advanced Orchestration):**
  - Memory provenance gating ([#4424](https://github.com/HKUDS/nanobot/pull/4424)).
  - Subagent model overrides ([#4415](https://github.com/HKUDS/nanobot/pull/4415)).
  - Cron job model presets ([#4416](https://github.com/HKUDS/nanobot/pull/4416)).
  - Heartbeat trigger commands ([#4437](https://github.com/HKUDS/nanobot/pull/4437)).
- **Channel Expansion:**
  - **Mattermost integration** ([PR #4459](https://github.com/HKUDS/nanobot/pull/4459)): Full WebSocket + REST API support.
  - **Gateway Webhooks** ([PR #4502](https://github.com/HKUDS/nanobot/pull/4502)): Inbound webhook triggers.
  - **PWA & Mobile UX** ([Issue #4479](https://github.com/HKUDS/nanobot/issues/4479)): Service worker, manifest, swipe gestures.
- **Security Hardening:**
  - OpenAI-compat API auth guardrail for wildcard hosts ([Issue #4490](https://github.com/HKUDS/nanobot/issues/4490)).
  - MCP idle timeout auto-kill to prevent zombie processes ([PR #4506](https://github.com/HKUDS/nanobot/pull/4506)).
- **Quality of Life:**
  - Skills subdirectory support ([PR #4504](https://github.com/HKUDS/nanobot/pull/4504)).
  - Search history memory tool ([PR #4439](https://github.com/HKUDS/nanobot/pull/4439)).

### 7. User Feedback Summary

- **Pain Points:**
  - "New features break my workflow." Telegram Web and DingTalk users are feeling instability from the latest feature pushes.
  - "The lightweight promise is broken." The Node.js dependency in the Docker image continues to erode trust in the project’s branding.
  - "MCP servers are leaky and crash-prone." Users are hitting resource exhaustion and hard gateway crashes.
  - "WebUI feels unfinished." Navigation, streaming controls, and mobile support are frustrating power users on the primary interface.
- **Drivers of Satisfaction:**
  - **High contributor velocity:** 41 PRs in 24 hours signals a healthy developer community.
  - **Rapid bug-fix cycles:** Issues like the DingTalk timeout and Telegram Web regressions saw fix PRs within hours.
  - **Strong roadmap alignment:** The "Codex" features are exactly what advanced users want for autonomous operation.

### 8. Backlog Watch

Several critical items have stalled or lack maintainer traction:

- **[Issue #660](https://github.com/HKUDS/nanobot/issues/660) (Ultra-lightweight debate):** **115 days open** with no official architectural response. This is becoming a persistent trust issue that needs a public roadmap statement.
- **[Issue #4490](https://github.com/HKUDS/nanobot/issues/4490) (API Auth Guard):** **Zero comments** from maintainers despite being flagged as a critical security gap for production deployments.
- **[Issue #4492](https://github.com/HKUDS/nanobot/issues/4492) (WebM/WAV Audio):** Root cause clearly identified, but no fix PR has been published. Blocks voice users on a major ASR provider.
- **[Issue #4500](https://github.com/HKUDS/nanobot/issues/4500) (WebUI UX Breakdown):** Filed by a frequent contributor with clear reproduction steps. High severity, needs immediate triage and assignment.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-25

---

## 1. Today's Overview

Project activity remains exceptionally high with **50 issues** and **50 pull requests** updated in the past 24 hours. The development focus is split between critical stability fixes (gateway stalls, credential pool corruption, desktop encoding bugs) and a massive community-driven codebase refactoring campaign removing unnecessary f-string overhead. No new releases were cut today, but 10 PRs were merged or closed, suggesting the project is consolidating toward a stable release candidate. Overall project health is strong, though the volume of open issues (37 active) and open PRs (40) indicates the core team faces meaningful triage pressure.

---

## 2. Releases

**No releases published on 2026-06-25.**

---

## 3. Project Progress (Merged/Closed PRs)

Ten pull requests were resolved today, marking concrete progress:

- **Gateway Reliability:** PR [#52263](https://github.com/NousResearch/hermes-agent/pull/52263) fixes a Discord relay bug where Direct Message replies were silently dropped because the author’s user ID was not re-attached on outbound egress.
- **Desktop Stability:** PR [#52273](https://github.com/NousResearch/hermes-agent/pull/52273) bounds tool-result rendering in the desktop GUI, preventing hard freezes and crashes when executing resource-intensive `/learn` commands over large directories.
- **Container Backend Fix:** PR [#50636](https://github.com/NousResearch/hermes-agent/pull/50636) sanitizes host/relative CWD overrides before they reach the Docker `-w` flag, fixing a terminal tool sandbox escape and configuration bug.
- **Rate-Limit Fallback Fix:** PR [#52230](https://github.com/NousResearch/hermes-agent/pull/52230) (with duplicate [#52233](https://github.com/NousResearch/hermes-agent/pull/52233) closed) ensures that 429 rate-limit errors from explicit auxiliary providers correctly trigger the fallback chain instead of silently dropping the task.
- **Codebase Cleanup (Batches 3–6):** Contributor `AlexFucuson9` drove a sweeping refactoring effort across the CLI, agent runtime, desktop, and cron modules—removing unnecessary f-string prefixes from over 300 static strings in PRs [#52262](https://github.com/NousResearch/hermes-agent/pull/52262), [#52268](https://github.com/NousResearch/hermes-agent/pull/52268), [#52269](https://github.com/NousResearch/hermes-agent/pull/52269), and [#52274](https://github.com/NousResearch/hermes-agent/pull/52274).

---

## 4. Community Hot Topics

The community is rallying around three key themes:

**Cost & Token Optimization (Dominant Theme)**
- Issue [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) — *Lazy Tool Schema Loading* (28 comments, 14 👍) remains the single most active discussion. It proposes a two-pass injection to eliminate 3,500–5,000 tokens of fixed overhead per call.
- Issue [#4379](https://github.com/NousResearch/hermes-agent/issues/4379) — *Token Overhead Analysis* (16 comments) provides hard data showing 73% of every API call is fixed overhead (~13.9K tokens). Together, these two issues represent the community’s #1 pain point.

**Multi-Agent Orchestration**
- Issue [#5257](https://github.com/NousResearch/hermes-agent/issues/5257) — *Generalized ACP Client* (11 comments, 16 👍) draws strong support for enabling Hermes to orchestrate Claude Code, Cursor, and Aider directly.

**Platform Expansion**
- Issue [#3725](https://github.com/NousResearch/hermes-agent/issues/3725) — *Rocket Chat Support* (11 comments, 10 👍).
- Issue [#39691](https://github.com/NousResearch/hermes-agent/issues/39691) — *headroom-ai Compression Integration* (7 comments, 10 👍).
- Issue [#42864](https://github.com/NousResearch/hermes-agent/issues/42864) — *Scope-Recall Memory Provider RFC* (5 comments) signals community demand for plugin-based memory backends.

**Ongoing Codex Migration Friction**
- Issue [#13834](https://github.com/NousResearch/hermes-agent/issues/13834) — *openai-codex fails* (12 comments, 3 👍) continues to see activity from users where the official Codex CLI works but Hermes does not.

---

## 5. Bugs & Stability

### Critical (P1)
- **Discord Gateway Heartbeat Stall:** Issue [#52197](https://github.com/NousResearch/hermes-agent/issues/52197) reports that cross-process agent-cache invalidation holds a lock that stalls the asyncio event loop, causing repeated gateway heartbeat timeouts.
- **Credential Pool Corruption:** Issue [#19566](https://github.com/NousResearch/hermes-agent/issues/19566) (8 comments) remains a P1: the OpenAI-Codex credential pool can silently drop newly added credentials during a stale `auth.json` rewrite during rotation.

### High Impact (P2 — Fresh Reports)
- **Local Inference Loop:** Issue [#52261](https://github.com/NousResearch/hermes-agent/issues/52261) *(New, 1 comment)* — Provider 400 errors from oMLX/MLX are misclassified as `context_overflow`, triggering a destructive compress/reset loop. Affects all local inference users.
- **Desktop Windows Encoding:** Issue [#52244](https://github.com/NousResearch/hermes-agent/issues/52244) *(New, 1 comment)* — Hermes Desktop on Windows silently truncates and garbles agent output, suspected to be a UTF-8 encoding issue in the rendering pipeline.
- **Anthropic Double-Compression Crash:** Issue [#52160](https://github.com/NousResearch/hermes-agent/issues/52160) *(1 comment)* — After two session compressions, the Anthropic adapter sends a request with `role: assistant` as the first message, triggering an HTTP 400 rejection.
- **Silent Tool Progress Drop:** Issue [#52212](https://github.com/NousResearch/hermes-agent/issues/52212) *(New, 1 comment)* — Non-edit platforms (WeChat, Signal, QQ, SMS, Email, etc.) silently discard all tool progress messages regardless of `tool_progress_grouping` settings.
- **Remote Desktop Auth Failure:** Issue [#52255](https://github.com/NousResearch/hermes-agent/issues/52255) *(New, 1 comment)* — Desktop remote mode gets stuck on the startup recovery screen when connecting to an authenticated remote gateway.
- **Secret Redaction Corruption:** Issue [#33801](https://github.com/NousResearch/hermes-agent/issues/33801) *(7 comments)* — The API key redaction system operates at the content layer, corrupting Python/Shell syntax in tool inputs and causing silent failures.
- **Rate-Limit Gate Fix Available:** PR [#52272](https://github.com/NousResearch/hermes-agent/pull/52272) provides a fix for reasoning-model thinking timeouts, reclassifying transport disconnects from `context_overflow` to `timeout`.
- **Cron Scheduler Conflict:** PR [#52259](https://github.com/NousResearch/hermes-agent/pull/52259) fixes a race condition where desktop and gateway cron schedulers clash on shared `HERMES_HOME`.
- **Delegate Terminal Timeout:** PR [#52260](https://github.com/NousResearch/hermes-agent/pull/52260) caps delegated child terminal calls to the delegation timeout budget, preventing runaway sub-agents.

---

## 6. Feature Requests & Roadmap Signals

The data strongly suggests the next release will focus on **efficiency, extensibility, and enterprise readiness**:

- **Lazy Tool Loading (Likely Imminent):** Issue [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) carries the label `needs-decision`. Active internal deliberation combined with overwhelming community support makes this a strong candidate for the next minor release.
- **Plugin-Based Memory Architecture:** Issues [#47349](https://github.com/NousResearch/hermes-agent/issues/47349) (Configurable Memory Backends) and [#42864](https://github.com/NousResearch/hermes-agent/issues/42864) (Scope Recall plugin RFC) point toward deprecating the rigid `memory.md` system in favor of fully swappable backends.
- **Incognito Mode:** PR [#19448](https://github.com/NousResearch/hermes-agent/pull/19448) (rebased cleanly onto main) adds ephemeral “incognito” turns for session isolation. This appears close to final review.
- **Cloud/Enterprise Expansion:** Open PRs for Vertex AI (PR [#8427](https://github.com/NousResearch/hermes-agent/pull/8427)) and Ollama Cloud (PR [#22648](https://github.com/NousResearch/hermes-agent/pull/22648)) indicate a roadmap push beyond consumer API keys toward GCP service accounts and self-hosted cloud deployments.
- **Generalized ACP Client:** Issue [#5257](https://github.com/NousResearch/hermes-agent/issues/5257) (16 👍) has strong community signaling but lacks direct maintainer engagement or a linked PR.

---

## 7. User Feedback Summary

### Pain Points
- **Cost Anxiety:** The dominant emotion is frustration with token waste. The hard data from Issue #4379 concretized what many felt: 73% of every call is fixed overhead. Users running local models or high-volume deployments feel this most acutely.
- **Codex Migration Friction:** Repeated reports (#13834, #19566) describe scenarios where the official Codex CLI works perfectly but Hermes’ `openai-codex` provider fails. This risks user trust in the provider parity.
- **Desktop Reliability:** Windows users are effectively blocked by the UTF-8 truncation bug (#52244). The freeze/crash cycle on large tasks (#52273, now fixed) was a widely felt regression.
- **Security Paradox:** Users report being stuck between a broken “smart” approval mode that ignores explicit owner approval (#46544) and an overly aggressive secret redaction system that corrupts valid code (#33801).

### Satisfaction Signals
- **Extensibility is a Win:** The number of custom plugins (Scope Recall, Rocket Chat proposal) and standalone tools (token profiling dashboard) being built *by the community* suggests the plugin architecture is genuinely empowering.
- **Platform Breadth Appreciated:** Despite bugs, users consistently highlight the range of supported providers (OpenAI, Anthropic, Gemini, Ollama, local) and messaging gateways (Discord, Telegram, CLI, Desktop) as a core strength.

---

## 8. Backlog Watch

The following issues require maintainer attention due to age, severity, or community investment:

| Issue | Priority | Created | Status & Risk |
|---|---|---|---|
| [#13834](https://github.com/NousResearch/hermes-agent/issues/13834) — Codex Provider Failure | P2 | Apr 22 | **Stale needs-repro.** High user engagement, no maintainer reproduction. Risks user loss to official Codex CLI. |
| [#17945](https://github.com/NousResearch/hermes-agent/issues/17945) — delegate_task 404 | P2 | Apr 30 | **Blocks auto-research.** `needs-repro` without update for 8 weeks. |
| [#33389](https://github.com/NousResearch/hermes-agent/issues/33389) — Vision Provider Config Ignored | P2 | May 27 | **Configuration broken.** Explicit `gemini` vision provider setting silently falls through to the main provider. |
| [#36216](https://github.com/NousResearch/hermes-agent/issues/36216) — Hindsight Data Loss | P3 | Jun 1 | **Silent data loss.** Turns are dropped when sessions end on non-modulo boundaries if `retain_every_n_turns > 1`. |
| [#4379](https://github.com/NousResearch/hermes-agent/issues/4379) — Token Overhead Analysis | P3 | Apr 1 | **Superseded by #6839**, but the original analysis remains unresolved and is cited by nearly every token-efficiency discussion. |
| [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) — Lazy Tool Schema Loading | P3 | Apr 9 | **Needs decision.** The community is waiting for a maintainer go/no-go to justify the implementation effort. |

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the structured PicoClaw project digest based on the provided GitHub data.

---

## PicoClaw Project Digest — 2026-06-25

### 1. Today’s Overview
Today’s data paints a picture of a project deep in a stabilization and security-hardening sprint. The most significant event is the closure of a coordinated batch of 12 security advisories (Issues #3068–#3082), indicating a successful external audit cycle has concluded. While zero pull requests were merged, developer activity remains high: contributor Alix-007 pushed a stack of four highly targeted fixes to the OpenAI-compatible provider and evolution engine, and a total of 8 PRs remain active. Community discussions around modern web framework support (Issue #3167) and streaming backends (Issue #2404) were closed without extensive public resolution, suggesting a potential misalignment between user expectations and the current roadmap. Overall, the project is prioritizing vulnerability remediation and internal platform reliability over the release of new features.

### 2. Releases
**No new releases.** The last published version predates the high volume of recent fixes, suggesting a new release is likely imminent to bundle the pending security patches and PR queue.

### 3. Project Progress
No pull requests were merged or closed in the last 24 hours. However, the active open PR queue represents substantial progress across several subsystems:

- **Provider & Model Stability:** Alix-007 contributed a concentrated stack of fixes for the `openai_compat` layer, including recovery of Seed XML tool calls (PR #3165), resolution of a build-breaking `undefined: log` error (PR #3166), and improved error handling for model list fetching (PR #3168).
- **Evolution Engine Optimization:** PR #3169 prevents the evolution system from wasting tokens on idle heartbeat turns.
- **Session Data Integrity:** PR #3115 by jp39 addresses a critical bug where inline `data:image/...` strings in generic tool output were incorrectly parsed as real media attachments, which could corrupt session history.
- **Core Agent Lifecycle:** PR #3116 completes the `turn.done` lifecycle signaling, a significant fix for state management in the Pico chat interface.
- **New Connectivity:** PR #3063 proposes a DeltaChat gateway, and PR #3118 adds a remote WebSocket mode to the `picoclaw agent` command, enabling headless operation.

### 4. Community Hot Topics
- **Streaming Feature Request (Issue #2404):** The most commented thread today (13 comments). The request for a `streaming: true` config flag was closed as stale. While the need for streaming support remains high among users, the closure implies maintainers are pursuing a different architectural approach for this feature.
- **Security Advisory Batch (Issues #3068–#3082):** The closure of 12 advisories from YLChen-007 is the dominant topic. While individual threads are short (2 comments each), the volume of reports represents a significant community contribution to the project's security posture.
- **PageAgent Vue/MVVM Support (Issue #3167):** A user (Wavekip) inquired about adaptation for Vue 2 + Element UI enterprise dashboards. The issue was closed with zero public comments. This rapid closure without public resolution creates ambiguity about the project's direction for dynamic web applications.

### 5. Bugs & Stability
Security and data integrity are the primary stability themes today.

- **Critical Security (12 Advisories Closed):** The recently closed advisories cover major attack surfaces, including: SSRF bypasses via ISATAP IPv6 (Issue #3074) and HTTP proxies (Issue #3078), an approval hook symlink race (Issue #3081), MQTT client_id spoofing (Issue #3068), a WeCom trigger policy bypass (Issue #3076), and a CSRF vulnerability in the launcher setup (Issue #3072). The simultaneous closure of these threads strongly suggests the corresponding patches are complete and awaiting release.
- **High Severity (Build Failure):** The `openai_compat` package currently suffers from an `undefined: log` build error on the main branch. A fix is proposed in PR #3166.
- **High Severity (Data Integrity):** PR #3115 addresses a session-history corruption bug caused by misidentification of inline data URLs in tool output.
- **Medium Severity (Token Waste):** PR #3169 fixes an efficiency issue where the evolution engine triggers a costly cold path for routine heartbeat turns.

### 6. Feature Requests & Roadmap Signals
- **Remote Agent Operation (PR #3118):** This feature is a strong candidate for the next release, as it is functionally complete and directly enables cloud/headless deployment scenarios.
- **Decentralized Gateways (PR #3063):** The addition of a DeltaChat gateway signals interest in expanding beyond mainstream platforms into federated and privacy-focused channels.
- **Streaming Support (Issue #2404):** Despite its closure, the demand for low-latency LLM interaction is persistent. It is likely to resurface, potentially as part of a broader asynchronous messaging refactor.
- **Enterprise Web UI Control (Issue #3167):** The lack of a roadmap signal for Vue/React support is a notable gap for enterprise users adopting PageAgent. The community is likely to pressure maintainers for a formal stance on stateful SPA compatibility.

### 7. User Feedback Summary
- **Security Confidence (Positive):** The coordinated disclosure and closure of 12 security issues builds trust with the power-user and security research community, demonstrating a mature vulnerability management process.
- **Enterprise Adoption Friction (Negative/Dissatisfaction):** The PageAgent Vue inquiry (Issue #3167) highlights a real pain point for users trying to automate complex, state-driven dashboards. The silent closure may frustrate potential enterprise adopters.
- **Feature Gap Frustration (Negative/Dissatisfaction):** Closing the streaming request (Issue #2404) without a public alternative may disappoint users relying on streaming-only API endpoints, creating a barrier to adoption for those specific backends.
- **Strong Contribution Vitality (Positive):** The presence of 8 open, high-quality PRs (including complex lifecycle and connectivity changes) signals a healthy, highly invested contributor base.

### 8. Backlog Watch
The mass stale cleanup has cleared the issue backlog, but the PR queue is accumulating critical path items needing maintainer attention:

- **PR #3063 (DeltaChat Gateway):** 17 days stale. A significant feature awaiting review.
- **PR #3115 (Media Extraction Bug Fix):** 13 days stale. A critical data-corruption fix waiting to land.
- **PR #3118 (Remote Agent Mode):** 13 days stale. A major architectural enabler for remote deployments.
- **PR #3116 (Turn.done Lifecycle):** 13 days stale. A core framework fix for message lifecycle management.
- **Communication Gap:** The silent closures of Issue #2404 (Streaming) and Issue #3167 (Vue Support) present a risk of community drift. Even if the decisions are final, providing public rationale for these closures would substantially improve community alignment.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the NanoClaw project digest based on the latest 24-hour activity window.

---

# NanoClaw Project Digest — 2026-06-25

## 1. Today’s Overview

Activity this period is **very high**, with 18 pull requests updated and one new active issue surfacing community frustration. The project is in a heavy development and security-hardening cycle, with major feature work landing for multi-instance Telegram bots, a native Matrix E2EE adapter, and remote MCP server support. A single user-facing issue dominated sentiment: the perceived loss of the Telegram multi-bot feature, which the team addressed with a merged PR within hours. Project health signals are mixed—the community contribution velocity is excellent, but a backlog of critical security and stability fixes lingers unmerged, threatening production readiness.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

Two pull requests were merged or closed today:

- **Closed/ Merged — [#2849 Telegram Multi-Bot](https://github.com/nanocoai/nanoclaw/pull/2849)** (grantland): Adds support for running multiple Telegram bot instances from a single NanoClaw instance by discovering `TELEGRAM_BOT_TOKEN_<SUFFIX>` entries in `.env`.
- **Closed/ Merged — [#2799 Security: `send_file` Path Traversal (CVE-2026-29611)](https://github.com/nanocoai/nanoclaw/pull/2799)** (sturdy4days): Confines `send_file` reads to `/workspace`, fixing a critical vulnerability where a compromised agent could read arbitrary container files.

**Active Features & Fixes in Flight:**
- **Matrix Native E2EE** ([#2844](https://github.com/nanocoai/nanoclaw/pull/2844)): Replaces the Chat SDK bridge with a Rust-native adapter for persistent end-to-end encryption.
- **Remote MCP Servers** ([#2847](https://github.com/nanocoai/nanoclaw/pull/2847)): Enables agents to connect to MCP servers over HTTP/SSE.
- **`/learn` Skill** ([#2843](https://github.com/nanocoai/nanoclaw/pull/2843)): New skill that distills a reusable skill from any source—directory, URL, or past conversation.
- **Generic Extension-Point Seams** ([#2842](https://github.com/nanocoai/nanoclaw/pull/2842)): Adds inert hooks across the host and container runtime for future extensibility.

## 4. Community Hot Topics

The most significant community signal this period is **Issue #2852 — "telegram multi-bot"** ([nanocoai/nanoclaw Issue #2852](https://github.com/nanocoai/nanoclaw/issues/2852)). The user reports a regression: "we had it, and then it got removed." They state that "instance" support is claimed but does not work in practice, ending with the pointed question *"Is it ever going to be implemented? or do we need to look elsewhere?"* This is a high-stakes feedback item that the maintainers have clearly prioritized, landing a fix in PR #2849 the same day.

Underlying this request is a clear **power-user need for multi-tenant or multi-workload bot separation** from a single NanoClaw deployment. The simultaneous submission of PRs #2849 (merged) and #2853 (open alternative) indicates strong contributor alignment around solving this immediately.

Other hot items include:
- **Security Hardening Cluster** ([#2800](https://github.com/nanocoai/nanoclaw/pull/2800), [#2801](https://github.com/nanocoai/nanoclaw/pull/2801), [#2802](https://github.com/nanocoai/nanoclaw/pull/2802) by sturdy4days): Multiple PRs addressing path traversal, socket timeouts, and router input sanitization. This represents a coordinated security sprint.
- **macOS Container Failure** ([#2854](https://github.com/nanocoai/nanoclaw/pull/2854)): Broad user impact—every agent API call fails on macOS due to CA certificate mount issues with Rancher Desktop.

## 5. Bugs & Stability

Issues are ranked by severity, with linked fix PRs where available:

| Severity | Issue / PR | Description | Fix Status |
|---|---|---|---|
| **Critical** | [CVE-2026-29611](https://github.com/nanocoai/nanoclaw/pull/2799) | Path traversal in `send_file` allowing arbitrary file reads | **Merged** ✅ |
| **High** | [#2854 macOS CA Mount](https://github.com/nanocoai/nanoclaw/pull/2854) | Complete failure of agent API on macOS (Rancher Desktop / Apple containers) | Fix open ⏳ |
| **High** | [#2800 Folder Escape / Image Injection](https://github.com/nanocoai/nanoclaw/pull/2800) | `ncl groups` persistent folder escape (CWE-22) and missing image tag pinning | Fix open ⏳ |
| **High** | [#2802 Socket Hardening](https://github.com/nanocoai/nanoclaw/pull/2802) | No timeout or buffer bound on `ncl` transport—risk of permanent hang or OOM | Fix open ⏳ |
| **High** | [#2750 Stale outbound.db Journals](https://github.com/nanocoai/nanoclaw/pull/2750) | Data corruption after container SIGKILL; oldest active high-severity fix (Jun 12) | Fix open ⏳ |
| **Medium** | [#2850 Signal Group Flags](https://github.com/nanocoai/nanoclaw/pull/2850) | Inbound Signal group messages missing `isMention` and `isGroup` flags | Fix open ⏳ |
| **Medium** | [#2815 / #2801 Router Primitive JSON](https://github.com/nanocoai/nanoclaw/pull/2815) | `safeParseContent` returns `undefined` fields on primitive JSON payloads | Fix open ⏳ |
| **Low** | [#2851 Test Poll Loops](https://github.com/nanocoai/nanoclaw/pull/2851) | Abandoned poll loops in test helpers cause flaky parallel test runs | Fix open ⏳ |

## 6. Feature Requests & Roadmap Signals

The single user issue this period is a **feature regression request**: Telegram multi-bot support (Issue #2852). The community responded by immediately merging a fix. Beyond the user request, the open PR landscape strongly signals the following incoming capabilities:

- **Multi-Instance Bot Architecture**: Telegram multi-bot (#2849) and the Matrix E2EE adapter (#2844) both suggest a pattern shift toward first-class multi-instance channel support. **Prediction**: This will land in the next minor release.
- **Remote MCP Protocol Support** ([#2847](https://github.com/nanocoai/nanoclaw/pull/2847)): Moving MCP beyond local stdio to HTTP/SSE enables networked agent tool ecosystems. **Prediction**: Blocked until the MCP specification stabilizes, likely v0.3 or v0.4.
- **Dynamic Self-Improvement** ([#2843 `/learn` skill](https://github.com/nanocoai/nanoclaw/pull/2843)): This is a major meta-capability. An agent that can create its own skills from arbitrary input pushes NanoClaw into autonomous agent tooling. **Prediction**: Experimental in the next release, flagship in fall 2026.
- **Plugin / Seam Architecture** ([#2842](https://github.com/nanocoai/nanoclaw/pull/2842)): Generic extension-point seams hint at a formal plugin or middleware API. **Prediction**: Foundation for a v1 plugin SDK.

## 7. User Feedback Summary

**Pain Points:**
- **Feature Regression (High Visibility):** The removal/breakage of Telegram multi-bot is the standout complaint. The user @Kwisss is actively evaluating alternatives ("need to look elsewhere"). This represents churn risk if the merged fix is not released and validated promptly.
- **macOS Blockage:** PR #2854 reports that agent API calls are completely broken on macOS with Rancher Desktop. This directly impacts a large segment of local development users.
- **Configuration Friction:** The user reports that “Claude cannot get [instance support] to work,” highlighting a potential UX or documentation gap for advanced multi-instance setups.

**Use Cases Emergent:**
- Power users are running multiple Telegram bots for different agent personas/tasks.
- Developers are seeking secure, containerized agent environments (evidenced by the security PR cluster).
- Users are experimenting with federated agent architectures via remote MCP servers.

**Satisfaction Indicators:**
- Despite the Telegram regression, community contributors (grantland, sturdy4days, foxsky, avri-schneider) are actively building and fixing. This indicates a deeply engaged core user base that is highly invested in the project’s success.

## 8. Backlog Watch

Several critical PRs have gone unmerged for significant periods, creating risk accumulation:

- **[PR #2750: Stale outbound.db Journals (Jun 12 – 13 days stale)](https://github.com/nanocoai/nanoclaw/pull/2750)**: Fixes two data-corruption issues (#2516, #2640) where container kills corrupt the outbound database. This is the highest-stakes unmerged fix. Every day without this merge risks production data loss for users relying on container isolation.
- **[PR #2800: Folder Escape & Image Pinning (Jun 17 – 8 days stale)](https://github.com/nanocoai/nanoclaw/pull/2800)**: Security hardening for group management. Path traversal and unverified image tags are high-severity attack vectors.
- **[PR #2802: Socket Hardening (Jun 17 – 8 days stale)](https://github.com/nanocoai/nanoclaw/pull/2802)**: No timeout or resource bounds on the `ncl` host socket. Can leave promises unsettled forever.
- **[PR #2815: Router Primitive JSON (Jun 18 – 7 days stale)](https://github.com/nanocoai/nanoclaw/pull/2815)**: Regression fix for content routing when primitive JSON is received.

**Notable:** The merge of CVE fix #2799 today is significant. It is the first of the sturdy4days security chain to land. The community and maintainers should prioritize merging the remaining three (#2800, #2801, #2802) as a unified patch release to protect production deployments.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-25

## Today's Overview

IronClaw saw intense activity over the past 24 hours with **45 PRs updated** (27 open, 18 merged/closed) and **19 issues updated** (16 open, 3 closed), reflecting a full-speed stabilization and feature push. The most critical development is a coordinated emergency fix cycle addressing a **runtime meltdown (`lease_expired` mass failures, ~4-minute total freeze)** that occurred on June 24, with three large mitigation PRs now in code review or recently opened. On the architectural front, the Reborn memory layer crossed a major milestone with the M2 lift to a provider-neutral contract crate (`#5163`), now merged. Dogfooding efforts (tracked in `#5119`) are driving a wave of UX and reliability reports, particularly around broken tool approval flows, signaling a strong focus on polishing the v2 hosted experience.

## Releases

**No new releases** were published today. The project remains in a rapid iteration cycle between semantic version increments.

## Project Progress

### Merged / Closed PRs

- **Memory Architecture Milestone — PR #5163 (Merged)**  
  Lift of the Reborn memory layer into `ironclaw_memory` (provider-neutral contract crate) and `ironclaw_memory_native` (native filesystem provider), behind an `Arc<dyn MemoryService>` facade. Strictly behavior-preserving, this is the M2 slice of the larger memory redesign (`#3537`).

- **CI Stability Restored — PR #5193 (Merged)**  
  Fixed a duplicate workflow key that was blocking `main` CI runs, plus a missed `spawn_subagent` test ignore. Unblocks the pipeline for all subsequent merges.

### Features & Major Fixes Advanced (Open PRs with Significant Activity)

- **Context Management / Progressive Tool Disclosure — PR #5149**  
  Flag-gated feature (default off) that curbs per-call prompt size by sending only relevant tool schemas instead of the full ~91 tools (~25.8k tokens per call), targeting the root cause of NEAR AI timeouts.

- **Stability Surge (Meltdown Response):**
  - **PR #5204:** Bounds NEAR AI reqwest calls to prevent 90s hangs from freezing the runner lease.
  - **PR #5206:** Isolates WASM execution to prevent tool execution from starving the tokio worker pool.
  - **PR #5203:** Fast-fails a dead/degraded provider instead of letting every user request wedge against the 120s timeout × 3 retries.
  - **PR #5202:** Fixes recurring trigger poller hang by making delivery hooks fully asynchronous.

- **Auth & Identity Fixes:**
  - **PR #5180:** Populates provider metadata on runtime auth-required gates so token savings actually propagate.
  - **PR #5145:** Refactors capability activity lifecycle for consistent stable identity across gates, prompts, and WebUI rendering.

- **WebUI Evolution:**
  - **PR #5068:** Wires global auto-approve + per-tool permission settings surface end-to-end.
  - **PR #5160:** Delivers all tools' live activity across resumed SSE drains (fixes "stuck" tool list in WebChat v2).
  - **PR #5199:** Unblocks Web UI log access for multi-tenancy users.
  - **PR #5084:** Redesigns the Automations page into a denser, scannable layout.

## Community Hot Topics

### 1. Prompt Safety False Positives Killing Benign Requests — Issue #5169
On a clean default Reborn setup, a bundled skill's documentation containing ordinary API vocabulary ("Authorization", "Bearer", "access token") trips the model-safety vocabulary denylist. The agent dies with a misleading *"temporary system issue"* message instead of surfacing the real block.

**Analysis:** Exposes a critical design tension between safety systems and skill distribution; skill authors have no escape hatch to declare safe vocabulary. No fix PR is currently attached, making this a high-priority open wound for user trust.

### 2. Tool Approval Flow Breakdown — Issues #5192, #5196, #5197, #4986
Filed primarily by @sunglow666 as part of the dogfooding tracker (`#5119`), this cluster of bugs reveals a fundamental disconnect between the agent's planning loop and user permission decisions:

- **#5197:** Disabling a tool causes the assistant to invoke unrelated tools instead of reporting unavailability.
- **#5196:** "Ask each time" fails with an authorization error after approval, triggering a duplicate approval loop.
- **#5192:** Denying a tool approval still generates additional approval requests.
- **#4986:** Recurring automations become permanently blocked waiting for tool approval.

**Analysis:** These four issues together point to a flawed re-evaluation of tool availability state *after* the user makes a permission decision. The model infers tool unavailability as "try another tool" rather than "report unavailable," and the authorization gate does not properly short-circuit future invocations. Fixing the tool permission lifecycle is the single highest-impact UX improvement available.

### 3. Observability Request — Issue #5182
A hosted operator describes the difficulty of extracting diagnostics from the Reborn binary. Manual scraping of process logs is the only debugging method currently available.

**Analysis:** Strong roadmap signal for log infrastructure investment. The recent meltdown amplifies the urgency of this request for production operators.

## Bugs & Stability

### Critical Severity

| Issue | Symptom | Fix Status |
|---|---|---|
| **Runtime Meltdown (June 24 incident)** | Mass `lease_expired` failures, ~4-minute total freeze, gateway 502s. Root causes: unbounded NEAR AI timeouts + WASM starving Tokio. | **Mitigation in progress** — PR #5204, PR #5206, PR #5203 |
| **Issue #5169** | Bundled skills trip denylist → agent dies with misleading error. | **No fix PR linked** |
| **Issue #5139** (Closed) | Reborn regression: web/research tasks hang at init, zero LLM calls. | **Closed** — root cause patched in 24h window |

### High Severity

| Issue | Symptom | Fix Status |
|---|---|---|
| **#5190** | Invalid bearer token enters WebUI shell but actions silently fail. | No fix PR linked |
| **#5196 / #5197 / #5192 / #4986** | Tool approval/prohibition entirely broken in multiple scenarios. | **PR #5068** partially addresses settings surface; core authorizer fix may be pending |
| **#5184** | Reborn startup fails when MCP product-auth lookup is unavailable. | No fix PR linked |
| **#5179** | Multi-tenancy users cannot access Web UI logs. | **PR #5199** removes the operator-config gate |

### Medium Severity

| Issue | Symptom |
|---|---|
| **#5189** | Successful tool calls don't stream activity details (failed calls do). |
| **#5191** | Internal skill activation / context budget messages leak into chat UI. |
| **#5188** | Reborn WebUI v2 sidebar not responsive across desktop and mobile. |

## Feature Requests & Roadmap Signals

1. **Production Observability (Issue #5182)** — Meaningful structured logs and failure diagnostics out of the Reborn binary for hosted deployments. Likely to be a priority for the next release given operational urgency.

2. **Enterprise Memory Controls (PR #5205)** — Stacks on the M2 memory lift with host-owned context sanitization and boundary allowlists, signaling governance features for regulated deployments.

3. **Memory Seeding (PR #5165)** — Optional initialization of the native memory provider with starting documents on the composition build path. Enables migration scripts, demos, and test fixtures.

4. **UI Polish Sprint (PR #5084, #5188, #5068)** — Automations page redesign, responsive sidebar, and tool permission settings surface all underway. The v2 WebUI is clearly being readied for broader rollout.

5. **Architecture Refactoring (PR #5137)** — Incremental decomposition of the `ironclaw_reborn_composition` god-crate (~132k lines) into isolated crates. A long-term maintainability investment.

## User Feedback Summary

**User Pain Points (High Intensity):**

- **"The agent doesn't listen to my permissions."** Multiple issues from the dogfooding campaign report that tool disable, deny, and "ask each time" actions are either ignored or produce contradictory behavior. This erodes trust in the assistant's ability to act on user intent.
- **"My safe request failed and I don't know why."** The prompt safety false positive produces a generic "temporary system issue" error, hiding the actual cause and frustrating users on clean setups.
- **"I can't see what's happening."** Missing activity details for successful tool calls, internal debug messages exposed in chat, and no logs for multi-tenancy users all contribute to a feeling of flying blind.
- **"Hosted deployments are fragile and opaque."** The startup failure on MCP unavailability and the lack of structured diagnostics make operators uneasy about production deployment.

**Use Cases Driving Activity:**
- Automated repository monitoring (sunglow666's GitHub watcher prompts).
- Daily QA reminder automations.
- Web research tasks (regression in #5139).
- Multi-tenant enterprise deployments (log access, service lifecycle).

**Satisfaction Signal:**
The team is shipping fixes rapidly—three meltdown PRs were opened in a single day. The dogfooding initiative is generating high-quality bug reports, indicating active internal use of the product before general release.

## Backlog Watch

### Issue #4108 — Nightly E2E Failed (Open since May 27, 2026)
This automated failure report has been open for **nearly a month** without being resolved or assigned. While PR #5193 fixed a CI syntax issue, the actual nightly E2E pipeline failure remains unaddressed. An active resolution plan or root cause investigation is overdue. This is the highest-signal backlog risk.

### Issue #4986 — Recurring Automation Blocked (Open since June 16, 2026)
9 days open and functionally blocks the automation feature for users whose agents require tool approval. Given the current sprint's focus on tool permissions, this should be prioritized in the next planning cycle.

### Dependabot PRs (#4002, #5138)
Large batch dependency bumps (#5138: 45 updates, #4002: 16 actions updates) remain open. These contain breaking changes (e.g., `agent-client-protocol` 0.10.4 → 1.0.0) and should be reviewed promptly to mitigate supply chain risk.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the structured LobsterAI project digest based on the provided data.

---

## LobsterAI Project Digest | 2026-06-25

### 1. Today’s Overview
LobsterAI experienced a massive surge in development activity over the past 24 hours, with **41 pull requests merged** against only 1 issue update. This extreme merge velocity indicates the team is in a heavy consolidation phase, aggressively integrating fixes and features across the stack. Project health is excellent, demonstrating high developer throughput and a clear focus on stabilizing the core subsystems. The lack of a new release today suggests this intensive activity is preliminary work for an imminent major version.

### 2. Releases
No new releases were published today. Given the extraordinary volume of merged improvements, a formal release candidate or stable release appears imminent.

### 3. Project Progress
The 41 merged PRs represent sweeping improvements across the entire application:
- **OpenClaw Core Stability**: Critical fixes landed to prevent gateway restart loops ([PR #2043](https://github.com/netease-youdao/LobsterAI/pull/2043)), improve cross-platform spawning on macOS/Linux ([PR #2195](https://github.com/netease-youdao/LobsterAI/pull/2195)), and prevent token burn during aborted tool loops ([PR #2049](https://github.com/netease-youdao/LobsterAI/pull/2049), [PR #2051](https://github.com/netease-youdao/LobsterAI/pull/2051)).
- **Cowork Feature Advancements**: Addressed session freezing ([PR #2047](https://github.com/netease-youdao/LobsterAI/pull/2047)) and introduced a new metadata-driven skill routing system ([PR #2078](https://github.com/netease-youdao/LobsterAI/pull/2078)), moving away from inlined prompts.
- **UI/Config & Platform Fixes**: Updated model selection UI ([PR #2053](https://github.com/netease-youdao/LobsterAI/pull/2053)), added support for MiniMax M3 and MIMO v2.5 ([PR #2089](https://github.com/netease-youdao/LobsterAI/pull/2089), [PR #2102](https://github.com/netease-youdao/LobsterAI/pull/2102)), fixed a WeChat integration bug ([PR #2086](https://github.com/netease-youdao/LobsterAI/pull/2086)), and replaced a deprecated auto-update launcher ([PR #2057](https://github.com/netease-youdao/LobsterAI/pull/2057)).

### 4. Community Hot Topics
The most visible community discussion centers on **[Issue #1394](https://github.com/netease-youdao/LobsterAI/issues/1394)** regarding the automatic deletion of non-repeating scheduled tasks after execution. The user advocates for retaining these tasks as editable templates, a feature that clashes with the current cleanup logic. While direct comments on the merged PRs are minimal, the *nature* of the fixes—particularly those preventing runaway token consumption and session freezing—reveals that developer actions are directly responding to widespread underlying user frustrations with cost and reliability.

### 5. Bugs & Stability
Stability has been the dominant theme today, with rapid turnaround on severe issues.
- **[Critical – Resolved]**: **Token Burn during Tool Loops**. Users experienced unbounded AI token consumption. The team rapidly introduced a missing upstream loop breaker ([PR #2049](https://github.com/netease-youdao/LobsterAI/pull/2049), [PR #2051](https://github.com/netease-youdao/LobsterAI/pull/2051)).
- **[High – Resolved]**: **Session Freezing** ([PR #2047](https://github.com/netease-youdao/LobsterAI/pull/2047)) and **OpenClaw Gateway Restart Loops** ([PR #2043](https://github.com/netease-youdao/LobsterAI/pull/2043)).
- **[Medium – Resolved]**: **Duplicate Final Summaries** ([PR #2197](https://github.com/netease-youdao/LobsterAI/pull/2197)), replacement of the deprecated **VBScript App Launcher** ([PR #2057](https://github.com/netease-youdao/LobsterAI/pull/2057)), and **WeChat Integration flaw** ([PR #2086](https://github.com/netease-youdao/LobsterAI/pull/2086)).
- **[Low – Active]**: **Scheduled Task Deletion** ([Issue #1394](https://github.com/netease-youdao/LobsterAI/issues/1394)). A workflow issue where non-repeating tasks are permanently removed after a single run, preventing reuse.

### 6. Feature Requests & Roadmap Signals
The most distinct roadmap signal is the shift toward **metadata-driven skill routing** for the Cowork feature ([PR #2078](https://github.com/netease-youdao/LobsterAI/pull/2078)). This architectural move away from inlining prompts toward structured metadata suggests the team is building a more modular and agent-centric agent ecosystem. The aggressive addition of models (MiniMax M3, MIMO v2.5) and the explicit preservation of user-configured context windows ([PR #2102](https://github.com/netease-youdao/LobsterAI/pull/2102)) highlight a focus on flexibility and keeping pace with the rapidly evolving LLM landscape. The next version will likely feature the new Cowork routing system as a headline capability.

### 7. User Feedback Summary
The implicit and explicit user feedback driving today’s work points to two major themes: **reliability** and **cost efficiency**.
- **Dissatisfaction (Resolved)**: The "token burn" loop issue represents a significant financial and reliability pain point that was addressed with high urgency.
- **Reliability (Resolved)**: Session freezing and gateway crashes impacted core workflow stability; fixes took priority.
- **Active Friction (Unresolved)**: The scheduled task lifecycle in Issue #1394 remains a workflow mismatch where application cleanup logic overrides user intent for persistence.
Overall, the speed at which the team turned around fixes for critical issues (PRs from May 25–26 merged today) demonstrates a highly responsive development cycle aligned with power-user needs.

### 8. Backlog Watch
**Issue #1394**: *“定时任务选择不重复执行时，执行一次后会自动被永久删除”* ([Link](https://github.com/netease-youdao/LobsterAI/issues/1394)). Created on April 3, 2026, and tagged as stale, this is the most significant unattended community request in the active dataset. While the team rightly prioritized fixing critical execution bugs, the underlying design question—whether one-shot scheduled tasks should remain ephemeral or persist as reusable templates—remains open. As the stabilization surge winds down, this workflow enhancement is a strong candidate for the next development cycle.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

## TinyAGI Project Digest — 2026-06-25

### 1. Today's Overview
TinyAGI experienced a quiet day on June 25, with zero open issues and zero open pull requests updated. The only activity was the formal closure of a critical Windows compatibility pull request from the prior cycle. No new releases were published. This lull suggests a stable plateau following a targeted bug-fix sprint, though the complete absence of new issues could indicate a natural pause between development cycles.

### 2. Releases
No new releases were published today.

### 3. Project Progress
One pull request was advanced to a closed/merged state:
- **[#281: fix: Windows cross-platform support in CLI](https://github.com/TinyAGI/tinyagi/pull/281)** (Author: mperkins0155)
  - Resolves three distinct Windows-native bugs that prevented CLI operation outside of WSL.
  - Key fix: Corrects a `MODULE_NOT_FOUND` error caused by Node.js generating doubled drive letters (e.g., `/C:/Users/...`) when resolving `import.meta.url` paths on Windows.
  - This patch expands the CLI’s portability for Windows-based developers.

### 4. Community Hot Topics
The only touched item is **[PR #281](https://github.com/TinyAGI/tinyagi/pull/281)**. Although it recorded 0 formal comments, the technical work around OS path resolution highlights a significant latent community demand: **native Windows support**. The underlying need is a friction-free, single-command setup for Windows developers who want to run TinyAGI without relying on a WSL environment.

### 5. Bugs & Stability
- **No new bugs reported** in the last 24 hours.
- The severe bug preventing Windows CLI execution (CRITICAL severity) was resolved via **PR #281**.
- The project now enters a period of enhanced stability for cross-platform users. No regressions were reported in the wake of this fix.

### 6. Feature Requests & Roadmap Signals
No new feature requests were filed or updated. Given the recent completion of the Windows compatibility patch, the immediate roadmap likely focuses on verifying the fix in a stable patch release before returning to pending feature development.

### 7. User Feedback Summary
No direct user feedback threads were updated today. The existence and closure of **PR #281** itself is the primary signal, indicating past user pain points with Windows CLI support have been heard and addressed by the maintainers.

### 8. Backlog Watch
The project backlog is currently clean. There are **zero open issues** and **zero open pull requests** requiring triage as of today. This indicates strong maintainer responsiveness on the most recent patch and provides no long-unanswered items needing immediate attention.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw (QwenPaw) Project Digest — 2026-06-25

*Data sourced from agentscope-ai/QwenPaw*

---

## 1. Today's Overview

QwenPaw is in a high-velocity stabilization sprint following the AgentScope 2.0 migration, with **25 issues** and **50 pull requests** updated in the last 24 hours. The community is actively stress-testing the beta, surfacing significant regressions in streaming, provider compatibility, and frontend stability. No new releases were cut today, but the team merged critical fixes for DashScope integration and context management. While maintainer responsiveness appears strong (PRs are often spawned directly from community bug reports), the sheer volume of open items (18 open active issues, 43 open PRs) signals a project under heavy maintenance load. Stability is the dominant narrative over net-new features.

---

## 2. Releases

**None.** No new versions were published today. The latest reported versions in the community are `v1.1.12.post2` (stable) and `v2.0.0b1` (beta).

---

## 3. Project Progress

7 PRs and 7 issues were merged or closed today, indicating steady churn despite the high open volume.

- **[Merged] DashScope Provider Fix ([#5491](agentscope-ai/QwenPaw PR #5491))**: Correctly handles `extra_body.generate_kwargs` and disables the default `enable_thinking` flag that was breaking compatibility.
- **[Closed/Resolved] Context Date Architecture ([#5498](agentscope-ai/QwenPaw PR #5498))**: Moved the `Current date` from static environment context to a per-user-message dynamic prefix. Directly addresses the discussion in [#5455](agentscope-ai/QwenPaw Issue #5455) to improve prompt cache stability.
- **[Closed] Shell Execution Parsing ([#5373](agentscope-ai/QwenPaw Issue #5373))**: The bug preventing shell special characters (pipes, redirection, stderr) has been resolved.
- **[Closed] Feishu Channel Routing ([#5264](agentscope-ai/QwenPaw Issue #5264))**: The regression where group chat replies were incorrectly routed to private chats has been fixed.
- **[Closed] Frontend Loading Performance ([#5015](agentscope-ai/QwenPaw Issue #5015))**: A longstanding question about UI lag under load was closed, presumably addressed by the ongoing 2.0 rework or config changes.

---

## 4. Community Hot Topics

**Most Active Issues (by comment count):**

- **Custom Provider Function Calling ([#5345](agentscope-ai/QwenPaw Issue #5345)) — 8 comments**: Users integrating custom OpenAI-compatible providers (e.g., OMLX) report that tools are never invoked, with the model only returning plain text. This is the hottest issue and represents a core capability gap for power users. The community strongly expects interchangeable provider support.

- **Timestamp Engineering Debate ([#5455](agentscope-ai/QwenPaw Issue #5455)) — 4 comments**: A sophisticated architectural discussion on whether the current time should be in system context vs. per-user prefix. The user's argument that the current implementation breaks prompt caching resonated enough to immediately spawn two competing fix PRs ([#5498](agentscope-ai/QwenPaw PR #5498), [#5499](agentscope-ai/QwenPaw PR #5499)).

- **Browser Autofill Hijack ([#5403](agentscope-ai/QwenPaw Issue #5403)) — 4 comments**: Browser password managers are incorrectly attaching credential autofill popups to the "Search providers" input field on the Model Configuration page. A persistent UX annoyance that affects daily configuration workflows.

- **Internal Server Error on Clean Install ([#5379](agentscope-ai/QwenPaw Issue #5379)) — 5 comments**: A fatal onboarding blocker for Windows users where accessing the web UI immediately returns a 500 error with a `get_remote_addr(transport)` traceback.

**Most Active PRs:**
The PRs with the highest implied activity relate to the 2.0 streaming restoration ([#5487](agentscope-ai/QwenPaw PR #5487)), mission mode integration ([#5442](agentscope-ai/QwenPaw PR #5442)), and token usage ring restoration ([#5493](agentscope-ai/QwenPaw PR #5493)), all of which represent regression fixes from the recent migration.

---

## 5. Bugs & Stability

Stability is the critical theme today. The AgentScope 2.0 migration has caused systemic regressions across nearly every component.

### Critical (Crashes / Data Loss)

- **MiniMax-M3 Silent Data Loss ([#5505](agentscope-ai/QwenPaw Issue #5505))**: When MiniMax content safety rejects a single image, the provider erroneously caches `rejects_media=True` for the entire model. All subsequent image requests have their media stripped *before* being sent to the model. This is a dangerous silent data/capability loss bug.
- **Session >500KB Crashes Console ([#5479](agentscope-ai/QwenPaw Issue #5479))**: The frontend completely crashes with a generic "unexpected error" when opening large session files, effectively locking users out of long-running conversations.
- **Large Tool-Use History Crash ([#5401](agentscope-ai/QwenPaw Issue #5401))**: Console white-screens when loading sessions with extensive tool-call histories due to unmapped `type: "data"` content blocks.
- **Internal Server Error on Start ([#5379](agentscope-ai/QwenPaw Issue #5379))**: Fresh Windows pip install fails to load the web UI entirely. Fatal onboarding blocker.

### High (Major Feature Loss)

- **Custom Provider Function Calling ([#5345](agentscope-ai/QwenPaw Issue #5345))**: Core agent capability (tool use) entirely broken when using non-Ollama OpenAI-compatible providers.
- **IM Channel Streaming Broken ([#5487](agentscope-ai/QwenPaw PR #5487))**: The entire streaming path for all IM channels (Feishu, DingTalk, QQ, Discord) is non-functional post-2.0 migration. Fix is open in PR.
- **Agent Identity Mismatch ([#5456](agentscope-ai/QwenPaw Issue #5456))**: 2.0b1 can build context with the wrong `agent_id` when processing channel requests, leading to incorrect agent behavior.
- **GLM-5.x Schema Failure ([#5472](agentscope-ai/QwenPaw Issue #5472))**: Tool call JSON schema generation fails on OpenCode Go's GLM models. A fix PR ([#5496](agentscope-ai/QwenPaw PR #5496)) is open to inline `$ref/$defs`.

### Medium (UI/UX Regressions)

- **Long Message CSS Layout Broken ([#5480](agentscope-ai/QwenPaw Issue #5480))**: Markdown rendering collapses on long messages; requires tab-switch to force recalculation.
- **Kimi/K2 Provider Schema ([#5427](agentscope-ai/QwenPaw Issue #5427))**: Kimi's Anthropic-compatible endpoint for Kimi K2 Code is not supported by the current OpenAI-only provider implementation.
- **Browser Autofill Hijack ([#5403](agentscope-ai/QwenPaw Issue #5403))**: Password manager blocks usability of the provider search field.
- **Token Usage Ring Missing ([#5493](agentscope-ai/QwenPaw PR #5493))**: The per-turn token usage visualization is completely absent in the 2.0 frontend (fix in PR).

---

## 6. Feature Requests & Roadmap Signals

Despite the stabilization crunch, several long-term roadmap signals emerged:

- **Plugin Distribution Standardization ([#5484](agentscope-ai/QwenPaw Issue #5484))**: A user requests pip/PyPI-based plugin installation to replace the current ZIP-only system. If adopted, this would be a major step toward a mature plugin ecosystem modeled after Hermes Agent.
- **OpenAI Response Format Support ([#5489](agentscope-ai/QwenPaw Issue #5489))**: Formal request to support OpenAI's response-format messages in the existing message flow, aligning with broader API standardization demands.
- **"Scroll" Context Manager (PR [#5321](agentscope-ai/QwenPaw PR #5321))**: A first-time contributor is adding a retrieval-driven context manager using SQLite. This represents a shift from compression to durable memory, signaling the project's ambition to handle long-running, complex agent sessions.
- **TUI Coding Mode Scoping ([#5448](agentscope-ai/QwenPaw PR #5448))**: Adds `qwenpaw .` / `qwenpaw tui [PROJECT]` to bind the TUI to specific project directories. Strong signal of deepening Coding Mode / IDE-competitive workflows.
- **Tauri Auto-Updater ([#4669](agentscope-ai/QwenPaw PR #4669))**: Open for exactly one month, this long-running PR adds desktop update infrastructure. A critical gating item for making desktop users first-class citizens.
- **Memory & Channel UX Polish ([#5482](agentscope-ai/QwenPaw PR #5482), [#5504](agentscope-ai/QwenPaw PR #5504))**: The team is actively polishing memory search defaults and introducing dual-layout channel pages, suggesting these areas are nearing feature-complete status.

---

## 7. User Feedback Summary

**Common Pain Points:**
- **Migration Instability**: The dominant user sentiment is frustration with regressions introduced by the 2.0 migration. Users accustomed to previously working features (streaming, tool calls) are hitting new blocks, generating a steady stream of "this worked before" reports.
- **Resource Consumption**: Direct feedback in [#5441](agentscope-ai/QwenPaw Issue #5441) ("1.4GB on startup") highlights performance bloat as a key pain point, especially for users with limited hardware.
- **Model Connectivity Fragmentation**: Users are actively integrating a wide variety of Chinese and global providers (OMLX, MiniMax, Kimi, GLM, DeepSeek). Each provider has unique API quirks, and the current abstraction layer struggles with the diversity. The community deeply desires "write once, run anywhere" provider configs.
- **Enterprise/Platform Friction**: White pages on intranets ([#5497](agentscope-ai/QwenPaw Issue #5497)), missing Python paths in Tauri ([#5317](agentscope-ai/QwenPaw Issue #5317)), and Windows-specific 500 errors ([#5379](agentscope-ai/QwenPaw Issue #5379)) indicate rough edges for non-Linux, non-macOS power users.

**Signs of Satisfaction:**
- The rapid conversion of user discussions into fix PRs (e.g., #5455 → #5498/#5499) demonstrates exceptional maintainer responsiveness.
- The sophistication of feature requests (retrieval-based memory, pip plugins, context engineering) signals a deep, technical power-user base that relies on QwenPaw for daily work.

---

## 8. Backlog Watch

Long-standing or critical items that need maintainer attention:

- **PR [#4669](agentscope-ai/QwenPaw PR #4669) — Tauri Auto-Updater**: Open since **2026-05-25** (exactly 1 month). A clean first-pass implementation. Blocking the desktop user update experience.
- **Issue [#5345](agentscope-ai/QwenPaw Issue #5345) — Custom Provider Function Calling**: Open since 2026-06-20. **Most commented issue (+8)**. This is a top-priority feature gap with no official triage response or workaround from the team yet. Growing risk of user abandonment if unsupported providers are core to their workflow.
- **Issue [#5379](agentscope-ai/QwenPaw Issue #5379) — Internal Server Error on Start**: Open since 2026-06-22. A "cannot use the product" scenario for Windows users. Should be treated as a P0 triage target.
- **Issue [#5231](agentscope-ai/QwenPaw Issue #5231) — MCP Tool Name Display**: Open since 2026-06-16. A UX enhancement request with community support but no maintainer engagement yet.
- **Issue [#5479](agentscope-ai/QwenPaw Issue #5479) — Large Session Crashes**: The frontend's inability to handle realistic session sizes (>500KB) is a hard wall for heavy users. This should be prioritized alongside the tool-use rendering crash ([#5401](agentscope-ai/QwenPaw Issue #5401)) as a core UX stability issue.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-25

## 1. Today's Overview

The ZeroClaw project is experiencing an intense surge in development activity, with **47 issues and 50 pull requests updated in the last 24 hours**. The focus is decisively on **production hardening**, **enterprise security** (OIDC, RBAC, supply chain signing), and the ambitious **WASM plugin architecture overhaul**. No formal release was cut today, but the massive volume of RFCs, fixes, and feature PRs suggests the project is in a critical feature-build and stabilization phase targeting milestones **v0.8.3** and **v0.9.0**. The community remains deeply technical, driving complex architectural decisions around multi-tenancy, plugin distribution, and delegation security.

---

## 2. Releases

No new releases today. The release cadence appears paused as major architectural components (OIDC provider seam, WASM component model host, delegation framework) converge.

---

## 3. Project Progress

**Merged/Closed PRs (5 total, visible in top data):**

- **[PR #8101](https://github.com/zeroclaw-labs/zeroclaw/pull/8101) (Merged):** `fix(fill-translations)` — Cleared orphaned `msgstr` continuation lines left behind after leak repair, fixing a data-loss bug where repaired entries remained non-empty.
- **[PR #8285](https://github.com/zeroclaw-labs/zeroclaw/pull/8285) (Merged):** `fix(delegate)` — Intersected the caller's per-agent `allowed_tools`/`excluded_tools` policy at the delegate boundary, closing a critical security gap where a sub-agent could invoke tools the parent forbids.
- **[PR #8313](https://github.com/zeroclaw-labs/zeroclaw/pull/8313) (Open):** `feat(skills)` — Defaults skills to compact injection mode, deprecating full mode. Instructions load on demand via `read_skill`.
- **[PR #8311](https://github.com/zeroclaw-labs/zeroclaw/pull/8311) (Open):** `feat(config)` — Adds a configurable `[runtime].shell` option, allowing users to specify which shell binary the native runtime uses.
- **[PR #8282](https://github.com/zeroclaw-labs/zeroclaw/pull/8282) (Open):** `fix(zerocode)` — Routes key handlers through the action layer in the TUI, enabling rebind overrides.

**Key In-Progress Features (Visible Activity):**
- **[PR #7928](https://github.com/zeroclaw-labs/zeroclaw/pull/7928) (XL, Open):** WASM component-model plugin host targeting `wit` v0 with Channel, Memory, and Tool traits — the single largest code change under review.
- **[PR #7771](https://github.com/zeroclaw-labs/zeroclaw/pull/7771) (L, Open):** Propagates `channel`, `agent_alias`, and `turn_id` to `ObserverEvent` variants for proper OTel trace correlation.
- **[PR #8145](https://github.com/zeroclaw-labs/zeroclaw/pull/8145) (M, Open):** Systematically adds ack reactions and explicit typing stubs across 20+ chat channels.
- **[PR #8033](https://github.com/zeroclaw-labs/zeroclaw/pull/8033) (XL, Open):** Revives `zeroclaw onboard` as a conversational chat-based setup assistant.

---

## 4. Community Hot Topics

The following issues and PRs attracted the most community engagement, revealing deep concerns around production readiness and security:

- **[Issue #5982](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) — Per-sender RBAC (9 comments):** The highest-engagement item. Community is actively scoping how a single ZeroClaw instance can serve isolated operator, customer, and developer classes. This is the top non-negotiable for multi-tenant production deployments.

- **[Issue #7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) — OIDC Authentication (6 comments):** The umbrella tracking issue for v0.9.0 security work (OIDC, SSH key, peercred, native auth). Enterprise users are treating this as a hard requirement for deployment.

- **[Issue #8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) — Supply-Chain Signing & SLSA Provenance (5 comments):** A highly mature RFC. The community is driving for hardware-backed PGP keys, multi-party quorum, and cosign verification as essential trust infrastructure for the plugin ecosystem.

- **[Issue #6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289) — Prompt-triggered Install Suggestions (5 comments):** Strong UX-centric debate. Users want ZeroClaw to automatically suggest and install missing skills when a prompt exposes a capability gap.

- **[PR #7928](https://github.com/zeroclaw-labs/zeroclaw/pull/7928) — WASI Plugin Host (XL, Open):** Generates the most code review traffic. Represents a direct execution of the roadmap to deprecate Extism and move to native `wasmtime` component-model hosting.

**Underlying Need:** The community is actively *productionizing* ZeroClaw. The demands for multi-tenancy (RBAC/OIDC), plugin integrity (signing/WASM sandboxing), and intelligent UX (skill suggestions) all point toward a maturing project ready for enterprise deployment.

---

## 5. Bugs & Stability

Reported bugs ranked by severity. Several high-severity items remain unmerged despite being open for weeks.

### Critical & High Severity (S1/P1)

- **[Issue #8151](https://github.com/zeroclaw-labs/zeroclaw/issues/8151) (CLOSED, S1):** Matrix deferred image reference lost after cached history. Bot denied seeing an image. **Closed today**, likely a hotfix.
- **[Issue #5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903) (P1, Open since April):** MCP stdio child processes accumulate on every heartbeat tick (estimate: 48 orphans/day). Severe resource leak. **No fix PR attached yet.** High complexity perhaps delaying resolution.
- **[Issue #8044](https://github.com/zeroclaw-labs/zeroclaw/issues/8044) (P1):** `/model --agent` scope has **no per-sender authorization**. Any channel user can change the agent's global model. High security bypass.
- **[Issue #7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733) (P1):** `mcp_bundles` per-agent scoping is parsed but **silently not enforced at runtime** — a complete null security isolation feature.
- **[Issue #7623](https://github.com/zeroclaw-labs/zeroclaw/issues/7623) (P1, In Progress):** Delegate tool with `requires_openai_auth` **still forwards the coordinator's API key** instead of the sub-agent's. Critical delegation security bug.
- **[Issue #8312](https://github.com/zeroclaw-labs/zeroclaw/issues/8312) (S2, New):** `fill-translations` data-loss bug distinct from #8039. Orphaned translation entries survive the leak-repair.

### Moderate Severity (P2)

- **[Issue #7873](https://github.com/zeroclaw-labs/zeroclaw/issues/7873) (P2):** Telegram media groups dispatched as multiple agent requests instead of one consolidated message.
- **[Issue #5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514) (P2, since April):** Each subsequent image in a Telegram batch accumulates into the next request.
- **[Issue #7737](https://github.com/zeroclaw-labs/zeroclaw/issues/7737) (P2):** Approval attribution uses a channel-global side channel; concurrent approvals can overwrite each other.
- **[Issue #8232](https://github.com/zeroclaw-labs/zeroclaw/pull/8232) (Open):** Fixes `replay_assistant_reasoning` export breaking multi-turn tool loops on Groq.

### Fix PRs Active

- **#8284 / #8285** — Closing the delegate tool gating gap.
- **#8145** — Fixing channel ack/typing across 20+ channels.
- **#7723 / #7958** — Fixing Telegram `mention_only` gate blocking bot replies.
- **#7485 / #8084** — Fixing Doctor false positives for custom providers.

---

## 6. Feature Requests & Roadmap Signals

### Strong Roadmap Signals (Likely v0.9.0 or Immediate)

- **OIDC & RBAC ([#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141), [#5982](https://github.com/zeroclaw-labs/zeroclaw/issues/5982))**: These are the top infrastructure priorities. The `AuthProvider` seam is being laid with children for OIDC, local password auth ([#8076](https://github.com/zeroclaw-labs/zeroclaw/issues/8076)), SSH key, and peercred.
- **OpenRouter Model Fallback ([#8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138))**: Two competing PRs ([#8141](https://github.com/zeroclaw-labs/zeroclaw/pull/8141), [#8207](https://github.com/zeroclaw-labs/zeroclaw/pull/8207)) suggest this will land very soon to support native OpenRouter `models` arrays for automatic failover.
- **Delegated Agent Modes ([#8238](https://github.com/zeroclaw-labs/zeroclaw/issues/8238), [#7743](https://github.com/zeroclaw-labs/zeroclaw/issues/7743))**: Demand for independent delegation where the sub-agent runs under its own policy and toolset.
- **WASM Plugin Overhaul**:
    - **[#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135):** Wasm-first plugin runtime (default-on, capability enforcement).
    - **[#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497):** OCI-compliant registries for plugin storage and discovery.
    - **[#7928](https://github.com/zeroclaw-labs/zeroclaw/pull/7928):** First component-model plugin host code.
    - **[#8187](https://github.com/zeroclaw-labs/zeroclaw/issues/8187):** Capability-gated WASI hardware host functions (IoT/Edge AI signal).

### Emerging / Speculative

- **Cron Pre-Hooks ([#5607](https://github.com/zeroclaw-labs/zeroclaw/issues/5607), Blocked):** Lightweight precondition gates for cron jobs. Users want skip-on-exit-10 behavior without a failure alert.
- **"Everything is a Plugin" ([#6489](https://github.com/zeroclaw-labs/zeroclaw/issues/6489)):** Grand vision to unify channels, providers, and integrations under a single plugin catalog. Currently low activity but defines the project's long-term north star.
- **In-App Upgrade ([#8173](https://github.com/zeroclaw-labs/zeroclaw/pull/8173)):** PR adds detect → show notes → apply → restart flow from the web dashboard.

---

## 7. User Feedback Summary

### Pain Points & Dissatisfaction

- **Security Isolation Gaps:** Users are directly hitting walls. "MCP scoping is a silent no-op" ([#7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733) by `metalmon`) and "Delegate API key still leaks" ([#7623](https://github.com/zeroclaw-labs/zeroclaw/issues/7623) by `shahar3000`) represent critical trust issues in multi-tenant or multi-agent setups.
- **Telegram UX Fragility:** Consistent pain around media groups ([#7873](https://github.com/zeroclaw-labs/zeroclaw/issues/7873)), image accumulation ([#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514)), and mention-only gates blocking replies ([#5866](https://github.com/zeroclaw-labs/zeroclaw/issues/5866), fixed by #7723/#7958). Users want polished group chat behavior.
- **OpenRouter Limitations:** Users cannot access native model failover arrays, impacting reliability and cost management ([#8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138) by `vinitasher`).

### Use Cases & Requests

- **Enterprise/SaaS:** OIDC, RBAC, and supply chain signing dominate. Users are clearly planning multi-tenant hosted deployments.
- **Infrastructure Control:** Request for configurable shell binary ([#8311](https://github.com/zeroclaw-labs/zeroclaw/pull/8311), ref #5246) shows power users want deeper runtime customization.
- **Plugin Ecosystem Growth:** There is strong desire for skill auto-discovery ([#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289)), WASM-based distribution ([#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497)), and hardware access ([#8187](https://github.com/zeroclaw-labs/zeroclaw/issues/8187)).

---

## 8. Backlog Watch

### Needs Maintainer Review
These RFCs and features represent the next wave of major decisions awaiting core maintainer sign-off:

- **[Issue #8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177):** Supply chain signing (SLSA, hardware PGP, cosign). A mature RFC needing final approval.
- **[Issue #7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497):** OCI registries for plugin storage. Deep architectural impact.
- **[Issue #8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138):** OpenRouter fallback config. Two competing implementations need a maintainer to pick a direction.
- **[Issue #8187](https://github.com/zeroclaw-labs/zeroclaw/issues/8187):** Capability-gated WASI hardware functions.
- **[Issue #8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135):** Wasm-first default-on runtime.

### Needs Author Action

- **[Issue #8226](https://github.com/zeroclaw-labs/zeroclaw/issues/8226):** Per-agent custom environment variables. Blocked pending author follow-up (`susyabashti`).

### Long-Standing Critical Items

- **[Issue #5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903) (P1, since April 2026):** MCP orphan process accumulation. It is unusual for a P1 resource leak to remain unmerged this long; it likely involves significant refactoring of the MCP process lifecycle.
- **[Issue #5607](https://github.com/zeroclaw-labs/zeroclaw/issues/5607) (P2, since April, Status: Blocked):** Pre-hook skip gates for cron jobs. A high-value feature stuck on upstream dependencies.
- **[Issue #6489](https://github.com/zeroclaw-labs/zeroclaw/issues/6489):** "Everything is a plugin" — the north star architecture. Low immediate activity but strategically critical.

### Project Health Assessment
Maintainers (`Audacity88`, `singlerider`, `JordanTheJet`, `ConYel`, `bheatwole`, `metalmon`) are highly responsive, quickly labeling, prioritizing, and assigning. The sheer volume of P1 security bugs and large architectural RFCs suggests the team is operating at peak capacity. The focus on security and plugin infrastructure indicates a project maturing rapidly from a single-user tool toward a production-grade multi-tenant platform.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*