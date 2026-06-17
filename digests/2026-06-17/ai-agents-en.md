# OpenClaw Ecosystem Digest 2026-06-17

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-17 03:46 UTC

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

Here is the structured project digest for OpenClaw based on the provided GitHub activity data for **2026-06-17**.

---

## 1. Today’s Overview

OpenClaw is experiencing a very high level of community and developer activity. In the last 24 hours, **500 issues** and **500 pull requests** were updated, with **91 PRs merged/closed** and **one new patch release (v2026.6.8)**. The new release focuses on reducing brittleness in Telegram and WhatsApp channel delivery. While the community is highly engaged in bug hunting and submitting fixes, the sheer volume of contributions is significantly outpacing maintainer review capacity: **466 open issues** and **409 open PRs** remain active, with a majority tagged with `clawsweeper:needs-maintainer-review`. The dominant stability themes across the backlog remain **silent message loss**, **session state corruption**, and **unreliable sub-agent orchestration**.

---

## 2. Releases

**v2026.6.8** was released today.
- **Richer Channel Delivery:**
    - **Telegram**: Structured text rendering is now more robust (tables, lists, expandable blockquotes, preserved line breaks). CLI-backed replies are now supported. ([Issue #92679](openclaw/openclaw Issue #92679), #931…)
    - **WhatsApp**: Now honors configured ACP bindings, fixing delivery configuration mismatches.
- **Migration Notes**: No explicit breaking changes or migration steps were included in the provided changelog excerpt.

---

## 3. Project Progress

Today saw **91 pull requests merged or closed**. Several key fixes advanced the codebase:

- **Discord/Slack Fixes**: `#93874` adds MiniMax `mm:` reasoning tag support to Slack monitors. `#93906` prevents stale tool-failed warnings in Discord when the reply was actually sent.
- **Telegram Quality of Life**: `#70630` silenced fabricated `"No added response from me."` filler messages in DMs.
- **Plugin System Stability**: `#93897` fixes a regression where the `openai-codex` config was silently deleted during plugin entry rewrites. `#93894` allows plugin `openclaw` symlinks that resolve outside the plugin root directory.
- **Media & Vision**: `#93848` fixes a critical bug where Telegram inbound images appeared as `<media:image>` placeholder text instead of being delivered as native vision blocks.
- **Feishu**: `#93850` resolves a deadlock in Feishu webhook URL verification when `encryptKey` is configured.
- **Infra & CI**: `#68936` adds a PR review autofix pipeline and Windows daemon. `#93889` refines the database guard to skip generated bundles, improving CI speed.
- **Cron & Jobs**: `#93847` fixes migrated cron jobs being silently skipped due to a `NULL agent_id`.

---

## 4. Community Hot Topics

The most active discussions reflect deep user demands for **reliability**, **feature parity**, and **platform support**.

- **`#75`** (109 comments, 79 👍) – Linux/Windows Clawdbot Apps:
    *Analysis:* The highest-reacting and most commented issue. Users are explicitly requesting desktop parity for macOS/iOS/Android nodes. This is a significant blocker for broader adoption across enterprise and self-hosted environments. ([Issue #75](openclaw/openclaw Issue #75))

- **`#44925`** (19 comments) – Subagent Completion Silently Lost (P1):
    *Analysis:* Users are discovering hard failure modes where sub-agent tasks time out or fail to announce completion without any error notification. This undermines trust in autonomous multi-agent orchestration. ([Issue #44925](openclaw/openclaw Issue #44925))

- **`#58450`** (15 comments, 3 👍) – Agent Promises Follow-up Without Action:
    *Analysis:* A dangerous UX pattern where the LLM hallucinates intent. The agent states "I’ll check this and get back to you" but triggers no cron, tool call, or sub-agent. This breaks user trust in asynchronous workflows. ([Issue #58450](openclaw/openclaw Issue #58450))

- **`#68596`** (14 comments, 8 👍) – Configurable Streaming Watchdog Timeout (P2):
    *Analysis:* A strong signal from power users adopting long-reasoning models (DeepSeek-R1, Kimi). The hardcoded 30s watchdog trigger is a frequent pain point. Very likely to land in a near-term release. ([Issue #68596](openclaw/openclaw Issue #68596))

- **`#39604`** (13 comments, 9 👍) – `web_fetch` Private Network Access:
    *Analysis:* The community is requesting an explicit opt-in for accessing internal network resources. Indicates growing use of OpenClaw inside local/professional networks. ([Issue #39604](openclaw/openclaw Issue #39604))

---

## 5. Bugs & Stability

This section ranks the most critical stability issues observed in today's activity.

**🥇 Critical (Platinum Hermit / P1):**
- **`#44925`** – Subagent completion silently lost with no retry or notification. (*No dedicated fix PR found blocked by `needs-maintainer-review`*). ([Issue #44925](openclaw/openclaw Issue #44925))
- **`#22676`** – Signal daemon `stop()` race condition on SIGUSR1 restart causes orphaned processes. (*System stability flaw*). ([Issue #22676](openclaw/openclaw Issue #22676))
- **`#92460`** – Isolated cron completion drops the explicit `delivery.channel: "webchat"` config entirely. (*Cron automation does not respect configuration*). ([Issue #92460](openclaw/openclaw Issue #92460))
- **`#54155`** – Gateway memory leak from 389MB to 14.7GB over 4 days. (*Critical SRE concern, open since March*). ([Issue #54155](openclaw/openclaw Issue #54155))
- **`#64810`** – Heartbeat/system events preempt and swallow in-progress Telegram replies. ([Issue #64810](openclaw/openclaw Issue #64810))

**🥈 Severe (Diamond Lobster / P1-P2):**
- **`#62505`** – Coding Agent regression: "never completes anything" (regression from 2026.4.2). ([Issue #62505](openclaw/openclaw Issue #62505))
- **`#50248`** – `sessions cleanup --fix-missing` falsely prunes fresh cron sessions -> **data loss**. ([Issue #50248](openclaw/openclaw Issue #50248))
- **`#59330`** – Control UI Raw mode permanently disabled by a config normalization bug. (14 👍). ([Issue #59330](openclaw/openclaw Issue #59330))
- **`#88657`** – DeepSeek V4 Flash produces incomplete turns via OpenRouter. (P2). ([Issue #88657](openclaw/openclaw Issue #88657))
- **`#40001`** – Write tool lacks append mode, causing isolated cron sessions to overwrite shared files -> **data loss**. (P1). ([Issue #40001](openclaw/openclaw Issue #40001))

**Notable Fix PRs Submitted Today (responds directly to above bugs):**
- **`#93907`** – Fixes flush-race duplicate assistant messages in persistent sessions.
- **`#93848`** – Fixes Telegram inbound media images appearing as placeholders.
- **`#93840`** – Fixes `web_fetch` ignoring the `NO_PROXY` environment variable.
- **`#93882`** – Fixes Telegram `/think` menu to show full levels for Ollama models.
- **`#93850`** – Fixes Feishu webhook URL verification deadlock.

---

## 6. Feature Requests & Roadmap Signals

The community is driving the following strong feature themes, likely for the next `2026.6.x` releases:

**High Likelihood (Close to Merge / High Consensus):**
- **`#68596`** – Configurable streaming watchdog timeout.
- **`#63829`** – Per-agent memory-wiki vault configuration.
- **`#81061`** – Pre-routing inbound message hook (`before_route_inbound_message`).

**Medium Likelihood (Strong Demand, Needs Design Decision):**
- **`#78308`** – Channel-mediated approval envelope for MCP tool calls.
- **`#64046`** – Sensitive data masking in configs, logs, and UI.
- **`#66252`** – Per-agent TTS/STT provider overrides for multi-language support.
- **`#40001`** – Append mode for the `write` tool to prevent cron data loss.

**Longer-Term/Lower Probability (Blocked on `needs-product-decision`):**
- **`#75`** – Linux/Windows native desktop apps.
- **`#54531`** – Force reply to originating channel guarantee.
- **`#39604`** – Private network access opt-in for `web_fetch`.

---

## 7. User Feedback Summary

**Major Pain Points:**
- **Unreliable Agent Execution**: The strongest feedback trend is that agents "just stop working" or silently lie about following up. Issues like `#62505` (Regression), `#44925` (Lost work), and `#58450` (False promises) are the top reliability complaints.
- **Data Loss**: Users are reporting data loss from both the `write` tool (overwriting) and the `sessions cleanup` command. This is a critical trust issue for users automating workflows.
- **Hard Onboarding**: Bugs like `#73814` (installer hangs), `#45765` (nested directories), and `#67366` (crash during token setup) create high friction.
- **Missing Platform Support**: Issue `#75` is a massive pain point for Linux and Windows users who feel locked out of the full OpenClaw desktop experience.

**Expressed Satisfaction:**
- The community is **highly engaged** and technically sophisticated. The submission of 500 PRs in a single day demonstrates that when maintainers designate a fix, the community can execute rapidly.
- Users appreciate the rapid release cycle (v2026.6.8 landing with "less brittle" channel delivery) and the project's general responsiveness to high-severity bugs once they gain visibility.

---

## 8. Backlog Watch

Several critical features and bugs remain in a prolonged "waiting" state, representing the highest risk to project health due to community sentiment or technical debt.

- **`#75` (Linux/Windows Apps):** **Open since 2026-01-01.** The most requested feature (79 👍) with zero movement. Requires a major allocation of engineering resources. ([Issue #75](openclaw/openclaw Issue #75))
- **`#54155` (Gateway Memory Leak):** **P1, Open since March 25.** A massive memory leak (389MB → 14.7GB) is a critical SRE issue that remains unassigned to a fix PR. ([Issue #54155](openclaw/openclaw Issue #54155))
- **`#11665` (Webhook Multi-turn):** **Open since February 8.** A documented feature (`sessionKey` for multi-turn hooks) that was never implemented. Blocks integration users.
- **`#59330` (Control UI Raw Mode):** **14 👍, Open since April 2.** A regressive UX break that power users have been waiting over two months to see resolved.
- **The `clawsweeper:needs-maintainer-review` Bottleneck:**
    The single largest project health risk visible in this data. A massive volume of the most critical P1/P2 bugs (including `#44925`, `#43367`, `#63216`) are blocked by the `needs-maintainer-review` or `needs-product-decision` labels. The community is out-fixing the core team's ability to review, merge, and make architectural decisions. This bottleneck will likely need to be addressed via maintainer hiring, triage rotation, or automated decision gates to prevent contributor burnout.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**AI Agent & Personal AI Assistant Open-Source Landscape**
**Date: 2026-06-17**

---

## 1. Ecosystem Overview

The open-source AI agent ecosystem is experiencing an unprecedented intensity spike, with competing agent frameworks generating thousands of daily contributions across GitHub. A clear bifurcation is emerging between generalist, multi-channel agent runtimes (OpenClaw, ZeroClaw, Hermes) and vertically integrated platforms targeting enterprise or niche use cases (IronClaw, CoPaw, Moltis). The defining theme of this cycle is **reliability engineering under scale** — every major project is actively fighting silent failures, memory leaks, context corruption, and crash loops that emerge under sustained real-world workloads. The most successful projects are now straining under their own momentum, facing maintainer review bottlenecks and security disclosure backlogs that threaten to erode the trust built by their rapid feature cycles.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed (24h) | Release Today | Health Assessment |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 91 | ✅ v2026.6.8 | 🟡 Feature-Rich, Bottlenecked |
| **ZeroClaw** | 50 | 50 | ~15 | ❌ | 🟡 High Velocity, Regressions |
| **CoPaw** | 44 | 40 | 25 | ✅ v1.1.12-beta.1 | 🟢 Hyper-Fast, Healthy |
| **Hermes Agent** | 50 | 50 | 3 | ❌ | 🟢 Robust, Multi-Platform |
| **IronClaw** | 50 | 50 | ~10 | ❌ | 🟢 Strong QA Cycle |
| **PicoClaw** | 15 | 15 | 12 | ✅ Nightly | 🟡 Security Disclosures Pending |
| **NanoBot** | N/A* | 24 | 14 | ❌ | 🟢 Polished, Iterating |
| **LobsterAI** | N/A* | 7 | 6 | ❌ | 🟢 Stable, Focused |
| **NanoClaw** | 6 | 5 | 4 | ❌ | 🟢 Responsive Maintainers |
| **NullClaw** | N/A* | 3 | 0 | ❌ | 🟡 Slow Resolution Cycle |
| **Moltis** | 4 | 2 | 0 | ❌ | 🟢 Niche, Responsive |
| **TinyClaw** | 0 | 1 | 0 | ❌ | 🟢 Stable / Dormant |
| **ZeptoClaw** | 0 | 1 | 0 | ❌ | 🔴 Stagnant / Idle |

*\*N/A indicates issues data was tightly coupled with PR volume or not distinctly reported.*

---

## 3. OpenClaw's Position

**Advantages vs Peers:**
- **Community Scale:** OpenClaw's contribution volume (500 issues/PRs daily) is an order of magnitude above any competitor, giving it unparalleled mindshare, plugin density, and channel integrations (Telegram, WhatsApp, Discord, Slack, Feishu).
- **Reference Status:** As the core reference implementation, it defines the ecosystem's vocabulary and architecture patterns. New features or fixes in OpenClaw often become ecosystem standards.
- **Maturity:** The widest array of working channel integrations and the most extensive plugin system. No other project matches its breadth of out-of-the-box connectivity.

**Technical Approach Differences:**
- Python-based with a highly modular plugin architecture, heavily relying on community-submitted fixes (`clawsweeper` system). This creates a reactive "stability through patches" model, which contrasts with ZeroClaw's Rust-based rigidity or CoPaw's integrated QA cycles.
- Sub-agent orchestration and session management are areas where OpenClaw is *less* mature than focused competitors — issues like silent subagent completion loss (#44925) and session state corruption are top pain points, ceding the "most reliable agent" crown to projects like NanoBot or Hermes.

**Weaknesses:**
- **Maintainer Bottleneck:** The single largest project health risk in the entire ecosystem. 466 open issues and 409 open PRs wait on `needs-maintainer-review`. Merge velocity lags behind volume.
- **Critical SRE Debt:** The gateway memory leak (#54155, open since March) and cron data loss bugs are unaddressed for weeks while community fixes pile up in review queues.
- **Desktop Gap:** The #1 community request (Issue #75, 79 👍) for Linux/Windows native apps has zero maintainer movement, leaving users to seek out desktop-first alternatives like CoPaw.

---

## 4. Shared Technical Focus Areas

The following requirements emerged independently across multiple projects in this 24-hour cycle:

### Context & Session Reliability
- **Projects:** OpenClaw, Hermes, CoPaw, NanoBot, PicoClaw
- **Specific Needs:** Context compaction freezes, session state corruption, silent prompt drops, unbounded context growth, `summarize_token_percent` config violations, context digest token caps.

### Multi-Channel Delivery & Platform Parity
- **Projects:** OpenClaw, ZeroClaw, Hermes, PicoClaw, CoPaw
- **Specific Needs:** Telegram markdown rendering, Slack `@handle` mangling, Discord tool warnings, Feishu deadlocks, Signal approval routing, Mattermost channel discovery.

### Cron & Scheduled Task Infrastructure
- **Projects:** NullClaw, NanoBot, LobsterAI, CoPaw, OpenClaw
- **Specific Needs:** DB-backed schedulers, cron config persistence, silent task failures returning `{success: true}`, per-job model presets, deadline/misfire windows.

### Plugin / MCP / WASM Extensibility
- **Projects:** ZeroClaw, PicoClaw, Hermes, IronClaw, OpenClaw
- **Specific Needs:** MCP tool ecosystem availability, channel registration hooks, extension lifecycle management, zombie subprocess handling, redaction layers.

### Local Model & Provider Compatibility
- **Projects:** NullClaw, Hermes, PicoClaw, ZeroClaw, CoPaw
- **Specific Needs:** Ollama incomplete answers, Qwen CLI auth, OpenRouter rate limit handling, MiniMax-M2.5 XML outputs, Gemini snake_case field names.

### Desktop Client Stability
- **Projects:** CoPaw, Hermes, ZeroClaw, OpenClaw, IronClaw
- **Specific Needs:** macOS crash loops (SIGSEGV), Linux TUI freeze at 100% CPU, Windows prebuilt binary regressions, Config cache pollution on desktop.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | CoPaw | Hermes Agent | IronClaw | NanoBot |
|---|---|---|---|---|---|---|
| **Primary User** | Prosumer / Hobbyist | Rust / MCP Enthusiast | Asian Enterprise / Coder | Enterprise Ops / Multi-Tenant | NEAR Ecosystem / Enterprise | CLI / Web Generalist |
| **Core Architecture** | Python, Plugin-Driven | Rust, WASM-Powered | Python, Desktop-First | Python, Adapter-Based | Full-Stack WebUI | Python, Minimalist |
| **Dominant Channel** | Telegram, Discord | Discord, Slack | Feishu, DingTalk | Telegram, WeCom, Mattermost | Web Gateway | Command Line, Web |
| **Competitive Advantage** | Largest Community, Broadest Integration | Performance, Security Focus | Context Management, Coding Agent | Enterprise Platform Parity | Automations, OAuth/SSO | UX Polish, Onboarding |
| **Biggest Risk** | Maintainer Review Bottleneck | Binary Regressions (v0.8.0) | Stability Under Sustained Use | Desktop TUI Fragility | QA Volume Outpacing Fix Velocity | Network/Proxy Friction |
| **Stance on Extensibility** | Plugin / Modular | WASM / Plugin | Hard-coded + Plugin | Gateway / Adapter | Internal / Native | Provider-Swappable |

**Key Architectural Divergences:**
- **ZeroClaw** (Rust) vs **the rest** (Python): ZeroClaw is positioning itself as the high-performance, secure runtime. Its WASM plugin model and the depth of its MCP dashboard are unique.
- **CoPaw** vs **OpenClaw**: CoPaw prioritizes desktop deep integration (macOS, Windows) and Feishu/DingTalk channels over the broad "connect to everything" approach of OpenClaw. CoPaw merged 25 PRs today vs OpenClaw's 91 but maintains a much tighter feedback loop.
- **Moltis vs everyone**: Full voice-first (WebRTC, live mode) with echo cancellation requirements. No other project is this audio-centric.
- **IronClaw vs everyone**: Focused internally on the NEAR UI platform, with deep investment in automations dashboards, OAuth, and approval workflows that assume a cloud-hosted, multi-tenant architecture.

---

## 6. Community Momentum & Maturity

### Tier 1: Hyper-Scale, High Churn
**OpenClaw, CoPaw, ZeroClaw**
- Maximum feature velocity and community investment.
- High regression rate, maintainer burnout risk, security debt accumulation.
- "Building the plane while flying it." These projects define the frontier but also bear the cost of instability.

### Tier 2: High Growth, High Discipline
**Hermes Agent, IronClaw, PicoClaw, NanoBot**
- Strong, focused feature delivery (WebRTC Voice, Engine V2, Automation UI, plugin hooks).
- Better maintainer responsiveness, tighter triage loops, fewer critical regressions.
- These projects are establishing themselves as the "reliable workhorses" of the ecosystem.

### Tier 3: Steady, Niche-Focused
**NanoClaw, LobsterAI, NullClaw**
- Steady or low activity. Focused on specific backend fixes (credential proxy, scheduled tasks, local inference).
- Risk of stagnation in feature velocity without broader community injection.
- Suitable for users whose needs precisely match their strengths.

### Tier 4: Bootstrapping or Dormant
**TinyClaw, Moltis, ZeptoClaw**
- Minimal daily engagement. Core issues (Windows support, audio pipeline) lack resolution.
- High risk for users seeking a reliable daily driver without contributing code.

---

## 7. Trend Signals

### The "Silent Failure" Crisis
The loudest community complaints across every project are about agents that *silently fail*: prompt drops that return no error (#2751), scheduled tasks returning `{success: true}` while doing nothing (#1424), sub-agent completion loss (#44925), and agents "lying" about follow-ups (#58450). **Reliability is the new feature.**

### Local Context Management is the Gate to Autonomy
Projects are universally investing in context compaction, summarization, `dream` loops, idle compact timers, and Headroom integration. The bottleneck for agent autonomy is no longer the LLM, but how the agent manages its own memory and history. This is the primary technical battleground for stickiness.

### Multi-Channel Parity is Table Stakes
Telegram markdown rendering, Slack `@handle` mangling, and Feishu deadlocks are not "nice to haves" — they are blocking bugs. Users expect a unified agent experience across all platforms. The projects that master cross-platform delivery (OpenClaw's Telegram/WhatsApp polish, Hermes' Mattermost parity) are pulling ahead.

### The Rise of Autonomic Infrastructure (Cron + Automation)
The flurry of automation dashboards, cron subagent engines, and scheduled task backends signals the market moving toward **"set and forget" agents**. The ability to schedule multi-agent workflows, inspect run history, and handle failures (rather than just delivering chat messages) is the next frontier of product value.

### Security Anxiety is Maturing
Credential proxying risk (#1669), SSO OAuth DM-parity (#5009), hardened CI pipelines (#7675), and request redaction layers (#47591) show that security is transitioning from an afterthought to a key product requirement. As agents gain access to files, tools, and networks, users are demanding verifiable guarantees.

### Consolidation Pressure
The "Claw" family fragmented across multiple repos (OpenClaw, NanoClaw, PicoClaw, ZeroClaw, NullClaw, TinyClaw, IronClaw, CoPaw) represents significant duplication of effort. While healthy for competition, the community may eventually consolidate around one or two major players (likely OpenClaw and ZeroClaw given their architectural differences and momentum) to standardize plugin formats, channel delivery, and security auditing.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

**NanoBot Project Digest – 2026-06-17**

---

### 1. Today’s Overview

NanoBot experienced a highly productive day on 2026-06-17, driven by strong maintainer and community activity. A total of 24 pull requests were updated, with 14 merged or closed, signaling a major push toward stability and enhanced usability. The development focus was decisively on polishing the user experience: the WebUI gained a powerful new Automation Management view ([#4330](https://github.com/HKUDS/nanobot/pull/4330)), persistent installer issues on macOS ([#4368](https://github.com/HKUDS/nanobot/pull/4368)) and raw Debian ([#4360](https://github.com/HKUDS/nanobot/issues/4360)) were resolved, and a critical bug preventing local model servers from working behind a proxy gained a fix PR ([#4367](https://github.com/HKUDS/nanobot/pull/4367)). While no official software release was cut today, the volume and quality of completed fixes suggest a stable point release is well-prepared. The project maintains a very healthy pulse, successfully balancing new features with rigorous bug squashing.

---

### 2. Releases

No new releases were published on 2026-06-17. The latest release remains the version prior to this date.

---

### 3. Project Progress

The following significant pull requests were merged or closed today, marking definitive progress:

- **WebUI Automation Management:** [PR #4330](https://github.com/HKUDS/nanobot/pull/4330) was merged, introducing a dedicated management view for user-created automations (filtering, editing, running, pausing) while keeping system jobs read-only.
- **Installer Robustness:** [PR #4368](https://github.com/HKUDS/nanobot/pull/4368) fixed the macOS installer to avoid system-wide pip installs blocked by PEP 668. [PR #4365](https://github.com/HKUDS/nanobot/pull/4365) updated documentation to use a safer `curl | sh` pattern for Docker compatibility.
- **API Reliability:** [PR #4358](https://github.com/HKUDS/nanobot/pull/4358) fixed a bug where empty API responses could duplicate user turns by ensuring the retry path does not re-record the user message.
- **Default Behaviors:** [PR #4370](https://github.com/HKUDS/nanobot/pull/4370) changed the default `idleCompactAfterMinutes` from `0` (off) to `15`, enabling smart background memory management.
- **Context Optimization:** [PR #4352](https://github.com/HKUDS/nanobot/pull/4352) capped the "Recent History" digest by token count instead of character count, preventing stealthy context overflows.
- **Provider Support:** [PR #4361](https://github.com/HKUDS/nanobot/pull/4361) added official thinking support for Kimi K2.7 models.
- **Dream UX:** [PR #4369](https://github.com/HKUDS/nanobot/pull/4369) replaced the opaque "no history" Dream response with a helpful explanation of how the Dream cursor and auto-compaction work.

---

### 4. Community Hot Topics

Several issues and PRs sparked discussion or represent key community interests:

- **Installer Woes:** [Issue #4360](https://github.com/HKUDS/nanobot/issues/4360) ("end of file unexpected" in Docker) accumulated 9 comments before being closed. It highlighted a significant break in the new user onboarding flow.
- **Reliability Concerns:** The bugs around proxy handling ([Issue #4366](https://github.com/HKUDS/nanobot/issues/4366)), API retry logic ([Issue #4079](https://github.com/HKUDS/nanobot/issues/4079)), and stream timeouts ([Issue #4065](https://github.com/HKUDS/nanobot/issues/4065)) clearly resonated with the user base, as they all garnered focused fix PRs within hours of being reported.
- **Automation Enthusiasm:** The merge of the Automation UI ([#4330](https://github.com/HKUDS/nanobot/pull/4330)) combined with the new feature request for cron-level model presetting ([#4378](https://github.com/HKUDS/nanobot/issues/4378)) indicates a strong and growing power-user segment eager for sophisticated agent orchestration.
- **External Integrations:** The community is actively working to expand NanoBot's reach, with a well-documented PR adding Keenable Search ([#4350](https://github.com/HKUDS/nanobot/pull/4350)) and an external service announcing A2A/MCP compatibility ([#4362](https://github.com/HKUDS/nanobot/issues/4362)).

---

### 5. Bugs & Stability

The following bugs were reported or are of high concern today, ranked by severity:

- **[Critical] Git Execution Blocked ([Issue #4375](https://github.com/HKUDS/nanobot/issues/4375)):** Git commands (`add`, `commit`, `push`) are blocked by the workspace security guard even within allowed subdirectories. This breaks core developer workflows. **Status:** Open. No fix PR yet.
- **[High] Proxy Hijacks Local Traffic ([Issue #4366](https://github.com/HKUDS/nanobot/issues/4366)):** Host system `HTTP_PROXY` settings route local model server requests into the void, breaking Ollama/vLLM. **Status:** Fix PR [#4367](https://github.com/HKUDS/nanobot/pull/4367) is open and awaiting merge.
- **[Medium] Workspace Read/Write Asymmetry ([Issue #4374](https://github.com/HKUDS/nanobot/issues/4374)):** Project workspaces read `SOUL.md` from the project root but write it to the default workspace, causing data fragmentation. **Status:** Open.
- **[Medium] Dream Disabled Still Injects History ([Issue #4242](https://github.com/HKUDS/nanobot/issues/4242)):** Setting `dream.enabled = false` prevents the cron job from running but does not stop the "Recent History" section from being injected into the system prompt. **Status:** Open, discussed in conjunction with [PR #4371](https://github.com/HKUDS/nanobot/pull/4371).

---

### 6. Feature Requests & Roadmap Signals

The most notable signals for the future direction of NanoBot include:

- **Advanced Scheduling:** [Issue #4378](https://github.com/HKUDS/nanobot/issues/4378) requests the ability to set model/preset configurations at the cron job level. This, combined with the new Automation UI ([#4330](https://github.com/HKUDS/nanobot/pull/4330)), strongly points to a future version with extremely granular agent lifecycle management.
- **User-Friendly First Run:** [Issue #4376](https://github.com/HKUDS/nanobot/issues/4376) explicitly calls for a rework of `nanobot onboard --wizard` to be less technical. Given the flurry of installer issues ([#4360](https://github.com/HKUDS/nanobot/issues/4360), [#4368](https://github.com/HKUDS/nanobot/pull/4368)), a focus on a "zero-to-hero" onboarding experience is a predictable and necessary roadmap item.
- **Provider Expansion:** [PR #4350](https://github.com/HKUDS/nanobot/pull/4350) adds Keenable as a web search provider, showing the project remains committed to offering a wide array of backend choices.
- **Trust & Safety:** [PR #4053](https://github.com/HKUDS/nanobot/pull/4053) aims to strictly enforce read-only workspace roots. Its lingering open status suggests it requires careful consideration, but its existence confirms a roadmap focus on security boundaries for tool execution.

---

### 7. User Feedback Summary

**Pain (Onboarding):** "Requires knowing many technical details" ([Issue #4376](https://github.com/HKUDS/nanobot/issues/4376)). The installer is not "just works" for macOS or raw Debian environments. The community is signaling a strong need for a polished setup experience.

**Pain (Networking):** Proxy configuration is a recurring headache. The "fix one thing, break another" nature of [Issue #4366](https://github.com/HKUDS/nanobot/issues/4366) is a classic devops pain point. Users want smart, automatic proxy handling that distinguishes localhost from external traffic.

**Pain (Consistency/Confidence):** Users are losing trust in features like Dream ([#4242](https://github.com/HKUDS/nanobot/issues/4242)) and Workspaces ([#4374](https://github.com/HKUDS/nanobot/issues/4374)) behaving non-intuitively. The gap between expected behavior and actual behavior causes confusion around context management.

**Satisfaction (Ecosystem Growth):** External developers are actively contributing sophisticated PRs (Keenable search, Anthropic tool ID sanitization). This shows the codebase has good developer ergonomics and the community is invested in the project's success.

**Satisfaction (Responsiveness):** The high-speed iteration is appreciated. Issues raised by users (e.g., hamb1y, michaelxer) receive fix PRs within hours or days, which fosters a highly collaborative and positive community spirit.

---

### 8. Backlog Watch

The following items remain open for an extended period and may require maintainer attention:

- **[PR #3662](https://github.com/HKUDS/nanobot/pull/3662): Avoid network loads during token estimation.** Opened 2026-05-06. A well-defined optimization that has been open for over six weeks. It addresses a specific pain point for offline or air-gapped environments where `tiktoken` downloads are blocked.
- **[PR #4053](https://github.com/HKUDS/nanobot/pull/4053): Keep read-only roots out of write paths.** Opened 2026-05-29. A crucial security fix that has been open for nearly three weeks. It should be prioritized for review and merge to secure filesystem tools from accidentally writing to read-only directories.
- **[Issue #4242](https://github.com/HKUDS/nanobot/issues/4242): Disabling dream.enabled still injects history.** Opened 2026-06-08. A clear bug with a long lifespan in a fast-moving project. Needs a definitive resolution, perhaps by marking it as blocked by [PR #4371](https://github.com/HKUDS/nanobot/pull/4371) or scheduling a dedicated fix.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — June 17, 2026

## 1. Today's Overview

Hermes Agent is experiencing a sustained surge in community engagement, with **50 Issues and 50 PRs updated in the last 24 hours**, of which **46 Issues and 47 PRs remain open**. This signals an extremely active, high-velocity development cycle. Activity is dominated by bug fixes and platform-specific gateway improvements (Telegram, Feishu, Signal, WeCom, Mattermost), alongside several significant feature PRs for voice and messaging infrastructure. No new releases were cut today, suggesting the maintainers are consolidating a large body of patches for a future stable release. While the rapid pace of change is driving strong feature velocity, a notable number of regressions in the desktop TUI and credential management subsystems is generating community friction.

---

## 2. Releases

No new releases were published in the last 24 hours. The current stable release (referenced in open bug reports as `v0.16.0`) remains the latest. User bug reports reference this version against Qwen CLI v0.18.1 and Python 3.12, indicating the general community deployment baseline.

---

## 3. Project Progress

**3 Pull Requests were merged or closed today**. The visible merged PR in the top 20 is:

- **[CLOSED] [#28981: fix: exclude .stash directory from skill scanning](https://github.com/NousResearch/hermes-agent/pull/28981)** by CountZer0. This adds `.stash` to exclusion sets in `skill_utils.py` and `skill_commands.py`, preventing the Stash skill-sync tool's working data from being scanned as a skill source.

**Significant features advanced in the open PR queue today:**

- **Real-time Voice Platform**: [#47330: feat(voice): real-time voice conversation platform (Daily + Deepgram Flux + Cartesia)](https://github.com/NousResearch/hermes-agent/pull/47330) by yungalgo. Implements WebRTC voice as an in-process Hermes gateway platform plugin.
- **Messaging Platform Parity**:
  - [#47593: feat(mattermost): channel discovery, raw-ID targeting, delete + reactions](https://github.com/NousResearch/hermes-agent/pull/47593) by sidorovanthon.
  - [#47594: fix(gateway): marshal send_message tool sends onto the adapter loop; deliver media in-process](https://github.com/NousResearch/hermes-agent/pull/47594) by sidorovanthon.
- **Developer Infrastructure**: [#47598: feat(cli): per-profile git credential provisioning at boot](https://github.com/NousResearch/hermes-agent/pull/47598) by NimbleCoAI.
- **Platform Fixes**: [#47596: fix(feishu): parse lark-cli interactive card formats for reply-to context](https://github.com/NousResearch/hermes-agent/pull/47596) by pinsily. [#47597: fix(qwen): preserve tool result strings](https://github.com/NousResearch/hermes-agent/pull/47597) by LeonSGP43.
- **TTS Infrastructure**: [#47588: feat(tts): generic streaming dispatcher for all chunked providers](https://github.com/NousResearch/hermes-agent/pull/47588) by Cdddo.
- **Security**: [#47591: Redact secrets in desktop tool transcripts](https://github.com/NousResearch/hermes-agent/pull/47591) by OmarB97.

---

## 4. Community Hot Topics

The most active discussions reveal deep community engagement with complex, high-impact topics:

**Most Discussed:**
- **[#34352: Solving the Multi-Tenant Hermes Problem](https://github.com/NousResearch/hermes-agent/issues/34352)** (8 comments). A community member from NimbleCoAI details how memory operations bypass the hook system entirely, making tenant isolation impossible without forking core. They report running a production fix for months. This is the strongest signal yet that enterprise/multi-user deployment is a top community priority.

**Most Upvoted:**
- **[#6841: Hermes tool-calling pipeline can corrupt tool names and JSON arguments, causing generic tool-call failures](https://github.com/NousResearch/hermes-agent/issues/6841)** (3👍, 2 comments). A persistent P1 bug affecting multiple tools. The community is actively watching this.
- **[#47042: Desktop model picker hides custom providers due to is_aggregator() false positive in dedup logic](https://github.com/NousResearch/hermes-agent/issues/47042)** (2👍). A UX regression strongly felt by power users running custom models.

**Persistent Platform Friction:**
- **[#6388: Telegram MarkdownV2 escape breaks bullet list display](https://github.com/NousResearch/hermes-agent/issues/6388)** (6 comments, 1👍). Open since April, this issue continues to generate discussion. A related issue [#47048](https://github.com/NousResearch/hermes-agent/issues/47048) was filed today detailing an overlapping double-render bug for tables.
- **[#513: Feature: Two-Phase Context Management](https://github.com/NousResearch/hermes-agent/issues/513)** (2 comments). A long-standing feature request inspired by Kilocode, proposing cheaper context compaction. Given the active Codex context growth bug ([#36801](https://github.com/NousResearch/hermes-agent/issues/36801)), this is likely to gain renewed attention.

---

## 5. Bugs & Stability

A significant influx of bug reports was filed today, ranging from P1 pipeline corruption to P3 UI polish items. The project is highly responsive—multiple fix PRs were issued on the same day as their corresponding bug reports.

**Critical / P1 Pipeline Issues:**
- **[#6841: Hermes tool-calling pipeline can corrupt tool names and JSON arguments](https://github.com/NousResearch/hermes-agent/issues/6841)** — Still open. Affects generic tool-call path across multiple tools. The highest severity persistently open bug.

**P2 — Regressions & Core Breakages:**
- **Desktop & Config Regressions:**
  - [#47042: Desktop model picker hides custom providers](https://github.com/NousResearch/hermes-agent/issues/47042)
  - [#47504: "New profile" / "Rename profile" dialogs accept uppercase input then warn instead of normalizing](https://github.com/NousResearch/hermes-agent/issues/47504)
  - [#47515: `hermes config set` silently coerces enum strings "off"/"on" to Python booleans](https://github.com/NousResearch/hermes-agent/issues/47515)
  - [#47116: With `show_reasoning: true`, final answer is deferred and dumped all at once instead of streaming](https://github.com/NousResearch/hermes-agent/issues/47116)
- **Platform Gateway Breakages:**
  - [#46866: Signal approval responses misrouted as steered mid-turn messages](https://github.com/NousResearch/hermes-agent/issues/46866)
  - [#46947: Outbound emails have no way to set a subject](https://github.com/NousResearch/hermes-agent/issues/46947)
  - [#47048: Telegram rich-message final reply overlaps already-streamed legacy MarkdownV2](https://github.com/NousResearch/hermes-agent/issues/47048)
  - [#47093: Telegram photos dropped permanently when get_file() times out before caching](https://github.com/NousResearch/hermes-agent/issues/47093)
- **Provider & Auth:**
  - [#46771: Incompatibility with modern Qwen CLI authentication](https://github.com/NousResearch/hermes-agent/issues/46771)
  - [#46856: OpenRouter provider error classified as unknown → no rate-limit cooldown](https://github.com/NousResearch/hermes-agent/issues/46856)
  - [#46891: Credential pool retry-delay parser doesn't handle absolute-datetime messages](https://github.com/NousResearch/hermes-agent/issues/46891)
  - [#47361: 18 HermesOverlay entries missing extra_env_vars](https://github.com/NousResearch/hermes-agent/issues/47361)
- **MCP Infrastructure:**
  - [#31246: MCP server misconfiguration invisible — logged at DEBUG](https://github.com/NousResearch/hermes-agent/issues/31246)
  - [#47509: Gateway MCP discovery failures logged at DEBUG, invisible at default log level](https://github.com/NousResearch/hermes-agent/issues/47509) (Fix PR [#47602](https://github.com/NousResearch/hermes-agent/pull/47602) issued)
  - [#47510: Gateway MCP stdio subprocesses accumulate as zombies on restart](https://github.com/NousResearch/hermes-agent/issues/47510)

**P3 — Stability & UX:**
- [#41737: Desktop update on Linux freezes at 100% and doesn't restart](https://github.com/NousResearch/hermes-agent/issues/41737)
- [#45924: Hermes + Gemma 4 12B error on basic queries](https://github.com/NousResearch/hermes-agent/issues/45924)
- [#47154: Dashboard file browser returns HTTP 500 on dangling symlinks](https://github.com/NousResearch/hermes-agent/issues/47154)

**Notable Fixes (Today):**
- [#46789: macOS Desktop segfault](https://github.com/NousResearch/hermes-agent/issues/46789) **CLOSED** by javierobcn.
- [#26599: Codex rejects extra_headers](https://github.com/NousResearch/hermes-agent/issues/26599) **CLOSED** by DmitryBMsk.
- [#46320: Desktop model switcher overwrite](https://github.com/NousResearch/hermes-agent/issues/46320) **CLOSED** by NeverLookBackAgain.

---

## 6. Feature Requests & Roadmap Signals

The development trajectory is strongly focused on making Hermes a robust, multi-platform enterprise agent, but desktop and configuration UX regressions are creating headwinds.

**Strong Roadmap Signals (Active PRs):**
- **Real-time Voice**: [#47330](https://github.com/NousResearch/hermes-agent/pull/47330) — This is the largest new capability in the queue. If merged, it positions Hermes as a leading open-source voice agent platform.
- **Mattermost Maturation**: [#47593](https://github.com/NousResearch/hermes-agent/pull/47593) — Channel discovery and reactions bring Mattermost to parity with Discord/Slack.
- **TTS Overhaul**: [#47588](https://github.com/NousResearch/hermes-agent/pull/47588) — A generic streaming dispatcher for all chunked TTS providers.
- **Runtime Transparency**: [#47600](https://github.com/NousResearch/hermes-agent/pull/47600) — Adds `provider_model` and `context_full` fields to the gateway runtime footer.

**Community Wishlist — Likely Candidates for Next Release:**
- **Multi-Tenant Isolation** ([#34352](https://github.com/NousResearch/hermes-agent/issues/34352)): The top community feature request. A fix is running in production.
- **Multi-Gateway Desktop Tabs** ([#45779](https://github.com/NousResearch/hermes-agent/issues/45779)): Power users managing multiple agents across devices.
- **Two-Phase Context Management** ([#513](https://github.com/NousResearch/hermes-agent/issues/513)): Renewed interest given active context growth bugs.

---

## 7. User Feedback Summary

**Pain Points:**
- **Telegram Markdown**: Rendering issues (bullets, tables) remain a top complaint, with active discussion on [#6388](https://github.com/NousResearch/hermes-agent/issues/6388) and [#47048](https://github.com/NousResearch/hermes-agent/issues/47048).
- **Desktop Regressions**: The model picker regression ([#47042](https://github.com/NousResearch/hermes-agent/issues/47042)) and profile dialog validation ([#47504](https://github.com/NousResearch/hermes-agent/issues/47504)) indicate the desktop TUI needs a stabilization pass.
- **MCP Ecosystem**: Silent failures ([#31246](https://github.com/NousResearch/hermes-agent/issues/31246)), zombie processes ([#47510](https://github.com/NousResearch/hermes-agent/issues/47510)), and invisible debug logs ([#47509](https://github.com/NousResearch/hermes-agent/issues/47509)) point to systemic MCP observability and lifecycle issues.
- **macOS Stability**: The segfault in the desktop app ([#46789](https://github.com/NousResearch/hermes-agent/issues/46789)) was a showstopper this week, though it has been closed.

**Use Cases:**
- Users are deploying Hermes in **production multi-tenant environments** ([#34352](https://github.com/NousResearch/hermes-agent/issues/34352)).
- **Multi-device power users** running agents across VPS, home servers, and Macs ([#45779](https://github.com/NousResearch/hermes-agent/issues/45779)).
- **Enterprise platform integration** (Feishu, WeCom, Mattermost, Telegram, Signal).

**Sentiment:**
- **Satisfaction**: The community is deeply engaged and technically sophisticated. The rapid issuance of fix PRs (often on the same day as bug reports) is a strong indicator of project health.
- **Friction**: The velocity of regressions, particularly in the desktop app and credential management, suggests that test coverage may not be keeping pace with feature development.

---

## 8. Backlog Watch

Several high-impact items remain open with significant community attention:

- **[#6841: Tool-calling pipeline corruption](https://github.com/NousResearch/hermes-agent/issues/6841)** (P1, April 2026). The highest severity persistent bug. No fix PR is visible in the top 20. Requires maintainer prioritization.
- **[#513: Two-Phase Context Management](https://github.com/NousResearch/hermes-agent/issues/513)** (Feature, March 2026). Long-standing feature request. The active Codex context growth bug ([#36801](https://github.com/NousResearch/hermes-agent/issues/36801)) is a symptom of this gap.
- **[#6388: Telegram MarkdownV2 escalation](https://github.com/NousResearch/hermes-agent/issues/6388)** (Bug, April 2026). Open for over two months with 6 comments. The root cause is non-trivial.
- **[#31246: MCP silent failures](https://github.com/NousResearch/hermes-agent/issues/31246)** (Bug, May 2026). Logging fix is in review ([#47602](https://github.com/NousResearch/hermes-agent/pull/47602)), but the zombie subprocess issue ([#47510](https://github.com/NousResearch/hermes-agent/issues/47510)) suggests the root cause goes deeper.
- **[#36801: Codex context unbounded growth](https://github.com/NousResearch/hermes-agent/issues/36801)** (Bug, June 2026). Specific to the popular Codex backend. Users report hard context resets on long sessions.
- **[#39806: Stale-state guard for background review writes](https://github.com/NousResearch/hermes-agent/pull/39806)** (PR, June 5). Open for nearly two weeks. Silent blocking issue for self-improving agents.

*End of Digest.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-17

## 1. Today's Overview
Project activity was exceptionally high, with **15 Issues and 15 Pull Requests updated** in the last 24 hours. PicoClaw is clearly in an intensive stabilization and security-hardening phase, driven significantly by a batch of high-severity security advisories filed by external researcher YLChen-007. Maintainers demonstrated strong delivery velocity, closing or merging **12 PRs** spanning critical bug fixes, new extensibility hooks, and core robustness improvements. A new **nightly build (v0.3.0-nightly.20260617)** was published reflecting the latest `main` branch. Overall, the project shows healthy momentum but faces rising pressure to triage a large security disclosure backlog.

---

## 2. Releases

- **Nightly Build v0.3.0-nightly.20260617.a16a1e15**  
  An automated nightly build published to capture the latest `main` branch state. Contains the features and bug fixes detailed in the Project Progress section below. No breaking changes or migration notes accompany this rolling release.  
  **Full changelog comparison:** [v0.3.0...main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)

---

## 3. Project Progress — Merged/Closed PRs (12 Items)

### New Features & Extensibility
- **[PR #3137](https://github.com/sipeed/picoclaw/pull/3137)** — `feat: allow configured remote cron commands`  
  Adds `tools.cron.command_allowed_remotes` config to scope cron execution to specific remote channels, improving security for scheduled tasks.
- **[PR #3120](https://github.com/sipeed/picoclaw/pull/3120)** — `feat(config): add RegisterChannelSettings hook for out-of-tree channels`  
  A major extensibility milestone: third-party channels can now register their own config structures without forking PicoClaw. Signals a clear roadmap toward a plugin ecosystem.

### Bug Fixes (Targeted Resolutions)
- **[PR #3135](https://github.com/sipeed/picoclaw/pull/3135)** — Fixes Telegram forum topics misrouting replies to `#General` by using composite `ChatID` in `InboundContext`.
- **[PR #2983](https://github.com/sipeed/picoclaw/pull/2983)** — Agent now retries semantically empty LLM responses (`content: null` with no tool calls).
- **[PR #2988](https://github.com/sipeed/picoclaw/pull/2988)** — Context compression now correctly respects the `summarize_token_percent` configuration setting.
- **[PR #2987](https://github.com/sipeed/picoclaw/pull/2987)** — `tool_calls` messages are no longer incorrectly dropped during active streaming sessions.
- **[PR #2990](https://github.com/sipeed/picoclaw/pull/2990)** — Web UI session history now displays the full conversation history instead of only the last message.

### Robustness & Code Quality
- **[PR #3132](https://github.com/sipeed/picoclaw/pull/3132)** — Adds `defer-recover` panic recovery to core-path goroutines (tool execution, event handling), preventing single panics from crashing the entire process.
- **[PRs #3127, #3129, #3130](https://github.com/sipeed/picoclaw/pull/3127)** — Explicit error handling cleanups: directory file descriptors, TTS write error paths, and `json.Marshal` errors in `seahorse` tools.

---

## 4. Community Hot Topics

- **Most Active Discussion: Streaming Support**  
  **[Issue #2404](https://github.com/sipeed/picoclaw/issues/2404)** remains the highest-traffic single thread (12 comments, +1 reaction). The request is straightforward: add a `"streaming": true` config flag for HTTP LLM backends to match the OpenAI Python client experience. The underlying need is for **real-time, low-latency interaction** with LLMs, which is a core expectation for any AI agent project in 2026.

- **Largest Topic by Disclosure Volume: Security Audit Wave**  
  Researcher **YLChen-007** filed **10 detailed security advisories** spanning **[Issues #3068 through #3082](https://github.com/sipeed/picoclaw/issues/3068)**. Topics include SSRF bypasses via ISATAP IPv6 address embedding and environment-configured HTTP proxies, MQTT `client_id` spoofing, WeCom group trigger bypass, CSRF in the launcher password setup, and command whitelist escapes via `jq`. While individual thread comments are minimal, the **collective volume and severity** represent the highest-impact community conversation. The deep need is **production-grade security assurance** — users deploying PicoClaw as an agent gateway need confidence in its attack surface.

- **Quick-Turnaround Fix: Telegram Forum Topics**  
  **[Issue #3110](https://github.com/sipeed/picoclaw/issues/3110)** (reported by Giordano10) describing improper topic routing in Telegram Supergroup Forums was met with a rapid fix ([PR #3135](https://github.com/sipeed/picoclaw/pull/3135)) within the same update window, demonstrating responsive maintenance.

---

## 5. Bugs & Stability

*Ranked by severity based on available data:*

### Critical 🚨
- **Security Advisory Cluster** ([Issues #3068–#3082](https://github.com/sipeed/picoclaw/issues/3068)):  
  Ten unpatched advisories exposing SSRF, auth bypass, CSRF, command injection, and replay attack vectors across multiple channels (MQTT, WeCom, LINE, OneBot, `web_fetch`, `exec`, Launcher API). **No dedicated fix PRs have been merged.** The project's stability posture depends entirely on internal triage velocity here. This is the single largest risk factor for project trust.

### Medium ⚠️
- **Telegram Forum Topic Misrouting** ([Issue #3110](https://github.com/sipeed/picoclaw/issues/3110)): Functional regression correctly identifying typing action in the right thread but delivering text to `#General`. **Resolved in [PR #3135](https://github.com/sipeed/picoclaw/pull/3135).**

### Low ✅
- **`su -c` Shell Execution Failure** ([Issue #3134](https://github.com/sipeed/picoclaw/issues/3134)): Agent gateway returns "No daemon is currently running!" on `su -c 'echo OK'`. Reported and closed within the same update cycle.
- **LLM Empty Response Handling** ([PR #2983](https://github.com/sipeed/picoclaw/pull/2983)) / **Streaming `tool_calls` Drop** ([PR #2987](https://github.com/sipeed/picoclaw/pull/2987)): Subtle agent loop bugs, both now merged.

### General Stability
- **[PR #3132](https://github.com/sipeed/picoclaw/pull/3132)** measurably improves resilience by wrapping core goroutines in panic recovery, a meaningful defence against cascading failures.

---

## 6. Feature Requests & Roadmap Signals

- **Strongest Roadmap Signal: Streaming Support**  
  **[Issue #2404](https://github.com/sipeed/picoclaw/issues/2404)** has been open since **April 7, 2026** (over 2 months) and remains the single most-commented feature request. Prediction: **Inclusion in the next minor stable release (v0.4.0)** given its community demand and the project's typical responsiveness to UX gaps.

- **Infrastructure Signal: Plugin Ecosystem**  
  The merge of **[PR #3120](https://github.com/sipeed/picoclaw/pull/3120)** (out-of-tree channel settings hooks) is a deliberate architectural investment. It strongly suggests the v0.4.0+ roadmap includes a stable public API for community-contributed channels, reducing the need to fork the core repository.

- **Pending Features (Open PRs Requiring Merge):**
  - **[PR #3116](https://github.com/sipeed/picoclaw/pull/3116)** — Complements the Pico `turn.done` lifecycle; critical for protocol-aware message routing.
  - **[PR #3115](https://github.com/sipeed/picoclaw/pull/3115)** — Prevents session history corruption when tool output contains `data:image/...;base64,...` strings.
  - **[PR #3136](https://github.com/sipeed/picoclaw/pull/3136)** — Adds snake_case `thought_signature` field for Gemini 3.5 Flash Agentic reasoning compatibility.

---

## 7. User Feedback Summary

**Pain Points Addressed Rapidly:**
- *Giordano10* reported Telegram forum topic misrouting ([Issue #3110](https://github.com/sipeed/picoclaw/issues/3110)) — fixed within days by [PR #3135](https://github.com/sipeed/picoclaw/pull/3135).
- *nongwoluanlai666* reported `su -c` failure in agent gateway ([Issue #3134](https://github.com/sipeed/picoclaw/issues/3134)) — closed same day.

**Subtle Configuration-Dependent Bugs:**
- Web UI session history truncation, context compression ignoring `summarize_token_percent`, and `tool_calls` dropping during streaming (resolved in [PRs #2990, #2988, #2987](https://github.com/sipeed/picoclaw/pull/2990)). These indicate a need for more comprehensive integration testing of configurable features.

**Underlying Use Cases:**
Active users are deploying PicoClaw as a **multi-channel AI agent gateway** integrating Telegram, LINE, WeCom, MQTT, and OneBot. Secondary use cases include **cron-driven scheduled actions** and **tool-augmented code execution** (`exec`, `read_file`, `jq`).

**Satisfaction/Dissatisfaction Balance:**
User sentiment appears to be **cautiously positive** — bug fix velocity is genuinely high and the project is structurally investing in extensibility ([PR #3120](https://github.com/sipeed/picoclaw/pull/3120)). However, the deluge of security disclosures ([Issues #3068–#3082](https://github.com/sipeed/picoclaw/issues/3068)) with no visible patch PRs represents a growing trust liability the project must address urgently.

---

## 8. Backlog Watch

### 🔴 Urgent: Security Disclosure Triage
The **10 advisories filed on June 9, 2026** by YLChen-007 ([Issues #3068–#3082](https://github.com/sipeed/picoclaw/issues/3068)) are the single most pressing backlog item. They have been updated (likely by stale-bot or maintainer tagging) but remain entirely open with **no linked fix PRs**. This cluster demands immediate public CVEs or patch releases to maintain community trust. The longer these sit open, the more they degrade the project's security reputation.

### 🟡 Stale High-Impact Feature Request
**[Issue #2404](https://github.com/sipeed/picoclaw/issues/2404)** (Streaming HTTP config) — open since **April 7 (71 days)**. While active, it has no milestone, no assignee, and no linked PR. Risk of going cold is moderate, but given it is the most-liked and most-commented issue, periodic status updates would meaningfully improve community sentiment.

### 🟢 Open PRs Awaiting Maintainer Review
- **[PR #3116](https://github.com/sipeed/picoclaw/pull/3116)** (turn.done lifecycle signaling) — important for Pico protocol message flow; opened June 12.
- **[PR #3115](https://github.com/sipeed/picoclaw/pull/3115)** (Inline data URL handling fix) — prevents session history corruption from tool output; opened June 12.
- **[PR #3136](https://github.com/sipeed/picoclaw/pull/3136)** (Gemini snake_case `thought_signature`) — compatibility fix for Gemini 3.5 users; opened June 16.

### Summary of Project Health
PicoClaw exhibits strong **feature velocity and maintenance responsiveness**, but its security posture is currently under external scrutiny. The project's next 2–3 release cycles are likely to be dominated by patching the security advisory backlog and finally delivering the long-awaited streaming support. The infrastructure investments in PR #3120 suggest a maturing project positioning itself for a broader contributor ecosystem.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-17
*Generated from GitHub activity for 2026-06-16.*

---

### 1. Today’s Overview
The project saw a productive 24 hours with **5 Pull Requests updated** (4 merged/closed) and **6 Issues updated** (5 active). The high merge rate signals strong maintainer focus on closing critical bugs and feature skills. A significant UX fix landed for budget-exhaustion handling (Issue #2751 / PR #2759) and a new webchat channel skill was merged. No new releases were cut today, but the accumulated merged work suggests a solid foundation for the next version. Overall project health is robust, with active triage of community issues and growing attention to enterprise/managed-fleet deployment patterns.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Project Progress
- **Budget Error Handling (Critical Fix):** PR [#2759](https://github.com/nanocoai/nanoclaw/issues/2759) by `assapin` was **merged**. It closes Issue [#2751](https://github.com/nanocoai/nanoclaw/issues/2751) by ensuring that budget/token-exhausted LLM turns are delivered as error responses to the user instead of being silently dropped.
- **Infrastructure Reliability:** PR [#2782](https://github.com/nanocoai/nanoclaw/issues/2782) by `0xemc` was **merged**. It makes the Tailscale Docker routing service self-healing, addressing a bug where Tailscale flushed IP rules mid-session and broke Docker connectivity.
- **Feature Skill:** PR [#2069](https://github.com/nanocoai/nanoclaw/issues/2069) by `javexed` was **merged**, introducing a new webchat channel skill to the project.
- **Documentation Clarity:** PR [#2775](https://github.com/nanocoai/nanoclaw/issues/2775) by `Koshkoshinsk` was **merged**, fixing the changelog to clarify that OneCLI gateway is a separate operator-managed upgrade, not an automatic part of a NanoClaw update.
- **Open Feature (Managed Fleets):** PR [#2780](https://github.com/nanocoai/nanoclaw/issues/2780) by `gabi-simons` is **open**, proposing an `NANOCLAW_DISABLE_UPGRADE_TRIPWIRE` environment variable for immutable image deployments.

### 4. Community Hot Topics
- **Anthropic Policy Compliance & Credential Proxy Risk:** Issue [#1669](https://github.com/nanocoai/nanoclaw/issues/1669) (*Created 2026-04-06, Updated 2026-06-16*) asks whether the Credential Proxy implementation risks triggering Anthropic anti-fraud bans. Despite low comment volume, this touches on a foundational trust-and-safety concern for any user routing traffic through a reverse proxy. The community needs an official maintainer assessment.
- **Slack @handle URL Mangling:** Issue [#2779](https://github.com/nanocoai/nanoclaw/issues/2779) (*Created 2026-06-16*) reports a high-friction bug where links containing `@handles` (e.g., HackMD, Mastodon) get rewritten as broken Slack mentions. This is a daily workflow blocker for teams sharing links via the Slack channel.
- **Silent Prompt Drops (Now Fixed):** Issue [#2751](https://github.com/nanocoai/nanoclaw/issues/2751) (*Closed by PR #2759*) generated significant user concern. Silent failures represent the worst possible UX for an agent platform, making the quick fix highly appreciated by the community.

### 5. Bugs & Stability
- **[HIGH] Slack URL @handle Mangling (#2779):** URLs containing `@` in their path are corrupted by Slack’s mention parser. No fix PR yet. This is a recent, high-impact regression for any Slack-connected deployment.
- **[MEDIUM] Container Runner Staleness Check (#2784):** The `container-runner` syncs agent source code into session directories using `index.ts` as the sole staleness marker. Changes to files like `ipc-mcp-stdio.ts` are not detected, resulting in stale runtime environments. Reported by `masslbp`.
- **[MEDIUM] Security Documentation Drift (#2783):** The `docs/SECURITY.md` describes a retired v1 trust model and references a non-existent skill. This creates confusion for operators and auditors relying on canonical security docs.
- **[LOW] OneCLI Changelog Misleading (#2775):** Resolved by merged PR #2775.
- **[RESOLVED] Silent Budget Drops (#2751):** Resolved by merged PR #2759.

### 6. Feature Requests & Roadmap Signals
- **Native Credentials Bypass (Likely Next):** Issue [#2781](https://github.com/nanocoai/nanoclaw/issues/2781) by `shekohex` requests an env var (`NANOCLAW_NATIVE_CREDENTIALS`) to skip the OneCLI gateway. This is a strong signal from downstream packagers deploying in sandboxed or heavily locked-down environments. Given the existing PR #2780 for managed-fleet opt-outs, expect the maintainers to prioritize enterprise deployment flexibility.
- **Webchat Channel (#2069):** The merge of this feature skill signals a roadmap priority for expanding beyond Slack/CLI into browser-based interfaces.
- **Upgrade Tripwire Opt-Out (#2780):** This open PR aligns with the Native Credentials request, indicating a concerted push toward supporting immutable, automated deployments.

### 7. User Feedback Summary
- **Satisfaction Point:** Users experienced a rapid resolution of the budget-exhaustion silent-drop bug (Issue #2751 / PR #2759), demonstrating responsive maintainers when critical UX failures are reported.
- **Package/Distribution Pain Point:** `shekohex` and other downstream packagers face friction from the OneCLI gateway dependency, expressing a clear need for a simpler, env-var-driven credential injection path.
- **Integration Pain Point:** `GitOnion` reports that sharing common online resources (HackMD, Medium) via Slack is broken, limiting the agent’s utility as a communication tool.
- **Trust Anxiety:** `LCJD99` (Issue #1669) expresses genuine concern about API account safety, reflecting a silent anxiety that likely affects a broader segment of users.
- **Developer Experience:** `masslbp` (Issue #2784) highlights DX friction for anyone hacking on the container runner due to incomplete file-watching logic.

### 8. Backlog Watch
- **Primary Concern: Issue #1669 — Credential Proxy Anthropic Account Ban Risk**
  - **Link:** [Issue #1669](https://github.com/nanocoai/nanoclaw/issues/1669)
  - **Age:** Created 2026-04-06 (over 2 months old)
  - **Status:** Open, 1 comment, no maintainer response.
  - **Assessment:** This is a foundational trust-and-safety issue that touches the core value proposition of the project. The lack of an official maintainer stance or technical deep-dive on how the proxy interacts with Anthropic’s anti-fraud systems is a significant gap. Prioritizing an official response here would greatly improve community confidence and reduce support burden downstream.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-17

## 1. Today's Overview
Today’s activity reveals a project in a constructive, maintenance-heavy phase. While no new releases were shipped, three Pull Requests saw active updates targeting critical deficiencies in automation and enterprise connectivity. Community-reported bugs in local LLM inference and cron token management continue to drive development focus. The rapid pairing of issue reports to dedicated fix PRs indicates a responsive maintainer cycle aimed at shoring up core reliability ahead of the next stable release.

## 2. Releases
No new releases were published.

## 3. Project Progress
No Pull Requests were merged in the last 24 hours, but three open branches received meaningful updates:

- **[PR #959 (fix/cron): Persist paired token for scheduler tool access (#839)](https://github.com/nullclaw/nullclaw/pull/959)** — Implements encrypted token persistence to the paired_token store on successful `/pair`, directly targeting the scheduler access failure reported in Issue #839. Security hardening via `SecretStore` (ChaCha20-Poly1305, `enc2:` envelope, mode `0600`).

- **[PR #958 (fix/teams): Accept lowercase `serviceurl` JWT claim](https://github.com/nullclaw/nullclaw/pull/958)** — Resolves a `403` rejection of inbound MS Teams messages by accepting lowercase `serviceurl` JWT claims alongside the expected camelCase `serviceUrl`, and raises the JWKS fetch cap.

- **[PR #783 (feat/cron): Cron subagent, run history, JSON output, security hardening](https://github.com/nullclaw/nullclaw/pull/783)** — Continued evolution of the massive cron subagent feature (DB-backed scheduler, atomic tick/enqueue/complete, per-job TZ offsets, delivery routing, operator alerts, `cron list --json` output). This long-running branch remains the project’s most significant under-review feature.

## 4. Community Hot Topics
- **[Issue #952 (Ollama incomplete answers)](https://github.com/nullclaw/nullclaw/issues/952)** — The newest and most concerning discussion for local LLM users. The agent fails to return complete sentences when using Gemma via Ollama. No dedicated fix PR has appeared yet, making this the highest-stakes open discussion thread. Underlying need: reliable full-context streaming from local models.

- **[Issue #839 (Scheduler token access)](https://github.com/nullclaw/nullclaw/issues/839)** — A longstanding core blocker from April 18 finally connected to a dedicated fix branch (PR #959). The underlying need is clear: automation reliability. This issue represents the project’s most impactful resolved pain point this cycle.

- **[PR #783 (Cron subagent)](https://github.com/nullclaw/nullclaw/pull/783)** — While comments are minimal on the thread, its sheer scope and longevity make it a de facto hot item. The community implicitly signals strong demand for scheduled task infrastructure.

## 5. Bugs & Stability
### Critical
- **Issue #952: Ollama returns incomplete answers (Local model regression)** — Core inference pipeline appears to truncate responses for local models (Gemma/Ollama). No fix PR in flight yet. **Severity: Critical**—directly undermines the project’s local-first value proposition.

- **Issue #839: Scheduler token access denied (Automation failure)** — `bit` cannot access the scheduler. Two-month-old regression now directly patched in PR #959. **Severity: High**—being actively remediated.

### Moderate
- **PR #958 addressing Teams 403 error (Integration regression)** — Bot Framework token validation fails on lowercase `serviceurl` JWT claims. Fix PR exists and is under review. **Severity: Moderate**—affects all inbound Teams traffic.

## 6. Feature Requests & Roadmap Signals
The most prominent roadmap signal is **[PR #783 (Cron subagent engine)](https://github.com/nullclaw/nullclaw/pull/783)**. This feature bundles a complete DB-backed scheduler, run history, JSON CLI output, and security hardening—suggesting a major leap in NullClaw’s autonomous operating capabilities. If merged, it unlocks fully auditable, scheduled multi-agent workflows.

Additionally, the intense interest in **[Issue #952 (Ollama completions)](https://github.com/nullclaw/nullclaw/issues/952)** signals that reliable local model inference is the community’s top unmet expectation. A streaming / token-buffering fix is likely to feature prominently in the next release.

## 7. User Feedback Summary
- **Pain Point: Local inference reliability.** The incomplete answer bug (#952) is a sharp regression for users relying on open-weight models. Expectation: "The agent should answer in complete sentences."
- **Pain Point: Automation uptime.** The scheduler token bug (#839) eroded trust in cron-based workflows for nearly two months. The PR #959 fix is welcomed but the delay drew negative attention.
- **Satisfaction Driver: Maintainer responsiveness.** The direct linkage of Issue #839 to PR #959 signals that maintainers are actively tracking production blockers and prioritizing architectural fixes over new features.

Overall sentiment skews toward frustration with stability regressions, tempered by confidence that core issues are being addressed surgically.

## 8. Backlog Watch
- **[Issue #839 (Apr 18) – Scheduler token access](https://github.com/nullclaw/nullclaw/issues/839)** — Languished for 59 days before attracting a dedicated fix PR. This timeframe is concerning for a core component like scheduled task execution. Close monitoring of PR #959’s merge velocity is advised.

- **[PR #783 (Apr 7) – Cron subagent engine](https://github.com/nullclaw/nullclaw/pull/783)** — Open for over 70 days. While complex features naturally require extensive review, the lack of merging risks feature drift and community fatigue. This PR remains the single largest unresolved item in the project’s development pipeline and should be a high priority for closure in the coming weeks.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-06-17

## 1. Today's Overview
IronClaw development is firing on all cylinders, with **50 issues** and **50 pull requests** updated in the last 24 hours across the Reborn platform. The day's activity is overwhelmingly dominated by two themes: a **massive QA audit of the Automations dashboard** and a **completion sprint for Engine V2 Milestone 0**. The core engineering team (serrrfirat, henrypark133, ilblackdragon) is responding to bugs at a rapid cadence—several QA findings from QA contributor sunglow666 already have fix PRs attached or merged within the same cycle. The Reborn WebUI is clearly the active battleground, with intense work streaming into automations management, OAuth security, approval workflows, and Google Drive integration. While the sheer volume of open issues (32/50) indicates a project still deep in feature development, the team's velocity and responsiveness signal solid project health.

## 2. Releases
No new releases were published today.

## 3. Project Progress
The most significant advancement today is the **closure of the Engine V2 Milestone 0 track**, signaling a transition from design to implementation.

**Merged/Closed Today:**
- **Engine V2 Milestone 0**: The parent design epic ([Issue #2721](https://github.com/nearai/ironclaw/issues/2721)), the evaluation criteria ([Issue #2725](https://github.com/nearai/ironclaw/issues/2725)), and the sub-tasks for CodeAct prompt tightening ([Issue #2724](https://github.com/nearai/ironclaw/issues/2724)) and orchestrator loop behavior ([Issue #2723](https://github.com/nearai/ironclaw/issues/2723)) are all closed, indicating the design phase for multi-route execution is complete.
- **Vision Support (OpenAI-compat)**: PR [#4902](https://github.com/nearai/ironclaw/pull/4902) (ilblackdragon) merged, adding inline base64 `image_url` content part support to `POST /v1/chat/completions`.
- **Sanitized Command Display**: PR [#4858](https://github.com/nearai/ironclaw/pull/4858) (think-in-universe) merged, fixing shell command visibility in approval dialogs and activity history.
- **Approval Gate Denial Fix**: PR [#4954](https://github.com/nearai/ironclaw/pull/4954) (henrypark133) merged, allowing approval-gate denial to surface to the model instead of canceling the run.
- **Benchmark Workflow**: PR [#4995](https://github.com/nearai/ironclaw/pull/4995) (pranavraja99) merged, forwarding `NEARAI_API_KEY` so Reborn runs use NEAR AI cloud.
- **UI Polish**: Issue [#4723](https://github.com/nearai/ironclaw/issues/4723) (composer hover state) and [#4857](https://github.com/nearai/ironclaw/issues/4857) (clean state provider label) were closed.
- **Content Digest Plumbing (PR2)**: PR [#5000](https://github.com/nearai/ironclaw/pull/5000) (serrrfirat) opened, adding inert content-digest plumbing for future output-aware progress tracking.
- **No-Progress Stop Honesty**: PR [#4993](https://github.com/nearai/ironclaw/pull/4993) (serrrfirat) opened, fixing the agent loop to report honest failures instead of faking completion on no-progress stops.

## 4. Community Hot Topics

**Automations Dashboard UX (Highest Volume)**
QA contributor **sunglow666** filed an extensive battery of issues today, making automations the single hottest topic:
- [#5004](https://github.com/nearai/ironclaw/issues/5004): Failure summary card provides no actionable information on which automation failed, why, or when.
- [#5005](https://github.com/nearai/ironclaw/issues/5005): No pause/resume/edit/delete actions from the dashboard.
- [#4980](https://github.com/nearai/ironclaw/issues/4980): Empty state does not explain *how* to create automations.
- [#4981](https://github.com/nearai/ironclaw/issues/4981): Status badges (MUTED, SIGNAL, INFO) are confusing and unrelated to automation state.
- [#4988](https://github.com/nearai/ironclaw/issues/4988): Recent runs visualization (colored dots) is unintuitive and lacks tooltips.
- [#4987](https://github.com/nearai/ironclaw/issues/4987): Automation run threads requiring approval are hidden from the normal conversation list.
- [#4918](https://github.com/nearai/ironclaw/issues/4918): Logs page shows zero entries for both successful and failed automation runs.

**Underlying Need**: Users require **enterprise-grade operability** for scheduled agent workflows. The current dashboard communicates state visually but provides no diagnostic tooling, no manual controls, and no clear path for intervention when an automation blocks. This is a critical UX gap for anyone trying to run IronClaw agents "in production."

**Slack OAuth Security**
Issue [#5009](https://github.com/nearai/ironclaw/issues/5009) from a security reviewer (henrypark133) demands structural DM-parity for the live Slack OAuth path, ensuring the authorization URL is only posted into verified personal DMs. This follows the triggered-run fix in PR [#4953](https://github.com/nearai/ironclaw/pull/4953). The underlying concern is preventing credential leaks in multi-tenant Slack setups.

## 5. Bugs & Stability

**Critical / High Severity**
- **Recurring Automation Blocked Pending Approval** ([Issue #4986](https://github.com/nearai/ironclaw/issues/4986)): Automations requiring `builtin.http` can become permanently stuck in "waiting for approval" state with no visible thread. **No fix PR attached yet** — this is a top-tier operational risk.
- **Local-Dev SSO Mismatch** ([Issue #4992](https://github.com/nearai/ironclaw/issues/4992)): Railway-hosted Reborn automations fail before run/thread creation due to SSO access mismatch. Fix PR [#5003](https://github.com/nearai/ironclaw/pull/5003) (thisisjoshford) is open and active.
- **WASM Google Drive Auth Dead-End** ([Issue #4991](https://github.com/nearai/ironclaw/issues/4991)): Expired OAuth tokens surface as opaque `operation_failed` errors with no refresh-retry or `AuthRequired` gate, leaving the agent stuck.

**Medium Severity**
- **Tool Activity Disappears on Railway** ([Issue #4853](https://github.com/nearai/ironclaw/issues/4853)): Tool activity count increases correctly during execution but entries disappear on completion in multi-tenant environments.
- **Tool Call Reload Bug** ([Issue #4942](https://github.com/nearai/ironclaw/issues/4942)): Failed tool calls remain invisible until manual reload.
- **Approval Denial State Persistence** ([Issue #4977](https://github.com/nearai/ironclaw/issues/4977)): Denied approvals can remain displayed as `RUN` until refresh, with ordering issues across repeated calls.
- **Linear Extraction Cap** ([Issue #4999](https://github.com/nearai/ironclaw/issues/4999)): Google Drive binary doc extraction is currently capped at 1 MB via the WASM round-trip.

**Low Severity / Polish**
- **"New" Button Font Size** ([Issue #4972](https://github.com/nearai/ironclaw/issues/4972)): Visual inconsistency in sidebar.
- **Skills Validation Persistence** ([Issue #5007](https://github.com/nearai/ironclaw/issues/5007)): Error message remains after fields are filled.
- **Limited Clickable Area** ([Issue #4982](https://github.com/nearai/ironclaw/issues/4982)): Only the name portion of an automation row is clickable for selection.

## 6. Feature Requests & Roadmap Signals
Several large features in flight today give strong signals about the near-term direction:

- **Agent Context Profile** (PR [#5008](https://github.com/nearai/ironclaw/pull/5008), henrypark133): A per-user, always-injected profile providing timezone, locale, and location. This is explicitly part 1 of a two-part memory split. **Expect this in the next release** — it is a large feature (XL) marked risk:low.
- **Binary Document Extraction** (PR [#4997](https://github.com/nearai/ironclaw/pull/4997), zetyquickly): Host-side text extraction for PDF/PPTX/DOCX/XLSX via the Google Drive download capability. Issue [#4999](https://github.com/nearai/ironclaw/issues/4999) immediately requests scaling past the 1 MB WASM cap, signaling high user demand.
- **Slack WebUI Migration** (PR [#4712](https://github.com/nearai/ironclaw/pull/4712), serrrfirat): Moving Slack setup from TOML into the WebUI. A large feature that lowers the barrier for channel integrations.
- **Preview Deployments** ([Issue #4881](https://github.com/nearai/ironclaw/issues/4881), think-in-universe): Request for Vercel-like preview deployments for PRs — a strong signal of scaling development infrastructure.
- **Engine V2 Admin Telemetry** ([Issue #4985](https://github.com/nearai/ironclaw/issues/4985), think-in-universe): Persisting LLM usage data so `/api/admin/usage` returns data under Engine V2, suggesting administrative tooling is a priority.
- **Extension Lifecycle** (PR [#4518](https://github.com/nearai/ironclaw/pull/4518), PR [#4996](https://github.com/nearai/ironclaw/pull/4996)): E2E coverage + stale onboarding fix for extensions suggests the extension system is nearing feature-complete.

## 7. User Feedback Summary
The primary user personas visible in the data are **QA engineers** (zetyquickly, sunglow666) and **internal dogfooding engineers** (think-in-universe).

**Pain Points:**
- **Automations UX is the #1 friction point.** Multiple issues describe a dashboard that displays state without enabling action. Users cannot diagnose failures, manage schedules, or even find run threads from the intended UI.
- **OAuth token handling is fragile.** Expired tokens cause hard failures with no recovery path (Google Drive) and approval-gated automations can deadlock (Slack, HTTP tools).
- **Real-time feedback is unreliable.** Tool activity entries disappear, approval denials don't persist, and failed calls require manual refresh.
- **Skills management is barebones.** The skills page is paginated but has no search, filtering, or sticky validation feedback.

**Satisfaction Indicators:**
- **Extremely fast fix cycles.** QA reports from sunglow666 often have a fix PR opened within hours or a day (e.g., [#4852](https://github.com/nearai/ironclaw/issues/4852) → [#4858](https://github.com/nearai/ironclaw/pull/4858)).
- **Heavy internal dogfooding** is documented in Issue [#4692](https://github.com/nearai/ironclaw/issues/4692), tracking issues found while using the local Reborn build as the primary agent during development. This is a strong signal of team confidence.
- **Community engagement is healthy.** `think-in-universe` is deeply engaged in both filing high-quality issues and submitting feature PRs, indicating a supportive core community around the project.

## 8. Backlog Watch

| Item | Opened | Status & Risk |
|------|--------|---------------|
| **PR #3890** – Multi-tenant isolation contract tests | 2026-05-22 | **25 days open.** An XS-sized PR adding contract tests for multi-tenancy isolation has been open for almost a month. Multi-tenancy is critical for the Reborn hosting model; this long wait suggests either blockers or a strategy shift. |
| **PR #4518** – Reborn extension lifecycle e2e coverage | 2026-06-06 | **11 days open.** No updates in 24h despite extensions being an active development area. |
| **Issue #4986** – Automation blocked pending approval | 2026-06-16 | **Critical bug, no fix PR attached.** A high-stakes automation blocker that warrants immediate tracking. |
| **Issue #4999** – Scale Google Drive extraction beyond 1 MB | 2026-06-16 | Follow-up to the just-merged extraction seam. Demand is already outpacing the initial design (WASM round-trip cap). |
| **Issue #5009** – Slack OAuth DM-parity (security) | 2026-06-17 | **Fresh security debt.** Opened today by a security reviewer. Will require careful planning before a fix lands. |

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-17

## 1. Today's Overview

The project saw a highly productive cycle today, with **7 pull requests updated** and **6 merged or closed**, reflecting a strong operational focus on stabilizing and enhancing core modules. Activity was heavily concentrated in the **Cowork** and **Artifacts** domains, spanning performance fixes, search improvements, and UI refinements. Issue triage remained quiet, with only one existing bug report updated. No new releases were published, so all merged changes will land in a future version bump.

## 2. Releases

No new releases were published in the last 24 hours. The current stable version referenced in recent issues is **LobsterAI v2026.4.1**.

## 3. Project Progress

Six pull requests were merged or closed today, demonstrating meaningful progress across the cowork and artifact systems.

**Cowork Collaboration Enhancements**
- **#2168** ([link](https://github.com/netease-youdao/LobsterAI/pull/2168)): Added a **scroll-to-bottom control** for cowork conversations, with smooth scrolling, wheel passthrough, and i18n labels.
- **#2170** ([link](https://github.com/netease-youdao/LobsterAI/pull/2170)): **Deep search upgrade** – cowork task titles are now queried directly from the SQLite database rather than filtering a preloaded session list, significantly improving search recall.
- **#2171** ([link](https://github.com/netease-youdao/LobsterAI/pull/2171)): **Performance fix** for long sessions; reduces rail navigation jank via memoized items and avoids smooth scrolling for long distance jumps.
- **#2173** ([link](https://github.com/netease-youdao/LobsterAI/pull/2173)): **Text rendering fix**; ensures user-entered line breaks are properly preserved in sent message bubbles.

**Artifacts & HTML Share Infrastructure**
- **#2172** ([link](https://github.com/netease-youdao/LobsterAI/pull/2172)): **Share recovery feature** – allows users to reactivate HTML shares previously closed due to quantity limits, with refined UI prompts for different closure reasons.
- **#2169** ([link](https://github.com/netease-youdao/LobsterAI/pull/2169)): **Preview card overhaul**; unified dark mode hover effects, multi-file collapsible display, and prioritized the built-in browser for opening HTML artifacts.

## 4. Community Hot Topics

Community interaction on GitHub was minimal in the 24-hour window, but the following items represent the most active discussion:

- **Issue #1425** — *快捷键重复无校验 (Shortcut duplication validation)* ([link](https://github.com/netease-youdao/LobsterAI/issues/1425))
  - *Comments: 1*  
  - The user reports that duplicate keyboard shortcuts are silently accepted without validation. Despite a `[stale]` label, the issue was updated, suggesting some maintainer awareness.

- **PR #1424** — *Silent scheduled task failures* ([link](https://github.com/netease-youdao/LobsterAI/pull/1424))
  - *Comments: None listed*  
  - This PR addresses a high-severity bug where scheduled task operations (stop, toggle, update) fail silently while returning `{ success: true }`. It has been open since April 3.

**Analysis:** The low interaction volume may indicate a small but active user base or that feedback flows through alternative channels (telemetry, customer support).

## 5. Bugs & Stability

**Reported / Open Bugs**
- **High Severity** — *Scheduled task silent failures (PR #1424)*: The `stop` IPC handler does not execute any action but returns `{ success: true }`, giving users a false sense of control over automation tasks. A fix is submitted but remains unmerged for over 2 months.
- **Medium Severity** — *Duplicate shortcut validation missing (Issue #1425)*: Users can save duplicate keybindings without a warning or rejection. A clear UX gap.

**Bugs Fixed Today**
- Cowork message text rendering inconsistencies (`#2173`).
- Rail navigation jank in extended cowork sessions (`#2171`).
- Inability to recover HTML shares disabled by quota limits (`#2172`).

## 6. Feature Requests & Roadmap Signals

No explicit feature requests were filed today, but the merged PRs strongly indicate ongoing roadmap priorities:

- **Advanced Session Management:** The move from UI-only search to SQLite-backed task search (`#2170`) signals a deeper investment in treating cowork sessions as a persistent, searchable knowledge base.
- **LLM-Native Browser Focus:** Prioritizing the built-in browser for artifact previews (`#2169`) reinforces the concept of LobsterAI as a self-contained environment for consuming and interacting with generated content.
- **Collaboration Polish:** The scroll-to-bottom control (`#2168`) and rail performance fixes (`#2171`) show the team is actively refining the real-time cowork experience for heavier usage patterns.

## 7. User Feedback Summary

No explicit satisfaction or dissatisfaction metrics (comments, reactions) were recorded today. However, inferred user pain points addressed by the latest merges include:

- **Difficulty locating past tasks** — The DB search fix (`#2170`) targets user struggles with session retrieval.
- **Performance frustration in long collaborations** — The jank reduction (`#2171`) addresses feedback from power users in extended cowork sessions.
- **Confusion over share limits** — The share recovery mechanism and refined UI prompts (`#2172`) suggest users were frustrated by opaque, permanent-looking share closures.

## 8. Backlog Watch

The following items require maintainer attention due to their age and potential impact:

- **PR #1424** ([link](https://github.com/netease-youdao/LobsterAI/pull/1424)) — **CRITICAL.** Open since 2026-04-03. Fixes a high-severity silent failure in the scheduled tasks module. The PR includes a comprehensive description of the bug and a detailed code fix. Urgent review and merge is recommended to prevent erosion of trust in task automation.

- **Issue #1425** ([link](https://github.com/netease-youdao/LobsterAI/issues/1425)) — **LINGERING UX BUG.** Open since 2026-04-03. Tagged `[stale]` despite recent activity. While low-severity, its long unresolved status suggests it may be deprioritized or awaiting a broader settings rewrite.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

**TinyClaw / TinyAGI Project Digest**
*Date: 2026-06-17*

---

### 1. Today's Overview
Today marks a low-activity period for the TinyAGI project, with no new issues filed, no releases cut, and no pull requests merged into the main branch. The project appears to be in a holding pattern following its last release, with the community and maintainer focus pivoting toward a single pending contribution. The clean issue board (zero open bugs) indicates good stability in the current stable version. The primary development signal today is the continued effort to bring native Windows support to the CLI.

### 2. Releases
**None.** No new releases were published today. The latest stable version remains the most recent release. [View all releases](https://github.com/TinyAGI/tinyagi/releases)

### 3. Project Progress
No code was merged into the main branch today. The project’s codebase is static relative to the previous commit. The entire development pipeline this period consists of a single open pull request awaiting review.

### 4. Community Hot Topics
The sole community interaction point today is **[PR #281: fix: Windows cross-platform support in CLI](https://github.com/TinyAGI/tinyagi/pull/281)** by `mperkins0155`. Despite zero comments or reactions at this time, the underlying need is significant. The PR directly addresses a critical platform gap preventing native Windows execution. The lack of prior issues on this topic suggests that either Windows users have been blocked silently or the issue was known but unactioned until now. This PR represents the community’s primary need for the project: expanding usability beyond Linux/WSL environments.

### 5. Bugs & Stability
No new bugs were reported via the issue tracker today. The project is currently maintaining a zero-bug backlog.

However, the review period highlights **three known Windows-specific bugs** of **High Severity** actively being resolved in **[PR #281](https://github.com/TinyAGI/tinyagi/pull/281)**:
1. **Critical `MODULE_NOT_FOUND` error** (Rank: Critical) – Caused by a doubled drive letter (`/C:/`) from improper URL-to-path resolution on Windows.
2. **Two additional unnamed CLI failures** (Rank: High) – Preventing the CLI from booting natively on Windows outside WSL.

**Status:** A fix PR exists and is awaiting maintainer review.

### 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. The strongest roadmap signal comes from the content of PR #281 itself. By targeting native Windows execution, the project is signaling a strategic shift toward **comprehensive cross-platform support**. Given the fundamental nature of this fix (it unlocks the entire CLI for a new OS segment), it is highly likely that Windows compatibility will be the primary feature of the next patch release (v0.x.x). This positions the project to capture users currently excluded by the WSL dependency.

### 7. User Feedback Summary
Direct user feedback is sparse today, but the data strongly implies a specific user pain point. Community contributor `mperkins0155` invested effort in diagnosing and implementing fixes for three distinct Windows bugs. This indicates a significant latent demand from the Windows user base who are unable to use the tool natively. The lack of earlier bug reports may imply that Windows users simply abandon the project upon encountering the initial `MODULE_NOT_FOUND` error rather than filing bugs. The primary sentiment inferred is **blocked access** for a non-trivial segment of potential users.

### 8. Backlog Watch
The project’s backlog is exceptionally clean. There are zero open issues and no long-running pull requests. The only item awaiting attention is **[PR #281](https://github.com/TinyAGI/tinyagi/pull/281)**, created within the last 48 hours. Maintainers currently have no accumulated technical debt or stale contributions requiring review, giving them a clear runway to focus on this single pending integration.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for 2026-06-17.

---

## Moltis Project Digest | 2026-06-17

### 1. Today's Overview

The Moltis project saw steady activity over the last 24 hours, driven primarily by dedicated user **khimaros**, who filed all four issues today, and maintainer **gptme-thomas**, who has two significant features awaiting review. Several critical audio-related bugs emerged, including an echo cancellation failure that renders live mode unusable in open environments. At the same time, a related whisper.cpp transcription bug was resolved quickly, suggesting a responsive triage process. No new releases were cut today, but the open pull requests point to imminent improvements in chat context injection and external agent configuration.

### 2. Releases

**No new releases published on 2026-06-17.** The latest release remains the version prior to the two open pull requests.

### 3. Project Progress

No pull requests were merged or closed today. Progress is ongoing in the development branch:
- **[PR #1124: Add context command support for chat turns](https://github.com/moltis-org/moltis/pull/1124)** *(Open, updated 2026-06-16)* – Introduces an optional `chat.context_command` that runs before each chat turn, appending stdout to the prompt context. This allows deployments to inject dynamically generated runtime context without manual intervention.
- **[PR #1125: Support model and effort selection for external agents](https://github.com/moltis-org/moltis/pull/1125)** *(Open, updated 2026-06-16)* – Adds first-class `/model` command support for external-agent providers, allowing users to select specific models and effort levels from configuration arrays.

Both PRs are authored by **gptme-thomas** and are currently open for review.

### 4. Community Hot Topics

The most active discussion this cycle is around configuration flexibility:
- **[Issue #1126: Allow configuring TTS output format](https://github.com/moltis-org/moltis/issues/1126)** *(2 comments)* – The only issue with more than one comment today. The user is requesting control over the format of TTS output, indicating a need to integrate Moltis with downstream audio processing pipelines.
- The two open PRs ([#1124](https://github.com/moltis-org/moltis/pull/1124), [#1125](https://github.com/moltis-org/moltis/pull/1125)) have not yet received community discussion, suggesting users are currently more focused on reporting pain points than reviewing code.

Notably, all four new issues this period came from a single power user (*khimaros*), indicating a small but engaged technical base running Moltis in self-hosted production-like environments.

### 5. Bugs & Stability

| Severity | Issue | Status | Summary |
|---|---|---|---|
| **High** | [#1129: Lack of echo cancellation causes agent to retrigger itself in live mode](https://github.com/moltis-org/moltis/issues/1129) | 🔴 Open, No fix PR | A critical feature gap blocking reliable live-mode audio use. The agent hears its own TTS output as a new command, causing an infinite retrigger loop. |
| **High (Resolved)** | [#1128: Transcription errors with self-hosted whisper.cpp](https://github.com/moltis-org/moltis/issues/1128) | ✅ Closed (2026-06-17) | A bug impacting self-hosted users was reported and resolved on the same day. The speed of closure suggests a straightforward fix or configuration clarification. |
| **Medium** | [#1127: Allow configuring RPC timeout](https://github.com/moltis-org/moltis/issues/1127) | 🟡 Open | A stability request rather than a crash, but critical for integrating Moltis with slow or unreliable backend services. |

### 6. Feature Requests & Roadmap Signals

The user *khimaros* filed two enhancements this cycle:
- **[Issue #1126: Configurable TTS output format](https://github.com/moltis-org/moltis/issues/1126)** – Signals a desire to standardize how Moltis emits audio data for external processing.
- **[Issue #1127: Configurable RPC timeout](https://github.com/moltis-org/moltis/issues/1127)** – Points to a need for production hardening against backend latency.

**Prediction for next release:** Given maintainer activity, **PR #1124** (context commands) and **PR #1125** (external agent model selection) are the strongest candidates for the next release. If development velocity holds, the RPC timeout feature (#1127) is a low-complexity, high-value request that could land shortly thereafter. The TTS output format and echo cancellation requests are deeper integrations that may require more architectural work before committing.

### 7. User Feedback Summary

User feedback this cycle is dominated by a single power user (*khimaros*) running a **self-hosted deployment**. The sentiment reveals a user pushing Moltis toward operational maturity:
- **Pain Points:** Audio pipeline reliability is the biggest concern—transcription errors (now fixed) and a lack of echo cancellation make voice interaction fragile.
- **Desired Use Case:** The user appears to be building an autonomous system that depends on Moltis as a voice interface, requiring predictable timeouts, controlled output formats, and stable live-mode loops.
- **Satisfaction:** The quick fix on the whisper.cpp bug (#1128) suggests the maintainer is responsive to critical issues, which aligns positively with health signals.

### 8. Backlog Watch

**No stale items identified.** All four issues and two pull requests in the 24-hour window were created or updated within the last two days (2026-06-15 through 2026-06-17). The project maintainer appears to be staying current with incoming feedback.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# QwenPaw Project Digest — 2026-06-17

*(Data sourced from GitHub: agentscope-ai/QwenPaw)*

---

## 1. Today's Overview

QwenPaw's development cycle on June 17 saw extremely high velocity: **44 issues** and **40 pull requests** updated in the past 24 hours, with roughly half of each being closed or merged. The community is squarely focused on production stability — the loudest conversations concern process freezes during long conversations and crash loops on macOS. The maintainers shipped a minor beta release (v1.1.12-beta.1) while merging **25 pull requests**, many of which were high-quality community patches targeting critical reliability gaps. Overall the project is healthy, responsive, and benefiting from a skilled contributor base, though the volume of stability bugs suggests growing pains as users push the platform into heavier workflows.

---

## 2. Releases

**v1.1.12-beta.1** was released, covering:

- **Security**: Isolated keychain master key per install
- **Desktop**: Hardened Tauri Windows CI against crates.io fetch failures
- **Console/Backend**: A refactor commit (details truncated in source data)

The beta tag and subsequent version bump to **v1.1.12b2** (PR [#5255](https://github.com/agentscope-ai/QwenPaw/pull/5255)) indicate the team is iterating quickly. No breaking changes or migration instructions were present in the release notes snippet.

---

## 3. Project Progress

The project merged or closed **25 PRs** today, spanning every major component:

**Console & UI:**
- Vietnamese (vi) interface language officially landed ([#5175](https://github.com/agentscope-ai/QwenPaw/pull/5175))
- Session list can now be filtered by title ([#5178](https://github.com/agentscope-ai/QwenPaw/pull/5178))
- User input queue added to console ([#5158](https://github.com/agentscope-ai/QwenPaw/pull/5158))
- OSC 8 clickable hyperlinks enabled in ConsoleChannel ([#5248](https://github.com/agentscope-ai/QwenPaw/pull/5248))
- Sidebar date grouping switched from relative to calendar dates ([#5257](https://github.com/agentscope-ai/QwenPaw/pull/5257))

**Cron & Scheduling:**
- Integration tests for Sprint 2.4 cron execution were added ([#5201](https://github.com/agentscope-ai/QwenPaw/pull/5201))
- `dream_cron` field fixed to properly disable dream jobs when cleared ([#5256](https://github.com/agentscope-ai/QwenPaw/pull/5256))

**Coding & Agent Behavior:**
- "Ponytail" coding philosophy formalized with a zero-dependency code indexer ([#5247](https://github.com/agentscope-ai/QwenPaw/pull/5247))

**Core/Config:**
- Deep copy operations removed from agent config caching for performance ([#5240](https://github.com/agentscope-ai/QwenPaw/pull/5240)) — *note: this contradicts the root cause of issue #5206 (see Bugs section).*

---

## 4. Community Hot Topics

| Item | Type | Comments | Core Topic |
|------|------|----------|------------|
| [#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218) | Open Bug | 14 | Sub-agent context compaction freezes process |
| [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) | Open Feature | 6 | Integrate Headroom compression layer |
| [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) | Open Bug | 6 | MiniMax-M2.5 returns XML, breaks compatibility |
| [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) | Open Question | 5 | Long conversations cause complete non-responsiveness |
| [#5209](https://github.com/agentscope-ai/QwenPaw/issues/5209) | Open Bug | 3 | macOS Tauri desktop crash loop (SIGSEGV) |

**Underlying analysis:** The community is simultaneously hitting the upper limits of context handling and desktop resilience. The freeze reports (#5218, #5161) drove two community fix PRs: **timeout protection in context compaction** ([#5242](https://github.com/agentscope-ai/QwenPaw/pull/5242)) and a **full Headroom SDK integration** ([#5244](https://github.com/agentscope-ai/QwenPaw/pull/5244)) to reduce tokens before compaction even runs. The macOS crash (#5209) similarly spawned two separate fix paths ([#5238](https://github.com/agentscope-ai/QwenPaw/pull/5238) for Tauri plugin startup, [#5246](https://github.com/agentscope-ai/QwenPaw/pull/5246) for ChromaDB segfault). This pattern of users reporting problems and immediately submitting fix PRs speaks to a highly invested, technically capable community.

---

## 5. Bugs & Stability

**Critical:**
- **macOS Tauri Desktop Crash Loop** ([#5209](https://github.com/agentscope-ai/QwenPaw/issues/5209)) — `EXC_BAD_ACCESS` every ~1 minute. Two fix PRs target root causes: ChromaDB null pointer in `chromadb_rust_bindings` ([#5246](https://github.com/agentscope-ai/QwenPaw/pull/5246)) and Tauri PyInstaller plugin startup loop ([#5238](https://github.com/agentscope-ai/QwenPaw/pull/5238)).
- **Sub-agent Context Compaction Freeze** ([#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218)) — Process completely unresponsive until manual restart. Fix PR adds timeout to `agent.reply()` in compaction ([#5242](https://github.com/agentscope-ai/QwenPaw/pull/5242)).

**High:**
- **Config Cache Pollution** ([#5206](https://github.com/agentscope-ai/QwenPaw/issues/5206)) — `load_agent_config()` returns cached object references instead of copies, so any mutation pollutes the global cache. **The fix merged today** ([#5240](https://github.com/agentscope-ai/QwenPaw/pull/5240)) *removes* deep copies from the caching path, which runs directly counter to this bug report and may require an escalation.
- **DingTalk Stream Channel Dies After Sleep** ([#5214](https://github.com/agentscope-ai/QwenPaw/issues/5214)) — macOS sleep freezes the asyncio event loop; TCP connection becomes half-open. No fix PR identified.
- **Cron Tasks Pending Forever** ([#5235](https://github.com/agentscope-ai/QwenPaw/issues/5235)) — Tasks stuck with `last_run_at: null` past scheduled time.
- **Custom Channel Listener Dies on Save** ([#5253](https://github.com/agentscope-ai/QwenPaw/issues/5253)) — Requires re-saving config to restart.
- **Infinite Thinking Loop** ([#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162)) — Agent enters self-reasoning deadlock.

**Medium:**
- **MiniMax-M2.5 XML Incompatibility** ([#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625)) — Unresolved since May 22.
- **uv Install vs Windows Installer DingTalk Behavior** ([#5237](https://github.com/agentscope-ai/QwenPaw/issues/5237)) — uv installed version cannot connect DingTalk; Windows exe works.
- **Windows MAX_PATH Overflow** ([#4988](https://github.com/agentscope-ai/QwenPaw/issues/4988)) — Session ID duplicated in filenames.

---

## 6. Feature Requests & Roadmap Signals

**Likely in v1.1.12 stable / v1.1.13:**

| Signal | Type | Why it's likely |
|--------|------|-----------------|
| **Headroom Context Manager** (PR [#5244](https://github.com/agentscope-ai/QwenPaw/pull/5244)) | Major feature | Direct answer to top community pain point (#5063, #5218). Written and ready for review. |
| **Silent Cron Mode** (PR [#5251](https://github.com/agentscope-ai/QwenPaw/pull/5251)) | UX feature | Solves #5250 where cron tasks flood main chat. Simple scope, high impact. |
| **Increased Cron Misfire Grace Window** (PR [#5241](https://github.com/agentscope-ai/QwenPaw/pull/5241)) | Bug fix | Direct response to #5235. Simple default change. |
| **Plugin Middleware Registration** (PR [#5221](https://github.com/agentscope-ai/QwenPaw/pull/5221)) | Architecture | Forms a basis for plugin ecosystem. Under review. |
| **Governance & Sandbox Interface** (PR [#5088](https://github.com/agentscope-ai/QwenPaw/pull/5088)) | Breaking Change | Under review; signals strategic push toward enterprise/security use case. |

**On the horizon:**
- **Agent Self-Evolution Mechanism** ([#5205](https://github.com/agentscope-ai/QwenPaw/issues/5205)) — 3 comments, popular concept of agents dynamically learning from mistakes.
- **WeCom Combined Media Messages** ([#5217](https://github.com/agentscope-ai/QwenPaw/issues/5217)) — User request for single-card rich media output.
- **Workspace Temp File Management** ([#5225](https://github.com/agentscope-ai/QwenPaw/issues/5225)) — Pain around tool outputs polluting workspace root.

---

## 7. User Feedback Summary

**Satisfaction:**
- The project enjoys an impressively engaged contributor base. Multiple first-time contributors submitted complex, high-quality patches (ChromaDB segfault fix, Headroom integration, Vietnamese translation, Ponytail coding philosophy). The 25 merged PRs in 24 hours demonstrate a maintenance team that is closely tracking community contributions.
- Feishu CardKit streaming cards are actively used and appreciated, with constructive UX feedback rather than outright complaints ([#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167)).

**Pain Points:**
1. **Stability under sustained usage** is the #1 theme. Long conversations cause freeze or non-response; desktop clients crash on macOS; sub-agent workflows deadlock. This is the barrier between QwenPaw as a toy/hobbyist tool and a daily-driver productivity tool.
2. **Channel resilience** is fragile. DingTalk silently dies on sleep; custom channels lose listeners on save; cron misbehavior interrupts live workflows.
3. **Configuration friction** creates repeated issues — config cache pollution, uv vs installer inconsistency, Windows path limits.

---

## 8. Backlog Watch

These items remain open and lack a clear maintainer response or fix path:

| Item | Type | Age / Status | Why flagged |
|------|------|--------------|-------------|
| [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) | Bug: MiniMax M2.5 XML | Since May 22 | No fix PR identified. User reports "experience severely affected." |
| [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) | Bug: Thinking loop | Since June 12 | No fix PR. Core agent behavior issue. |
| [#5207](https://github.com/agentscope-ai/QwenPaw/issues/5207) | Bug: Path inconsistency | Since June 15 | No fix PR. Breaks fundamentally for shell command workflows. |
| [#5225](https://github.com/agentscope-ai/QwenPaw/issues/5225) | Feature: Temp file mgmt | Since June 16 | Detailed user proposal, no maintainer response. |
| [#5088](https://github.com/agentscope-ai/QwenPaw/pull/5088) | Breaking Change PR | Since June 10 | Large architectural change still pending review. |
| [#5221](https://github.com/agentscope-ai/QwenPaw/pull/5221) | Feature PR: Middleware | Since June 16 | Significant API addition awaiting review. |
| [#5241](https://github.com/agentscope-ai/QwenPaw/pull/5241) | Fix PR: Cron misfire | Since June 16 | Simple default change, no maintainer response. |
| [#5213](https://github.com/agentscope-ai/QwenPaw/pull/5213) | Fix PR: MCP layout | Since June 16 | Console UI fix in review queue. |

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

Here is the ZeptoClaw project digest for June 17, 2026, based on the provided GitHub activity.

---

## ZeptoClaw Project Digest – 2026-06-17

### 1. Today’s Overview
ZeptoClaw exhibited very low activity on June 17, 2026. No new issues were filed, no pull requests were merged, and no new releases were cut. The only recorded event was an automated dependency update pull request from Dependabot (PR #630). The project was functionally quiet, reflecting a maintenance phase or a day with no active development or community engagement. While stability appears intact, the complete lack of user interaction or code integration signals a stagnant day for the project.

### 2. Releases
**No new releases today.**
There are no upcoming or newly published versions of ZeptoClaw to report for this date.

### 3. Project Progress
**No features or fixes were merged today.**
No pull requests were closed or merged into the main branch. Development progress was effectively zero, with no code changes integrated into the repository.

### 4. Community Hot Topics
**No active community discussions were recorded.**
There are currently zero open or updated issues, and the single open pull request (PR #630) has generated no comments or reactions. The community did not participate in any discussions in the last 24 hours.

### 5. Bugs & Stability
**No stability concerns were raised.**
No new bugs, crashes, or regressions were filed today. The project currently has no unresolved bug reports, indicating a stable baseline.

### 6. Feature Requests & Roadmap Signals
**No feature requests received.**
No user-submitted proposals or roadmap discussions occurred today. There is no new signal to predict what might be included in the next version.

### 7. User Feedback Summary
**No user feedback recorded.**
There were no expressions of satisfaction, dissatisfaction, or pain points from users in the last 24 hours. Sentiment sampling for this period is not possible due to a lack of data.

### 8. Backlog Watch
**Open PR requiring maintainer attention:**

- **[PR #630: chore(deps): bump debian from `b6e2a15` to `4e401d9`](https://github.com/qhkm/zeptoclaw/pull/630)**
  *Opened by Dependabot | Updated: 2026-06-16*
  This automated pull request bumps the base Docker image from `trixie-slim` to the latest SHA digest. It remains open without review or merge. While not critical, keeping base images current is important for supply chain security and build stability. This item should be reviewed and merged in due course by a maintainer.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

**ZeroClaw Project Digest — 2026-06-17**

Generated from ZeroClaw Labs (github.com/zeroclaw-labs/zeroclaw)

---

### 1. Today’s Overview

ZeroClaw remains in a phase of extraordinarily high-velocity development. With **50 issues and 50 PRs updated** in the past 24 hours, the project is buzzing around its v0.8.x milestones. Activity is split between large architectural RFCs, a major wave of new bug reports against the latest v0.8.0 stable binaries, and intense code churn on the `master` branch. No formal release was cut today, but the rate of issue closure and PR advancement suggests the team is fighting to stabilize the codebase while rapidly adding new surfaces like the MCP Dashboard and WASM plugins. Community engagement is high, though several critical documentation gaps and prebuilt binary regressions are generating friction.

---

### 2. Releases

**None today.** The project is currently between releases, with the next minor versions tracked in the community milestone issue [#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970) (v0.8.1) and the MCP Dashboard tracker [#7320](https://github.com/zeroclaw-labs/zeroclaw/issues/7320) (v0.8.3).

---

### 3. Project Progress

Despite no new release, significant work landed or was closed today:

**Closed / Merged Highlights:**
- **Webhook Routing:** [#6312](https://github.com/zeroclaw-labs/zeroclaw/issues/6312) — Per-alias webhook path routing closed, enabling multi-instance gateways.
- **Telegram Custom API:** [#6807](https://github.com/zeroclaw-labs/zeroclaw/issues/6807) — Custom API endpoint support for Telegram is now available (resolved).
- **Memory Clear:** [#6150](https://github.com/zeroclaw-labs/zeroclaw/issues/6150) — Fast channel-native `/clear` commands shipped for Telegram/Discord.
- **Shell Agent Loop:** [#7143](https://github.com/zeroclaw-labs/zeroclaw/issues/7143) — The critical bug causing Slack agents to exhaust `max_tool_iterations` with near-duplicate commands was fixed.
- **Internationalization/CLI:** [#6995](https://github.com/zeroclaw-labs/zeroclaw/issues/6995) (CJK backspace in `zeroclaw agent`) and [#6859](https://github.com/zeroclaw-labs/zeroclaw/issues/6859) (Windows code-page tests) were resolved.
- **Cron Fix:** [#6648](https://github.com/zeroclaw-labs/zeroclaw/issues/6648) — `cron session_target=main` now correctly reuses the primary session instead of running in isolation.

**Active Fix PRs Making Progress:**
- **Live UI & Real-Time:** [#7778](https://github.com/zeroclaw-labs/zeroclaw/pull/7778) (emit tool_call at dispatch so live cards render) and [#7678](https://github.com/zeroclaw-labs/zeroclaw/pull/7678) (thread CanvasStore into WS/ACP sessions) are critical for the web UI experience.
- **Config & Credentials:** [#7726](https://github.com/zeroclaw-labs/zeroclaw/pull/7726) (makes Slack `bot_token` optional for env-fallback) and [#7826](https://github.com/zeroclaw-labs/zeroclaw/pull/7826) (moves credential redaction to the render layer) address regressions in rich config setups.
- **Heartbeat & Skills:** [#7680](https://github.com/zeroclaw-labs/zeroclaw/pull/7680) (allows any channel as heartbeat target: "matrix" etc.) and [#7730](https://github.com/zeroclaw-labs/zeroclaw/pull/7730) (skill review summary parsing) smooth out runtime edge cases.

---

### 4. Community Hot Topics

The most active discussion threads reveal deep engagement with both governance and bleeding-edge architecture:

- **Governance & Scalability:** **[#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) — RFC: Work Lanes, Board Automation, and Label Cleanup (11 comments)**
    The highest-traffic issue. This governance RFC for 0.8.0 is in rollout and is the community’s primary forum for defining how work is triaged as the project scales beyond a single maintainer model.

- **Enterprise / Security Stance:** **[#7675](https://github.com/zeroclaw-labs/zeroclaw/issues/7675) — RFC: Hardened CI Pipeline (2 comments)**
    Tagged `needs-maintainer-review`, this RFC pushes for SBOM generation and supply-chain security. It signals strong enterprise pressure on the project.

- **Architectural Reliability:** **[#7759](https://github.com/zeroclaw-labs/zeroclaw/issues/7759) — Decouple Gateway WS from Agent Turn (2 comments)**
    A critical request to prevent agent-turn cancellation on client disconnect. The need for production-grade state management is a recurring theme in the feedback.

- **Milestone Coordination:** **[#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970) — v0.8.1 Integration Tracker (3 comments)**
    The community is actively using this tracker to coordinate what makes the next minor cut, demonstrating a structured release workflow.

---

### 5. Bugs & Stability

Today’s bug reports are heavily concentrated in **regressions from the v0.8.0 stable release** and **provider interoperability**.

**S1 — Workflow Blocked:**
- **MCP Tools Unavailable (Anthropic/OpenAI):** [#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756) — Registered MCP tools do not reach the model on certain providers, completely blocking tool ecosystem usage for users on those families.
- **Code History Breaks Anthropic API:** [#7804](https://github.com/zeroclaw-labs/zeroclaw/issues/7804) — Long-running Code/ACP sessions can send non-alternating messages to Anthropic, triggering a hard 400 error.
- **Documentation Blocking Onboarding:** [#7758](https://github.com/zeroclaw-labs/zeroclaw/issues/7758) — User reports configuration is completely impossible to write from current docs (“S1 — workflow blocked”).

**S1/S2 — Regression (High Impact):**
- **Prebuilt Binaries Missing Features:** **[#7787](https://github.com/zeroclaw-labs/zeroclaw/issues/7787) (P1)** — The official v0.8.0 binary ships *without* Slack/Discord features. Users are forced to revert to 0.7.5. This is a high-urgency CI/packaging bug.

**S2 — Degraded Behavior:**
- **Runtime Profile Ignored in Channels:** [#7809](https://github.com/zeroclaw-labs/zeroclaw/issues/7809) — Channel turns ignore `strict_tool_parsing` and `parallel_tools` runtime-profile flags.
- **Telegram Voice Peer SSOT Violation:** [#7795](https://github.com/zeroclaw-labs/zeroclaw/issues/7795) — Config-derived peers cached at startup cause latent stale state errors.
- **Shell Approval Loop:** [#7820](https://github.com/zeroclaw-labs/zeroclaw/issues/7820) — Agent repeats identical `pwd` shell calls, re-requesting user approval each time.
- **Zerocode UX Regressions:** [#7799](https://github.com/zeroclaw-labs/zeroclaw/issues/7799) (resumed sessions blank), [#7800](https://github.com/zeroclaw-labs/zeroclaw/issues/7800) (misleading keybindings/macOS), [#7815](https://github.com/zeroclaw-labs/zeroclaw/issues/7815) (opaque config source display).

---

### 6. Feature Requests & Roadmap Signals

The community is clearly steering the project toward enterprise readiness and better tooling.

- **Next Up (v0.8.x):** The **MCP Dashboard** tracker [#7320](https://github.com/zeroclaw-labs/zeroclaw/issues/7320) is the central milestone. **WASM Plugin Lifecycle Hooks** ([#7822](https://github.com/zeroclaw-labs/zeroclaw/issues/7822)) are being actively debated.
- **Gateway/State Architecture:** The WS decoupling proposal [#7759](https://github.com/zeroclaw-labs/zeroclaw/issues/7759) is a strong signal for where the runtime is going.
- **Channel Expansion:**
    - **WeCom:** Proactive messaging support requested [#7824](https://github.com/zeroclaw-labs/zeroclaw/issues/7824).
    - **Discord:** Promoted to the default channel bundle via [#7825](https://github.com/zeroclaw-labs/zeroclaw/pull/7825).
- **Config Management:** The request for **typed delete-with-cascade** ([#7175](https://github.com/zeroclaw-labs/zeroclaw/issues/7175)) suggests the new schema v3 system, while powerful, lacks easy reversal commands.
- **Cron Enhancement:** [#7762](https://github.com/zeroclaw-labs/zeroclaw/issues/7762) requests the ability to run cron tasks with a **specific (cheaper) model**, indicating a real production deployment pattern.

---

### 7. User Feedback Summary

**Pain Points:**
- **Documentation Crisis:** The feedback in [#7758](https://github.com/zeroclaw-labs/zeroclaw/issues/7758) is the starkest yet: *“It doesn't matter how good the code is if the documentation is crap.”* The config syntax is opaque to new users.
- **Binary Integrity:** The Slack/Discord regression in the v0.8.0 prebuilt binary ([#7787](https://github.com/zeroclaw-labs/zeroclaw/issues/7787)) erodes trust in official builds.
- **Onboarding Friction:** The quickstart wizard missing a port field (PR [#7215](https://github.com/zeroclaw-labs/zeroclaw/pull/7215)) continues to block new users.

**Satisfaction / Praise:**
- Despite the bugs, users are deeply engaged and value the architecture. From [#7143](https://github.com/zeroclaw-labs/zeroclaw/issues/7143): *“Thank you for the project. It is great to see a Rust-based agent runtime that is much lighter on resources than many other agent systems we have tried.”*
- The community is collaborating on RFCs and trackers, signaling a healthy, invested user base.

---

### 8. Backlog Watch

Several important items are lingering without resolution or are blocked:

- **Stale High-Priority Bug:**
    - **[#5266](https://github.com/zeroclaw-labs/zeroclaw/issues/5266) (P1, Apr 3):** Pairing code not shown when gateway runs on alternate port. This has been open for over 2 months with no fix PR.
    - **[#6643](https://github.com/zeroclaw-labs/zeroclaw/issues/6643) (P2, May 13):** GLM-5.1 “thoughts” leaking into responses. Reopened previously, remains contested.

- **RFC Awaiting Maintainer Decision:**
    - **[#7675](https://github.com/zeroclaw-labs/zeroclaw/issues/7675) (Hardened CI Pipeline):** Tagged `needs-maintainer-review`. The project’s security posture is dependent on a decision here.

- **Blocked PRs (Author Action Required):**
    - [#7094](https://github.com/zeroclaw-labs/zeroclaw/pull/7094) — `zeroclaw models set <model>` CLI persist fix.
    - [#7215](https://github.com/zeroclaw-labs/zeroclaw/pull/7215) — Quickstart wizard port field.
    - [#7340](https://github.com/zeroclaw-labs/zeroclaw/pull/7340) — Browser tool URL validation refactor.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*