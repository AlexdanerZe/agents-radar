# OpenClaw Ecosystem Digest 2026-06-26

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-26 03:23 UTC

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

Here is the project digest for **OpenClaw** on **2026-06-26**.

---

### 1. Today’s Overview
The OpenClaw project remains extremely active, with **500 issues** and **500 pull requests** updated in the last 24 hours. While **94 PRs** were merged or closed, **477 open issues** and **406 open PRs** reveal a heavy and growing backlog. No new releases were published today, indicating the team is in a stabilization and bug-fix cycle rather than a feature launch. The most energy is concentrated on critical stability problems—specifically memory leaks, context overflow handling, and channel delivery reliability—with a disproportionate number of the highest-severity (“Diamond Lobster” / “Platinum Hermit”) items still awaiting maintainer review.

### 2. Releases
**No new releases were tagged on 2026-06-26.**

### 3. Project Progress
Despite the backlog, the **94 closed/merged PRs** represent real forward motion across several fronts:

- **Security hardening of external integrations:** A coordinated wave of “bound response reads” fixes protects against OOM from untrusted endpoints.  
  – PR [#96886](https://github.com/openclaw/openclaw/pull/96886) (fix: fal)  
  – PR [#96904](https://github.com/openclaw/openclaw/pull/96904) (fix: together, pixverse)  
  – PR [#96920](https://github.com/openclaw/openclaw/pull/96920) (fix: google-media)

- **Channel reliability fixes:**  
  – PR [#72513](https://github.com/openclaw/openclaw/pull/72513) was closed, fixing Mattermost `post_edited` websocket events that caused ignored @mentions.  
  – PR [#95903](https://github.com/openclaw/openclaw/pull/95903) advances a fix for oversize Telegram markdown chunks that exceed the 4096-char API limit.

- **Developer tooling:**  
  – PR [#96544](https://github.com/openclaw/openclaw/pull/96544) was merged, fixing `openclaw doctor --fix` key collisions in model-ref maps.  
  – PR [#69346](https://github.com/openclaw/openclaw/pull/69346) progresses actionable diagnostics for empty-stream config errors in the embedded runner.

- **Cron and automation:**  
  – PR [#94849](https://github.com/openclaw/openclaw/pull/94849) fixes a cron dispatch blind spot where recovered agentTurn tool warnings suppressed legitimate output.

### 4. Community Hot Topics
The most engaged issues and PRs reveal deep frustration and high expectations around agent-state fidelity and long-session stability.

- **Agent trust & false promises**  
  Issue [#58450](https://github.com/openclaw/openclaw/issues/58450) (*Agent can promise a later follow-up without starting any action*) remains one of the hottest threads, with **15 comments** and **3 👍**. Users view the discrepancy between “what the agent says” and “what the agent does” as a fundamental trust break.  
  – *Related:* [#50165](https://github.com/openclaw/openclaw/issues/50165) (subagents appearing finished before work is done).

- **Context overflow death spiral**  
  Issue [#63216](https://github.com/openclaw/openclaw/issues/63216) (repeated hard resets despite high `reserveTokensFloor`) draws **11 comments** and **3 👍**. Community members report that the system becomes unusable under moderate conversational load, with Bootstrap files consuming 20–30% of the token budget on every turn (see issue [#67419](https://github.com/openclaw/openclaw/issues/67419)).

- **ClawHub security impasse**  
  Issue [#50090](https://github.com/openclaw/openclaw/issues/50090) (*Community Skill Development & ClawHub*) is the longest-running feature discussion, now at **15 comments**. The community is eager for the skills ecosystem but increasingly frustrated by the stalled security review.

- **Telegram message loss**  
  Issue [#64810](https://github.com/openclaw/openclaw/issues/64810) (*Heartbeat swallows Telegram replies*) is a vivid example of a broader concern: system events preempting user-facing messages on mobile channels.

### 5. Bugs & Stability
Stability is under serious strain. The highest-severity cluster involves memory growth, context reset loops, and security boundaries.

| Severity | Issue | Summary |
|---|---|---|
| **CRITICAL / Crash** | [#55334](https://github.com/openclaw/openclaw/issues/55334) | `sessions.json` unbounded growth → gateway OOM (~50–100 MB/min). |
| **CRITICAL / Crash** | [#54155](https://github.com/openclaw/openclaw/issues/54155) | Gateway memory leak 389MB → 14.7GB over 4 days. |
| **CRITICAL / Crash-Loop** | [#63216](https://github.com/openclaw/openclaw/issues/63216) | Unstoppable hard-reset retry loop; flush & compaction insufficient. *[Fix PR needed]* |
| **CRITICAL / Security** | [#65624](https://github.com/openclaw/openclaw/issues/65624) | Mattermost cleartext callback URLs expose reusable tokens (CVSS 8.6). *[Fix PR waiting: #64546]* |
| **HIGH / Data Integrity** | [#58450](https://github.com/openclaw/openclaw/issues/58450) | Agent promises action but never executes; user-facing hallucination. |
| **HIGH / Message Loss** | [#64810](https://github.com/openclaw/openclaw/issues/64810) | Heartbeat/system events interrupt and bury in-progress Telegram replies. |
| **HIGH / Regression** | [#53599](https://github.com/openclaw/openclaw/issues/53599) | Chrome extension relay removed without cross-machine replacement. *[5 👍, strong reg.]* |
| **HIGH / State Loss** | [#66443](https://github.com/openclaw/openclaw/issues/66443) | Overflow recovery duplicates `role=user` messages, amplifying the transcript. |
| **MEDIUM / Data Loss** | [#50093](https://github.com/openclaw/openclaw/issues/50093) | WhatsApp silently drops messages sent during reconnection windows. |

**Key takeaway:** A **coordinated fix PR push is emerging** for the memory/overflow issues, but the `needs-maintainer-review` bottleneck means most of these are not yet resolved.

### 6. Feature Requests & Roadmap Signals
The community is signaling a clear desire for a more robust, enterprise-grade architecture.

- **Memory architecture overhaul** – Multiple RFCs and features point to replacing the single-memory-slot model:  
  – [#60572](https://github.com/openclaw/openclaw/issues/60572) *Multi-Slot Memory Architecture* (3 👍)  
  – [#63990](https://github.com/openclaw/openclaw/issues/63990) *Multi-index embedding memory with model-aware failover*  
  – [#54373](https://github.com/openclaw/openclaw/issues/54373) *Context Provenance metadata*  

- **Security infrastructure** – Features requested for compliance-heavy use cases:  
  – [#56349](https://github.com/openclaw/openclaw/issues/56349) *Unbypassable outbound policy enforcement*  
  – [#64046](https://github.com/openclaw/openclaw/issues/64046) *Sensitive data masking in logs, config, and UI*  
  – [#64438](https://github.com/openclaw/openclaw/issues/64438) *Remote Reranker Endpoint support*  

- **Channel UX** – Users want persistent state for long-running turns ([#52640](https://github.com/openclaw/openclaw/issues/52640)) and per-agent voice configuration ([#66252](https://github.com/openclaw/openclaw/issues/66252)).

- **Provider resilience** – PR [#64127](https://github.com/openclaw/openclaw/pull/64127) (*Provider circuit breaker for quota exhaustion*) is a strong candidate for the next patch release, addressing a common production pain point.

### 7. User Feedback Summary
The sentiment is polarized between deep frustration with current instability and strong long-term commitment.

- **Pain points users are loudest about:**
  - **Memory death spirals:** “Sessions blow up after a few dozen turns with no warning.”
  - **False agent promises:** “The agent says ‘I’ll check this’ and then does nothing—this breaks my users’ trust.”
  - **Channel dropouts:** “Messages to Telegram just vanish when a heartbeat fires.”
  - **Hardcoded developer paths:** Issue [#51429](https://github.com/openclaw/openclaw/issues/51429) (“Someone hardcoded their working path and it was merged”) generated strong angry-reactions, though it was quickly flagged.

- **Satisfaction drivers:**
  - **High fix throughput:** “94 PRs closed in one day shows the team is listening.”
  - **Quality of bug reports:** Users are providing detailed CVSS vectors, CPU/memory profiles, and reproducible test cases.
  - **Long-term vision:** The number of ambitious RFCs (multi-session, context provenance) suggests users are heavily invested despite the friction.

### 8. Backlog Watch
A growing number of high-impact items are stuck in the `needs-maintainer-review` and `needs-product-decision` states, creating a dangerous bottleneck for the project’s trajectory.

| Priority | Issue/PR | Age | Concern |
|---|---|---|---|
| **BLOCKING** | [#50090](https://github.com/openclaw/openclaw/issues/50090) – ClawHub security | Opened Mar 19 | **No product decision in 3 months.** The entire skills ecosystem is frozen. |
| **CRITICAL** | [#45740](https://github.com/openclaw/openclaw/issues/45740) – gh-issues prompt injection | Opened Mar 14 | Linked fix PR exists. Attack vector is live. |
| **CRITICAL** | [#65624](https://github.com/openclaw/openclaw/issues/65624) – Mattermost token exposure | Opened Apr 13 | Fix PR [#64546](https://github.com/openclaw/openclaw/pull/64546) is in `waiting on author`. High CVSS. |
| **REGRESSION** | [#53599](https://github.com/openclaw/openclaw/issues/53599) – Chrome ext. removal | Opened Mar 24 | 5 👍, no clear resolution path. |
| **STALLED** | [#11665](https://github.com/openclaw/openclaw/issues/11665) – Webhook multi-turn sessions | Opened Feb 8 | The oldest active high-traffic issue. Updated regularly but stuck on `needs-product-decision`. |

**Summary for maintainers:** The project is at a critical inflection point. The volume of community contribution is healthy, but the **15+ open items with `needs-maintainer-review`** labels—combined with severe memory and crash-loop bugs—threatens to overwhelm the review pipeline. **Immediate triage attention is recommended for the Mattermost security vulnerability (#65624 / #64546) and the prompt injection vector (#45740 / linked PR).**

---

## Cross-Ecosystem Comparison

## Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Analysis Date:** 2026-06-26
**Scope:** 13 tracked projects, 9 with measurable activity

---

### 1. Ecosystem Overview

The open-source personal AI agent landscape on June 26, 2026 is defined by a collective sprint toward reliability and production hardening, moving past the initial prototype phase. Activity is concentrated in a handful of high-velocity projects—OpenClaw, ZeroClaw, Hermes Agent, and CoPaw—while several smaller or specialized projects remain dormant. A universal demand for robust memory management, strict security policy engines, and flawless multi-platform channel delivery cuts across every active project. Despite widespread frustration with stability regressions and context death spirals, community engagement remains remarkably deep, driven by technically sophisticated users who are heavily invested in the long-term architecture of autonomous AI systems.

---

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | PRs Merged/Closed | Release Status | Health Signal |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 94 | None | High volume, severe backlog, stability crisis |
| **ZeroClaw** | 43 | 50 | 4 | v0.8.2 bump merged | Deep RFC culture, low merge ratio, intense dev |
| **Hermes Agent** | 50 | 50 | 14 | None | Post-release triage, responsive patch cycle |
| **CoPaw (QwenPaw)** | 25 | 50 | 21 | None | Post-migration churn, high community trust |
| **IronClaw** | 50 | 50 | 18 | None (v2 prep) | Heavy feature dev, critical UX gaps unaddressed |
| **NanoBot** | 25 | 40 | 15 | None (patching) | Excellent security response velocity |
| **PicoClaw** | 3 | 19 | 6 | None | Targeted fixes, efficient maintainer engagement |
| **NanoClaw** | 1 | 16 | 11 | None | Highest merge ratio, disciplined feature delivery |
| **LobsterAI** | 1 | 8 | 8 | None | Clean stabilization cycle, minimal bugs |
| **NullClaw / TinyClaw / Moltis / ZeptoClaw** | 0 | 0 | 0 | None | Dormant—no community signal |

**Key Observations:**
- **NanoClaw** leads in execution efficiency (69% merge rate)
- **OpenClaw** dominates raw volume but shows the most concerning stability profile
- **ZeroClaw** shows the deepest architectural discourse but a low daily merge ratio
- 4 of 13 tracked projects show zero activity, indicating consolidation or abandonment

---

### 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Largest community by order of magnitude**—500 issues and 500 PRs updated in 24 hours, dwarfing the 50-item scale of Tier 2 projects. It functions as the de facto "Linux of AI Agents" and reference implementation for the ecosystem.
- **Broadest scope and channel coverage**—Mattermost, Telegram, WhatsApp, Chrome extension, and extensive provider integrations provide the widest integration surface.
- **Rich ecosystem ambition**—ClawHub, Skill Development, and RFC processes signal a platform-level vision that other projects are still building toward.

**Technical Approach Differences:**
- OpenClaw operates as a deeply integrated monolithic system. It prioritizes configuration flexibility and maximum capability over architectural purity. This stands in contrast to ZeroClaw's modular WASM-runtime approach, IronClaw's API-first v2 architecture, or NanoBot's lean, security-hardened Python stack.
- The cost of this flexibility is evident: OpenClaw carries the worst stability profile in the ecosystem (OOM loops, context death spirals, critical security vulnerabilities), while smaller competitors are shipping cleaner, more predictable experiences.

**Community Size Comparison:**
OpenClaw's absolute engagement dwarfs all peers, but the ratio of community contribution to maintainer review is severely imbalanced (15+ items stuck on `needs-maintainer-review`). Peer projects like NanoClaw and NanoBot demonstrate that a smaller, more involved community with a higher maintainer-to-contributor ratio can deliver superior stability outcomes. OpenClaw risks fragmentation if the perception of unmaintained regressions persists.

---

### 4. Shared Technical Focus Areas

**1. Memory & Context Explosion Management**
Every active project has significant open work on this. The standard single-context-window model is failing under real-world usage.
- OpenClaw (#63216, #60572, #63990) — context death spirals, multi-slot memory RFCS
- Hermes Agent (#38240, #39691) — token bloat watchdog, compression proposals
- IronClaw (#5260, #5264) — model memory as userland extension, native SQL storage
- CoPaw (#5321) — SQLite-backed scroll context with recall REPL
- NanoBot (#4402) — eager memory consolidation PR
- **Core Requirement:** Durable, indexed, multi-slot memory with provenance that survives session boundaries.

**2. Security Hardening & Policy Engines**
The community uniformly demands provable, unbypassable security boundaries.
- NanoBot — 8 critical MCP/exec bypass disclosures resolved in 24 hours
- ZeroClaw (#8279) — S0 delegate tool allowlist bypass closed immediately
- IronClaw (#5261 Epic) — capability policy, multi-user auth, admin REST surface
- OpenClaw (#56349, #64046, #50090) — policy enforcement, data masking, ClawHub security
- **Core Requirement:** Admin-enforced, runtime-enforced, deny-by-default authorization on tools, delegation, and outbound connections.

**3. Channel Reliability & UX Parity**
Silent failure of messages on mobile and desktop channels is a universal pain point.
- OpenClaw (#64810) — Telegram heartbeat swallows messages
- Hermes Agent (#28004) — Telegram typing indicator stuck
- NanoClaw (#2471, #2472) — Slack threading and session isolation merged
- PicoClaw (#3044) — Matrix identity parsing regression fixed
- **Core Requirement:** Reliable delivery guarantees, rich formatting parity (blocks, cards, files), and per-channel session management.

**4. Multi-Agent Orchestration & Governance**
Teams are demanding flexible, secure delegation patterns.
- ZeroClaw (#8238, #8303) — independent delegate mode, durable goal mode
- CoPaw (#5523) — subagent tool discovery regression in runtime 2.0
- LobsterAI (Cowork Mode) — multi-agent plan mode with subagent polling
- IronClaw (#5261) — user roles, availability resolver, policy delta store
- **Core Requirement:** Escalatable, auditable, policy-governed delegation to sub-agents.

---

### 5. Differentiation Analysis

| Project | Core Strength | Target User | Architecture | Key Differentiator |
|---|---|---|---|---|
| **OpenClaw** | Broadest ecosystem & largest community | Power users, tinkerers | Heavy monolith, configuration-driven | "Standard Library" of AI agents—huge scope but high complexity |
| **ZeroClaw** | Architectural rigor & R&D velocity | Developers, architects | Rust/WASM runtime, RFC-driven | "Cloud Native Agent" with supply-chain signing & durable sessions |
| **Hermes Agent** | Integrated desktop/TUI UX | End users, desktop operators | Python + Electron/TUI | "Desktop-first AI companion" with strong security boundaries |
| **NanoClaw** | Feature execution efficiency | Operations power users | Python, clean codebase | Highest feature velocity per contributor, disciplined execution |
| **IronClaw** | Enterprise governance | Teams, organizations | Python, V2 API | "Enterprise Agent Platform"—capability policies, multi-tenant |
| **CoPaw (QwenPaw)** | OS-level automation | Browser/desktop developers | Python, AgentScope runtime | "Screen/System Agent" specialist—Windows desktop automation |
| **NanoBot** | Security response & hardening | Security researchers | Modular Python | Fastest incident response cycle in the ecosystem |
| **LobsterAI** | Research-focused multi-agent | Researchers | Python | Cowork planning mode, rigorous plan-mode engineering |
| **PicoClaw** | Lightweight & efficient | Matrix/decentralization users | Go | Minimal footprint, strong CLI, focused channel support |

---

### 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating / Pre-Release (High Risk, High Reward)**
- **OpenClaw:** Titanic community effort with the largest absolute engagement. However, the severity of critical backend bugs (OOM, context death spirals) combined with a strained review pipeline threatens contributor retention. Momentum is high but fragile.
- **ZeroClaw:** Exceptional architectural discourse (RFC culture). v0.8.2 bump merged; Wasm plugin runtime and goal mode signal a maturing platform. Review bottleneck is the primary risk.
- **CoPaw (QwenPaw):** High churn following the AgentScope 2.0 migration. Community trust is demonstrated by first-time contributors filing production-quality PRs. Stability is catching up to feature scope.

**Tier 2: Consolidating & Hardening**
- **NanoBot:** Delivered a masterclass in rapid security incident response. The 24-hour triage of 8 critical bypass disclosures is the benchmark for the industry. Poised for a v0.2.2 security patch.
- **Hermes Agent:** Aggressively correcting regressions from the latest build release. Gateway session reliability and desktop build fragility are the core focus areas.
- **IronClaw:** Deep in the v2 Reborn feature cycle, but internal dogfooding reveals critical UX gaps (approval flow broken, automation non-functional). Enterprise delivery timeline is at risk if these are not prioritized.

**Tier 3: Steady State / Healthy Velocity**
- **NanoClaw:** Highest execution discipline in the ecosystem. Low issue formation, high merge rate. The model for a healthy, scalable open-source agent project.
- **PicoClaw:** Efficient Go project with strong maintainer engagement. Targeted releases with clear scope (Matrix identity fix, Evolution token drain).
- **LobsterAI:** Clean stabilization cycle. Focused entirely on hardening the Cowork mode and plugin sandbox before the next release.

**Tier 4: Inactive / Dormant**
- NullClaw, TinyClaw, Moltis, ZeptoClaw: No activity across any signal. Risk of archival or abandonment. Contributes to ecosystem fragmentation but reduces competition for the active projects.

---

### 7. Trend Signals

**1. Security is the Gatekeeper to Production**
The wave of high-severity disclosures (NanoBot's 8 critical bypasses, ZeroClaw's S0 delegate exploit, OpenClaw's unfixed Mattermost token exposure) combined with the rise of dedicated policy engines (IronClaw Epic, ZeroClaw RFCs) sends a clear signal: **unbypassable authorization layers are the #1 prerequisite for production deployment.** Projects without this are being actively relegated to "toy" status by operations and security teams. The community is no longer forgiving of security regressions.

**2. Memory Management is the Next Competitive Frontier**
The universal "context death spiral" and the variety of proposed solutions (multi-slot memory, SQLite-backed scroll, eager consolidation, model-aware failover) indicate that **solving long-term, structured memory is the single biggest UX unlock.** The project that ships a clean, durable, efficient memory system will establish a decisive competitive moat over projects still relying on single-context-window hacks.

**3. The Convergence of Chat and Ops**
Features like IronClaw's Capability Policy, ZeroClaw's Goal Mode, and NanoClaw's admin approvals/container resource limits blur the line between a chatbot and an infrastructure platform. **Users demand agents that are simultaneously delightful to chat with and rigorously manageable like a cloud service.** The agent-as-a-platform (IronClaw) vs. agent-as-tool (NanoBot) split is widening.

**4. Channel Parity over Model Parity**
The majority of high-severity bugs this week had nothing to do with models. They were about Telegram message loss, Slack thread handling, Matrix identity parsing, and DingTalk formatting. **The real engineering moat is moving from reasoning quality to channel reliability.** The model is becoming a commodity; the integration surface is the differentiator. Users will choose the agent that works reliably everywhere they already live.

**5. From Interactive Q&A to Autonomous Background Workers**
Goal Modes, Cron Schedulers, automated skill pipelines (ClawHub, SkillForge), and subagent governors (ZeroClaw, IronClaw) show the community pushing agents from "conversational assistants" to **"background autonomous workers."** The demand for durable execution, retry policies, and admin oversight of scheduled tasks is rising sharply, pointing toward agent-as-microservice architectures becoming mainstream.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest | 2026-06-26

## 1. Today's Overview
Project activity surged today driven by a rapid security disclosure and response cycle. A security researcher systematically disclosed eight critical vulnerabilities targeting the MCP integration and `exec` tool allowlists, dominating the update feed. The maintainers demonstrated exceptional incident response velocity, closing the majority of these high-severity issues within 24 hours. Overall, **25 issues were updated (19 closed)** and **40 PRs saw activity (15 merged/closed)**. No new releases were cut today, strongly indicating that the project is consolidating incoming patches for an imminent security point release.

---

## 2. Releases
**No new releases today.** The current stable version is v0.2.1 (as referenced in several closed issues). Given the volume of critical fixes rolling in—exec allowlist bypasses, MCP scope filtering errors, and login shell secrets leakage—an emergency patch release (v0.2.2 or v0.3.0) is expected in the coming days.

---

## 3. Project Progress
**Merged/Closed PRs (15 total, key highlights):**
- **Security — Filesystem Boundaries:** [#4099](https://github.com/HKUDS/nanobot/pull/4099) was merged, enforcing that `extra_allowed_dirs` are strictly read-only for write tools (fixes [#4073](https://github.com/HKUDS/nanobot/issues/4073)).
- **Security — MCP Scope:** Multiple researcher disclosures regarding the `enabledTools` filter failing to restrict Resources and Prompts ([#4434](https://github.com/HKUDS/nanobot/issues/4434), [#4435](https://github.com/HKUDS/nanobot/issues/4435), [#4517](https://github.com/HKUDS/nanobot/issues/4517), [#4519](https://github.com/HKUDS/nanobot/issues/4519)) were closed. A fix was prototyped in [#4524](https://github.com/HKUDS/nanobot/pull/4524).
- **Security — Exec Bypass:** Multiple `exec.allowPatterns` bypass vectors (chained commands, comment tails, wrapper prefixes) were closed ([#4514](https://github.com/HKUDS/nanobot/issues/4514), [#4515](https://github.com/HKUDS/nanobot/issues/4515), [#4516](https://github.com/HKUDS/nanobot/issues/4516), [#4520](https://github.com/HKUDS/nanobot/issues/4520)).
- **Bug Fix:** Xiaomi MiMo ASR transcription failure fixed via frontend WebM→WAV conversion ([#4493](https://github.com/HKUDS/nanobot/pull/4493), fixes [#4492](https://github.com/HKUDS/nanobot/issues/4492)).

**Features in Progress (Open PRs Updated Today):**
- Gateway webhook trigger system ([#4502](https://github.com/HKUDS/nanobot/pull/4502))
- PWA support and mobile swipe gestures for WebUI ([#4494](https://github.com/HKUDS/nanobot/pull/4494))
- Nested subdirectory organization for skills ([#4504](https://github.com/HKUDS/nanobot/pull/4504))
- Opt-in eager memory consolidation ([#4402](https://github.com/HKUDS/nanobot/pull/4402))
- Extra `bwrap` bind roots for exec sandboxing ([#4404](https://github.com/HKUDS/nanobot/pull/4404))
- MCP server idle timeout auto-kill ([#4506](https://github.com/HKUDS/nanobot/pull/4506))

---

## 4. Community Hot Topics
1. **Systemic Security Audit (YLChen-007)**
   A single researcher filed a barrage of deep architectural security issues against MCP trust boundaries and the exec tool's pattern-based allowlist. The issues received few comments but represent the most significant structural scrutiny the project has faced. The underlying community need is clear: a shift from regex/allowlist patterns toward a hardened, deny-by-default, principal-of-least-privilege security model for tool execution and MCP capability exposure.

2. **Historical Supply Chain Trust (Issue [#2439](https://github.com/HKUDS/nanobot/issues/2439))**
   The discussion around the `litellm_init.pth` malicious code incident continues to draw reactions (6 comments, 4 👍). This reflects enduring community vigilance and a demand for radical transparency and auditing verification regarding past supply chain incidents.

---

## 5. Bugs & Stability (Ranked by Severity)

**Critical**
- **`exec.allowPatterns` Whitelist Bypasses:** Multiple methods (chaining, comment-tails, wrapper prefixes) to bypass command sandboxing. Fixes already deployed.
- **MCP `enabledTools` Scope Bypass:** Allowlist fails to restrict Resources and Prompts, exposing the full MCP server surface. Fixes already deployed.

**High**
- **Login Shell Execution Leaks Secrets:** [#4518](https://github.com/HKUDS/nanobot/issues/4518) – Exec tool defaults to sourcing `~/.bash_profile`, re-exposing secrets to the agent. **Open; fix PR** [#4525](https://github.com/HKUDS/nanobot/pull/4525) under review.
- **Shell-Chain Allowlist Bypass:** [#4521](https://github.com/HKUDS/nanobot/issues/4521) – Remaining exec bypass vector via shell chaining. **Open; fix PR** [#4526](https://github.com/HKUDS/nanobot/pull/4526) under review.

**Medium**
- **Windows Service/Background Process Glitches:** ([#4511](https://github.com/HKUDS/nanobot/issues/4511), [#4513](https://github.com/HKUDS/nanobot/issues/4513)) – Restarting the gateway when run via `nssm` or `--background` causes port conflicts and inconsistent process tracking.
- **Telegram Web Rich Message Regression:** ([#4488](https://github.com/HKUDS/nanobot/issues/4488)) – Recent rich text features cause "unsupported message" errors on Telegram Web.

**Low**
- **DingTalk Timeout/Formatting:** ([#4497](https://github.com/HKUDS/nanobot/issues/4497)) – HTTP timeouts and unsupported rich text fields in DingTalk integration.

---

## 6. Feature Requests & Roadmap Signals

**Imminent (v0.2.2):** Security hardening of MCP scoping, exec sandboxing (fullmatch pattern evaluation), and default login-shell behavior.

**Likely for Next Major Release (v0.3.0):**
- **Infrastructure:** Gateway Webhooks ([#4502](https://github.com/HKUDS/nanobot/pull/4502)) represent a major leap in extensibility. MCP server idle timeout ([#4506](https://github.com/HKUDS/nanobot/pull/4506)) addresses desktop resource leaks from zombie processes.
- **UX/Platform:** PWA support and mobile gestures ([#4479](https://github.com/HKUDS/nanobot/issues/4479) / [#4494](https://github.com/HKUDS/nanobot/pull/4494)) are strongly requested for mobile users. Skills in subdirectories ([#4504](https://github.com/HKUDS/nanobot/pull/4504)) improve organization for power users.
- **Agent Capabilities:** Proposals for a formal `ask_clarification` tool ([#4508](https://github.com/HKUDS/nanobot/issues/4508)) and configurable subagent tool error behavior point to a push for robust, human-in-the-loop interactions. Eager memory consolidation ([#4402](https://github.com/HKUDS/nanobot/pull/4402)) reduces token waste.
- **Provider Flexibility:** Custom provider thinking parameters ([#4429](https://github.com/HKUDS/nanobot/issues/4429)) and support for non-OpenAI reasoning models reflect growing adoption beyond the default ecosystem.

---

## 7. User Feedback Summary
- **Security Confidence is the Dominant Theme:** The wave of bypass disclosures has validated user concerns about pattern-based allowlists. The maintainers' rapid 24-hour triage cycle (7 critical issues closed within a day) sends a strong positive signal, but the community will expect a formal post-mortem and hardened architecture.
- **Windows Deployment Friction:** Users (Quincy-Zh) report significant pain points deploying Nanobot as a Windows service (`nssm`) and managing background processes. This is a clear platform gap for enterprise adoption.
- **Telegram/Web Parity:** The regression for Telegram Web users highlights a need for better multi-platform testing of rich UI features.
- **Positive Maintenance Velocity:** Despite the heavy bug load, the rapid opening of fix PRs in direct response to every disclosure demonstrates strong maintainer engagement and project responsiveness.

---

## 8. Backlog Watch
- **[PR #4441](https://github.com/HKUDS/nanobot/pull/4441) — MCP Reconnect Crash (Unreviewed):** Addresses a `RuntimeError` crash in the gateway during MCP server reconnections (`streamable_http`). Open since 2026-06-21 with **zero maintainer comments**. This is a blocking stability issue for all users relying on MCP servers.
- **[PR #4533](https://github.com/HKUDS/nanobot/pull/4533) — Session Key Collision (Unreviewed):** Fixes a disk collision where different session keys (e.g., `telegram:a_b` vs `telegram:a:b`) map to the same file. Impacts data integrity for multi-platform deployments.
- **[PR #4534](https://github.com/HKUDS/nanobot/pull/4534) — Agent Verification Gates (Unreviewed):** A large architectural addition introducing verification gates and provider recovery. Needs architectural review.
- **[Issue #4508](https://github.com/HKUDS/nanobot/issues/4508) — `ask_clarification` Tool (No Comments):** A clean, well-scoped feature proposal with no maintainer engagement yet. High potential value for improving agent robustness on ambiguous inputs.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for June 26, 2026.

---

## Hermes Agent Project Digest — 2026-06-26

### 1. Today's Overview
Project velocity is exceptionally high today, with **100 items (50 Issues + 50 PRs) updated in the last 24 hours**. This level of activity strongly indicates a post-release stabilization sprint, as the team rapidly triages regressions introduced by recent merges. **14 issues were closed** alongside aggressive PR submissions targeting gateway session reliability, desktop build tooling, and security fixes. While the project is clearly in a volatile patch cycle, the maintenance response is strong.

### 2. Releases
No new versions were published today.

### 3. Project Progress
Today’s work focused heavily on damage control and core stability improvements:

- **Desktop Crash Triage:** A critical launch crash caused by an un-bundled `simple-git` dependency (NousResearch/hermes-agent Issue #52735) was swiftly triaged and closed. Related reports on Windows (NousResearch/hermes-agent Issue #52753) and the systemic build issue (NousResearch/hermes-agent Issue #52764) were addressed.
- **Gateway Session Reliability:** Multiple PRs were opened to fix state corruption: Prune stale `sessions.json` entries on startup (NousResearch/hermes-agent PR #52808), clear stale `resume_pending` markers (NousResearch/hermes-agent PR #52818), and fix stale DB fields causing prompt cache misses (NousResearch/hermes-agent PR #52813).
- **Security Patch:** CRITICAL email spoofing vulnerability (GHSA-rxqh-5572-8m77) was patched via SPF/DKIM/DMARC enforcement (NousResearch/hermes-agent PR #52801).
- **Platform & DX:** TUI `/learn` command routing was fixed (NousResearch/hermes-agent PR #52817). WSL2 clipboard and Linux titlebar fixes landed (NousResearch/hermes-agent PR #52819). The long-standing TUI status bar degradation fix (#3291) was finalized.
- **Performance:** Auth store reuse (NousResearch/hermes-agent PR #52438) and lightweight profile listing (NousResearch/hermes-agent PR #52433) were proposed to reduce overhead.

### 4. Community Hot Topics
High comment and reaction counts expose the community’s deepest concerns:

- **Skills Engine & Token Optimization:** The automated Skills Index Watchdog (NousResearch/hermes-agent Issue #38240, 12 comments) and the Headroom-ai compression proposal (NousResearch/hermes-agent Issue #39691, 10 👍) highlight a heavy user focus on reducing token bloat and keeping skills pipelines healthy.
- **Platform Fidelity:** High demand for native message rendering continues with Slack Block Kit (NousResearch/hermes-agent Issue #8552, 9 👍, 8 comments) and Telegram Rich Messages (NousResearch/hermes-agent Issue #44428, 5 👍, 7 comments).
- **Security Design:** The credential proxy daemon discussion (NousResearch/hermes-agent Issue #4656, 11 comments) remains a hot topic as users explore zero-knowledge patterns for sandboxed agents.
- **Regression Sensitivity:** The community is actively tracking feature regressions, notably the broken Dashboard chat (NousResearch/hermes-agent Issue #36658, 8 comments, 2 👍) and the Curator archiving active skills (NousResearch/hermes-agent Issue #29912, 7 comments).

### 5. Bugs & Stability
*Ranked by severity, with fix status:*

**Critical (P0):**
- Resume/Cron messages send stale DB fields, breaking provider prompt caches entirely. **Fix PR #52813 exists.**

**High (P1):**
- Desktop app launch crash (`simple-git` bundling) — **Closed** (NousResearch/hermes-agent Issue #52735, #52753).
- Web/WeChat session history leaks — **Closed** (NousResearch/hermes-agent Issue #49106).
- Gateway cache invalidation stalls Discord heartbeats — **Closed** (NousResearch/hermes-agent Issue #52197).
- Windows Docker terminal backend exposes entire home directory — **Closed** (NousResearch/hermes-agent Issue #48137).
- openai-codex multi-profile token rotation race — **Closed** (NousResearch/hermes-agent Issue #48415).
- Telegram polling gateway silently stops — **Closed** (NousResearch/hermes-agent Issue #48495).
- Email spoofing vulnerability — **Fix PR #52801 exists.**

**Moderate (P2):**
- Windows 10 installer fails at desktop stage (NousResearch/hermes-agent Issue #46260).
- Telegram typing indicator stuck indefinitely (NousResearch/hermes-agent Issue #28004).
- Gateway INSERT omits `active` column (memory loss) (NousResearch/hermes-agent Issue #51646).
- Curator may archive active operational skills (NousResearch/hermes-agent Issue #29912).
- Cron script-path guard rejects profile-scoped jobs (NousResearch/hermes-agent Issue #40801).
- New `hermes update` produces broken Desktop asar (NousResearch/hermes-agent Issue #52764).

### 6. Feature Requests & Roadmap Signals
Today’s requests lean heavily into **release stability and quality-of-life improvements**:

- **Version Management:** Add `--latest-release` flag to `hermes update` to avoid tracking `main` (NousResearch/hermes-agent Issue #52814).
- **System Tray:** Minimize to system tray instead of closing on Windows/Linux (NousResearch/hermes-agent Issue #52787).
- **TUI Status:** Show cron scheduler liveness in the TUI status bar (NousResearch/hermes-agent Issue #52815). A companion PR was already opened (NousResearch/hermes-agent PR #52822).
- **Context Bloat:** Extract contributor docs from `AGENTS.md` to save ~25K tokens per session (NousResearch/hermes-agent Issue #52821).
- **WSL/Linux DX:** Auto-create Linux `.desktop` entry on first launch (NousResearch/hermes-agent Issue #52769).
- **Platform Upgrades:** Feishu Card 2.0 rendering (NousResearch/hermes-agent Issue #46470) and Vertex AI / Gemini provider (NousResearch/hermes-agent PR #8427) remain high-value targets.

**Prediction:** Given the intense focus on `sessions.json`, `resume_pending` markers, and DB field hygiene, the next minor release will likely be branded a **"Gateway State & Session Reliability"** release. Expect the TUI cron indicator and AGENTS.md token fix to land shortly.

### 7. User Feedback Summary
- **Dissatisfaction / Pain Points:**
    - **Build Fragility:** The desktop app is highly vulnerable to dependency changes in `main` (simple-git ASAR error). Users are requesting stable release tags.
    - **Session State Gaps:** Users are frustrated by leaking session histories and silent gateway disconnections requiring full restarts.
    - **Windows/WSL2 Friction:** Persistent installer failures (NousResearch/hermes-agent Issue #46260) and clipboard gaps (NousResearch/hermes-agent PR #52819) make the Windows experience feel incomplete.
    - **Silent Failures:** The cron scheduler and Telegram gateway can stop working without visible indicators.

- **Satisfaction:**
    - **Rapid Triage:** The community widely appreciated the swift response to the P0 desktop crash and P1 security patches.
    - **Security Focus:** Users recognize the project’s investment in agent security boundaries (iron-proxy, credential daemon, email spoofing fix).
    - **Technical Depth:** The quality of discussion in issues like #4656 and #29912 shows a highly sophisticated user base contributing design-level feedback.

### 8. Backlog Watch
Several high-impact or high-risk items remain stalled without recent maintainer action:

- **Credential Proxy Daemon** (NousResearch/hermes-agent Issue #4656) — Opened April 2, 85 days stale. High security value, complex design.
- **Slack Block Kit Support** (NousResearch/hermes-agent Issue #8552) — Opened April 12, 75 days stale. 9 👍, strong demand.
- **Vertex AI / Gemini Provider PR** (NousResearch/hermes-agent PR #8427) — Opened April 12, 75 days stale. Broadens model access.
- **Curator Archives Active Skills (P1)** (NousResearch/hermes-agent Issue #29912) — Opened May 21, 36 days stale. High operational risk.
- **Feishu Native Tables PR** (NousResearch/hermes-agent PR #27922) — Opened May 18, 39 days stale. Unblocks Feishu UX.
- **iron-proxy Egress Firewall PR** (NousResearch/hermes-agent PR #30179) — Opened May 22, 35 days stale. Large security review.
- **Dashboard Chat Broken** (NousResearch/hermes-agent Issue #36658) — Opened June 1, 25 days stale. Affects all desktop GUI users.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest based on activity over the last 24 hours (June 25–26, 2026).

---

## PicoClaw Project Digest — 2026-06-26

### 1. Today’s Overview
The project saw very high maintenance velocity on June 25, with **19 pull requests and 3 issues updated** in a single day. While no new release was tagged, six PRs were merged, shipping fixes for a Matrix identity regression, a runaway token drain in Evolution mode, and a build-breaking `log.Printf` error. Dependabot opened eight dependency bumps (Copilot SDK, Telego, LINE, Systray, SQLite), indicating active dependency hygiene. Two large feature PRs—a Delta Chat gateway and a remote agent WebSocket mode—remain open and await maintainer bandwidth. The volume of activity, paired with an absence of a formal release, strongly suggests a v0.2.10 or v0.3.0 release is building on `main`.

### 2. Releases
No new releases in the last 24 hours.

### 3. Project Progress

#### Merged/Closed (6 PRs)
- **Matrix Identity Fix** ([PR #3045](https://github.com/sipeed/picoclaw/pull/3045)) — Fixed `allow_from` ACLs broken by colon-parsing of Matrix user IDs (`@alice:example.com`). A high-priority regression fix for the Matrix channel.
- **Evolution Token Drain** ([PR #3169](https://github.com/sipeed/picoclaw/pull/3169)) — Prevents the expensive evolution "cold path" from firing on heartbeat turns, directly fixing Issue #3012. Added a regression test.
- **Build Breaking Fix** ([PR #3166](https://github.com/sipeed/picoclaw/pull/3166)) — Replaced unqualified `log.Printf` call with the structured logger in `openai_compat`, fixing a compilation error.
- **Model List Error Handling** ([PR #3168](https://github.com/sipeed/picoclaw/pull/3168)) — Surfaces body read failures when an OpenAI-compatible provider returns a non-200 response.
- **Skill Install Validation** ([PR #3092](https://github.com/sipeed/picoclaw/pull/3092)) — Added `ok` checks for type assertions on `args["version"]` and `args["force"]`, eliminating silent failures during skill install.
- **Dependency Bump** ([PR #3145](https://github.com/sipeed/picoclaw/pull/3145)) — GitHub Copilot SDK updated from v0.2.0 to v1.0.2.

#### Open / Under Review (Highlights)
- **DeltaChat Gateway** ([PR #3063](https://github.com/sipeed/picoclaw/pull/3063)) — New channel protocol gateway for DeltaChat.
- **Remote Agent WebSocket Mode** ([PR #3118](https://github.com/sipeed/picoclaw/pull/3118)) — Enables `picoclaw agent --remote ws://...` for headless/remote operation.
- **Session History Corruption Fix** ([PR #3115](https://github.com/sipeed/picoclaw/pull/3115)) — Stops `read_file` / `exec` tool output containing `data:image/...` strings from being misclassified as real media attachments.
- **Spawn Duplicate Message Fix** ([PR #3142](https://github.com/sipeed/picoclaw/pull/3142)) — Clears the `ForUser` field in sub-turn ToolResults to prevent duplicate pushes.
- **Go Expert Error Handling** ([#3170](https://github.com/sipeed/picoclaw/pull/3170), [#3171](https://github.com/sipeed/picoclaw/pull/3171), [#3172](https://github.com/sipeed/picoclaw/pull/3172)) — A series of patches by `chengzhichao-xydt` closing resource leak and panic paths in the LINE channel, agent base64 encoder, and retry loops.

### 4. Community Hot Topics
- **Security Foundation (Issue #3088):** The request to replace `libolm` with `vodozemac` is the most active open feature request. With 2 👍 and `priority: high` / `help wanted` labels, the community is clearly pushing for a modernized Matrix cryptographic stack. The fact that it is labeled stale despite its high priority suggests maintainers are looking for external contributors or bandwidth to address it.
- **Evolution Mode Token Drain (Issue #3012):** This 5-comment thread reflected real user frustration over runaway token consumption in Evolution draft mode. The rapid turnaround to Issue submission to fix merge (PR #3169 merged today) indicates strong maintainer attentiveness to cost-related bugs.
- **Long-Running Cron Issues (Issue #1757):** Closed today after 10 comments and months of lifecycle. The thread highlights a pain point in getting periodic tasks to work reliably with the Telegram channel. The deep discussion (March 18–June 25) shows users are heavily relying on scheduler features.

### 5. Bugs & Stability
| Severity | Bug | Status | Details |
|---|---|---|---|
| **Critical** | Evolution token drain | **Fixed** (PR #3169) | Continuous token consumption when Evolution was enabled. Regulated by skipping cold path on heartbeats. |
| **High** | Matrix `allow_from` broken | **Fixed** (PR #3045) | Users with standard Matrix IDs (`@user:domain`) were silently rejected. Complete channel functionality restored. |
| **Medium** | Session history corruption | Open (PR #3115) | Tool output with inline base64 corrupts the message history. Potential data loss for debugging/development. |
| **Medium** | Spawn duplicate messages | Open (PR #3142) | Async sub-agents cause duplicate user pushes. Significant UX regression for multi-agent workflows. |
| **Low** | Resource leaks / Panics | Open (PR #3170-3172) | Encoders not closed on error; untyped `sync.Map` accesses in LINE channel. PRs submitted for review. |
| **Low** | Skills install silent failure | **Fixed** (PR #3092) | Bad types in `version`/`force` args silently defaulted to zero values. |

### 6. Feature Requests & Roadmap Signals
- **DeltaChat Integration (#3063):** The push for decentralized protocol support signals a roadmap expansion beyond centralized messengers. Likely to be a headline feature in a future minor release.
- **Vodozemac Migration (#3088):** The single highest-impact infrastructure task open. Given the security implications of keeping `libolm`, it is a strong candidate to ship in **v0.3.0** or a dedicated security patch.
- **Remote Agent WebSocket Mode (#3118):** Reflects growing demand from developers to run PicoClaw as a server-side agent (CI/CD, headless AI assistants). If merged, this would enable microservice-style deployment.
- **Prediction for Next Release (v0.2.10 / v0.3.0):** Stacked bug fixes in the current merge queue (Spawn duplicates, Base64 corruption) are likely to land soon. The `vodozemac` swap is the biggest unknown factor for a v0.3.0 release date.

### 7. User Feedback Summary
- **Cost Awareness:** Users enabling experimental features (Evolution) are hitting hard token limits. The team’s quick response (#3012 → #3169) is a strong signal of trust restoration.
- **Matrix Fragility:** The identity parsing regression (#3044) caused silent DX failure. Users want Matrix to be a first-class, reliable channel.
- **Operational Users:** The long cron bug thread (#1757) reveals a user segment deploying PicoClaw for scheduled automation, which puts pressure on stability and channel error handling.
- **Developer UX:** The large number of open PRs cleaning up Go idioms (close error handling, panics, log.Printf) suggests the codebase has high standards, but contributors occasionally hit gotchas that get promptly caught in review.

### 8. Backlog Watch
- [**🟡 High Priority / Stale**] **Vodozemac Migration** ([Issue #3088](https://github.com/sipeed/picoclaw/issues/3088)) — Created June 9, labeled `help wanted`. This is the most critical technical debt item. Without maintainer time allocation, it risks lingering and increasing the security surface of the Matrix channel.
- [**🟢 Awaiting Review**] **DeltaChat Gateway** ([PR #3063](https://github.com/sipeed/picoclaw/pull/3063)) — Pending since June 8. Risking merge conflicts and contributor demotivation.
- [**🟢 Awaiting Review**] **Remote Agent Mode** ([PR #3118](https://github.com/sipeed/picoclaw/pull/3118)) — Pending since June 12. A high-visibility feature that should be triaged for the v0.3.0 scope.
- [**🔴 UX Critical**] **Spawn Duplicate Messages** ([PR #3142](https://github.com/sipeed/picoclaw/pull/3142)) — Has the `stale` bot label but directly impacts core interaction loops. Should be prioritized for review to prevent user churn on multi-agent features.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the NanoClaw project digest for 2026-06-26.

---

## NanoClaw Project Digest | 2026-06-26

### 1. Today's Overview
June 25–26 was a high-velocity development day for NanoClaw, with 16 pull requests moving through the pipeline and 11 successfully merged or closed. The team focused heavily on operational hardening—security, authentication, resource management, and platform compatibility. New issue formation was quiet, with only a single feature request opened, suggesting the community is currently satisfied with the direction of development. While no releases were cut today, the volume and quality of merged work strongly implies a minor or patch release is assembling on the horizon.

---

### 2. Releases
**None.** No new versions were published in the last 24 hours.

---

### 3. Project Progress
The project landed 11 changes spanning significant new features and critical stability fixes. Progress was clustered around a few key themes:

**Slack Integration (PRs #2471, #2472)**
- **Merged:** A long-awaited fix for `session_mode=per-thread` in Slack DMs. Top-level posts now create independent sessions, and the bot replies in-thread rather than as flat top-level messages. This resolves a major UX pain point for Slack power users.
  - Links: [PR #2472](https://github.com/nanocoai/nanoclaw/pull/2472), [PR #2471](https://github.com/nanocoai/nanoclaw/pull/2471)

**Approvals Workflow (PR #2832)**
- **Merged:** Added an optional "Reject with reason" button to approval cards. When declined with a reason, the requesting agent can adapt its behavior rather than just receiving a blank "declined."
  - Link: [PR #2832](https://github.com/nanocoai/nanoclaw/pull/2832)

**Authentication & Resilience (PR #2855)**
- **Merged:** Introduced a subscription-primary credential posture with automatic API-key failover. The Claude subscription (OAuth) is now primary; the API key acts as a hot standby with operator alerts when the primary fails.
  - Link: [PR #2855](https://github.com/nanocoai/nanoclaw/pull/2855)

**Container & Resource Management (PR #2856)**
- **Merged:** Added opt-in environment variables (`CONTAINER_CPU_LIMIT`, `CONTAINER_MEMORY_LIMIT`) to cap agent container resources, preventing single agents from monopolizing shared host resources.
  - Link: [PR #2856](https://github.com/nanocoai/nanoclaw/pull/2856)

**Skill Ecosystem (PRs #2843, #2858)**
- **Merged:** `/learn`, a new skill that distills a reusable skill from an arbitrary source (directory, URL, or past conversation).
  - Link: [PR #2843](https://github.com/nanocoai/nanoclaw/pull/2843)
- **Open/Fixes:** The `/add-clidash` utility skill (#2795) received maintainer-requested fixes in a follow-up PR (#2858), including a `mkdir -p` guard and updated Node engine requirements.
  - Link: [PR #2858](https://github.com/nanocoai/nanoclaw/pull/2858)

---

### 4. Community Hot Topics
**Multi-Admin Approvals ([Issue #2857](https://github.com/nanocoai/nanoclaw/issues/2857))**
The single issue opened in the past 24 hours targets a clear gap in the new approvals system: the lack of a fallback chain. If the single designated admin is unavailable, no one else can approve an agent action. The request includes two concrete proposals: enabling the agent to re-ask a different admin, and providing a terminal/CLI approval path for machine owners.

**Prompt Hygiene ([PR #2824](https://github.com/nanocoai/nanoclaw/pull/2824))**
A community contributor (CutSnake01) has submitted a fix to drop a stale "Global Memory" instruction from the main seed prompt. While quiet in discussion, this PR touches the core agent behavior for every user and signals a community interest in cleaning up legacy prompt artifacts.

---

### 5. Bugs & Stability
The majority of merged PRs addressed bugs and stability. Ranked by severity:

- **Critical – Workspace Path Traversal (PR #2817) — *FIX MERGED***: A security vulnerability in `send_file` was closed. The fix enforces strict realpath-based confinement to the workspace directory and blocks symlinks pointing outside. All self-hosted users should prioritize updating.
- **High – macOS SSL Failures (PR #2854) — *FIX MERGED***: On macOS with Rancher Desktop, every agent API call failed with a self-signed certificate error. The root cause was a TMPDIR misconfiguration preventing gateway CA bundles from mounting into containers.
- **High – V2 Migration Crash (PR #2859) — *OPEN FIX***: Older v1 installs (e.g., 1.1.0) lack the `is_main` column, causing the `1b-db` migration step to crash with `no such column`. This blocks setup for a segment of the user base. A fix is under review.
- **Medium – Router Crash on Primitive JSON (PR #2815) — *FIX MERGED***: The router's `safeParseContent` handler now properly guards against primitive JSON values (strings, numbers, arrays) instead of crashing.
- **Medium – Stale Systemd/Launchd Registrations (PR #2830) — *FIX MERGED***: Deleting a NanoClaw checkout without running the uninstaller left dead OS-level service registrations, causing recurring launch failures and resource accumulation.
- **Low – CLI Socket Counting / UTF-8 (PR #2813) — *FIX MERGED***: Socket response cap now measures bytes before UTF-8 decoding, fixing an edge-case bug with multi-byte characters.

---

### 6. Feature Requests & Roadmap Signals
The roadmap is clearly pivoting toward **administrative robustness** and **enterprise-class operations**.

- **Approvals Evolution:** The single open feature request ([#2857](https://github.com/nanocoai/nanoclaw/issues/2857)) asks for multi-admin chains and CLI approvals. Given the intense recent activity on the approvals system (PR #2832 merged today), a follow-up expanding the admin model is a strong candidate for the next feature release.
- **Operations Suite:** The merging of container resource limits ([#2856](https://github.com/nanocoai/nanoclaw/pull/2856)) and credential failover ([#2855](https://github.com/nanocoai/nanoclaw/pull/2855)) signals an upstream investment in multi-tenant and high-availability deployments.
- **Platform Parity:** The Slack threading fixes ([#2471](https://github.com/nanocoai/nanoclaw/pull/2471), [#2472](https://github.com/nanocoai/nanoclaw/pull/2472)) close a long-standing parity gap between the Slack channel and other platforms.

---

### 7. User Feedback Summary
User pain points extracted from this data center on **operational reliability**.

- **Deployment Bottlenecks:** The need for multi-admin approvals (Issue #2857) reflects real-world friction where a single admin becomes a blocker for agent workflows.
- **Platform Friction:** The macOS SSL bug ([#2854](https://github.com/nanocoai/nanoclaw/pull/2854)) and the v1-to-v2 migration crash ([#2859](https://github.com/nanocoai/nanoclaw/pull/2859)) represent immediate deploy-blocking issues that were or are being rapidly addressed.
- **Positive Engagement:** The `/learn` skill contribution ([#2843](https://github.com/nanocoai/nanoclaw/pull/2843)) and the iterative back-and-forth on `/add-clidash` (#2795 / #2858) demonstrate strong community buy-in and responsive maintainership.

---

### 8. Backlog Watch
Most items are very fresh, but one PR requires attention:

- **Awaiting Maintainer Triage:** **[PR #2824](https://github.com/nanocoai/nanoclaw/pull/2824)** (Drop stale "Global Memory" instruction) has been open since June 20 without a maintainer update. It is a small, low-risk prompt cleanup affecting all users.
- **Superseded Contributions:** **[PR #2795](https://github.com/nanocoai/nanoclaw/pull/2795)** (Add-clidash skill) is functionally superseded by the newer **[PR #2858](https://github.com/nanocoai/nanoclaw/pull/2858)**. Closing the older PR would clean up the open queue.
- **New Open Fixes:** PRs [#2859](https://github.com/nanocoai/nanoclaw/pull/2859) (Migration fix) and [#2860](https://github.com/nanocoai/nanoclaw/pull/2860) (Logging silence) were opened today and require standard review. No items appear heavily neglected.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-26

## Today's Overview

The IronClaw project is experiencing an intense period of feature development and stability hardening, focused entirely on the Reborn (v2) stack. Activity was recorded on **50 issues** and **50 pull requests**, with **18 PRs merged or closed**, yet no formal release was cut — confirming the team is deeply entrenched in a pre-release integration cycle. The dual themes dominating the day are the foundational architecture for an enterprise **Capability Policy** system (Epic #5261) and an aggressive **UX bug-squashing campaign** sourced from internal dogfooding (Epic #5119). Concurrent performance patches targeting the Postgres backend (CAS batching, event-log write-behind) signal a proactive push toward operational maturity.

## Releases

*None published today.*

---

## Project Progress

The closing of 18 pull requests today marks significant cleanup of the Reborn backlog. **Merged/Closed highlights:**

### UX & Usability Fixes
- **Tool Permission Persistence** — fixed `"Approve & always allow"` not persisting to Settings → Tools ([Issue #5243](https://github.com/nearai/ironclaw/issues/5243))
- **Chat Stability** — resolved message input freezing during agent responses ([Issue #5208](https://github.com/nearai/ironclaw/issues/5208)) and message state loss when an approval gate was active ([Issue #5210](https://github.com/nearai/ironclaw/issues/5210))
- **Onboarding** — improved automation empty state to guide users on creation via chat ([Issue #4980](https://github.com/nearai/ironclaw/issues/4980))
- **UI Polish** — re-enabled auto-scroll for new responses ([Issue #5211](https://github.com/nearai/ironclaw/issues/5211)), added consistent message timestamps ([Issue #5212](https://github.com/nearai/ironclaw/issues/5212)), and removed operator-only tools error on the Settings page ([Issue #5242](https://github.com/nearai/ironclaw/issues/5242))

### Infrastructure & Performance
- **CAS Optimization** — directory pre-check for `postgres_put` reduced from 3 DB round-trips to 1 ([PR #5255](https://github.com/nearai/ironclaw/pull/5255))
- **Logs Page** — WebUI v2 logs page made properly scrollable ([PR #5278](https://github.com/nearai/ironclaw/pull/5278))

---

## Community Hot Topics

The most active issues and PRs reveal the community's core focus areas:

### Capability Policy Epic (#5261)
Authored by **zetyquickly**, this is the dominant structural effort. It transforms IronClaw from a single-user tool into a multi-user platform with admin-governed tools and per-user authentication. Sub-issues landing today include User Roles ([#5266](https://github.com/nearai/ironclaw/issues/5266)), Availability Resolver ([#5267](https://github.com/nearai/ironclaw/issues/5267)), Admin REST surface ([#5268](https://github.com/nearai/ironclaw/issues/5268)), Multi-user Auth ([#5272](https://github.com/nearai/ironclaw/issues/5272)), and the Policy Delta Store ([#5273](https://github.com/nearai/ironclaw/issues/5273)). Corresponding PRs ([#5277](https://github.com/nearai/ironclaw/pull/5277), [#5286](https://github.com/nearai/ironclaw/pull/5286), [#5288](https://github.com/nearai/ironclaw/pull/5288)) are being actively reviewed and merged. This has the highest velocity of any feature on the board.

### Memory System (#5260 / #5205)
**BenKurrek's** massive (XL) PR implementing model memory as a userland extension ([#5205](https://github.com/nearai/ironclaw/pull/5205)) is under active review. The detailed follow-up tracking issue ([#5264](https://github.com/nearai/ironclaw/issues/5264)) lists remaining work including native SQL storage and semantic search. This represents the project's commitment to persistent context and self-learning agents.

### Trace Commons (#5280)
A high-risk, broad-scope PR from **zmanian** introduces instance-wide enrollment, per-user contributor accounts, and submitted-trace inspection. This moves observability from a personal debugging tool to a team/collaborative infrastructure component.

---

## Bugs & Stability

### CRITICAL
- **Scheduled Automation Completely Broken** ([#5276](https://github.com/nearai/ironclaw/issues/5276)) — The "Daily PR Digest" automation shows a 0% success rate due to a "No thread attached" error. Scheduled task execution is currently non-functional.

### HIGH
- **Approval Flow Broken / Duplicative:**
    - Denying a tool does not stop the agent from re-requesting it ([#5192](https://github.com/nearai/ironclaw/issues/5192))
    - "Ask each time" mode triggers `authorization` errors and creates duplicate approval flows ([#5196](https://github.com/nearai/ironclaw/issues/5196))
    - "Approve & always allow" fails to persist for `nearai.web_search` ([#5283](https://github.com/nearai/ironclaw/issues/5283))
    - *No specific fix PRs have been merged for the core approval logic yet. This remains the most painful user-facing stability issue.*

- **Non-Converging Retry Loops** — The agent enters infinite retry loops on identical failures, running to the wall-clock timeout instead of failing fast. *Fix PRs [#5287](https://github.com/nearai/ironclaw/pull/5287) and [#5285](https://github.com/nearai/ironclaw/pull/5285) are currently open.*

### MEDIUM
- **Error Masking** ([#5289](https://github.com/nearai/ironclaw/issues/5289)) — `builtin.json` failures are hidden behind a generic "driver protocol error", blocking end-user debugging entirely.
- **Internal Data Leakage** ([#5191](https://github.com/nearai/ironclaw/issues/5191)) — Internal skill orchestration and context budget debug messages are exposed in the user-facing chat UI.
- **Activity Identity Invariants** ([#5219](https://github.com/nearai/ironclaw/issues/5219)) — Remaining risk of activity identity drift after the lifecycle refactor, requiring hardening.

### LOW
- **Logs Link Placement** ([#5282](https://github.com/nearai/ironclaw/issues/5282)) — Appears inside the composer during runs. *Fix PR [#5284](https://github.com/nearai/ironclaw/pull/5284) is open.*
- **Logs Link Basename Duplicate** ([#5275](https://github.com/nearai/ironclaw/pull/5275)) — Rendered `/v2/v2/logs`. *Fix PR is open.*

---

## Feature Requests & Roadmap Signals

The roadmap is clearly visible in the clusters of PRs and issues landing today.

### Likely in the Next Release
- **Multi-User Authentication & Policy** — The readiness of PRs [#5286](https://github.com/nearai/ironclaw/pull/5286) (StaticUserTokenAuthenticator) and [#5288](https://github.com/nearai/ironclaw/pull/5288) (CapabilityPolicyDeltaStore) suggests full admin-governed multi-user support is the highest priority for the next cut.
- **Memory System** — PR [#5205](https://github.com/nearai/ironclaw/pull/5205) is too large and foundational to omit. The tracking issue [#5260](https://github.com/nearai/ironclaw/issues/5260) represents a north-star vision for self-learning agents.

### Architecture Signals
- **Native Storage Primitives** ([#5269](https://github.com/nearai/ironclaw/pull/5269)) — A design doc proposes moving beyond the generic `RootFilesystem` abstraction toward native, indexed Postgres access. This is a major architectural maturity step.
- **Write-Heavy Performance Engineering** — Issues and PRs for event-log write-behind coalescing ([#5257](https://github.com/nearai/ironclaw/pull/5257)) and heartbeat lease offloading ([#5253](https://github.com/nearai/ironclaw/issues/5253)) show the team proactively fixing performance bottlenecks at scale before they reach users.

---

## User Feedback Summary

The dogfooding campaign ([#5119](https://github.com/nearai/ironclaw/issues/5119)) is the primary feedback source, revealing sharp contrasts between potential and current stability.

- **Dissatisfaction with Safety UX:** The approval system is the #1 pain point. "Deny" does not prevent re-requests. "Always Allow" resets. "Ask each time" creates loops. Users cannot trust the safety guardrails, which undermines confidence in deploying autonomous agents.
- **Reliability Anxiety:** The automation failure ([#5276](https://github.com/nearai/ironclaw/issues/5276)) and infinite retry loops create a sense of unreliability. Users want clean, clear failure — not silent retries until timeout.
- **Onboarding Improvements Noted:** The closure of [#4980](https://github.com/nearai/ironclaw/issues/4980) (empty state guidance) and [#5212](https://github.com/nearai/ironclaw/issues/5212) (timestamps) shows the team is actively listening to first-run friction, a positive signal for user retention.
- **Basic UX Expectations Unmet:** Feedback on frozen inputs ([#5208](https://github.com/nearai/ironclaw/issues/5208)) and broken logs links ([#5275](https://github.com/nearai/ironclaw/pull/5275)) indicates that while core features advance, interface stability is still catching up to user expectations.

---

## Backlog Watch

- **[PR #5094: `/v1/models` & OpenAI Compatible Surface](https://github.com/nearai/ironclaw/pull/5094)** — Open since June 19th. While updated today, this PR enables a critical API compatibility layer. Its XL size and scope require significant maintainer bandwidth to land, yet it is a blocker for external tool ecosystem integration.

- **[Issue #5221: DeepSeek Harness Backlog](https://github.com/nearai/ironclaw/issues/5221)** — Tracks 9 candidates for harness improvements. While actively managed, it represents a large, open-ended evaluation pipeline debt that could surface integration friction if model behavior shifts.

- **[Issue #5119: Dogfooding Epic](https://github.com/nearai/ironclaw/issues/5119)** — While productive, the sheer volume of approval-flow complaints ([#5192](https://github.com/nearai/ironclaw/issues/5192), [#5196](https://github.com/nearai/ironclaw/issues/5196), [#5243](https://github.com/nearai/ironclaw/issues/5243), [#5283](https://github.com/nearai/ironclaw/issues/5283)) suggests an architectural design flaw in the permission resolution layer rather than a set of isolated bugs. A systematic redesign of the approval gate may be needed, and the epic should be carefully guarded against scope creep.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for June 26, 2026, based exclusively on the provided GitHub data.

---

### 1. Today’s Overview

The project saw a burst of stabilization work today with **8 PRs merged** and no new open PRs, while issue activity remained minimal (1 stale issue updated). The core maintainers focused heavily on two key areas: the **Cowork multi-agent planning mode** and the **OpenClaw plugin/extension sandbox**. No new releases were cut, signaling that the team is consolidating features and fixing regressions before the next publishable version. Despite high merge velocity, a single long-standing UI bug (#1392) remains open and unresolved, highlighting a potential disparity between backend stability work and frontend reliability.

### 2. Releases

None. No new versions were published in the last 24 hours.

### 3. Project Progress

All eight updated PRs were merged today, spanning three main areas of the codebase:

- **Cowork / Plan Mode (4 PRs):**
  - [PR #2204](https://github.com/netease-youdao/LobsterAI/pull/2204): Fixed tag parsing by preferring block-level `proposed_plan` tags over inline mentions, preventing raw tags from leaking into the chat UI.
  - [PR #2200](https://github.com/netease-youdao/LobsterAI/pull/2200): Resolved duplicate visible plan messages caused by stream jitter (specifically targeting Qwen models) by treating minor snapshot regressions as stream noise rather than new segments.
  - [PR #2199](https://github.com/netease-youdao/LobsterAI/pull/2199): Extended subagent polling to continue after the parent session completes, ensuring agent runs fully finish, with a 5-minute timeout and late-refresh fallback.
  - [PR #2205](https://github.com/netease-youdao/LobsterAI/pull/2205): Replaced the plan mode prompt icon with a theme-aware SVG component.

- **OpenClaw Plugin System (3 PRs):**
  - [PR #2202](https://github.com/netease-youdao/LobsterAI/pull/2202): Added the bundled browser plugin to the managed allowlist so it remains enabled under restrictive configurations.
  - [PR #2203](https://github.com/netease-youdao/LobsterAI/pull/2203): Declared TypeScript entries for local extensions, allowed the precompiler to write JS metadata even without prior `openclaw.extensions` declarations, and tightened packaging checks.
  - [PR #2201](https://github.com/netease-youdao/LobsterAI/pull/2201): Fixed duplicated assistant replies during `sessions_yield` by reusing committed segments and finalized thinking messages.

- **General Settings (1 PR):**
  - [PR #2206](https://github.com/netease-youdao/LobsterAI/pull/2206): Improved the "Launch at Login" feature by verifying OS state before persisting local settings, cleaning up legacy argument variants, and adding diagnostic logs.

### 4. Community Hot Topics

The only issue updated in the period is the primary community signal:

- **[Issue #1392: Scheduled task toggle unresponsive](https://github.com/netease-youdao/LobsterAI/issues/1392)**
  - *Status:* Open, stale (created Apr 3, updated Jun 25).
  - *Activity:* 1 comment, 0 reactions.
  - *Analysis:* This issue describes a UI defect where specific scheduled task toggles cannot be clicked to disable the task. With zero support reactions and a `[stale]` label, it appears the maintainers have not been able to reproduce it reliably or it affects a narrow edge case. The underlying need is for complete reliability of the scheduler UI—users expect immediate visual feedback when interacting with any toggle.

### 5. Bugs & Stability

- **High Severity (Unfixed):**
  - [Issue #1392](https://github.com/netease-youdao/LobsterAI/issues/1392) – Scheduled task toggle unresponsive. No fix PR attached. This bug has persisted for 84 days without a resolution or formal closure.

- **Medium Severity (Fixed Today):**
  - **Duplicate plan messages** ([PR #2200](https://github.com/netease-youdao/LobsterAI/pull/2200)) – Fixed stream jitter causing splits in plan mode output.
  - **Duplicate agent sync messages** ([PR #2201](https://github.com/netease-youdao/LobsterAI/pull/2201)) – Fixed duplicated replies in OpenClaw agent handoffs.
  - **Launch-at-Login state drift** ([PR #2206](https://github.com/netease-youdao/LobsterAI/pull/2206)) – Fixed config not syncing correctly with the OS.
  - **Missing browser plugin** ([PR #2202](https://github.com/netease-youdao/LobsterAI/pull/2202)) – Fixed a regression where the browser plugin was dropped from the allowlist.

- **Stability Improvement:**
  - [PR #2199](https://github.com/netease-youdao/LobsterAI/pull/2199) prevents orphaned subagents by keeping the polling loop alive after the parent session finishes.

### 6. Feature Requests & Roadmap Signals

No formal feature requests were updated today. The roadmap signals point entirely toward **stabilization and polish**:

- **OpenClaw is nearing release readiness:** Three PRs today focused on build pipeline correctness, allowlist management, and message deduplication in the plugin sandbox.
- **Cowork plan mode is being hardened:** Fixes for stream jitter, tag rendering, and subagent lifecycle suggest this feature is being stress-tested for general availability.
- **UI polish:** The icon update in [PR #2205](https://github.com/netease-youdao/LobsterAI/pull/2205) to a theme-aware SVG hints at a broader UI refresh coming in the next release.

### 7. User Feedback Summary

- **Pain Point (UI Interaction):** The scheduler toggle bug ([Issue #1392](https://github.com/netease-youdao/LobsterAI/issues/1392)) implies users expect perfect reactivity from control toggles. The long resolution time may erode trust in the scheduler feature.
- **Pain Point (Message Bloat):** Duplicate messages in plan mode and agent handoffs (fixed in PR #2200, #2201) are a clear source of user confusion. The swift merges suggest these issues were actively reported and prioritized.
- **Pain Point (Startup Reliability):** The launch-at-login fix ([PR #2206](https://github.com/netease-youdao/LobsterAI/pull/2206)) indicates users noticed the setting did not persist between reboots.

### 8. Backlog Watch

- **[Issue #1392](https://github.com/netease-youdao/LobsterAI/issues/1392) – Stale UI Bug (84 days old)**
  - This is the single most pressing item in the backlog. Despite being marked `[stale]`, the bug remains unreproduced or unfixed. If the maintainers are unable to replicate the issue, a formal comment or documentation of the specific environment conditions is needed to avoid losing the report. Leaving it in limbo risks confusing future users who experience the same failure.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

**CoPaw (QwenPaw) Project Digest**
**Date:** 2026-06-26
**Analyzed Data:** 25 Updated Issues, 50 Updated PRs, 0 Releases

---

### 1. Today's Overview

The QwenPaw project within the CoPaw ecosystem recorded extremely high activity over the past 24 hours, with **25 issues** updated and **50 pull requests** active. Despite no release cut today, the project is in an intense stabilization and migration phase. Over 20 PRs were merged or closed, primarily addressing regressions from the recent AgentScope 2.0 migration and lingering resource management bugs in the browser automation module. The community is deeply engaged, with several first-time contributors submitting critical fixes, indicating strong user attachment despite stability frustrations.

### 2. Releases

**None.** No versions were tagged today. The most recent versions referenced in the issue tracker remain `v1.1.12.post1` and `v1.1.12.post2`. Based on the volume of incoming fixes—particularly for UI rendering (#5538), model schema parsing (#5496), and resource leaks (#5536)—the community is expecting a patch release (`v1.1.12.post3` or `v1.1.13`) in the coming days.

### 3. Project Progress

Despite the absence of a release, the codebase saw substantial improvement through **21 merged/closed PRs** today. Key areas of advancement include:

- **UI Stability:** A community PR ([#5538](https://github.com/agentscope-ai/QwenPaw/pull/5538)) permanently fixed the Console markdown rendering bug (#5480) by correcting `white-space: pre-wrap` application during streaming. A UI layout fix for the TokenUsage page was also merged ([#5544](https://github.com/agentscope-ai/QwenPaw/pull/5544)).
- **Model Compatibility:** A critical schema parsing incompatibility with the `GLM-5.x` series through OpenCode Go was resolved by inlining `$ref/$defs` in tool schemas ([#5496](https://github.com/agentscope-ai/QwenPaw/pull/5496)).
- **Core Tooling:** A regression in `spawn_subagent` tool discovery on Runtime 2.0 was identified and re-registered ([#5523](https://github.com/agentscope-ai/QwenPaw/issues/5523)), though the fix is still incoming. A hard cap on `send_file_to_user` file size was merged for safety ([#5457](https://github.com/agentscope-ai/QwenPaw/pull/5457)).
- **TUI & Documentation:** The TUI mode saw restoration of ACP commands and inline approvals post-migration ([#5443](https://github.com/agentscope-ai/QwenPaw/pull/5443)). Documentation for Langfuse tracing deployment was added ([#5380](https://github.com/agentscope-ai/QwenPaw/pull/5380)).
- **Governance:** A pattern for generalizing governance policies was merged ([#5471](https://github.com/agentscope-ai/QwenPaw/pull/5471)), and a follow-up PR to generalize the pattern is already open ([#5546](https://github.com/agentscope-ai/QwenPaw/pull/5546)).

### 4. Community Hot Topics

The most active discussions reveal a community deeply concerned with reliability and provider compatibility:

- **Function Calling Parity (Closed, 8 comments):** The lack of tool calling support for custom OpenAI-compatible providers (e.g. OMLX) was a major pain point resolved in [#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345). The closed resolution indicates a fix was deployed, restoring functional parity with native Ollama support.
- **Browser Resource Leak Regression (2 comments):** Issue [#5520](https://github.com/agentscope-ai/QwenPaw/issues/5520) reports that the `browser_use stop()` fix for the original Chrome process leak (#2733) is regressing. Renderer processes survive termination, accumulating memory. A user immediately submitted a fix PR ([#5536](https://github.com/agentscope-ai/QwenPaw/pull/5536)), demonstrating high community investment in this feature.
- **Installation Failures (6 comments):** Issue [#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379) details a `get_remote_addr` crash that causes an immediate `Internal Server Error` on fresh pip installs. This is a P0 stability blocker for new users.
- **Conversation Infinite Loop (5 comments):** Issue [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) describes the Agent entering a thinking loop. This has been open since June 12 and is a high-severity core logic bug lacking a linked fix PR, making it a significant risk for production users.

### 5. Bugs & Stability

Stability scores a mixed grade today. While high-severity bugs are being submitted aggressively, the community is equally aggressive in filing patches.

**Critical/High Severity (Open):**
- **Conversation Hangs (#5162):** Agent enters an infinite thinking loop. No PR linked.
- **Install Crash (#5379):** `Internal Server Error` on fresh install. No PR linked.
- **Browser Memory Leak (#5520):** Regression of #2733. PR [#5536](https://github.com/agentscope-ai/QwenPaw/pull/5536) is submitted but not yet merged.
- **Large Session Crash (#5479):** Frontend crashes rendering sessions > 500KB.
- **Heartbeat Task Failures (#5539):** Hardcoded 120s timeout breaks complex inbox tasks.

**Medium Severity (Open):**
- **MiniMax Vision Caching (#5505):** Image rejection is incorrectly cached as `rejects_media=True`, crippling vision features.
- **File Preview 404 (#5508):** `send_file_to_user` broken on Windows native app.
- **Tool Schema Breaking Proxies (#5543):** `"type": "null"` schema crashes third-party APIs. PR [#5545](https://github.com/agentscope-ai/QwenPaw/pull/5545) submitted.

**Fixed Today:**
- Console UI rendering glitch (#5480) fixed in [#5538](https://github.com/agentscope-ai/QwenPaw/pull/5538).
- GLM-5.x JSON parsing crash (#5472) fixed in [#5496](https://github.com/agentscope-ai/QwenPaw/pull/5496).

### 6. Feature Requests & Roadmap Signals

The project is clearly targeting a **multi-platform OS agent** vision. Signals from open PRs and feature requests suggest several v1.2.0 candidates:

- **Windows Desktop Automation (#5187 PC):** A massive new `computer_use` tool is awaiting review. It uses UIA + Tauri to control the Windows desktop directly. This is the single largest roadmap signal in the data today.
- **Plugin Ecosystem Expansion:** The `DataPaw` plugin ([#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)) adds 12 BI analysis skills, signaling a push for enterprise/data analytics use cases.
- **Advanced Context Management:** The `scroll` context manager ([#5321](https://github.com/agentscope-ai/QwenPaw/pull/5321)) proposes a SQLite-backed durable history with a recall REPL, moving away from pure summarization.
- **Enterprise Features:** Support for private/enterprise DingTalk endpoints ([#4887](https://github.com/agentscope-ai/QwenPaw/issues/4887)) and dynamic model failover ([#5527](https://github.com/agentscope-ai/QwenPaw/issues/5527)).
- **Governance & Safety:** Feature requests for hard caps on tool result sizes ([#5342](https://github.com/agentscope-ai/QwenPaw/issues/5342)) to prevent context explosion.

### 7. User Feedback Summary

- **Pain Points:** Stability is the dominant theme. Users expressed frustration with the reliability of the `browser_use` tool (Linux launching, memory leaks) and inconsistent support for non-standard LLM providers. Windows users face a poor experience with the native app failing on file previews (#5508) and certain installations (#5379).
- **Use Cases:** The user base is technical and demanding. They are integrating QwenPaw into complex pipelines involving third-party model providers, private enterprise APIs (DingTalk), and advanced MCP tools. The deep technical nature of bugs filed (e.g., `json_schema_converter.cc` failures) confirms a developer-heavy audience.
- **Satisfaction:** Despite the bugs, user satisfaction with the project's *direction* appears high. The volume of first-time contributors submitting production-quality PRs (fixing schema parsing, markdown rendering, and process management) signals a highly engaged and technically capable community that sees value in the project.

### 8. Backlog Watch

Several items risk becoming stale if maintainer attention is not applied:

- **Infinite Loop Bug (#5162):** Open since June 12 with no assigned developer or fix PR. This is a P0 core logic bug that has been neglected for two weeks.
- **Responses API Support (#2188):** A feature request for support of the newer OpenAI Responses API format for custom providers. Open since March 24 with no maintainer response.
- **Discord Channel Consistency (#904):** Open since March 7 requesting file download standardization for the Discord channel. Minor but shows a lack of triage on older issues.
- **Large PR Review Bottleneck:** High-value feature PRs like **Windows Automation** ([#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187)), **Scroll Context** ([#5321](https://github.com/agentscope-ai/QwenPaw/pull/5321)), and **DataPaw** ([#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)) remain open under review. Review velocity appears to be a constraint given the massive influx of code contributions.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — June 26, 2026

## 1. Today's Overview
The ZeroClaw project sustained an **exceptionally high level of activity** over the last 24 hours, with 43 issues and 50 pull requests updated across the repository. The immediate closure of a critical security vulnerability (S0 delegate bypass) and the merging of the v0.8.2 version-bump PR signal a project that is both iterating rapidly and responding quickly to high-severity threats. While runtime stability bugs like the MCP orphan leak and Telegram image duplication remain unmerged, the overall development velocity is strong, drawing increasing community participation in RFCs and architectural decisions. The large ratio of open-to-closed PRs (46:4) suggests a bottleneck in the review pipeline as the codebase scales.

## 2. Releases
**No new releases were published in the 24-hour window.** However, the v0.8.2 release bump and changelog were merged ([PR #8234](https://github.com/zeroclaw-labs/zeroclaw/pull/8234)), along with pinned i18n translations ([PR #8332](https://github.com/zeroclaw-labs/zeroclaw/pull/8332)). An official v0.8.2 release is likely imminent or already cut.

## 3. Project Progress
The project saw focused progress on release engineering, security hardening, and stabilization:

- **Release Engineering:** The workspace version and all packaging surfaces were bumped from v0.8.1 to v0.8.2 ([PR #8234](https://github.com/zeroclaw-labs/zeroclaw/pull/8234), merged). Internationalization (i18n) translations were pinned for the release, and new Matrix room management tool keys were backfilled for non-English locales ([PR #8265](https://github.com/zeroclaw-labs/zeroclaw/pull/8265), merged; [PR #8332](https://github.com/zeroclaw-labs/zeroclaw/pull/8332), merged).
- **Security Hardening:** The critical bug where the `delegate` tool bypassed the parent's tool allowlist (Issue [#8279](https://github.com/zeroclaw-labs/zeroclaw/issues/8279), S0) was closed, addressing a severe filter-propagation flaw.
- **Runtime Stability:**
  - Fixed a panic in the agent loop caused by negative history trimming during tool-result accounting ([PR #8218](https://github.com/zeroclaw-labs/zeroclaw/pull/8218), merged).
  - Loop detector now correctly excludes failed tool results from progress checks, preventing false-positive task termination ([PR #8213](https://github.com/zeroclaw-labs/zeroclaw/pull/8213)).
  - CLI one-shot mode no longer loses telemetry and token totals upon process exit ([PR #8146](https://github.com/zeroclaw-labs/zeroclaw/pull/8146)).
- **Infrastructure & Testing:**
  - ACP bridge config loading now correctly strips UTF-8 BOMs ([PR #8326](https://github.com/zeroclaw-labs/zeroclaw/pull/8326)).
  - Nix builds were repaired by adding NAR hash generation for git dependencies ([PR #8336](https://github.com/zeroclaw-labs/zeroclaw/pull/8336)).
  - Response-cache timestamp tests were decoupled from wall-clock time to prevent flakiness ([PR #8323](https://github.com/zeroclaw-labs/zeroclaw/pull/8323)).
  - Provider alias predicates and trace case parsing gained unit test coverage ([PR #8241](https://github.com/zeroclaw-labs/zeroclaw/pull/8241), [PR #8252](https://github.com/zeroclaw-labs/zeroclaw/pull/8252)).
- **New Features Work:**
  - Rotating log persistence mode with size/date/retention controls was implemented to fill the gap between rolling and full logging ([PR #8307](https://github.com/zeroclaw-labs/zeroclaw/pull/8307)).
  - TTL-based session cleanup for channels was added to prevent unbounded history growth ([PR #8139](https://github.com/zeroclaw-labs/zeroclaw/pull/8139)).
  - Herdr agent lifecycle reporting was integrated for interactive CLI sessions ([PR #8337](https://github.com/zeroclaw-labs/zeroclaw/pull/8337)).
  - ACP elicitation Phase 1 was submitted, adopting the proper `elicitation/create` JSON-RPC method for multiple-choice prompts ([PR #8338](https://github.com/zeroclaw-labs/zeroclaw/pull/8338)).
  - The `before_llm_call` modifying hook was wired into the tool-call loop ([PR #7846](https://github.com/zeroclaw-labs/zeroclaw/pull/7846)).

## 4. Community Hot Topics
The most active discussions reveal a community deeply engaged with the project's architectural and governance trajectory:

- **Governance & Process:** The Work Lanes, Board Automation, and Label Cleanup RFC ([#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)) remains the single most active discussion with **11 comments**. The underlying need is clear: the community wants the project's own CI/git workflow to scale without burdening maintainers with manual bookkeeping.
- **Security & Trust:** The Supply Chain Signing RFC ([#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)) generated **8 comments**, driven by impending WASM plugin distribution. Users are signaling that plugin integrity verification is a prerequisite for production adoption.
- **Agent Architecture:**
  - **Goal Mode** ([#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)) received immediate community support (1+ reaction), asking for a first-class durable session mode that bridges interactive turns and cron workflows.
  - **Independent Delegate Mode** ([#8238](https://github.com/zeroclaw-labs/zeroclaw/issues/8238), 4 comments) reflects user demand for flexible multi-agent policies, likely in response to the strict boundaries imposed by the current bounded-delegation default.
- **Long-Running Bugs:** The MCP orphan process leak ([#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903)) and Telegram image duplication ([#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514)) continue to accumulate community engagement (4 comments each), with users expressing frustration over long-unmerged fixes.

## 5. Bugs & Stability

*Ranked by severity:*

| Severity | Issue | Description | Status | Fix/PR Exists? |
|---|---|---|---|---|
| **S0 – Critical** | [#8279](https://github.com/zeroclaw-labs/zeroclaw/issues/8279) | `delegate` bypasses parent tool allowlist — S0 data loss/security risk. | **Closed** | Resolved effectively immediately. |
| **S1 – High** | [#8312](https://github.com/zeroclaw-labs/zeroclaw/issues/8312) | `fill-translations` leak-repair leaves stale entries that re-ship leaked text. | **Open** | Fix not evident in the 24-hour window. |
| **S1 – High** | [#8327](https://github.com/zeroclaw-labs/zeroclaw/issues/8327) | Native tool calling sends `[IMAGE:...]` markers as plain text, inflating token counts. | **Open** | A fix PR [#8339](https://github.com/zeroclaw-labs/zeroclaw/pull/8339) was opened simultaneously. |
| **S1 – High** | [#8154](https://github.com/zeroclaw-labs/zeroclaw/issues/8154) | Kimi Code endpoint dead (404 regression) — blocks Moonshot/Kimi users. | **Closed** | Closed alongside the report. |
| **S2 – Degraded** | [#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334) | `skills install`/`list`/`remove` target `data_dir`, which no multi-agent runtime loads. | **Open** | Filed June 25, no fix PR yet. Breaks core skill workflow. |
| **S2 – Degraded** | [#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903) | MCP stdio children accumulate as orphans per daemon heartbeat tick. | **Open** (68 days) | No fix PR in window. Remains a persistent runtime burden. |
| **S2 – Degraded** | [#7087](https://github.com/zeroclaw-labs/zeroclaw/issues/7087) | `zeroclaw models set` falls through to model doctor instead of saving. | **Closed** | Closed. |
| **S3 – Minor** | [#8236](https://github.com/zeroclaw-labs/zeroclaw/issues/8236) | Voice_wake build break on `--all-features` due to missing struct field. | **Closed** | Closed. |

**Regressions flagged:** The Kimi Code endpoint regression ([#8154](https://github.com/zeroclaw-labs/zeroclaw/issues/8154)) was the most impactful provider-specific regression, while the new multi-agent skill install bug ([#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334)) is a functional regression in a headlining feature path.

## 6. Feature Requests & Roadmap Signals

Several strong roadmap signals emerged:

- **🔮 Likely for v0.8.3 (Next):**
  - **In-app upgrade from web dashboard** ([RFC #8170](https://github.com/zeroclaw-labs/zeroclaw/issues/8170), implementation [PR #8173](https://github.com/zeroclaw-labs/zeroclaw/pull/8173)) — accepted and already in review.
  - **Rotating log persistence** ([PR #8307](https://github.com/zeroclaw-labs/zeroclaw/pull/8307)) — operator-facing quality-of-life improvement.
  - **ACP Elicitation Phase 1** ([PR #8338](https://github.com/zeroclaw-labs/zeroclaw/pull/8338)) — improving the ACP channel protocol.
  - **Channel session TTL** ([PR #8139](https://github.com/zeroclaw-labs/zeroclaw/pull/8139)) — practical storage management.

- **🔮 Likely for v0.9.0 (Auth/Security/Milestone):**
  - **Wasm-first plugin runtime** ([RFC #8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135)) — ground-up shift.
  - **OCI-compliant container registries for plugin storage/discovery** ([RFC #7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497)).
  - **Supply chain signing and SLSA provenance** ([RFC #8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)).
  - **Goal mode** ([RFC #8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)) — durable autonomous sessions.

- **📌 Community-driven QoL Requests:**
  - **OpenRouter fallbacks** ([#8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138)) — trivial config change for significant reliability gain.
  - **Lighter core via external integrations** ([#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)) — fundamental architectural debate on whether to shave the codebase or integrate deeper.

## 7. User Feedback Summary

- **Dissatisfaction & Pain Points:**
  - *Security Confidence:* The delegate policy bypass ([#8279](https://github.com/zeroclaw-labs/zeroclaw/issues/8279)) eroded trust in multi-agent governance. Users want provable policy isolation.
  - *CLI/Workflow Friction:* The broken `skills install` command ([#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334)) and MCP orphan leak ([#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903)) degrade the core developer experience.
  - *Feature Gaps:* Users repeatedly cite the need for durable execution (Goal Mode) and flexible agent handoff policies ([#8238](https://github.com/zeroclaw-labs/zeroclaw/issues/8238), [#7743](https://github.com/zeroclaw-labs/zeroclaw/issues/7743)) to handle complex real-world workflows.

- **Satisfaction & Engagement:**
  - *Responsiveness:* The swift closure of [#8279](https://github.com/zeroclaw-labs/zeroclaw/issues/8279) (S0) and [#8154](https://github.com/zeroclaw-labs/zeroclaw/issues/8154) (Kimi regression) demonstrates healthy incident response, which builds community trust.
  - *RFC Culture:* Users are highly engaged in designing the project's future, from governance ([#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)) to supply chain security ([#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)). This collaborative culture is a strong positive signal.
  - *Testing Rigor:* The community appreciates the increasing focus on test coverage (provider aliases, trace case loading) as a sign of maturation.

## 8. Backlog Watch

The following items require maintainer attention or are at risk of blocking the roadmap:

- **Longest-standing Critical Bug:**
  - **MCP Orphan Process Leak** ([#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903)) — Open **68 days**. Accepted as P1, but no resolution in sight. Daemon users are silently accumulating dozens of orphan MCP processes. This is the highest-impact unaddressed stability bug.

- **Longest-standing Functional Bug:**
  - **Telegram Image Duplication** ([#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514)) — Open **79 days**. Degrades the Telegram channel experience significantly.

- **Stalled Architecture RFCs:**
  - **Lighter Core via External Skills** ([#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)) — Open **60 days**. Needs a maintainer decision. This debate directly impacts the scope of future plugin/embedding work.
  - **React → Wasm Web UI** ([#8132](https://github.com/zeroclaw-labs/zeroclaw/issues/8132)) — Tagged `needs-author-action`. Revisions are awaited.
  - **Wasm-first Plugin Runtime** ([#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135)) — Tagged `needs-maintainer-review`. This is the heart of the plugin roadmap; blocking it blocks multiple downstream RFCs.

- **New Items Requiring Immediate Signals:**
  - **SkillForge Orphaned** ([#8309](https://github.com/zeroclaw-labs/zeroclaw/issues/8309)) — The auto-skill-integration engine from February is wired to nothing. Either wire it up or remove it to reduce code surface.
  - **Skills Install Broken for Multi-Agent** ([#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334)) — Filed yesterday, P1. Breaks the headline skill workflow for multi-agent users.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*