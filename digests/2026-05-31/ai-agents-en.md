# OpenClaw Ecosystem Digest 2026-05-31

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-31 03:31 UTC

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

Here is the OpenClaw project digest for **2026-05-31**, compiled from the latest GitHub activity.

---

## OpenClaw Project Digest — 2026-05-31

### 1. Today’s Overview

Project activity remains at an extremely high intensity, with **500 issues and 500 PRs** updated in the last 24 hours (427 open issues, 317 open PRs, 73 closed issues, 183 merged/closed PRs). Two releases landed in the period—v2026.5.30-beta.1 and v2026.5.28—each carrying meaningful agent-runtime and channel-delivery fixes. The community is reporting a notable volume of **regressions tied to the rapid release cycle**, particularly around the Codex harness, Feishu dispatch, and session-state recovery. Despite this, fix velocity is equally high, with maintainers and contributors rapidly closing critical bugs and landing substantial architectural changes like the SQLite runtime-state refactor.

---

### 2. Releases

Two releases updated or published in the last 24h:

- **v2026.5.30-beta.1**  
  Agents and CLI-backed runtimes recover more cleanly from interrupted tool calls, stale session bindings, compaction handoffs, and media delivery retries (`#88129`, `#88136`, `#88141`, `#88162`, `#88182`). Channels and mobile delivery are steadier across Telegram, WhatsApp, iMessage, and Slack.

- **v2026.5.28**  
  Agent and Codex runtime recovery tightened: subagents maintain cwd/workspace separation, hook context stays prompt-local, session locks release on timeout abort, stale restart continuations are avoided, and Codex app-server/helper failures are better contained.

No breaking changes or migration notes were flagged in the provided release highlights.

---

### 3. Project Progress

**183 pull requests** were merged or closed in the last 24 hours. Major advances and fixes that landed include:

- **Codex Stability**: `#87725` (closed) fixed the Codex missing-terminal fallback leaking into Discord channels; `#86820` (closed) fixed Codex OAuth compaction failing without a raw API key; `#87436` (closed) prevented the Codex harness from recreating legacy openai-codex session route state after `doctor --fix`.
- **Channel Reliability**: `#87646` (closed) resolved the Feishu dispatch `TypeError: reading 'run'` crash; `#79116` (merged) enriched the `before_dispatch` hook event with message and media metadata.
- **Performance**: `#78664` (open, with proof) caches provider tool schema normalization; `#78852` (open, ready for maintainer look) reuses media tool availability scans; `#88238` (open, ready for maintainer look) batches memory embeddings across files to fill provider batch jobs efficiently.
- **Features**: `#87548` (ready for maintainer) renders image blocks in Control UI tool output cards; `#81851` (needs proof) introduces the `claude-cli-interactive` backend with a local TLS proxy; `#87072` (ready for maintainer) adds an opt-in interleaved progress lane for Telegram.
- **Configuration & Policy**: `#87056` (waiting on author) adds data-handling policy conformance checks; `#88288` (waiting on author) skips state-dir dotenv values that are unresolved shell references.

---

### 4. Community Hot Topics

The following issues and PRs attracted the most comments, reactions, and severity tags:

- **`#87646` [CLOSED, Platinum Hermit]** — Feishu dispatch crash after v2026.5.27 upgrade (`TypeError: read property 'run' of undefined`). **12 comments, 1 👍**. A sister issue (`#88234`) was filed later with the same stack trace, suggesting the fix may have regressed or had a partial deployment gap.
- **`#86820` [CLOSED, 6 👍]** — Codex OAuth compaction falls back to direct OpenAI API and fails. Topically tied to the broader “Codex harness vs. user-facing route” tension users are experiencing.
- **`#87744` [OPEN, Platinum Hermit]** — Codex-backed Telegram turns repeatedly time out waiting for `turn/completed`. **6 comments, 2 👍**. Users report the agent completes the work internally but the terminal event is never dispatched.
- **`#88020` [OPEN, Diamond Lobster]** — `REPLAY_INVALID_RE` missing the Anthropic "Invalid signature in thinking block" error, causing hard session failures instead of recovery retries.
- **`#87650` [CLOSED, 4 👍]** — `openclaw doctor --fix` and `openclaw onboard` did not recover a Codex provider/runtime mismatch after a v2026.5.22 → v2026.5.27 upgrade.

**Underlying demand**: Users want **upgrade stability** and **runtime-agnostic recovery**. Many of the hottest threads center on the Codex bridge silently breaking after a minor version bump, indicating that the smooth-upgrade path is a top community priority.

---

### 5. Bugs & Stability

Bugs are heavily concentrated in two areas: **Codex integration** and **channel delivery**. Ranked by severity:

**Critical / P1 (Active, with fix PRs or clear repro paths):**
- `#88020` — Anthropic thinking block signature ignored; session fails hard.
- `#88352` — Codex transient/fresh starts drop prior session context after `#88262`.
- `#87801` — `supportsAdaptiveThinking()` omits `opus-4-8`, causing 400 + silent fallback.
- `#86996` — Active Memory + Codex app-server path causes hook timeouts and event-loop stalls.
- `#88394` — Plugins failing to fail closed on trusted policy errors.

**High Impact (Channel Delivery):**
- `#87744` (Telegram Codex timeouts), `#87307` (Matrix thread replies broken), `#75969` (Slack responses in wrong thread), `#87938` (Feishu DM sessions rebuilt after restart causing duplicate keys), `#73602` (WhatsApp flaps / Telegram polling stalls on WSL2).

**Long-Standing / Stale (P1/P2 with diamond/platinum tags):**
- `#65156` — SQLite ABI mismatch kills memory vector search (since April 12).
- `#73814` — Installer `curl | bash` hangs (since April 28).
- `#48780` — Windows `exec()`/`read()` corrupted with `</arg_value>>` suffix (since March 17).
- `#66443` — Overflow recovery duplicates user messages (since April 14).

**Recently Closed High-Severity Bugs:**
- `#87646` (Feishu dispatch crash), `#86820` (Codex OAuth/compaction), `#87436` (Codex legacy state), `#87725` (Codex leak to Discord).

---

### 6. Feature Requests & Roadmap Signals

Strong signals are emerging around three themes:

1. **Memory Architecture Flexibility** — `#88504` (multi-slot memory role architecture for recall, compaction, capture, and search) and `#88238` (batch memory embeddings) indicate the team is overhauling how memory plugins compose.
2. **Policy & Governance** — `#87056` (data-handling conformance checks) and `#88394` (fail-closed on policy errors) show hardening around enterprise/regulated deployment use cases.
3. **Local Model Optimization** — `#88212` (auto-trim lean local model tools) and the persistent traction of `#75648` (hard-coded 60s embedded-run timeout) signal growing demand for first-class local model support.

**Predicted next-version inclusions**: Multi-slot memory roles, the SQLite runtime-state refactor (`#81402`), Discord reasoning-delta accumulation (`#87339`), and improved Feishu TTS config (`#81258`).

---

### 7. User Feedback Summary

**Satisfaction Drivers:**
- Users working with Realtime Talk continue to provide positive feedback, calling it “genuinely useful and low-latency” (`#76952`).
- Plugin ecosystem contributors are shipping substantial, well-tested feature PRs (memory roles, policy checks, CLI backends).

**Pain Points:**
- **Upgrade fatigue**: Multiple users report that each minor version introduces regressions requiring manual recovery or `doctor --fix` runs that sometimes don't work (`#87650`, `#76884`).
- **Codex integration opacity**: Users in `#87744`, `#86996`, and `#75739` describe silent internal failures (turns completing but never delivering, latency spikes, metadata misassignment) that are difficult to diagnose without deep platform knowledge.
- **Downgrade path broken**: `#75502` documents a failed downgrade from v2026.4.29 to v2026.4.27 due to stale `installs.json` entries, which left the operator stranded.

**Overall Mood**: Passionate and engaged, but frustrated by the stability churn. The high patch velocity is appreciated, but the community is signaling a clear desire for a **stabilization release** focused on the Codex bridge and session-state durability.

---

### 8. Backlog Watch

Several high-severity issues and critical PRs remain in a stale or waiting state:

| Item | Type | State | Summary |
|---|---|---|---|
| `#48780` | Bug | Stale (Mar 17) | P1: Windows `exec()`/`read()` corrupted — lacks maintainer action. |
| `#65156` | Bug | Stale (Apr 12) | Diamond Lobster: Memory vector search broken by SQLite ABI mismatch. |
| `#76315` | Bug | Stale (May 2) | Gateway unstable under subagent load on Linux (WhatsApp 408, stalls). |
| `#77116` | Bug | Stale (May 4) | Feishu channel crash loop after v2026.5.2 upgrade (appId compatibility). |
| `#73814` | Bug | Stale (Apr 28) | Installer `curl | bash` hang — Platinum Hermit rating. |
| `#75502` | Bug | Stale (May 1) | Downgrade fails due to stale plugin install records. |
| `#74907` | Bug | Stale (Apr 30) | Multi-tool turn replay produces orphan `tool_use` blocks. |
| `#81402` | PR | Waiting on author (May 13) | Critical SQLite runtime-state refactor — stalled despite high impact. |
| `#75128` | PR | Waiting on author (Apr 30) | Boot.md context leak fix for fallback models — stale for 30 days. |
| `#85851` | PR | Needs proof (May 14) | Claude CLI interactive backend — massive scope, unclear path to merge. |

These items represent **sustained risk**: the SQLite ABI bug has blocked memory-vector features for 49 days, the Windows corruption issue for 75 days, and the SQLite runtime refactor is the largest pending internal change.

---

## Cross-Ecosystem Comparison

### 1. Ecosystem Overview

The open-source AI agent ecosystem on 2026-05-31 is defined by a universal "security awakening" and a growing backlash against upgrade instability. While ZeroClaw and IronClaw land ambitious architectural milestones (Desktop/voice automation, protocol expansion), established players like OpenClaw and CoPaw face mounting user frustration over regressions introduced by rapid release cycles. Cross-platform session persistence and memory architecture are emerging as the next key differentiators, moving the landscape beyond simple single-chat agents towards ambient, multi-tenant platforms. The market is now punishing fragile upgrade paths and rewarding projects with transparent, high-velocity bug triage.

### 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release (24h) | Health Score | Rationale |
|---|---|---|---|---|---|
| **OpenClaw** | ~500 | ~500 | v2026.5.30-beta.1 | Fair | Highest volume, but severe regression churn in Codex & session state |
| **Hermes Agent** | ~50 | ~50 | None (v0.15.x) | Good | Fast triage, critical P0 security bug (#35584) still open |
| **ZeroClaw** | ~50 | ~50 / 28 merged | None | Excellent | Bulk feature landing (Desktop, Voice), security fixes merged |
| **IronClaw** | 4 | 18 / 11 merged | None (Blocked) | Good | Strong "Reborn" architectural momentum, blocked crates.io pipeline |
| **NanoBot** | 6 | 15 / merged | None | Excellent | Highly responsive maintainers; critical bugs (session lock, SSRF) closed same period |
| **PicoClaw** | 7 | 12 | Nightly build | Fair | Strong community contributions, but v0.2.9 has critical Web UI regression |
| **NanoClaw** | 3 | 16 / 4 merged | None | Good | Rising security hardening (supply chain, MCP bounds), critical Mac filesystem bugs |
| **CoPaw** | 9 | 1 | None (v1.1.x) | Poor | Critical Windows flash bug & `/mission` freeze unfixed; moderate velocity |
| **LobsterAI** | 0 | 2 (stale) | None | Stalled | No community engagement; PRs waiting 8+ weeks for merge |
| **Moltis** | 0 | 1 | None | Good (Niche) | Focused, clean engineering stream (Codex streaming fix) |
| **NullClaw** | 0 | 0 | None | Inactive | No activity detected |
| **TinyClaw** | 0 | 0 | None | Inactive | No activity detected |
| **ZeptoClaw** | 0 | 0 | None | Inactive | No activity detected |

### 3. OpenClaw's Position

OpenClaw retains its role as the **"core reference"** implementation with an unmatched breadth of channel integrations and the largest absolute community footprint. Its `doctor --fix` tooling and rapid beta cadence demonstrate a strong commitment to operational tooling. However, its main technical differentiators—a massive channel delivery matrix and the SQLite runtime refactor—come at the cost of **significant upgrade fatigue**. No other project reports the same level of community demand for a dedicated "stabilization release." Peers like **NanoBot** and **NanoClaw** manage to avoid severe regressions by prioritizing smaller, well-tested patches over sweeping structural changes. OpenClaw leads in raw capability surface area but is currently paying the price in community trust due to churn in the Codex harness and session-state durability.

### 4. Shared Technical Focus Areas

Several requirements emerged simultaneously across multiple projects, indicating ecosystem-wide shifts:

- **Zero-Trust Agent Tool Governance** (All active projects)
  - *Hermes Agent:* MCP server tool approval, per-user gateway restrictions.
  - *IronClaw:* Deny-by-default delegation policy, identity injection scanning.
  - *NanoClaw:* Supply chain sandboxing for MCP packages.
  - *ZeroClaw:* `allowed_tools` enforcement, process-memory limits.
  - *OpenClaw:* Data-handling conformance checks, fail-closed policy errors.

- **Multi-Channel & Cross-Platform Persistence**
  - *Hermes Agent:* Cross-platform session handoff (CLI, Telegram, iMessage) — highest-voted open feature (#8366).
  - *NanoClaw:* Multi-tenancy / multi-agent group support.
  - *ZeroClaw:* Desktop menu-bar parity and unified output routing.
  - *OpenClaw:* Session-state recovery across Telegram, Feishu, Slack, Matrix.

- **Memory Architecture as a First-Class Platform**
  - *OpenClaw:* Multi-slot memory roles, batch memory embeddings.
  - *NanoBot:* Dream toggle, Manual Memory Mode, Lightweight RAG.
  - *Hermes:* “Brain-as-Source-of-Truth” PRD for personal knowledge stores.

- **LLM Streaming & Edge Cases** (Codex/Anthropic)
  - *OpenClaw:* Codex OAuth compaction, legacy state recovery.
  - *Moltis:* Streaming tool-call argument delta hardening.
  - *Hermes:* Thinking/redacted_thinking block preservation for Anthropic.
  - *PicoClaw:* Codex OAuth empty response handling.

- **Desktop Automation & Voice**
  - *ZeroClaw:* macOS GUI control, permission flows, full-duplex VAD pipeline.
  - *CoPaw:* Desktop Windows Shell execution (currently breaking).
  - *NanoBot:* Configurable STT models and OpenRouter provider.

### 5. Differentiation Analysis

| Dimension | Architecture | Target User | Key Differentiator |
|---|---|---|---|
| **OpenClaw** | Python (Monolith) | Generalist / LiveOps | Broadcast channel reach, largest plugin ecosystem |
| **Hermes** | Python (Modular) | Security-Conscious Developer | MCP approval system, cross-platform handoff, TUI polish |
| **ZeroClaw** | Python + Tauri | Desktop/Voice Pioneer | macOS automation, full-duplex voice, integration RFCs |
| **IronClaw** | Rust | Infrastructure Engineer | WASM safety, “Reborn” protocol, performance isolation |
| **NanoBot** | Python (Minimal) | Self-Hoster / Maintainer | Reliability excellence, user-toggle memory, rapid triage |
| **NanoClaw** | Node.js / TypeScript | Enterprise Operator | Multi-instance config, backup/restore, supply chain hardening |
| **PicoClaw** | Go | Lightweight/Edge User | i18n agility (Bangla), image paste/drag-drop, cron tooling |
| **CoPaw** | Python (Desktop UI) | Windows Power User / CN Market | Desktop client scripts, ACP multi-agent interop, financial plugins |
| **Moltis** | Python (Library) | Streaming Protocol Developers | Deep Codex streaming reliability (single PR focus) |
| **LobsterAI** | Python (UI) | End-User UX | MCP modal polish, Mac shortcut fixes (currently stalled) |

### 6. Community Momentum & Maturity

**Tier 1: Maximum Velocity / Broadest Impact**
- **OpenClaw**: The "Linux kernel" of personal AI agents. Unmatched volume. Transitioning from rapid feature expansion to forced stabilization.
- **Hermes Agent**: Very high velocity with a security-first brand. Strong, well-documented user bug reports.
- **ZeroClaw**: Disruptive scope. Bulk feature landing (Desktop, Voice) and architectural RFCs signal a project aggressively pursuing next-gen interfaces.
- **IronClaw**: High architectural ambition ("Reborn") with strong Rust leadership. The crates.io publishing block is the only drag on community momentum.

**Tier 2: High Velocity / Focused Maturity**
- **NanoBot**: Excellent user responsiveness. Demonstrates the value of *targeted maintenance cycles* over sweeping releases. A model for “healthy” project velocity.
- **PicoClaw**: High contributor velocity (many external PRs). Needs to stabilize v0.2.9 regressions to maintain trust.
- **NanoClaw**: Strong security and enterprise feature maturation (multi-tenancy, backup).

**Tier 3: Moderate / Stabilizing (At Risk)**
- **CoPaw**: Active bug reports but slow fix velocity. Critical Windows bugs eroding desktop user base.

**Tier 4: Low / Niche / Stalled**
- **Moltis**: Targeted, clean engineering. Low risk but low strategic impact.
- **LobsterAI**: Stalled. Losing relevance without maintainer movement.
- **NullClaw, TinyClaw, ZeptoClaw**: Inactive. Likely candidates for project consolidation or deprecation.

### 7. Trend Signals

1. **Security is the Product.** The volume and sophistication of P0/P1 security features (MCP sandboxing, policy engines, credential isolation) across every active project is the single strongest signal. AI agents are moving into production environments where untrusted code execution requires robust governance. *For developers: Prioritize a modular permission system early; it is no longer a “v2” feature.*

2. **Upgrade Path is a Competitive Moat.** The backlash against OpenClaw’s regressions and CoPaw’s unfixed bugs is a warning. Users are demanding reliable, testable migration paths. *For adopters: Evaluate projects on their stability track record as much as their feature set. NanoBot’s validation of targeted patches over sweeping releases is a strong pattern.*

3. **Memory is the New Context Window.** The universal push towards structured, multi-role, and user-controlled memory (OpenClaw, NanoBot, Hermes) signals that basic RAG is table stakes. Active memory management is the new differentiator. *For contributors: Memory roles, compaction strategies, and “manual mode” toggles are the richest plugin surface area today.*

4. **Desktop and Voice are the Next Interface Division.** ZeroClaw's Desktop push and CoPaw’s Desktop-focus (despite bugs) confirm that pure CLI/mobile chat is insufficient for ambient computing. Full-duplex low-latency voice and local machine automation are the next battlegrounds.

5. **Community Trust = Fix Velocity + Transparency.** Projects that acknowledge regressions openly and fix them fast (NanoBot, Hermes) generate significantly more user goodwill than those with silent fix cycles or breaking changes on minor bumps. *For developers: Prioritize a rapid hotfix pipeline. It is your strongest marketing asset.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-05-31

## 1. Today's Overview

NanoBot experienced an elevated level of development activity on May 31, with **15 pull requests** and **6 issues** updated over the past 24 hours. The central themes of this sprint were **reliability, security, and user configurability**. The team successfully merged several high-impact patches, including a critical concurrency fix for the agent dispatch system, E2EE verification support for the Matrix channel, and a long-awaited configuration toggle for the Dream memory job. This pace signals a proactive maintenance phase, quickly resolving user-reported bugs while pushing foundational features like manual memory management and WebUI improvements over the finish line.

## 2. Releases

No new software releases were published on this date.

## 3. Project Progress

Several significant changes were merged or closed on May 31:

- **Locking & Concurrency:** [PR #4104](HKUDS/nanobot PR #4104) (*fix: acquire per-session lock in process_direct*) was merged, closing [#4080](HKUDS/nanobot Issue #4080). This resolves a dangerous race condition where direct processing calls could bypass session locks and corrupt history.
- **Matrix Integration:** [PR #4110](HKUDS/nanobot PR #4110) (*fix: handle SAS device verification*) was merged, closing [#4042](HKUDS/nanobot Issue #4042). This provides opt-in support for Matrix's self-verification protocol, silencing warning messages for Element X users.
- **Platform Stability:** [PR #4054](HKUDS/nanobot PR #4054) (*fix: coerce typeless Anthropic content blocks + add Dream enable toggle*) was merged, closing both [#3993](HKUDS/nanobot Issue #3993) and [#3885](HKUDS/nanobot Issue #3885).
- **Security Hardening:** [PR #4086](HKUDS/nanobot PR #4086) (*normalize IPv6-mapped IPv4 in SSRF checks*) and [PR #4106](HKUDS/nanobot PR #4106) (*bound inbound Matrix media downloads*) were merged.
- **UI/UX:** [PR #4108](HKUDS/nanobot PR #4108) (*refine output timeline and model controls*) was merged, delivering an overhauled WebUI activity timeline.

## 4. Community Hot Topics

Conversations centered around three major themes: **Memory control**, **Matrix client compatibility**, and **notification reliability**.

- **Issue [#3885](HKUDS/nanobot Issue #3885)** (*Dream sys job global switch*) garnered 4 comments and was resolved by PR #4054. The user community clearly values granular control over automatic memory processes.
- **Issue [#4042](HKUDS/nanobot Issue #4042)** (*Matrix E2EE warnings on Element X*) was actively resolved with PR #4110, showing sensitivity to the mobile client experience.
- **Heartbeat Bug:** Issue [#4111](HKUDS/nanobot Issue #4111) sparked significant developer interest, with two separate fix PRs submitted simultaneously ([#4112](HKUDS/nanobot PR #4112) and [#4114](HKUDS/nanobot PR #4114)), indicating a strong community drive to maintain core reliability.

## 5. Bugs & Stability

**Severity: Critical**
- **Session History Corruption ([#4080](HKUDS/nanobot Issue #4080)):** `process_direct()` bypassed per-session dispatch locks, allowing concurrent processing to corrupt history. **Status: Fixed** in PR #4104.
- **Matrix Media DoS / Unbounded Downloads ([#4106](HKUDS/nanobot Issue #4106)):** The Matrix channel lacked bounds on inbound media downloads. **Status: Fixed** in PR #4106.

**Severity: High**
- **Anthropic API Error ([#3993](HKUDS/nanobot Issue #3993)):** Tool returns with bare dicts failed against the Anthropic API due to a missing required `type` field. **Status: Fixed** in PR #4054.

**Severity: Medium**
- **Heartbeat Spam ([#4111](HKUDS/nanobot Issue #4111)):** The cron-based Heartbeat job incorrectly sends "All clear." notifications to Feishu when no tasks exist. **Status: Under Review** via competing PRs #4112 and #4114.

**Severity: Low / Security Hardening**
- **SSRF Bypass ([#4086](HKUDS/nanobot Issue #4086)):** IPv6-mapped IPv4 addresses could bypass SSRF filters. **Status: Fixed** in PR #4086.

## 6. Feature Requests & Roadmap Signals

User requests fulfilled today provide strong signals for what is coming next:

- **Memory Management:** The merge of [PR #4050](HKUDS/nanobot PR #4050) (*Manual Memory Mode*) and the fix for [#3885](HKUDS/nanobot Issue #3885) (*Dream Toggle*) confirms the team is investing heavily in flexible memory. The new **Lightweight RAG** feature ([PR #4109](HKUDS/nanobot PR #4109)) is a strong candidate for the next major feature version.
- **Voice & STT:** [PR #4113](HKUDS/nanobot PR #4113) introduces configurable STT models and an OpenRouter provider. This is likely to land soon given the demand for multi-provider voice support.
- **Portability:** [PR #4034](HKUDS/nanobot PR #4034) (*GitAgent Protocol*) is awaiting triage. If accepted, it could make NanoBot agents compatible with a broader open standard ecosystem.
- **Sandboxing:** Issue [#4107](HKUDS/nanobot Issue #4107) requesting configurable `bwrap` bind mounts is a small, well-scoped request that could easily make the next release.
- **Cross-Instance Collaboration:** [PR #3992](HKUDS/nanobot PR #3992) (*Agent Collaboration Bus*) signals a major architectural shift toward distributed multi-agent systems.

## 7. User Feedback Summary

- **Acclaimed Responsiveness:** Users directly reported pain points—Memory toggles ([#3885](HKUDS/nanobot Issue #3885)), Anthropic errors ([#3993](HKUDS/nanobot Issue #3993)), Matrix verification ([#4042](HKUDS/nanobot Issue #4042)), SSRF bypasses ([#4086](HKUDS/nanobot Issue #4086))—and saw them resolved within days or even hours. This responsiveness generates a strong sense of project health.
- **Pain Points Addressed:** High-level frustration around rigid memory scheduling and specific client incompatibility issues has been significantly reduced.
- **Emerging Friction:** The Heartbeat spam issue ([#4111](HKUDS/nanobot Issue #4111)) highlights a UX friction point for users of cron-based notifications. The sandbox configuration limitation ([#4107](HKUDS/nanobot Issue #4107)) signals maturing enterprise deployment patterns requiring greater isolation control.
- **Satisfaction:** The community appears highly satisfied with the direction of memory and agent tooling, as evidenced by the rapid positive engagement on manual memory and RAG features.

## 8. Backlog Watch

A few items in the queue warrant maintainer attention:

- **[PR #3992](HKUDS/nanobot PR #3992) (Agent Collab Bus):** This massive feature has been open since May 24 without maintainer comments. As a significant architectural change (cross-instance messaging), it represents a potential fork in the roadmap and requires design feedback to prevent contributor stagnation.
- **[PR #3994](HKUDS/nanobot PR #3994) & [PR #3997](HKUDS/nanobot PR #3997) (Config & Performance):** Authored by the same contributor, these refactoring and performance PRs (Registry-driven provider config, Tokenizer pre-warming) have been idle for nearly a week. A simple "interest check" or review assignment would keep the contributor engaged.
- **[PR #4034](HKUDS/nanobot PR #4034) (GitAgent Protocol):** The author has self-tagged this as a "[duplicate]". Maintainer confirmation of existing support or rejection of the protocol specification is needed to avoid contributor burnout.
- **[PR #4112](HKUDS/nanobot PR #4112) vs. [PR #4114](HKUDS/nanobot PR #4114) (Heartbeat Fix):** The presence of two competing fix PRs for the same issue ([#4111](HKUDS/nanobot Issue #4111)) requires swift maintainer triage to converge on a single solution and prevent duplicated effort.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-31

## 1. Today's Overview

Hermes Agent is in a high-velocity post-release cycle following v0.15, with **50 issues and 50 pull requests** updated in the last 24 hours. The project is actively stabilizing the recent release, with several critical regressions (Docker restart loops, session history poisoning, dashboard reload issues) identified and already closed. Community engagement remains extremely strong, with users filing sophisticated security-focused feature requests—particularly around MCP tool approval, per-user gateway restrictions, and tool-level permission gating. The maintainer team is responding quickly, merging 10 items today while keeping another 40 PRs open for review. The dominant narrative is a project scaling rapidly in capability and user base, now absorbing the pressure of that growth through aggressive bug fixing and transparent issue tracking.

---

## 2. Releases

**No new releases today.** The most recent release series remains v0.15.x, which appears to be the source of several regressions currently being addressed (see Bugs & Stability).

---

## 3. Project Progress

The team closed or merged **10 items today**, signaling strong forward momentum:

- **Stability & Regressions Fixed**
  - [Dashboard infinite reload loop in loopback mode](https://github.com/NousResearch/hermes-agent/issues/34202) — **Closed.** Root cause was `hasValidSession()` triggering `GET /api/auth/me` without allowing the response to settle.
  - [Cross-provider poisoned history](https://github.com/NousResearch/hermes-agent/issues/35543) — **Closed.** Thinking-mode `reasoning_content` from DeepSeek/Kimi/MiMo was causing HTTP 400 errors on strict providers like Cerebras.
  - [Gateway Docker restart loop under s6-overlay](https://github.com/NousResearch/hermes-agent/issues/35393) — **Closed.** v0.15.x introduced a regression; confirmed resolved on v0.14.0 downgrade path.
  - [Kanban DB file descriptor exhaustion](https://github.com/NousResearch/hermes-agent/issues/33580) — **Closed.** SQLite connection leak causing "Too many open files" on macOS.
  - [Windows MEDIA file delivery silent failure](https://github.com/NousResearch/hermes-agent/issues/35546) — **Closed.** Unquoted Windows drive-letter paths in `MEDIA:` convention.

- **UX & Client Improvements**
  - [macOS desktop install + self-update](https://github.com/NousResearch/hermes-agent/pull/35607) — **Merged.** Fixes `HERMES_HOME` path alignment between Tauri installer and Python runtime.
  - [Claude-style startup banner](https://github.com/NousResearch/hermes-agent/pull/35501) — **Merged.** Adds skin-configurable banner modes (`full`, `claude`).
  - [TUI mouse-burst noise swallowing](https://github.com/NousResearch/hermes-agent/pull/35512) — **Merged.** Prevents degraded SGR/ANSI sequences from locking the composer on Windows Terminal.

- **Open PRs Nearing Completion**
  - [Anthropic thinking/tool_use block order fix](https://github.com/NousResearch/hermes-agent/pull/35586) — Critical P1 fix for multi-turn agentic turns producing HTTP 400 on Anthropic API.
  - [Skill manager symlink support](https://github.com/NousResearch/hermes-agent/pull/35244) — Fixes `skill_manage` failing on skill directories added via symbolic links.

---

## 4. Community Hot Topics

**1. Cross-Platform Session Handoff** ([Issue #8366](https://github.com/NousResearch/hermes-agent/issues/8366))
The most upvoted open issue today (6 👍, 4 comments). Users want seamless continuity across CLI, Telegram, and iMessage sessions—picking up a task started on one platform and continuing on another without context loss. This is the single strongest community signal for Hermes evolving from a single-platform agent into a persistent, ambient presence.

**2. MCP Server Tool Approval** ([Issue #16462](https://github.com/NousResearch/hermes-agent/issues/16462))
High engagement on security: MCP servers' tools become callable immediately upon registration, with no human approval step. The community is pushing for first-invoke confirmation—a pattern that would bring MCP in line with the existing `approvals.mode` for shell commands.

**3. Slack Gateway History Access** ([Issue #6345](https://github.com/NousResearch/hermes-agent/issues/6345))
3 👍, 2 comments. A recurring request for the Slack gateway to expose `conversations.history` as a tool, enabling the agent to reference prior channel context. This reflects a broader desire for gateway agents to act *proactively* rather than just *reactively* to the current message.

**4. Broad Tool Permission Gating** ([Issue #21849](https://github.com/NousResearch/hermes-agent/issues/21849), [Issue #35479](https://github.com/NousResearch/hermes-agent/issues/35479), [Issue #33905](https://github.com/NousResearch/hermes-agent/issues/33905))
A convergent cluster of three distinct feature requests all asking for the same fundamental capability: replacing Hermes' narrow shell-command-only approval system with **per-tool, per-user, per-session permission policies**. This is the top architectural signal from the community today.

**5. Terminal Freeze on `/new`/`/clear`/`/reset`** ([Issue #33961](https://github.com/NousResearch/hermes-agent/issues/33961))
4 comments, high frustration. Slash commands that should reset the session are freezing the terminal entirely, with Ctrl+C failing. Users are hitting this repeatedly in daily workflow.

---

## 5. Bugs & Stability

| Severity | Issue | Description | Status |
|----------|-------|-------------|--------|
| **P0 (Security)** | [#35584](https://github.com/NousResearch/hermes-agent/issues/35584) | Gateway attaches `config.yaml` to agent response when file write is denied — credential leak via `extract_local_files` | **Open; no fix PR linked** |
| **P1** | [#35595](https://github.com/NousResearch/hermes-agent/issues/35595) | `/model` command returns structured field list instead of human-readable message (v0.15 regression) | **Open** |
| **P1** | [#17861](https://github.com/NousResearch/hermes-agent/issues/17861) | Multi-turn history loses `thinking`/`redacted_thinking` blocks — Anthropic raw content array not preserved | Fix PR [#35586](https://github.com/NousResearch/hermes-agent/pull/35586) open |
| **P2** | [#33961](https://github.com/NousResearch/hermes-agent/issues/33961) | `/new`, `/clear`, `/reset` commands freeze terminal session | **Open** |
| **P2** | [#32737](https://github.com/NousResearch/hermes-agent/issues/32737) | Tirith shell scanner blocks `local_executable \| python3` as high-severity (false positive) | **Open** |
| **P2** | [#35654](https://github.com/NousResearch/hermes-agent/issues/35654) | Browser tool fails on Windows with shell characters (`&`, `|`, `<`, `>`) in arguments | **Open** |
| **P2** | [#35652](https://github.com/NousResearch/hermes-agent/issues/35652) | TUI background completion notifications routed to wrong live session | **Open** |
| **P2** | [#35576](https://github.com/NousResearch/hermes-agent/issues/35576) | Feishu gateway: stale `thread_id` on gateway restart causes 99992402 validation error | **Open** |
| **P2** | [#5129](https://github.com/NousResearch/hermes-agent/issues/5129) | Background memory review spawns second provider instance on same DB | **Open** (since April 4) |
| **P3** | [#35561](https://github.com/NousResearch/hermes-agent/issues/35561) | Cron tool hidden if tool definitions cached before gateway env is set | **Open** |
| **P3** | [#28291](https://github.com/NousResearch/hermes-agent/issues/28291) | `moonshot_schema._fill_missing_type` crashes on JSON Schema union types | **Open** |

**Notable:** The P0 security issue ([#35584](https://github.com/NousResearch/hermes-agent/issues/35584))—where a denied write to `config.yaml` can result in the file being attached to the agent's message—is the most urgent open bug and should be prioritized by maintainers.

---

## 6. Feature Requests & Roadmap Signals

**Likely for Next Release (v0.16)**

1. **Unified Tool Permission System** — The cluster of requests ([#16462](https://github.com/NousResearch/hermes-agent/issues/16462), [#21849](https://github.com/NousResearch/hermes-agent/issues/21849), [#33905](https://github.com/NousResearch/hermes-agent/issues/33905), [#35479](https://github.com/NousResearch/hermes-agent/issues/35479)) all point toward a single, extensible permissions module replacing the current narrow shell-command-only gate. This would cover MCP tools, file tools, browser automation, and per-user restrictions. Expect a PRD or working group to coalesce these.

2. **Model Catalog Updates** — [PR #35659](https://github.com/NousResearch/hermes-agent/pull/35659) adds `deepseek-v4-flash`, trims redundant model variants, and restructures pickers by maker. Likely to merge quickly.

3. **CLI/TUI Polish** — [PR #35657](https://github.com/NousResearch/hermes-agent/pull/35657) (WSL terminal dimension clamping) and [PR #35658](https://github.com/NousResearch/hermes-agent/pull/35658) (config migration prompt clarity) are small, low-risk fixes nearing merge.

4. **MCP Reconnection Hardening** — [PR #35661](https://github.com/NousResearch/hermes-agent/pull/35661) fixes a compounding bug where MCP server disconnects are permanent without a full gateway restart.

**Longer-Term Roadmap Signals**

- **Brain-as-Source-of-Truth** ([#27657](https://github.com/NousResearch/hermes-agent/issues/27657)) — A detailed PRD for integrating an existing personal knowledge store as Hermes' core memory, going beyond session search and LLM-wiki.
- **Dynamic Context Pruning** ([#20717](https://github.com/NousResearch/hermes-agent/issues/20717)) — Moving from reactive compression to proactive stale-context management.
- **i18n Language Pack System** ([PR #35127](https://github.com/NousResearch/hermes-agent/pull/35127)) — YAML-based translation system for CLI and gateway UI messages, indicating global expansion plans.
- **Desktop App** ([PR #20059](https://github.com/NousResearch/hermes-agent/pull/20059)) — Electron/Vite desktop client continues steady progress, now with the macOS install path resolved ([#35607](https://github.com/NousResearch/hermes-agent/pull/35607) merged).

---

## 7. User Feedback Summary

**Pain Points:**
- **v0.15 Regressions** are the dominant theme in recent user reports. The `/model` command breaking human-readable output ([#35595](https://github.com/NousResearch/hermes-agent/issues/35595)) and Docker instability ([#35393](https://github.com/NousResearch/hermes-agent/issues/35393)) represent friction from the upgrade path.
- **Terminal Freezing** ([#33961](https://github.com/NousResearch/hermes-agent/issues/33961)) is a daily workflow blocker for CLI users, with no workaround available.
- **Windows Incompatibility** is a recurring pain point: browser tool shell characters ([#35654](https://github.com/NousResearch/hermes-agent/issues/35654)), WSL terminal dimensions ([#35657](https://github.com/NousResearch/hermes-agent/issues/35657)), and unquoted MEDIA paths ([#35546](https://github.com/NousResearch/hermes-agent/issues/35546)) all surfaced today alone.
- **Documentation Gaps** — The bundled `google-workspace` skill's `SKILL.md` references `--services`/`--format` flags that don't exist in `setup.py`, causing failed auth flows ([#35560](https://github.com/NousResearch/hermes-agent/issues/35560)).

**Desires & Use Cases:**
- **Multi-Platform Continuity**: Users want "pick up where I left off" across desktop CLI, Telegram, and iMessage ([#8366](https://github.com/NousResearch/hermes-agent/issues/8366)).
- **Secure Multi-User Gateways**: Users running Hermes in shared environments (Feishu groups, Slack workspaces) need per-user tool access restrictions, not all-or-nothing ([#35479](https://github.com/NousResearch/hermes-agent/issues/35479)).
- **Developer Workflows**: Users are actively running Hermes headlessly, integrating with cron, and importing Claude Code skills—this is a power-user community pushing the agent into CI/CD and development pipelines.
- **Self-Hosting & Control**: The volume and quality of security-related feature requests (MCP approval, tool gating) show a user base that values safety and auditability over pure automation.

**Engagement Quality:** The user community continues to file exceptionally well-documented issues. Bug reports include root cause analysis from code inspection, reproduction scripts, and proposed fixes. Several issues today were filed *by Hermes itself* on behalf of users, demonstrating dogfooding of the tool's own debugging capabilities.

---

## 8. Backlog Watch

Several important items remain unaddressed or lack official maintainer response:

| Item | Date | Age | Priority Signal | Notes |
|------|------|-----|-----------------|-------|
| [#5129](https://github.com/NousResearch/hermes-agent/issues/5129) - Memory review creates second provider instance | Apr 4, 2026 | ~58 days | Core architecture issue affecting memory DB stability | Unanswered; duplicates DB connections for SQLite providers |
| [#6345](https://github.com/NousResearch/hermes-agent/issues/6345) - Slack gateway history tool | Apr 9, 2026 | ~53 days | 3 👍, logical feature for Slack parity | No official response or milestone |
| [#8366](https://github.com/NousResearch/hermes-agent/issues/8366) - Cross-platform handoff | Apr 12, 2026 | ~50 days | 6 👍 (highest of all open issues) | Most requested feature; no maintainer roadmap update |
| [PR #17480](https://github.com/NousResearch/hermes-agent/pull/17480) - Codex auth fallbacks | Apr 29, 2026 | ~33 days | Enterprise billing/usage path | Stale; no recent activity from reviewer |
| [PR #21774](https://github.com/NousResearch/hermes-agent/pull/21774) - Google Workspace OAuth hardening | May 8, 2026 | ~24 days | Addresses docs gap from [#35560](https://github.com/NousResearch/hermes-agent/issues/35560) | Has merge conflicts; needs rebase |
| [PR #20059](https://github.com/NousResearch/hermes-agent/pull/20059) - Desktop app | May 5, 2026 | ~27 days | Major feature, large diff | Active but no milestone assigned |

**Recommendation:** The maintainer team should consider a "Backlog Triage" pass to:
1. Assign milestones or explicit deferral labels to the top-voted feature requests.
2. Provide guidance on [#5129](https://github.com/NousResearch/hermes-agent/issues/5129) to prevent community duplication of effort on memory architecture changes.
3. Merge or close the longer-open PRs ([#17480](https://github.com/NousResearch/hermes-agent/pull/17480), [#21774](https://github.com/NousResearch/hermes-agent/pull/21774)) to clear the review queue and maintain contributor momentum.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-31

## 1. Today's Overview

Activity levels are extremely high, with **7 issues** and **12 pull requests** updated in the last 24 hours, alongside the release of a new nightly build. The `v0.2.9` stable release is the current baseline, but it has drawn immediate bug reports from the community regarding Web UI message history corruption and context compression display errors. While these stability concerns are pressing, the project is buoyed by an exceptionally strong wave of community contributions—three PRs were merged today adding Azure Identity authentication, Bangla i18n support, and image drag-and-drop in the web frontend. The open PR queue shows sustained work on agent-facing tooling (cron management, message attachments, policy filters), suggesting a feature-rich `v0.3.0` cycle is underway. Overall project health is **active but requires urgent triage on the v0.2.9 regressions**.

## 2. Releases

**Nightly Build — `v0.2.9-nightly.20260531.1ce353ba`**

> **Full Changelog**: [https://github.com/sipeed/picoclaw/compare/v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

An automated nightly snapshot built against the `main` branch. As noted in the release notes, this build may be unstable and is intended for early adopters and testing. No breaking changes or migration notes are documented for this incremental nightly, as it primarily reflects changes merged since `v0.2.9`.

## 3. Project Progress

**Merged PRs (3 in last 24h):**
- [#2969](https://github.com/sipeed/picoclaw/pull/2969) **feat(web): add chat image paste and drag-and-drop upload** — The web frontend now supports pasting images from the clipboard and drag-and-drop file upload, with MIME type normalization and mixed clipboard payload handling.
- [#2971](https://github.com/sipeed/picoclaw/pull/2971) **feat(provider): Add optional Azure Identity support for Azure OpenAI provider** — Enables an `azidentity` build tag for Azure Identity-based authentication, targeting enterprise environments where local auth is restricted.
- [#2974](https://github.com/sipeed/picoclaw/pull/2974) **feat(i18n): Add Bangla support bn-in** — Adds full Bangla language support for the web UI.

**Closed Issues (4 in last 24h):**
- [#2742](https://github.com/sipeed/picoclaw/issues/2742) [BUG] Gateway starts with no channels in v0.2.8 (Closed after 6 comments)
- [#2880](https://github.com/sipeed/picoclaw/issues/2880) [BUG] Android "permission denied" error on Xiaomi Pocophone (Stable, Closed)
- [#2970](https://github.com/sipeed/picoclaw/issues/2970) [Feature] Azure Identity Support (Completed via PR #2971)
- [#2973](https://github.com/sipeed/picoclaw/issues/2973) [Feature] i18n: Add support for Bangla (Completed via PR #2974)

## 4. Community Hot Topics

- [#2952](https://github.com/sipeed/picoclaw/issues/2952) **[Feature] 好久没发新版本了** (3 comments) — A multi-threaded Chinese-language issue encompassing multiple pain points: the `exec` tool failing to pass `actions:run` to models, a QQ channel restart loop bug, and a request for the model configuration UI to default to saved provider keys with an API test connection button. This issue is effectively a community-driven mini-roadmap and signals unmet expectations around agent tool orchestration and channel stability.

- [#2972](https://github.com/sipeed/picoclaw/issues/2972) **[BUG] Web UI message chaos in v0.2.9** (2 comments) — Strong initial report of a functional regression. User reports that every new session attaches old message history, which severely impacts the chat UX.

- [#2742](https://github.com/sipeed/picoclaw/issues/2742) **[BUG] Gateway starts with no channels in v0.2.8** (6 comments, Closed) — This was a high-engagement bug despite being older (created May 1). Its resolution implies a fix for gateway channel initialization is now in the codebase.

- [#2977](https://github.com/sipeed/picoclaw/pull/2977) **feat(cron): add get and update actions** (Created today) — Freshly opened PR to let agents inspect and partially update persisted cron jobs without destructive `remove -> add` cycles. High relevance for agent workflow engineering.

## 5. Bugs & Stability

**Critical Severity:**
- [#2972](https://github.com/sipeed/picoclaw/issues/2972) — **[Web UI] Message history leak in v0.2.9.** Every new session retains stale message context. This is a severe regression for any user interacting via the web interface. No fix PR has been associated yet.
- [#2968](https://github.com/sipeed/picoclaw/issues/2968) — **[Context Management] `/context` always shows "Compress at: 76800 tokens"** (1 comment, 1 👍). The context compression display is stuck on a fixed value instead of reflecting actual token counts. This may also indicate a functional defect in context window management for v0.2.9.

**Medium Severity:**
- [#2952](https://github.com/sipeed/picoclaw/issues/2952) — **`exec` actions:run model compatibility.** The `exec` tool fails when upstream models do not automatically include the `actions:run` prefix, causing an excess command execution.
- [#2952](https://github.com/sipeed/picoclaw/issues/2952) (Sub-issue) — **QQ channel restart loop.** Restarting the QQ channel causes it to restart again on any subsequent message, requiring context history to be manually cleared.

**Bugs with Fix PRs in Progress:**
- [#2967](https://github.com/sipeed/picoclaw/pull/2967) — **fix(codex): preserve streamed output text deltas.** Resolves Codex OAuth empty responses when `response.output` is `null` in the final event (Open PR).
- [#2965](https://github.com/sipeed/picoclaw/pull/2965) — **fix(tools): stop workspace guard misreading scheme-less URLs.** Prevents the `exec` tool from treating URL path components (e.g., `wttr.in/Beijing?T`) as absolute filesystem paths when `restrict_to_workspace` is enabled (Open PR).
- [#2976](https://github.com/sipeed/picoclaw/pull/2976) — **fix: Makefile handle space in Go version string.** Build fix for environments using Go 1.25.10 with specific build flags (Open PR).

**Low / Information:**
- [#2880](https://github.com/sipeed/picoclaw/issues/2880) — Stale Xiaomi Android permission bug, closed without extensive action.

## 6. Feature Requests & Roadmap Signals

**Landed this cycle:**
- **Azure Identity auth** for Azure OpenAI provider ([#2971](https://github.com/sipeed/picoclaw/pull/2971)) — Enterprise compliance feature, widely requested.
- **Bangla i18n** ([#2974](https://github.com/sipeed/picoclaw/pull/2974)) — Growing international localization signals.
- **Web UI image paste/upload** ([#2969](https://github.com/sipeed/picoclaw/pull/2969)) — Key UX improvement for multimodal workflows.

**Strong signals for v0.3.0:**
- [#2977](https://github.com/sipeed/picoclaw/pull/2977) **Cron tool `get`/`update` actions** — Likely to land very soon (hot off the press). Agents will get non-destructive cron manipulation.
- [#2975](https://github.com/sipeed/picoclaw/pull/2975) **Telegram: treat reply to bot as mention** — Community polish for group chat UX.
- [#2856](https://github.com/sipeed/picoclaw/pull/2856) **Media attachments in `message` tool** (Stale, 3 weeks) — Rich outbound delivery for agents.
- [#2838](https://github.com/sipeed/picoclaw/pull/2838) **Agent tool policy filters** (Stale, 3 weeks) — Allow/deny glob patterns for built-in and MCP tools.
- [#2952](https://github.com/sipeed/picoclaw/issues/2952) **Model UI defaults** — Automatic provider pre-fill, drop-down selection, and API test / model list discovery. Strong UX roadmap signal for configuration.

## 7. User Feedback Summary

**Pain Points & Dissatisfaction:**
- The `v0.2.9` upgrade has caused a **functional regression** in the Web UI ([#2972](https://github.com/sipeed/picoclaw/issues/2972)) and context management ([#2968](https://github.com/sipeed/picoclaw/issues/2968)), undermining trust in the latest stable release. User `xpader` reported both.
- The `exec` tool continues to exhibit **cross-model reliability issues** ([#2952](https://github.com/sipeed/picoclaw/issues/2952)), forcing unnecessary extra commands.
- There is an **unmet expectation for polished channel behavior**, particularly the QQ channel restart loop which forces users to clear history manually.
- User `xhynice` ([#2952](https://github.com/sipeed/picoclaw/issues/2952)) explicitly notes that certain behaviors do not follow the `agent.md` specification, indicating a **specification-compliance gap**.

**Positive Signals & Satisfaction:**
- The **community contribution pipeline is exceptionally strong.** Multiple external contributors (kunalk16, lc6464, bogdanovich, Jlan45, maxmilian, SutraHsing) are actively submitting PRs, demonstrating a healthy and invested developer community.
- There is **direct user demand for enterprise and localization features** (Azure Identity, Bangla i18n), suggesting production deployments and a global user base.
- Users are willing to **run nightly builds** and provide detailed bug reports (FreeBSD platform, specific provider chains), which is a sign of a dedicated technical user base.

## 8. Backlog Watch

**Critical—Need Maintainer Triage:**
- [#2972](https://github.com/sipeed/picoclaw/issues/2972) **Web UI message chaos in v0.2.9** — No assignee, no linked fix PR. Highest impact regression in active release.
- [#2968](https://github.com/sipeed/picoclaw/issues/2968) **Context compression token display bug** — Appears related to the same v0.2.9 release wave. Needs investigation.

**Unanswered Complex Community Report:**
- [#2952](https://github.com/sipeed/picoclaw/issues/2952) **Feature request / bug compilation** — Submitted 4 days ago with 3 comments, no maintainer response yet. The combination of bugs (exec, QQ restart) and UX request (model dropdown) requires a considered reply and actionable triage.

**Stalled Major Feature PRs:**
- [#2856](https://github.com/sipeed/picoclaw/pull/2856) **feat(message): support media attachments** (bogdanovich, open since May 11) — Significant scope, no recent interaction. High value for agent capabilities.
- [#2838](https://github.com/sipeed/picoclaw/pull/2838) **feat(agent): support frontmatter tool policy filters** (bogdanovich, open since May 9) — Architectural change for agent security and tool access control. Long idle time risks merge conflicts and contributor burnout.

**Dependency Updates:**
- [#2963](https://github.com/sipeed/picoclaw/pull/2963) **bump larksuite/oapi-sdk-go** (Dependabot, 2 days old)
- [#2962](https://github.com/sipeed/picoclaw/pull/2962) **bump anthropic-sdk-go** (Dependabot, 2 days old)
— Routine, but should be merged promptly to keep the supply chain secure.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**Project Digest: NanoClaw — 2026-05-31**

---

### 1. Today's Overview
Project activity remained extremely high, with 16 PRs and 3 issues updated in the last 24 hours. The team merged 4 PRs spanning infrastructure hardening, new chat features, and efficiency improvements. The dominant themes are **security hardening** and **multi-instance/enterprise readiness**, though a pair of severe filesystem regressions on Apple Container creates a critical risk for Mac-based deployments. Community contribution velocity remains strong, but the supply-chain risk opened around MCP packages is the single highest-attention item in the tracker today.

### 2. Releases
No new releases were published today. The project continues in a rapid-development cycle between stable tags, with energy concentrated on targeted PR merges rather than a formal release cut.

### 3. Project Progress
Four PRs were merged or closed in the last 24 hours, advancing infrastructure, chat features, and developer experience:

- **Multi-Instance Proxy Fix** ([#2652](https://github.com/nanocoai/nanoclaw/pull/2652)) — `matty271828` rewired the OneCLI proxy port logic so that `instances.conf` setups with custom `ONECLI_BASE_PORT` / `ONECLI_PORT_STRIDE` generate correct `HTTPS_PROXY`/`HTTP_PROXY` values instead of hardcoding the default gateway port.
- **Group Chat Context Window** ([#2645](https://github.com/nanocoai/nanoclaw/pull/2645)) — `yairixStudio` added an optional per-agent-group window that sends the last N unseen messages as a `[Context — last N messages]` block when an agent is @-mentioned, significantly improving conversation awareness in group channels.
- **Enhanced Transcript Metadata** ([#2521](https://github.com/nanocoai/nanoclaw/pull/2521)) — `crookies` added `from-channel` and `from-type` attributes to XML message output, directly enabling multi-channel dashboard users to identify origin adapters.
- **IPC Async Migration** ([#6](https://github.com/nanocoai/nanoclaw/pull/6)) — `gavrielc` replaced the legacy synchronous `setTimeout` polling with `fs.watch`-driven file watching, reducing event-loop blocking in the IPC subsystem.

---

### 4. Community Hot Topics

- **[#2641: Supply Chain Risk](https://github.com/nanocoai/nanoclaw/issues/2641)** — Opened by `NoamGit`, this issue warns about the `@gongrzhe/server-gmail-autoauth-mcp` package instructing the agent to auto-install a strangers’ code that then solicits a Gmail password. The underlying need is **sandboxed or explicitly-consented MCP package execution**. With a Medium article amplifying the concern, this is the most security-sensitive open item despite low reaction counts.

- **[#2044: Discord URL Handling Regression](https://github.com/nanocoai/nanoclaw/issues/2044)** — Accumulating 2 👍 reactions, `pwinnski` reports that v2 converts `<URL>` to `[URL](URL)`, which defeats Discord’s native syntax for suppressing link previews. The community expects **behavioral parity with prior adapter versions** and adherence to standard Discord markdown conventions.

- **[#2653: Multi-User Support](https://github.com/nanocoai/nanoclaw/issues/2653)** — A fresh request from `elancode` to run separate Telegram bots and agent groups for multiple users on a single Mac Mini. The author notes the data model already supports this, but the `src/` server runtime is the blocker, signaling strong latent demand for **true multi-tenancy** in the next release.

---

### 5. Bugs & Stability
Ranked by severity:

- **Critical — Apple Container Phantom Inodes ([#2649](https://github.com/nanocoai/nanoclaw/pull/2649), [#2650](https://github.com/nanocoai/nanoclaw/pull/2650))** — A serious virtio-fs regression where nested file mounts for `container.json` and the composed `CLAUDE.md` return `stat()` success but `EACCES` on read, silently disabling *every* MCP server added through `ncl groups config add-mcp-server` on Mac hosts. **Fix PRs are open** by `jurre-mbt-it` and include an overlay-timer retry as a companion workaround.

- **Critical — Interactive Response Boundary ([#2651](https://github.com/nanocoai/nanoclaw/pull/2651))** — `Hinotoi-agent` has an open PR that hardens `ask_user_question` by validating that the response originates from the same channel `platformId`/`threadId` where the question was delivered. **Fix PR is open.**

- **High — MCP Supply Chain Credential Leak ([#2641](https://github.com/nanocoai/nanoclaw/issues/2641))** — No fix PR exists yet. The ecosystem risk of auto-installing MCP packages that exfiltrate credentials remains unmitigated.

- **Medium — Platform ID Encoding Inconsistency ([#2654](https://github.com/nanocoai/nanoclaw/pull/2654))** — `elancode` fixes a case where caller-supplied `<prefix>:<id>` values were rejected when the prefix didn’t match the channel registry key. **Fix PR is open.**

- **Medium — Discord URL Preview Suppression ([#2044](https://github.com/nanocoai/nanoclaw/issues/2044))** — Open for over a month with no fix PR.

---

### 6. Feature Requests & Roadmap Signals

- **Multi-Tenancy ([#2653](https://github.com/nanocoai/nanoclaw/issues/2653))** — The data model for users/roles/`agent_group` is already in place. The server-side `src/` blocker is the prime candidate for the **v2.1 release**. This is the strongest roadmap signal in the current data.

- **Local Voice Transcription ([#2317](https://github.com/nanocoai/nanoclaw/pull/2317))** — The `/add-voice-transcription-free-whisper` skill supports both `openai-whisper` (GPU) and `whisper.cpp` (CPU-only) backends. Pre-flight detection is already written. Merge looks imminent, unlocking private voice channels without API fees.

- **Backup & Restore ([#2084](https://github.com/nanocoai/nanoclaw/pull/2084))** — Daily snapshots with pluggable local/S3 storage and a CLI restore command. Important operational feature for any team considering production deployment. Still awaiting maintainer review.

- **Session Tracing to Hugging Face ([#2648](https://github.com/nanocoai/nanoclaw/pull/2648))** — A new skill for uploading session traces via `/upload-trace`, suggesting a push toward community-driven debugging and model evaluation tooling.

---

### 7. User Feedback Summary

- **Critical Friction:** Mac (Apple Container) users face a show-stopping bug that silently breaks all MCP servers—the highest-severity UX issue currently open.
- **Dissatisfaction on Discord:** `pwinnski` (and implicit voters on [#2044](https://github.com/nanocoai/nanoclaw/issues/2044)) are frustrated that a v2 behavioral change made a feature worse with no workaround.
- **Security Anxiety:** `NoamGit`’s advisory on [#2641](https://github.com/nanocoai/nanoclaw/issues/2641) taps into a growing community fear about auto-executing untrusted MCP packages. Trust and sandboxing are emerging as non-negotiable requirements.
- **Operational Desires:** `elancore` wants to migrate from a single-user setup to a shared family agent. `crookies` praised the logging system but needed source-channel tracking for dashboards. The community is actively demanding **multi-user, observable, and resilient** deployments.
- **Contribution Sentiment:** With 12 open PRs and 4 merged in 24 hours, contributor engagement is very high, suggesting strong satisfaction with the project direction and maintainer receptiveness.

---

### 8. Backlog Watch

- **[#212: WebUI Control Panel](https://github.com/nanocoai/nanoclaw/pull/212)** — This 11-tab, Lit + Vite + Fastify PR from February remains flagged as "Blocked / Pending Closure." Last updated May 30 but no maintainer merge decision. If the project wants this, it likely needs community help to rebase or split it; if abandoned, a formal close would reduce noise.

- **[#2044: Discord URL Regression](https://github.com/nanocoai/nanoclaw/issues/2044)** — Unresolved since April 27. The user is waiting on a fix or acknowledged workaround. A month of silence on a well-understood regression risks alienating a vocal user segment.

- **[#2084: Backup System](https://github.com/nanocoai/nanoclaw/pull/2084)** — Filed April 28 with a polished design (daily snapshots, S3 pluggable, CLI restore). Zero maintainer comments to date. For operators evaluating NanoClaw for production, the absence of a decision here is a red flag.

- **[#2647: Trae/solo agent r2 idy0](https://github.com/nanocoai/nanoclaw/pull/2647)** — Appears to be a generated placeholder or test PR. Requires maintainer triage to either provide review feedback or close.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-31

## 1. Today's Overview

IronClaw logged an exceptionally high-velocity day, with **18 PRs moved** (11 merged/closed) and **4 issues updated**. Activity is evenly split between the ambitious **"Reborn" architectural push**—advancing auth surfaces, triggers, and inbound/outbound delivery facades—and a focused batch of **agent loop hardening patches** (memory compaction, LLM interruptibility, security injection scanning). Several new regular contributors (`neoguyverx`, `italic-jinxin`, `danielwpz`) landed meaningful changes alongside core maintainers, indicating a growing and healthy team. The primary cloud over the project is the **ongoing crates.io publishing stall (Issue #3259)**, which continues to block downstream consumers from accessing features and CVE fixes shipped in v0.25.0–v0.27.0.

## 2. Releases

*No new releases in the last 24 hours.* GitHub tags are at `ironclaw-v0.27.0` (Apr 29, 2026), but [crates.io](https://crates.io/crates/ironclaw) remains stuck at `0.24.0` (Mar 31, 2026).

---

## 3. Project Progress

**Reborn Architecture (Major Milestones):**
- [#4245](https://github.com/nearai/ironclaw/issues/4245) — **Product-facing auth HTTP routes** merged. Exposes manual-token onboarding, account recovery, and refresh endpoints.
- [#4254](https://github.com/nearai/ironclaw/pull/4254) — **Trusted inbound facade** merged. Adds replay-first idempotency and trusted binding resolution for trigger ingress.
- [#4255](https://github.com/nearai/ironclaw/pull/4255) — **Outbound delivery resolution domain types** merged.
- Still open: Triggers crate skeleton ([#4261](https://github.com/nearai/ironclaw/pull/4261)), Outbound communication preferences store ([#4260](https://github.com/nearai/ironclaw/pull/4260)), Slack ProductAdapter ([#4035](https://github.com/nearai/ironclaw/pull/4035)), WebUI OAuth enrichment ([#4257](https://github.com/nearai/ironclaw/pull/4257)).

**Agent Loop Hardening (neoguyverx "Patch" Series):**
- [#4250](https://github.com/nearai/ironclaw/pull/4250) — **Interruptible in-flight LLM calls.** `CancellationToken` wired into `ChatDelegate` so `/interrupt` terminates HTTP streams immediately instead of waiting for completion.
- [#4251](https://github.com/nearai/ironclaw/pull/4251) — **Structured compaction summary.** Replaces free-form LLM summaries with a 7-section template for consistent handoff context.
- [#4252](https://github.com/nearai/ironclaw/pull/4252) — **Memory write behavioral nudge.** Injects a system message prompting `memory_write` after N idle iterations.

**Security & Identity:**
- [#4253](https://github.com/nearai/ironclaw/pull/4253) — **Read-time injection scan for identity files** merged. Scans `AGENTS.md`, `SOUL.md`, etc. for known prompt-injection patterns before verbatim system prompt injection.

**MCP & Tooling:**
- [#4246](https://github.com/nearai/ironclaw/pull/4246) — NEAR AI MCP credentials migrated from static `SecretHandle` to `ProductAuthAccount` runtime credential source.

**Bug Fixes (Merged):**
- [#4258](https://github.com/nearai/ironclaw/pull/4258) — Fixed agent loop terminally failing on dispatch errors (stringified JSON arrays for headers, oneOf/anyOf coercion).
- [#4259](https://github.com/nearai/ironclaw/pull/4259) — Fixed `capability_info` introspection failing for synthetic tools, causing cascading agent failures when models tried to inspect their own tool surface.

---

## 4. Community Hot Topics

- **[#3259 – Crates.io Publishing Block](https://github.com/nearai/ironclaw/issues/3259) (12 comments, Open)**
  The highest-traffic issue by far. Downstream consumers are pinned to v0.24.0 despite the project shipping v0.25.0–v0.27.0. The underlying need is clear: access to new features and, critically, **wasmtime 28.x CVE fixes**. This is a growing trust and dependency management issue for the community.

- **[#228 – Deny-by-default Delegation Policy](https://github.com/nearai/ironclaw/issues/228) (1 comment, Open)**
  A long-running feature request that attracts attention from users running IronClaw in production settings. The underlying need is for **safety and cost governance**—preventing runaway sub-job creation from prompt injection or LLM hallucination.

- **[#4108 – Nightly E2E Failing](https://github.com/nearai/ironclaw/issues/4108) (0 comments, Open)**
  CI stability is a frequent source of background noise. Silent failure on main branch raises risk for any potential release.

---

## 5. Bugs & Stability

*Ranked by severity:*

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **Critical** (CI) | [#4108](https://github.com/nearai/ironclaw/issues/4108) | **Nightly E2E failing** on `v2-engine`. Main branch CI is red, blocking release confidence. | No fix PR yet |
| **Critical** (Functional) | [#4258](https://github.com/nearai/ironclaw/pull/4258) | **Dispatch failures causing terminal run failure** instead of recoverable tool error. Model passes stringified JSON for `builtin.http` headers, agent silently kills the run. | **Fixed** (Merged) |
| **High** (Functional) | [#4259](https://github.com/nearai/ironclaw/pull/4259) | **Synthetic capabilities un-introspectable.** Calling `capability_info { name: "capability_info" }` crashes. Blocks models from validating their own tool surfaces. | **Fixed** (Merged) |
| **Medium** (Performance) | [#4206](https://github.com/nearai/ironclaw/issues/4206) | **Runtime HTTP egress synchronous end-to-end.** Blocks the runtime during network calls. | **Fixed** (Closed) |
| **Medium** (Agent UX) | [#4250](https://github.com/nearai/ironclaw/pull/4250) | **Uninterruptible HTTP streams.** User `/interrupt` ignored until LLM stream completes. | **Fixed** (Merged) |

---

## 6. Feature Requests & Roadmap Signals

- **"Reborn" Architecture (Near-term Prediction):** The relentless delivery of `[codex]` PRs for triggers ([#4261](https://github.com/nearai/ironclaw/pull/4261)), inbound facades ([#4254](https://github.com/nearai/ironclaw/pull/4254)), outbound delivery ([#4255](https://github.com/nearai/ironclaw/pull/4255)), and auth ([#4245](https://github.com/nearai/ironclaw/pull/4245)) suggests the **next major release (v0.28.0+)** will be a Reborn-focused drop. Expect Slack adapter ([#4035](https://github.com/nearai/ironclaw/pull/4035)) and GitHub SSO ([#4229](https://github.com/nearai/ironclaw/pull/4229)) to land imminently.
- **Agent Safety & Governance:** The deny-by-default delegation policy ([#228](https://github.com/nearai/ironclaw/issues/228)) remains the top unaddressed user-facing security feature. The injection scanning work ([#4253](https://github.com/nearai/ironclaw/pull/4253)) may be a prerequisite or stepping stone.
- **Provider Reasoning Preservation ([#4230](https://github.com/nearai/ironclaw/pull/4230)):** An open PR that would preserve OpenAI Codex reasoning summaries and enable Anthropic thinking blocks. This signals a push toward **transparent model reasoning**, likely for the next agent UX iteration.

---

## 7. User Feedback Summary

- **High Dissatisfaction – Release Process:** The dominant user pain point is the **crates.io publishing gap** ([#3259](https://github.com/nearai/ironclaw/issues/3259)). Users are explicitly blocked from consuming critical WASM CVE fixes and new features, eroding trust in the delivery pipeline.
- **High Responsiveness – Runtime Bugs:** The quick successive merges of [#4258](https://github.com/nearai/ironclaw/pull/4258) and [#4259](https://github.com/nearai/ironclaw/pull/4259) demonstrate the team is very responsive to agent-loop-breaking bugs. Users experiencing silent failures or un-introspectable tools will see rapid relief.
- **Unmet Safety Needs:** The delegation policy request ([#228](https://github.com/nearai/ironclaw/issues/228)) languishes with no clear maintainer signal, suggesting a gap for deployment-scale safety controls.
- **Agent UX Improvements:** The patches from `neoguyverx` (interrupts, memory nudges, structured compaction) all address real friction in long-running agent sessions. This suggests the team is listening to feedback around context window management and user control.

---

## 8. Backlog Watch

| Priority | Item | Age | Why It Needs Attention |
|----------|------|-----|------------------------|
| **P0** | [#3259 – Crates.io Publish Block](https://github.com/nearai/ironclaw/issues/3259) | 26 days | **Top community blocker.** Downstream users cannot consume v0.27.0 features or WASM CVE fixes. Single biggest drag on project health. |
| **P1** | [#228 – Deny-by-default Delegation Policy](https://github.com/nearai/ironclaw/issues/228) | 101 days | Long-standing enhancement with no maintainer decision or design doc. Growing risk surface for enterprise deployments. |
| **P2** | [#4108 – Nightly E2E Failure](https://github.com/nearai/ironclaw/issues/4108) | 4 days | Red CI on main branch. Blocks release confidence. Must be resolved before any crates.io push. |
| **P2** | [#4035 – Slack Reborn Adapter](https://github.com/nearai/ironclaw/pull/4035) | 6 days | Key Reborn milestone PR awaiting review. Holding up the integration roadmap. |
| **P3** | [#4230 – Provider Reasoning Preservation](https://github.com/nearai/ironclaw/pull/4230) | 2 days | Open feature PR. Needs review before this UX improvement stalls. |

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

**LobsterAI Project Digest — 2026-05-31**

---

**1. Today's Overview**
Activity on LobsterAI remains at a low ebb today. No new issues were filed, no pull requests were merged, and no releases were published. The sole tracked activity was the update of two open pull requests, both of which had previously been flagged as `[stale]`. This suggests maintainers are performing review maintenance on lingering contributions, but the project is currently in a low-velocity phase with no new features or rapid bug fixes landing.

**2. Releases**
No new versions were released today. The project's latest published stable build remains unchanged.

**3. Project Progress**
No pull requests were merged or closed today. Progress was limited to maintenance activity on two open PRs, both revised on May 30th:

- **PR #1466** ([link](https://github.com/netease-youdao/LobsterAI/pull/1466)): `fix(mcp): modal close button unreachable when content grows tall`
- **PR #1467** ([link](https://github.com/netease-youdao/LobsterAI/pull/1467)): `fix(shortcuts): display Cmd (⌘) instead of Ctrl on macOS`

Neither has advanced to a mergeable state or received additional community engagement.

**4. Community Hot Topics**
No issues or pull requests generated community discussion today. The two open PRs (#1466, #1467) recorded no new reactions or comments. This silence may indicate these are recognized as low-urgency polish fixes awaiting internal bandwidth, or that the active user base is not closely tracking these particular items.

**5. Bugs & Stability**
No new bugs were reported today. Two existing issues remain open with pending fixes under review:

- **Medium Severity — MCP Modal Overflow (PR #1466):** The Modal Content grows tall (e.g., adding multiple env vars or headers), causing the Cancel/Close buttons to scroll out of view. The proposed fix restricts scrolling to the form body rather than the entire modal panel.
- **Low Severity — macOS Shortcut Labels (PR #1467):** The Settings > Shortcuts panel displays "Ctrl" on macOS instead of the native "Cmd" glyph. This is a cosmetic platform detection issue, but it degrades the user experience for Apple users.

No regressions or crashes were reported in the tracked period.

**6. Feature Requests & Roadmap Signals**
No explicit feature requests were filed today. The profile of the two open PRs provides the clearest signal of near-term priorities:

- **MCP Form UX Polish (PR #1466):** The team is investing in the reliability of the MCP configuration interface—a core workflow for AI agent tool integration. This suggests a focus on hardening existing functionality rather than scope expansion.
- **Platform-Specific UI Consistency (PR #1467):** Targeted polish for macOS indicates the project is maintaining its cross-platform commitments.

*Prediction:* The next minor release will likely bundle these two UI/UX fixes if they receive final approvals.

**7. User Feedback Summary**
No direct user feedback was captured via issues or PR comments today. Implicit feedback can be inferred from the open PRs:

- **Pain Point (PR #1466):** Power users configuring extensive MCP environments experience a degraded form interaction where control buttons become unreachable—suggesting a need for better modal overflow handling.
- **Pain Point (PR #1467):** macOS users face inconsistent shortcut notations in the Settings panel, causing confusion or incorrect key presses.

**8. Backlog Watch**
Two PRs are at risk of becoming permanently stalled:

| Item | Created | Last Update | Status | Risk |
|------|---------|-------------|--------|------|
| **PR #1466** ([link](https://github.com/netease-youdao/LobsterAI/pull/1466)) | 2026-04-04 | 2026-05-30 | `[stale]` / Open | UI fix for MCP modal unmerged for ~8 weeks |
| **PR #1467** ([link](https://github.com/netease-youdao/LobsterAI/pull/1467)) | 2026-04-04 | 2026-05-30 | `[stale]` / Open | macOS shortcut fix unmerged for ~8 weeks |

Both are authored by the same contributor (`linlihua`) and were created on the same day. The nearly two-month wait without merge or closure suggests constrained maintainer capacity or unresolved review criteria. Community members relying on macOS shortcut accuracy or MCP modal stability should watch these PRs closely, as they risk closing as inactive if momentum is not regained.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest: 2026-05-31**

### 1. Today's Overview
Project activity today was minimal in volume but concentrated on a technically significant Pull Request. No new releases were published, and no community issues were opened or resolved in the last 24 hours. The entire development pulse revolves around hardening the OpenAI Codex streaming provider for reliable tool-call argument handling. This quiet, engineering-focused day suggests the team is investing in core Agent infrastructure reliability rather than shipping new features or managing a large community support queue.

### 2. Releases
**No new releases today.** Users continue to run on the latest previously published stable versions. No migration notes or breaking change announcements have been issued for this date.

### 3. Project Progress
**No Pull Requests were merged or closed today.**
- **[PR #1088](https://github.com/moltis-org/moltis/pull/1088) (Open): `[codex] Handle OpenAI Codex final tool-call arguments`** authored by `s-salamatov`. This PR advances the project by recording `response.function_call_arguments.done` payloads, synthesizing missing streaming argument deltas from final arguments, and preventing empty argument strings from breaking decode diagnostics. It represents a targeted improvement to streaming reliability.

### 4. Community Hot Topics
Community discussion was effectively silent today, with zero reactions or comments across all tracked items. The only active item drawing attention is:
- **[PR #1088](https://github.com/moltis-org/moltis/pull/1088): [codex] Handle OpenAI Codex final tool-call arguments.** Although it lacks discussion comments, the underlying need is clear: developers building autonomous agents require deterministic tool-call argument streaming that does not fail on incomplete API responses. This PR addresses a subtle but critical edge case in the agent workflow.

### 5. Bugs & Stability
- **Severity: Medium.** A stability gap exists in the OpenAI Codex provider where final tool-call arguments may fail to stream delta events, causing decode diagnostics to behave unpredictably or block agent workflows.
- **Status:** Fix in progress via **[PR #1088](https://github.com/moltis-org/moltis/pull/1088)** (not yet merged). The PR synthesizes missing argument deltas and ensures empty accumulated argument strings do not block diagnostic flow.
- No other bugs, crashes, or regressions were filed today.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were opened today. The current roadmap signal points strongly toward **streaming protocol hardening**. The work in PR #1088 implies the team is prioritising making tool-call streaming resilient to API quirks before building higher-level orchestration features. A future minor release may include improved streaming guarantees as a direct outcome of this PR.

### 7. User Feedback Summary
Direct user feedback was absent from GitHub issues today, offering no new satisfaction or dissatisfaction signals. However, the specific engineering effort in **[PR #1088](https://github.com/moltis-org/moltis/pull/1088)** implies an identified failure mode where the OpenAI Codex provider does not consistently emit argument deltas. This likely reflects a real-world pain point for agent developers using streaming tool calls, and the team is proactively closing that reliability gap.

### 8. Backlog Watch
- **Open Issues: 0.** The issue tracker is completely clean with no unresolved user reports awaiting maintainer attention.
- **Open PRs: 1.** Only **[PR #1088](https://github.com/moltis-org/moltis/pull/1088)** is open and was actively updated today. It does not appear to be stalled.
- **Conclusion:** The project backlog is in excellent health. There are no long-unanswered questions or neglected contributions that pose a risk to community trust. Maintainers appear to be resolving reported items promptly.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw (QwenPaw) Project Digest — 2026-05-31

**Data Source:** github.com/agentscope-ai/CoPaw (Issues & PRs updated in the last 24 hours)

---

## 1. Today's Overview

Project activity on 2026-05-31 was moderate, driven almost entirely by community bug reports and feature discovery. Nine issues were updated, with the Windows Shell Execution UI glitch dominating the conversation across multiple threads. One pull request addressing provider compatibility received renewed attention, but no development branches were merged and no new releases were published. The report cadence suggests a strong power-user base actively stress-testing the Desktop client, Docker environments, and multi-agent integration pathways. The project appears to be in a stabilization phase where critical Windows bugs and protocol interoperability issues are top-of-mind for the community but have not yet been resolved.

---

## 2. Releases

**No new releases were published today.** The latest available versions remain QwenPaw v1.1.7 (Console) and QwenPaw Desktop Tauri v1.1.9, as cited in active bug reports.

---

## 3. Project Progress

**No pull requests were merged today.**

- **Open PR ([#4689](https://github.com/agentscope-ai/CoPaw/pull/4689))** – `feat(providers): route non-standard generate_kwargs into extra_body`. Author: leoleils. Updated: 2026-05-31. This PR aims to fix silent rejection of provider-specific parameters (e.g., DashScope's `enable_search`) by the OpenAI Python SDK. This is the only development action today and signals ongoing backend work for broader API provider compatibility.

- **Closed Issue ([#4828](https://github.com/agentscope-ai/CoPaw/issues/4828))** – Duplicate report of the Windows console flash bug. Closed to consolidate conversation into the original thread ([#4123](https://github.com/agentscope-ai/CoPaw/issues/4123)).

---

## 4. Community Hot Topics

The most intense community discussions revolved around three core areas:

**1. Windows Console Flash Bug (Highest Engagement)**
Multiple users independently reported and reinforced the same bug across three related threads:
- [#4123](https://github.com/agentscope-ai/CoPaw/issues/4123) (8 comments, open since May 8)
- [#4829](https://github.com/agentscope-ai/CoPaw/issues/4829) (2 comments)
- [#4828](https://github.com/agentscope-ai/CoPaw/issues/4828) (closed as duplicate)

The recurring visual glitch where `execute_shell_command` pops a visible cmd.exe window is severely impacting daily workflow on Windows. With no fix yet visible, user patience is clearly wearing thin.

**2. ACP & Multi-Agent Integration ([#4824](https://github.com/agentscope-ai/CoPaw/issues/4824))**
A significant discussion around connecting QwenPaw to Claude Code via Agent Communication Protocol. Users are hitting `protocolVersion` format mismatches, causing `delegate_external_agent` to fail internally. This reflects strong demand for QwenPaw to function as an interoperable node in a multi-agent ecosystem.

**3. Workspace Organization ([#4408](https://github.com/agentscope-ai/CoPaw/issues/4408))**
A long-running feature request (7 comments) advocating for default state files to be placed into a hidden `.qwenpaw` directory to keep user workspaces tidy. This has broad community consensus as a quality-of-life improvement.

---

## 5. Bugs & Stability

**Ranked by Severity:**

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **CRITICAL** | [#4123](https://github.com/agentscope-ai/CoPaw/issues/4123), [#4829](https://github.com/agentscope-ai/CoPaw/issues/4829) | **Windows Console Flash:** `execute_shell_command` flashes a visible cmd.exe window on every call. Open since May 8. Effects compounded when commands are chained. | None identified |
| **HIGH** | [#4454](https://github.com/agentscope-ai/CoPaw/issues/4454) | **`/mission` Command Freeze:** Console becomes completely unresponsive after executing `/mission`. Persists across session resets and mission directory purges. Suggests a deadlock in the control flow. | None identified |
| **MEDIUM** | [#4824](https://github.com/agentscope-ai/CoPaw/issues/4824) | **ACP Protocol Mismatch:** `protocolVersion` format conflicts between QwenPaw and external ACP agents (Claude Code) block delegate execution entirely. | None identified |

**Stability Assessment:** The Windows client stability is the most pressing concern. The duplication of reports (#4123, #4828, #4829, all describing the same root cause) indicates a clear signal that this is the #1 blocker for the Windows user base.

---

## 6. Feature Requests & Roadmap Signals

Several requests today signal where the community hopes QwenPaw is heading:

- **Desktop Path Interactivity ([#4830](https://github.com/agentscope-ai/CoPaw/issues/4830)):** Users want local file paths in model outputs to be automatically rendered as clickable links that open the OS file manager. This is a natural UX evolution for the Desktop client.

- **Agent Interruption Modes ([#4826](https://github.com/agentscope-ai/CoPaw/issues/4826)):** A structured request for three user message handling strategies: Interrupt (cancel current task), Wait (finish task first), and Queue (insert after current tool call). This mirrors mature agent frameworks like Hermes and suggests a need for better human-agent orchestration.

- **Docker Environment Hardening ([#4831](https://github.com/agentscope-ai/CoPaw/issues/4831)):** Request to pre-bundle `psycopg2-binary`, `pytz`, and `mootdx` (a Chinese A-share market data library) in the official Docker image. This reveals a practical use case in financial data operations and database management, where Agent scripts break on container rebuild.

- **Provider API Flexibility ([PR #4689](https://github.com/agentscope-ai/CoPaw/pull/4689)):** Continued work on routing non-standard parameters hints at official support for non-OpenAI providers (or proxy wrappers) in the next patch release.

**Predictions for Next Release (v1.2.0):**
- Provider compatibility fixes from [#4689](https://github.com/agentscope-ai/CoPaw/pull/4689) are likely to land.
- The Windows flash fix is the highest priority bug fix candidate.
- Workspace hygiene ([#4408](https://github.com/agentscope-ai/CoPaw/issues/4408)) has strong momentum for a minor version release.

---

## 7. User Feedback Summary

**Use Cases Identified:**
- **Desktop Agent Workflow:** Windows power users relying on shell automation for development tasks.
- **Multi-Agent Systems:** Users trying to wire QwenPaw into a broader tool ecosystem via ACP (Claude Code).
- **Financial & Data Operations:** Users deploying persistent Agent scripts in Docker for stock data retrieval (mootdx) and PostgreSQL administration (psycopg2).
- **Code Generation & Review:** General agentic coding support.

**Satisfaction Indicators:**
- **High Dissatisfaction:** Windows console flashing is a recurring, unresolved visual regression that significantly erodes trust in the Desktop product.
- **Frustration with Interop:** The ACP protocol mismatch suggests the integration surface is not yet stable enough for production multi-agent setups.
- **Positive Enthusiasm for UX Polish:** Requests for clickable paths and interruption modes signal that users find the core agent capabilities strong and want refinements to the human interface layer.
- **Power User Demographics:** The specificity of requests (mootdx, ACP, interrupt modes) points to a technically sophisticated, non-English-native user base with high expectations for tool reliability.

---

## 8. Backlog Watch

These issues and PRs warrant immediate maintainer attention due to age, severity, or community investment:

| Item | Days Waiting | Reason for Watch |
|------|--------------|------------------|
| **[#4123](https://github.com/agentscope-ai/CoPaw/issues/4123) Windows Flash Bug** | 23 days (since May 8) | **Most critical open bug.** Duplicate reports accumulating. High user frustration. No public fix plan or milestone assigned. |
| **[#4454](https://github.com/agentscope-ai/CoPaw/issues/4454) `/mission` Freeze** | 14 days (since May 17) | High-severity console blocker with no maintainer response logged in the summary. |
| **[#4408](https://github.com/agentscope-ai/CoPaw/issues/4408) Workspace Organization** | 16 days (since May 15) | Broad community consensus for the feature. No milestone or maintainer sign-off visible. |
| **[#4689](https://github.com/agentscope-ai/CoPaw/pull/4689) Provider Fix PR** | 5 days (since May 26) | Unreviewed. A straightforward patch that would resolve real integration pain for non-OpenAI endpoints. Merging would signal active maintenance. |
| **[#4824](https://github.com/agentscope-ai/CoPaw/issues/4824) ACP Protocol** | 1 day | Fresh but represents a growing class of multi-agent interoperability requests. Early triage could prevent duplicate and frustration. |

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for **2026-05-31**.

---

## ZeroClaw Project Digest

### 1. Today's Overview
ZeroClaw saw extremely high activity on 2026-05-31, with a full pipeline of 50 issues and 50 pull requests updated. This day functioned as a significant "landing day": a massive batch of desktop capability features (macOS UI control, permission flows) authored by `theonlyhennygod and foundational full-duplex voice work by `hurtdidit` were closed and merged. 36 issues and 28 PRs were resolved, signaling a strong push toward stabilizing the `v0.8.0-beta` line. No new releases were cut, but the codebase absorbed substantial architectural work that brings the desktop experience and voice pipeline closer to production readiness.

### 2. Releases
No new releases were generated on this date.

### 3. Project Progress
Today marks a major milestone for the **Desktop application** and **Voice** capabilities.

- **Desktop/MacOS:** Six PRs by `theonlyhennygod` landed core capability handlers (click, type, read_ax, notify, approval) and comprehensive permission management flows (Accessibility, Screen Recording, Microphone, Input Monitoring, Full Disk Access, Local Network). These (#6761-#6767) closed the long-standing feature request #6499. A dozen desktop menu-bar parity issues (#6321-#6336, #5649) were also bulk-closed, bringing the menu-bar chat to functional parity with the web dashboard for sessions, settings, tool approvals, and drag-and-drop.
- **Voice Pipeline:** The full-duplex voice vision advanced significantly with the merging of the VAD pipeline, energy-based Voice Activity Detector, and speech capture buffer with STT dispatch (#5974, #5976, #5978).
- **TUI/CLI:** The terminal UI received quality-of-life fixes, including first-run empty state guidance (#6858) and Tab/Shift+Tab mode cycling for compact keyboards (#6952).

### 4. Community Hot Topics
The most engaging threads reflect deep architectural concerns and a strong desire for desktop automation.

- **Computer-Use & Desktop Automation (#6909):** The highest-commented open issue this period. Users are highly interested in having ZeroClaw agents interact with the local GUI (screenshots, mouse, keyboard), mirroring capabilities seen in OpenAI Codex.
- **Architecture RFCs (#6883, #6954, #6969):** Authored by `mov-xound-glitch`, these three RFCs attracted consistent community discussion. They address gaps in the current message pipeline: shared reply constructors, routing scheduled tasks through the orchestrator, and a unified output routing model to control *how* and *where* replies are delivered.
- **TUI Integrator (#6848):** The largest open PR is the integration branch (`feat(integration)`) for the "zero-code" TUI, RPC socket transport, and `DenyWithEdit` approval. It is explicitly marked as "DO NOT MERGE" while seeking first-round feedback from the community.

### 5. Bugs & Stability
Security and provider stability received focused attention on this date.

- **Critical (P1):**
    - **allowed_tools Gap (#6876):** A confirmed bug where `allowed_tools` settings do not restrict MCP tools. This is a serious security governance gap. The fix is directly targeted by open PR #6914.
    - **Subprocess OOM (#6916):** A production vulnerability where child processes (e.g., `wkhtmltopdf`) can allocate unbounded memory. PR #6916 proposing process-memory limits is awaiting review.
    - **Kimi Provider Failure (#7022):** A new P1 bug report indicates the Kimi K2.6 model fails with a 400 error due to the provider adapter always sending a baseline `temperature` of 0.7. No fix PR exists yet.
- **Resolved Fixes:** Several infrastructure bugs were squashed today: WhatsApp LID JID resolution for DM delivery (#7008), proper handling of HTTP-date `Retry-After` headers in webhooks (#7027), and keeping runtime reload defaults context-scoped across agents (#6905).

### 6. Feature Requests & Roadmap Signals
The roadmap trajectory is clearly split between **Desktop Maturation** and **Agent Governance**.

- **Desktop is Almost at Parity:** The bulk closing of ~15 desktop-specific issues strongly suggests the menu-bar Tauri app has achieved feature parity with the web dashboard.
- **Voice:** The merging of the VAD and STT pipeline directly fulfills the full-duplex barge-in request (#5896). This is highly likely to be a headline feature in the next release.
- **Agent Governance RFCs:** The architectural proposals (#6954, #6969) to route scheduled tasks and output controls through the main message pipeline signal a push to unify all agent policies (safety, context, history, modality) into a single core abstraction.
- **Predictions for Next Version:** The landscape strongly points to `v0.8.0-beta-2`, packaging the new TUI, RPC transport, refined approval flows (DenyWithEdit), and the initial voice pipeline. Lower-priority scouting for WASM plugin capabilities (e.g., office document parsing, #7024) suggests future scope expansion.

### 7. User Feedback Summary
Real user pain points and use cases are driving the current architecture.

- **Governance Pain Points:** Users are reporting significant friction with agent control. The inability to restrict MCP tools via `allowed_tools` (#6876) is a critical security gap. The loss of controlled reply delivery (#6969) represents a UX regression for users migrating from related AI agent systems who relied on explicit per-peer modality preferences.
- **Desktop Power Users:** The rapid turnaround and closing of desktop menu-bar requests show a highly responsive team for the "menu-bar power user" workflow.
- **Integrator Use Case:** The production OOM issue (#6916) highlights real-world deployment stress where agents fall back to shell commands. The user base spans voice-first integrators, TUI-focused operators, and desktop automation enthusiasts.

### 8. Backlog Watch
A significant cluster of high-priority security features remains stalled, awaiting maintainer bandwidth.

- **Blocked Security Suite (alex-nax):** Issues **#6914** (allowed_tools enforcement, P1), **#6916** (process memory limits, P1), **#6915** (skill-scoped tool activation, P2), and **#6917** (Composio action scoping, P2) are all simultaneously labeled `status:blocked` and `needs-maintainer-review`. These are foundational for the agent governance model and their movement is likely a prerequisite for the `v0.8.0-beta-2` milestone.
- **Integration Bottleneck:** The massive integration PR **#6848** is explicitly seeking first-round feedback. It remains the largest single blocker for the next tag.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*