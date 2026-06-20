# OpenClaw 生态日报 2026-06-20

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-20 03:23 UTC

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

## OpenClaw 项目深度报告

好的，这是根据您提供的 OpenClaw GitHub 数据生成的 2026-06-20 项目动态日报。

---

# OpenClaw 项目动态日报 (2026-06-20)

## 1. 今日速览

OpenClaw 项目在 2026-06-20 迎来了极高强度的更新，24小时内共有 500 条 Issue 活跃（新开/活跃 453 条，关闭 47 条），同时有 500 个 PR 被更新（待合并 453 个，已合并/关闭 47 个）。尽管吞吐量巨大，**项目的健康状态正面临严峻挑战**。P0/P1 级别的 Bug 激增，尤其是网关内存泄漏、数据丢失和会话隔离失败等问题成为社区焦点。新版本 `v2026.6.9-beta.1` 虽更新了 Telegram 渠道，但也带入了回归问题。当前项目正处于“高速迭代”与“稳定性危机”并存的阶段。

## 2. 版本发布

*   **最新版本：** `v2026.6.9-beta.1`
*   **更新亮点：**
    *   **Telegram 交付升级：** 支持富文本 HTML、Markdown 和贴纸路径的发送；更忠实地渲染进度草稿和命令输出；确保 mentions 和 spooled handlers 在正确的交付路径上。
*   **迁移风险提示：**
    *   从社区反馈来看，该版本及上一个 `v2026.6.8` 版本在 Telegram 上出现了严重兼容性问题。用户反馈在 Telegram Web 上收到“This message is currently not supported”的错误 ([#93794](openclaw/openclaw Issue #93794))，且 `/usage` 命令返回的信息丢失 ([#93905](openclaw/openclaw Issue #93905))。
    *   **建议：** Telegram 重度用户建议暂缓升级，并密切关注上述两个 Issue 的修复进度。

## 3. 项目进展

*   **合并/关闭动态：** 今日共有 **47 个 PR 被合并** 及 **47 个 Issue 被关闭**，清理了部分阻塞项。
    *   **Slack 交付修复：** 长期困扰用户的“Slack 线程响应无法交付”问题（[#78061](openclaw/openclaw Issue #78061)）已关闭，降低了 Slack 渠道的丢消息率。
    *   **Telegram 回归修复：** v2026.6.8 引入的 Telegram Web 消息不兼容问题（[#93794](openclaw/openclaw Issue #93794)）已被关闭，推测修复补丁已合并。
*   **审核瓶颈：** 目前仍有 **453 个 PR** 处于待合并状态。大量社区贡献（如核心诊断功能 [#86627](openclaw/openclaw PR #86627)、安全改进 [#84738](openclaw/openclaw PR #84738)）仍在排队等待审核，维护者的响应速度可能正在成为新的瓶颈。

## 4. 社区热点

*   **🔥 最高讨论量：核心架构迁移策略 ([#88838](openclaw/openclaw Issue #88838)，31条评论)**
    社区就“将核心会话/转录状态迁移至 SQLite”这一大型重写展开了激烈讨论。开发者 `jalehman` 提议采用“**通过访问器抽象层进行渐进式迁移**（branch-by-abstraction）”的方案，获得了广泛共识。社区强烈反对一次性大规模重写，反映出用户对当前稳定性的极度敏感。
*   **😡 用户恐慌最严重：P0 级内存泄漏 ([#91588](openclaw/openclaw Issue #91588)，13条评论)**
    网关内存从 350MB 泄漏至 15.5GB 并导致 OOM 被内核杀死的问题，让大量用户感到不安。该 Issue 是目前项目面临的最大单一故障风险。
*   **💡 需求共鸣最强：Per-Agent 记忆隔离 ([#63829](openclaw/openclaw Issue #63829)，10条评论，9个 👍)**
    功能请求 #63829 获得了极高的社区共鸣。在多Agent场景下，用户迫切需要每个Agent拥有独立的 `memory-wiki` 隔离能力。这表明用户群体正从单一助手向**复杂的多Agent协作生态**演进。

## 5. Bug 与稳定性

*   **🔴 P0 级（严重崩溃/数据丢失）：**
    *   **#91588:** 网关内存泄漏 (OOM Kill) → 无关联修复PR。
    *   **#84882:** `memory-core` 静默删除用户记忆文件 (Data Loss) → 已有关联修复 PR。
*   **🟠 P1 级（核心功能异常/重度回归）：**
    *   **会话隔离崩溃：**
        *   [#84903](openclaw/openclaw Issue #84903): 单会话阻塞全局事件循环。
        *   [#84771](openclaw/openclaw Issue #84771): 启动时同步预热导致事件循环阻塞长达28~64秒。
    *   **模型路由/客户端异常：**
        *   [#85103](openclaw/openclaw Issue #85103): 模型回退链在提供商标配耗尽时彻底失效。
        *   [#85126](openclaw/openclaw Issue #85126): 控制 UI 创建会话时自动选择错误认证配置。
        *   [#90325](openclaw/openclaw Issue #90325): Matrix 渠道在 v2026.6.1 后完全崩溃（TypeError）。
        *   [#93905](openclaw/openclaw Issue #93905): `/usage` 命令在 Telegram 上失效（回归）。
    *   **Subagent 交付异常：**
        *   [#90840](openclaw/openclaw Issue #90840): Subagent 原始输出直接发送给用户（隐私泄露风险）。
        *   [#92076](openclaw/openclaw Issue #92076): 请求方 Session 不活跃时，Subagent 结果完全丢失。
        *   [#85030](openclaw/openclaw Issue #85030): MCP 工具无法注入到 Subagent 会话。
    *   **配置与运维问题：**
        *   [#90711](openclaw/openclaw Issue #90711): macOS 上 `launchd plist` 将 stderr 重定向到 /dev/null，吞没日志。
        *   [#91212](openclaw/openclaw Issue #91212): 网关重启后，消息恢复机制在通道传输未就绪时提前启动，导致消息静默丢失。
        *   [#92415](openclaw/openclaw Issue #92415): `/model` 切换后 Session 内部模型快照未刷新，导致后续推理使用错误参数。

## 6. 功能请求与路线图信号

*   **近期可能被纳入的功能（已有相关 PR）：**
    *   **#93807 (P2 & Security): 修复 `web_fetch` 代理忽略 `NO_PROXY`。** 这既是 Bug 也是 SSRF 风险。鉴于标签带有 `linked-pr-open`，预计相关修复很快会合并。
    *   **#90354 (P2): 内存预压缩写入的限界验证。** 该功能旨在防止模型向记忆文件写入过大或错误数据，是提升 `memory-core` 组件鲁棒性的关键补充。
*   **长期路线图信号：**
    *   **#90916: 主题会话家族。** 用户希望一个 Agent 能拥有多条隔离的上下文“赛道”，这是 AI 助手从“对话窗口”向“个人工作台”演进的重要标志。
    *   **#53638: 频道/群组级别的模型覆盖。** 允许在不同群组使用不同模型，是企业化管理和精细化控制的基础功能，自3月份提出已积压3个月。
    *   **#46656: WebChat 内联按钮支持。** 目前 `buttons` 参数仅对 Telegram 生效，扩展到 WebChat 是提升前端交互一致性的关键需求。

## 7. 用户反馈摘要

*   **“升级充满不确定性”：** 多位用户在升级到新版本后遭遇了服务不可用或核心功能失效。例如，macOS 用户 `tess020126-cmyk` 报告升级后 `LaunchAgent` 无法恢复，最终只能通过 Time Machine 回滚（[#85027](openclaw/openclaw Issue #85027)）。这种级别的回归严重侵蚀了用户对项目稳定性的信任。
*   **“Subagent 特性中看不中用”：** 尽管 Subagent 功能被大力宣传，但实际使用体验极差。用户反馈包括：子任务结果无法回调（[#92076](openclaw/openclaw Issue #92076)）、子会话中用不了 MCP 工具（[#85030](openclaw/openclaw Issue #85030)）、父会话的提示词不在子会话中生效等。多 Agent 编排的可用性因交付链路不稳定而大打折扣。
*   **“性能波动像过山车”：** 用户 `samson1357924` 发现 `doctor --fix` 在相邻版本间的执行时间相差 4-5 倍（从 55s 涨到 229s+）（[#85333](openclaw/openclaw Issue #85333)）。这种无预警的性能回归让运维管理变得非常被动。

## 8. 待处理积压

*   **需要立即响应的紧急事项：**
    *   **#91588 (P0 内存泄漏)：** 已开放 11 天，作为项目当前最大风险点，建议成立紧急工作组立即定位根因。
    *   **#84771 (启动阻塞) 与 #84903 (会话隔离失败)：** 这两个 P1 架构级 Bug 严重限制了项目的多租户和高可用能力，亟需维护者给出产品决策或修复方案。
*   **维护者审核提醒：**
    *   **大量 `needs-maintainer-review` 标签堆积：** 诸如 [#85030](openclaw/openclaw Issue #85030) (MCP Subagent)、[#85126](openclaw/openclaw Issue #85126) (认证配置) 等 P1 级别 Issue 带有此标签并已开放近一个月。请维护者加快审核闭环，避免优秀贡献者因响应不及时而流失。
    *   **安全风险残留（#84738）：** 用于停止向 `models.json` 写入明文 API 密钥的 PR [#84738](openclaw/openclaw PR #84738) 自 5 月 21 日起便在等待作者回应。建议维护者主动联系，推进此安全修复。

---

## 横向生态对比

# 个人AI助手开源生态横向对比分析报告
**分析周期：** 2026-06-20 | **分析师：** AI Agent生态研究组

---

## 1. 生态全景

2026年6月20日，个人AI助手与自主智能体开源生态呈现出 **“高速迭代与稳定性阵痛并存”** 的典型特征。头部项目（OpenClaw、Hermes Agent、ZeroClaw、IronClaw）日均更新Issue/PR数量均超过50条，社区贡献热情持续高涨。但高频更新也暴露出普遍问题：版本回归频繁（OpenClaw Telegram兼容性、ZeroClaw Slack缺失、CoPaw图片发送回归），多Agent编排可用性差（Subagent交付丢失、内存泄漏），以及安全漏洞集中爆发（SSRF绕过、prompt泄露、凭证配置风险）。生态正从“单一对话助手”向 **“多Agent协作平台”** 和 **“企业级生产工具”** 加速演进，但稳定性、安全性和审查效率成为制约升级的关键瓶颈。

---

## 2. 各项目活跃度对比

| 项目 | 今日Issues活动数 | 今日PR活动数 | 版本发布 | 健康度评估 |
|------|----------------|-------------|---------|-----------|
| **OpenClaw** | 500（活跃453，关闭47） | 500（待合并453，合并/关闭47） | v2026.6.9-beta.1 | **风险**：极高吞吐但P0级内存泄漏/数据丢失，稳定性危机 |
| **Hermes Agent** | 50（新开/活跃40，关闭10） | 50（待合并43，合并/关闭7） | v0.17.0 "The Reach" | **优秀**：大版本后密集打磨，社区自愈能力强 |
| **ZeroClaw** | 28 | 50（待合并47，合并/关闭3） | 无 | **良好但预警**：活跃极高，但构建缺失与安全Bug需立即响应 |
| **IronClaw** | 4更新 | 30（合并/关闭12，待合并18） | 无 | **优秀**：功能框架快速落地，CI/测试基建大幅加固 |
| **NanoBot** | 11（5新开） | 34（合并/关闭19，待合并15） | 无 | **良好**：生产稳定性修复密集，模型降级/流中断等问题已闭环 |
| **CoPaw (QwenPaw)** | 11 | 17（含合并+待合并） | 无 | **优秀**：ChromaDB崩溃根除，社区响应快，智谱兼容多人协作修复 |
| **PicoClaw** | 4 | 7 | Nightly构建 | **一般**：贡献积极但大量PR stale，配置合并逻辑混乱 |
| **NanoClaw** | 0 | 5（全部待合并） | 无 | **一般**：开发输入有力，但评审合并停滞，零互动值得警惕 |
| **LobsterAI** | 4（3关闭+1新提案） | 0 | 无 | **中等**：处于战略清洗期，大型RFC浮现但代码无变动 |
| **NullClaw** | 3（2开放+1关闭） | 1（待合并） | 无 | **较低**：维护者回应滞后，长期问题积压（飞书→3个月） |
| **TinyClaw** | 0 | 0 | — | **休眠** |
| **Moltis** | 0 | 0 | — | **休眠** |
| **ZeptoClaw** | 0 | 0 | — | **休眠** |

---

## 3. OpenClaw在生态中的定位

OpenClaw是生态中 **社区规模最大、吞吐量最高** 的项目（日500+ Issue/PR），但也是 **稳定性危机最突出** 的参照核心。与竞争对手相比：

- **vs Hermes Agent**：Hermes v0.17.0合入800个PR后质量更平稳，P0级Bug少于OpenClaw；OpenClaw在Telegram交互细节上更丰富（富文本、贴纸），但回归更频繁。
- **vs ZeroClaw**：ZeroClaw在Discord深度集成和企业级OIDC认证上领先，但OpenClaw在渠道覆盖面（Telegram/Slack/Matrix）和社区请求量级（453个待合并PR）上仍占统治地位。
- **vs IronClaw**：IronClaw面向企业内部审批流程和Projects管理，OpenClaw则更偏向个人/极客用户的全能AI助手，缺乏类似IronClaw的审批UI和功能标志系统。
- **技术路线差异**：OpenClaw提议大规模迁移至SQLite（#88838），采用branch-by-abstraction方式进行；其他项目（如NanoBot、ZeroClaw）更倾向于增量修复而非架构重写。OpenClaw的激进决策在当前稳定性脆弱期引发社区强烈反对。

**整体定位**：OpenClaw是生态中的“航空母舰”——功能最全、社区最大，但甲板上的火情（内存泄漏、数据丢失、会话隔离失败）正在消耗用户信任。其技术决策与稳定性恢复速度将直接影响生态信心。

---

## 4. 共同关注的技术方向

### ① 多Agent编排与Subagent稳定性
- **涉及项目**：OpenClaw、NanoBot、Hermes、PicoClaw、CoPaw、ZeroClaw
- **具体诉求**：Subagent结果无法回调（OpenClaw #92076）、子会话MCP工具不可用（OpenClaw #85030）、模型重载忽视（Hermes #49332）、Spawn覆盖模型（NanoBot PR #4415）、Agent禁用后频道仍在线（ZeroClaw #8013）、协作触发关键词不全（CoPaw #5179）。多Agent从实验性功能向可靠生产级能力迈进，但交付链路断点普遍。

### ② 记忆/状态持久化的可靠性
- **涉及项目**：OpenClaw、NanoBot、Hermes、PicoClaw、CoPaw、ZeroClaw
- **具体诉求**：memory-core静默删除文件（OpenClaw #84882）、Dream模式技能漂移（NanoBot PR #3591）、上下文压缩后指令丢失（Hermes #49307）、Agent“失忆”（PicoClaw #3150）、ChromaDB索引膨胀崩溃（CoPaw #4795，已修）、配置持久化顺序倒置（ZeroClaw #7907/7941）。记忆是智能体的核心资产，各项目普遍在持久化时机、容量控制和隔离性上遇到瓶颈。

### ③ 安全防线（SSRF、凭证泄露、权限控制）
- **涉及项目**：OpenClaw、NanoBot、Hermes、PicoClaw、ZeroClaw、IronClaw
- **具体诉求**：`web_fetch`忽略`NO_PROXY`/ISATAP绕过（OpenClaw #93807、PicoClaw #3143）、API密钥明文写入配置文件（NanoBot #84738）、零知识凭证代理呼吁（Hermes #4656）、内存工具策略绕过（Hermes #49386）、审批权限描述误导（IronClaw #5088）。社区对安全的需求已从“应用层沙盒”升级到“网络层零信任”。

### ④ 模型路由与降级韧性
- **涉及项目**：OpenClaw、NanoBot、CoPaw、Hermes、NullClaw
- **具体诉求**：模型回退链失效（OpenClaw #85103）、空响应不触发降级（NanoBot #4287）、Gemma 4 finish_reason='length'截断（Hermes #49297/OpenClaw未提但同类）、DeepSeek推理卡死（CoPaw #5328）、Ollama不完整回答（NullClaw #952）。多供应商策略已成标配，但降级逻辑、超时保护和供应商兼容性仍是薄弱环节。

### ⑤ 跨平台兼容与版本回归
- **涉及项目**：几乎所有活跃项目
- **具体诉求**：Telegram回归报错（OpenClaw #93794）、v0.8.0缺失Slack/Discord（ZeroClaw #7787）、飞书WebSocket渲染空（NanoBot #4342）、Windows路径冲突（PicoClaw #2472, Hermes #49242）、macOS launchd吞日志（OpenClaw #90711）。平台多样性是双刃剑，每轮发布几乎都会带来至少一个渠道的降级，回归测试覆盖率成为共同短板。

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | NanoBot | IronClaw | ZeroClaw | PicoClaw | CoPaw |
|------|----------|-------------|---------|----------|----------|---------|-------|
| **核心语言/框架** | Python | Python | Python | Rust | Rust | Go | Python |
| **功能侧重** | 全渠道全能AI助手 | 桌面端+多平台网关+社区贡献者生态 | 生产级模型降级与流处理韧性 | 企业级审批、Projects、OIDC认证 | Discord重度集成+OIDC+安全架构 | 多Agent协作总线+SSRF防御 | ChromaDB记忆管理+多模型兼容 |
| **目标用户** | 个人极客/重度自部署用户 | 开发者和桌面端用户 | API服务与Telegram Bot生产环境 | 企业与团队协作场景 | 社区运营/企业安全敏感用户 | 安全意识强的自部署用户 | 多模型切换频繁的普通用户 |
| **架构特点** | 单体+大量插件；计划SQLite迁移 | 插件丰富，Desktop端Electron+WebUI | 轻量高性能，强调fallback机制 | 微服务倾向，CI/测试体系完备 | Rust并发强，二进制分发（但问题多） | Go编译快，单二进制部署 | Tauri桌面+WebUI，ChromaDB向量引擎 |
| **审查效率** | 瓶颈明显（453个待合PR） | 较好，但stephenschoettler部分PR滞留 | 较快，19/34当日合并 | 较好，12/30当日合并 | 拥堵（47待合） | 慢，大量PR Stale | 较快，17个PR跟进紧凑 |

**关键差异点**：IronClaw和ZeroClaw在安全与企业方向投入最深；NanoBot专注于API链路可靠性；Hermes Agent在桌面交互和社区参与感上领先；OpenClaw虽然全面但稳定性垫底；CoPaw在记忆系统上单点突破；PicoClaw以Go语言和Agent总线差异化杀入。

---

## 6. 社区热度与成熟度分层

| 层级 | 项目 | 判据 |
|------|------|------|
| **🔥 高速迭代且相对稳定** | Hermes Agent, IronClaw, CoPaw | 日PR合入>10，Bug修复闭环快，核心特性持续落地，社区反馈有回应 |
| **⚡ 极高吞吐但有明显风险** | OpenClaw, ZeroClaw | 日活动量最高，但P0级Bug、构建缺失或数据丢失严重，用户信任面临考验 |
| **✅ 稳健发展但节奏偏慢** | NanoBot, PicoClaw, NanoClaw | 输入质量高，但审查合入效率制约了贡献者回报（PicoClaw多个PR stale >2周，NanoClaw PR零合并） |
| **⏳ 战略清洗/积累期** | LobsterAI, NullClaw | 代码变动少，LobsterAI出现重量级RFC但无合入；NullClaw维护者长期不回应关键Issue |
| **💤 休眠** | TinyClaw, Moltis, ZeptoClaw | 24h零活动 |

**质量巩固阶段**：Hermes Agent、IronClaw、NanoBot处于“功能推进+质量加固”并行期，Bug修复和新功能合入比例平衡。
**快速迭代阶段**：OpenClaw、ZeroClaw、CoPaw侧重功能数量和社区贡献吸纳，但稳定性修补滞后。
**孵化/转型期**：LobsterAI正从IDE脚本工具转向AI协作者平台，仍处于规划阶段。

---

## 7. 值得关注的趋势信号

### 🔹 多Agent编排“看上去很美”，实用性仍需攻坚
Subagent/Spawn/Delegate模式几乎成为每个项目的标配，但从OpenClaw #92076（结果丢失）、Hermes #49332（模型重载被忽略）、CoPaw #5179（关键词不全）来看，完整的端到端多Agent交付链路尚未在任何项目中达到“生产可用”。这是下一波竞争的决胜点。

### 🔹 记忆系统的“数据基座”属性愈发关键
从OpenClaw的memory-core静默删除，到CoPaw的ChromaDB 37G膨胀崩溃，再到PicoClaw用户的“失忆”恐慌，**记忆系统的可靠性、隔离性和持久化策略**正取代单纯的对话能力成为用户最敏感的天花板。Per-Agent记忆隔离（OpenClaw #63829）和Dream范围控制（NanoBot #3591）是高频呼声。

### 🔹 安全前移成为基础设施级需求
SSRF绕过（PicoClaw #3143, OpenClaw #93807）、零知识代理（Hermes #4656）、审批权限模型（IronClaw #5062）、Agent禁用后频道仍在（ZeroClaw #8013）——安全议题已从“边界防御”深入到“运行时零信任”。**安全不再是特性，而是准入条件**。

### 🔹 审查效率成为生态发展的硬约束
OpenClaw 453个待合并PR、ZeroClaw 47个、Hermes 43个、PicoClaw多个Stale PR、NanoClaw 5个PR零互动——社区贡献的热情远超过维护者处理的速度。**大量高质量贡献因审查积压而“空转”**，甚至导致贡献者流失（如NanoClaw #2605积压27天）。自动化测试、bot review、分层维护者机制将是大项目必要投资。

### 🔹 版本回归频发，测试覆盖呼唤“防御性发布”
ZeroClaw v0.8.0缺失Slack/Discord、OpenClaw v2026.6.9-beta.1 Telegram不兼容、CoPaw v1.1.12图片发送回归、Hermes v0.17.0 Gemma4截断未修复——几乎每个项目的版本发布都带着至少一个已知回归。**用户升级意愿被严重侵蚀**。建立更完善的E2E测试矩阵和渠道兼容性CI，是挽回信任的必要手段。

---

**给技术决策者和开发者的建议：**
- 若追求**极致稳定**，建议关注Hermes Agent（v0.17.0后修复密集）和NanoBot（降级机制完善）；
- 若需要**企业级管控**（审批、SSO、OIDC），IronClaw和ZeroClaw方向最明确；
- 若重视**安全加固**，PicoClaw（SSRF专项修复）和ZeroClaw（OIDC架构）值得跟进；
- 若希望**贡献代码并快速看到合入**，CoPaw、IronClaw当前反馈最快；
- **谨慎升级**OpenClaw最新beta版本，至少等待P0泄漏Bug（#91588）修复后再考虑迁移。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报
**日期：** 2026-06-20
**项目：** [NanoBot (github.com/HKUDS/nanobot)](https://github.com/HKUDS/nanobot)

---

## 1. 今日速览

NanoBot 在 6 月 20 日维持极高开发活跃度。**过去 24 小时内共更新 11 个 Issue（其中 5 个为新开）、34 个 PR（其中 19 个已合并/关闭）**，当前无新版本发布。从数据看，项目正处于密集的缺陷修复与功能迭代并行阶段：一方面围绕生产稳定性（空响应降级、流中断、工作区不对称）集中收敛 Bug，另一方面在推理力度自动调节、子智能体聚合、CLI TUI 等领域积极扩展能力边界。社区参与深度良好，有用户直接定位到核心性能瓶颈并提交优化 PR，整体项目健康度与交付节奏处于高位。

---

## 2. 版本发布

本日无新版本发布。

---

## 3. 项目进展

今日合并/关闭了多项关键 PR，项目健壮性与功能覆盖度显著提升：

- **工具可配置性**：[PR #4138](https://github.com/HKUDS/nanobot/issues/4138) 为内置文件系统工具新增 `tools.file.enable` 开关，使模型能力可被精细限制，对齐 `exec` / `web` 工具的配置模式，方便在 MCP 沙箱等限制性环境中部署。
- **连接稳定性**：[PR #4230](https://github.com/HKUDS/nanobot/issues/4230) 修复 `streamableHttp` MCP 传输协议因默认 `timeout=None` 导致的无限期挂起问题，增强 MCP 扩展的鲁棒性。
- **数据一致性**：[PR #4246](https://github.com/HKUDS/nanobot/issues/4246) 修复 `delete_session()` 未能清理遗留全局目录会话文件的问题，杜绝历史聊天记录因路径不一致而意外“复活”的 Bug。
- **多模态增强**：[PR #4394](https://github.com/HKUDS/nanobot/issues/4394) 支持 OpenAI 图片编辑 API（`/images/edits` 路由），补齐参考图编辑链路。
- **渠道兼容**：[PR #4342](https://github.com/HKUDS/nanobot/issues/4342) 修复飞书渠道因 WebSocket 卡片结构差异导致内容渲染为空的问题。

此外，新提交的 [PR #4421](https://github.com/HKUDS/nanobot/issues/4421)（工具定义 Token 编码缓存）与 [PR #4411](https://github.com/HKUDS/nanobot/issues/4411)（SuspendTurn 暂停回合支持）预示了下一步性能优化与异步人机交互能力的前进方向。

---

## 4. 社区热点

**Issue #4013：升级后流式输出硬中断（5 条评论）**  
用户 `mxnbf` 反馈从 v0.1.5 升级到 v0.2.0 后，LLM 流式输出在 90 秒后被硬中断，“使所有实际工作变得无用”。该 Issue 今日已关闭，推测已纳入修复路径，但作为近期高频痛点，社区对其解决方案高度关注。  
🔗 [Issue #4013](https://github.com/HKUDS/nanobot/issues/4013)

**Issue #4374：项目工作区读写路径不对称（3 条评论）**  
用户 `maximilize` 精准报告了 Project Workspaces 中的一个设计不对称 Bug：`SOUL.md` / `USER.md` 从项目路径读取，却被写入默认工作区。该反馈属于高质量 Bug 报告，具备清晰复现路径，今日已修复关闭。  
🔗 [Issue #4374](https://github.com/HKUDS/nanobot/issues/4374)

**PR #4329：CLI TUI 模式（持续活跃）**  
该 PR 为 `nanobot agent` 命令新增终端内 TUI 交互界面，虽未合并，但在多轮 review 中更新频繁，社区对交互体验升级的诉求可见一斑。  
🔗 [PR #4329](https://github.com/HKUDS/nanobot/issues/4329)

---

## 5. Bug 与稳定性

**严重级别：**

| Issue | 问题描述 | 状态 |
|---|---|---|
| [#4287](https://github.com/HKUDS/nanobot/issues/4287) | LLM 返回空响应时，NanoBot 不触发备用模型降级（`non-fallbackable` 错误分类），导致请求丢失 | ✅ 已关闭 |
| [#4345](https://github.com/HKUDS/nanobot/issues/4345) | 图片输入被剥离降级为文本后，替代文本使模型误以为“看见”了图片，并且泄露文件路径 | ✅ 已关闭 |
| [#4013](https://github.com/HKUDS/nanobot/issues/4013) | 流式推理超过 90 秒被硬中断，阻断后续对话 | ✅ 已关闭 |
| [#4052](https://github.com/HKUDS/nanobot/issues/4052) | MCP `notifications/progress` 消息被 Pydantic 校验拒绝，导致长任务无法正常推送进度 | ✅ 已关闭 |

**轻度 / 回归：**

| Issue | 问题描述 | 状态 |
|---|---|---|
| [#4410](https://github.com/HKUDS/nanobot/issues/4410) | v0.15 升级后心跳任务无视指令，持续向用户发送无意义消息。项目方已定位到 `agent/loop.py:1008-1009` | 🔴 新建未修复 |
| [#4420](https://github.com/HKUDS/nanobot/issues/4420) | `estimate_prompt_tokens` 每轮迭代对不变的工具定义做冗余 tiktoken 编码，造成性能瓶颈 | 🔴 新建，已有修复 PR [#4421](https://github.com/HKUDS/nanobot/pull/4421) |

---

## 6. 功能请求与路线图信号

**短期高概率纳入**：

- **令牌估算缓存优化**（[#4420](https://github.com/HKUDS/nanobot/issues/4420)）：社区用户 `codeLong1024` 已定位原因，同日 [PR #4421](https://github.com/HKUDS/nanobot/issues/4421) 即提交了缓存方案，预计快速合入。
- **模型预设与任务分发增强**：[PR #4416](https://github.com/HKUDS/nanobot/issues/4416) 支持 Cron 任务指定 `model_preset`，[PR #4415](https://github.com/HKUDS/nanobot/issues/4415) 支持 Spawn 子智能体时覆盖模型，表明项目正为多模型混合编排场景铺路。

**中期路线图信号**：

- **推理力度自动升级**（[#4419](https://github.com/HKUDS/nanobot/issues/4419)）：应对多供应商推理模型对 `reasoningEffort` 参数的支持，用户提议在当前静态配置基础上增加动态自动调节机制。
- **子智能体结果聚合模式**（[PR #4414](https://github.com/HKUDS/nanobot/issues/4414)）：新增 `aggregated` 模式，将并发子任务的阶段性结果聚合后统一推送，提升高频任务场景下的信噪比。
- **SuspendTurn 回合暂停**（[PR #4411](https://github.com/HKUDS/nanobot/issues/4411)）：为工具链引入异步人机交互中场暂停能力，拓展审批流等真实场景。

---

## 7. 用户反馈摘要

**核心痛点：**

> “它是一个非常好的工具，但升级后流中断使所有实际工作变得无用。” —— `mxnbf` on [#4013](https://github.com/HKUDS/nanobot/issues/4013)

> “我在用 NanoBot 跑 Telegram bot 生产环境，高峰期 DeepSeek 返回空响应时并未触发备用模型，这应该是一个可降级的错误。” —— `glebov` on [#4287](https://github.com/HKUDS/nanobot/issues/4287)

> “降级时模型拿到的是「[用户发送了图片：/path/to/file.jpg]」这样的文字，它以为自己看见了图片，产生了幻觉。” —— `BearMett` on [#4345](https://github.com/HKUDS/nanobot/issues/4345)

**社区积极性正面信号：**

- 用户在 [#4013](https://github.com/HKUDS/nanobot/issues/4013) 开头肯定 v0.1.5 体验优异（“way to say ty”），说明产品基础体验扎实，Bug 主要集中在迁移后的回归场景。
- [#4420](https://github.com/HKUDS/nanobot/issues/4420) 用户在实现自己数字员工项目时主动深入上游代码定位性能瓶颈，体现出社区的高参与度和工程素养。

---

## 8. 待处理积压

以下长期开放或需决策层关注的 PR / Issue 建议优先响应：

| 项目 | 类型 | 挂起时长 | 说明 |
|---|---|---|---|
| [PR #1945](https://github.com/HKUDS/nanobot/issues/1945) XMPP 渠道支持 | 功能 | 3 个月+ | 功能较为完整，但渠道维护成本高，需社区或维护者决定是否正式合入 |
| [PR #3591](https://github.com/HKUDS/nanobot/issues/3591) Dream 更新范围控制 | 功能 | 1.5 个月 | 允许限制 Dream 仅更新记忆/上下文，防止技能漂移，用户期待度高 |
| [PR #3662](https://github.com/HKUDS/nanobot/issues/3662) Token 估算脱网加载 | 优化 | 1.5 个月 | 与今日新 Issue #4420 / PR #4421 高度重叠，建议合并评审 |
| [Issue #4410](https://github.com/HKUDS/nanobot/issues/4410) 升级后心跳消息异常 | 回归 Bug | 新开 | 虽为今日新开，但涉及 v0.15 → 新版行为回归，已有社区成员提交修复 PR [#4412](https://github.com/HKUDS/nanobot/issues/4412)，建议加速审查 |

---

**编辑点评：** 本期日报集中反映了 NanoBot 从快速扩张期向“生产加固期”过渡的特征。17 个活跃 PR 的同时推进、用户主导的性能优化贡献、以及围绕模型可靠性（降级、中断、幻觉）的密集修复，都是项目向成熟度冲刺的积极信号。建议团队在持续推进新功能的同时，重点审查积压的渠道类 PR（#1945）与核心模块长期分支（#3591），避免技术债累积影响社区信心。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 | 2026-06-20

> 数据源：NousResearch/hermes-agent | 报告周期：2026-06-19 ~ 2026-06-20

---

## 1. 今日速览

大版本 v0.17.0 "The Reach" 发布后次日，Hermes Agent 社区迅速进入密集的版本打磨阶段。24 小时内共更新 **50 个 Issue**（新开/活跃 40，已关闭 10）与 **50 个 PR**（43 个待合并，7 个已合并/关闭），社区活跃度保持在极高的水平。

尽管 v0.17.0 带来了约 800 个合并 PR 的巨幅更新，但用户在日常使用中遇到了若干严重回归，特别是在 **Gemma 4 模型兼容性**、**桌面端 GUI 交互**及**跨平台网关稳定性**方面。社区贡献者的反应非常迅速，以 `likunoc` 和 `stephenschoettler` 为代表，在提交 Bug 报告后数小时内即输出了高质量的修复 PR，显示出项目成熟的自愈生态。

项目整体健康度极佳，正处在大版本发布后的最佳窗口期。维护者可重点利用当前热度，加快 **43 个待合并 PR** 的审查与合入速度。


## 2. 版本发布

### Hermes Agent v0.17.0 (v2026.6.19) — "The Reach Release"

**更新规模**
- 累积：~1,475 个 Commit、800 个合并 PR、300+ 关闭 Issue
- 代码变更：1,693 个文件、235,390 行新增、50,730 行删除
- 社区参与：**245 位社区贡献者**

**核心主题**
该版本在上一个桌面化里程碑（v0.16.0）的基础上，横向延伸了 Agent 的平台触达能力。核心依赖包括 PID 命名空间隔离强化（`#4432`）、大规模跨平台 Gateway 交付流程重构，以及 GEM 工具集的扩展。

**⚠️ 迁移与兼容性注意**
- **数据库 Schema 迁移**：SQLite WAL 状态处理有重大更新（参见 PR `#49354`），升级后首次启动时需关注状态存储迁移日志。
- **插件 API 变更**：插件发现与加载路径有所调整，建议第三方插件开发者验证其兼容性。
- **⚠️ 已知重要未决问题**：该版本 **仍未彻底修复 Ollama + Gemma 4 的 `finish_reason='length'` 截断问题**。用户 `xRedCrystalx` 已重新开题（`#49297`），官方回应可能以后续 HotFix 形式跟进。建议使用 Ollama + Gemma 4 的用户暂时回退或关注维护者更新。


## 3. 项目进展

### 今日合并/关闭的核心修复（7 个 PR）

| 领域 | 合并/关闭 | 描述 |
|---|---|---|
| 网关稳定性 | [#49260] 关闭 | 修复 Signal 实时适配器在发送 Cron 定时消息时的静默传递故障，确保 AI 定时简报准确送达 |
| 桌面端体验 | [#43476] 关闭 | 修复 Desktop 版 `/goal` 命令被吞没，无视觉反馈的问题 |
| 部署稳定性 | [#36641] 关闭 | 修复 Docker 容器重建后 WhatsApp Bridge 依赖安装失败的问题 |
| 环境兼容 | [#21788] 关闭 | 修复 Dashboard 中 `.venv` 与 `venv` 并存导致 gateway 误退出的问题 |
| 模型兼容 | [#39281] 关闭 | Gemma 4 的部分兼容性修复（但用户反馈仍未彻底解决，见`#49297`） |

### 高价值活跃 PR（待合入）

| PR | 类型 | 关键进展 |
|---|---|---|
| [#49037](https://github.com/NousResearch/hermes-agent/pull/49037) | 核心架构 | **一级 Project 架构**：彻底重构会话管理树，废弃基于 Git 分支的推测模型，转为后端权威的 `Project → Repo → Lane` 模型 |
| [#49389](https://github.com/NousResearch/hermes-agent/pull/49389) | Bug 修复 | **小米 MiMo 视觉修复**：`likunoc` 在提交 Bug 报告 `#49388` 后数小时内提出修复，修复了图像降级为文字摘要的严重问题 |
| [#49252](https://github.com/NousResearch/hermes-agent/pull/49252) | 性能优化 | **自改进成本优化**：`teknium1` 通过辅助模型路由、上下文消化及自适应节奏，显著降低后台审查过程的 Token 消耗 |
| [#49387](https://github.com/NousResearch/hermes-agent/pull/49387) | 本地化 | **俄语翻译 complete**：覆盖近 1000 个字符串，Hermes Desktop 国际化再进一步 |
| [#49384](https://github.com/NousResearch/hermes-agent/pull/49384) | 平台覆盖 | **Linux 桌面入口注册**：解决 Linux 用户在应用启动器中找不到 Hermes Desktop 图标的问题 |
| [#49392](https://github.com/NousResearch/hermes-agent/pull/49392) | 文档 | **Shell Hook 协议文档**：为开发者详细说明各事件的 `extra` 字段负载格式 |


## 4. 社区热点

### 🔴 热点 1：Gemma 4 兼容性难题（[#45924](https://github.com/NousResearch/hermes-agent/issues/45924)、[#49297](https://github.com/NousResearch/hermes-agent/issues/49297)）
用户 `xRedCrystalx` 明确表示："Updated hermes today to v0.17.0 and issue still persists"，并在旧 Issue `#39281` 关闭后被迫重新开题。Bug 表现为模型输出因 `finish_reason='length'` 频繁截断，甚至无法完成最基本的 "Hello" 对话。该问题已跨越两个大版本，发展成为社区信任度的一大考验。受影响的典型场景为 **MacBook 24GB + Ollama + Gemma 4 12B** 的本地部署组合。

### 🟡 热点 2：凭证代理守护进程（[#4656](https://github.com/NousResearch/hermes-agent/issues/4656)）
自 4 月 2 日以来累积 **11 条评论**，是社区最高呼声的 Infra 功能。该倡议呼吁在 Agent 网络传输层实现一个零知识的 HTTP/HTTPS 代理，旨从根本上隔离主进程与子进程的 API Key 泄露风险。Issue `#3628`（环境作用域）和 PR `#4432`（PID 命名空间隔离）虽然降低了攻击面，但均无法解决配置文件外泄的问题。该议题是企业级部署者的核心痛点。

### 🟢 热点 3：小米 MiMo 视觉问题的完美协作（[#49388](https://github.com/NousResearch/hermes-agent/issues/49388)、[#49389](https://github.com/NousResearch/hermes-agent/pull/49389)）
展示了理想的社区协作闭环：`likunoc` 在提交包含深层根源分析（两个独立根源）的 Bug 报告后，当天随即提交了修复 PR。这种 "Report + Fix" 的模式值得表扬。


## 5. Bug 与稳定性

### 紧急（P1）

| Issue | Bug 描述 | 影响 |
|---|---|---|
| [#49307](https://github.com/NousResearch/hermes-agent/issues/49307) | **上下文压缩导致回复重复与指令丢失**（Critical） | 在上下文压缩后，Agent 不仅产生大段重复回答，新增的系统指令也会丢失。 |
| [#49361](https://github.com/NousResearch/hermes-agent/issues/49361) | **CLI 会话对 Session Index 不可见** | 所有 CLI/TUI 会话文件存在于磁盘但无法通过 `session list` 索引，自动恢复功能完全失效。 |
| **(已关闭) [#49260](https://github.com/NousResearch/hermes-agent/issues/49260)** | Signal 适配器消息静默丢失 | 定时业务消息显示 "delivered" 但用户从未收到。 |

### 较高（P2）

| Issue | Bug 描述 | 状态 |
|---|---|---|
| [#47868](https://github.com/NousResearch/hermes-agent/issues/47868) | **严格 API Provider 拒绝泄漏的元数据** | `messages[]` 中残留 `timestamp` 等字段导致 OpenCode Go / Fireworks 后端返回 400 |
| [#49345](https://github.com/NousResearch/hermes-agent/issues/49345) | **桌面端"启动网关"按钮失效** | 监控仪表盘中的 "Start Gateway" 点击无响应 |
| [#49386](https://github.com/NousResearch/hermes-agent/issues/49386) | **内存工具策略绕过（安全）** | 配置 `disabled_toolsets=["memory"]` 后外部 memory-provider 仍可被调用 |
| [#49388](https://github.com/NousResearch/hermes-agent/issues/49388) | **Xiaomi MiMo 视觉降级** | 图像被退化为纯文字摘要 | **已有修复 PR #49389** |
| [#49332](https://github.com/NousResearch/hermes-agent/issues/49332) | **`delegate_task` 模型重载被忽略** | 子任务 `model` 参数完全无效，强制使用主模型 |
| [#49242](https://github.com/NousResearch/hermes-agent/issues/49242) | **Windows Node/npm 路径冲突** | WhatsApp 网关和 Desktop 更新器未优先使用 Hermes 自带的 Node |

### 常规（P3）
- 中文输入逗号/句号触发设置画面（[#49326](https://github.com/NousResearch/hermes-agent/issues/49326)）
- Raft CLI 未启用时持续误报 Warning（[#49336](https://github.com/NousResearch/hermes-agent/issues/49336)）
- CLI 忙闲指示器硬编码 `msg=interrupt`（[#49390](https://github.com/NousResearch/hermes-agent/issues/49390)）
- Tool 循环保护未覆盖 `skills_list`/`skill_view`（[#49075](https://github.com/NousResearch/hermes-agent/issues/49075)）


## 6. 功能请求与路线图信号

### 🔮 高概率纳入 v0.18 的特征

| 议题/PR | 功能 | 现状 |
|---|---|---|
| [PR #49037](https://github.com/NousResearch/hermes-agent/pull/49037) | **一级 Projects 架构** | 重构会话管理，极大概率优先合入 |
| [Issue #49363](https://github.com/NousResearch/hermes-agent/issues/49363) | **桌面端仪表盘插件系统** | Web 端强大的插件运行时向 Electron 桌面端对齐 |
| [Issue #49229](https://github.com/NousResearch/hermes-agent/issues/49229) | **Zulip 平台集成** | 已被封闭 PR `#3335` 实现，待合入主干 |
| [Issue #49279](https://github.com/NousResearch/hermes-agent/issues/49279) | **GLM-5.x 原生推理支持** | 扩展 OpenCodeGo Profile 对智谱 GLM-5 系列的支持 |
| [PR #49384](https://github.com/NousResearch/hermes-agent/pull/49384) | **Linux 桌面入口注册** | 修复 Linux 用户的应用启动器缺失问题 |

### 💡 社区长期愿景
- **零知识凭证代理**（[#4656](https://github.com/NousResearch/hermes-agent/issues/4656)）：被视为接入企业网络与严格合规审查的必备模块，亟需官方路线图回应。
- **辅助视觉 Provider 继承**（[#48991](https://github.com/NousResearch/hermes-agent/issues/48991)）：`auxiliary.vision.provider=auto` 不继承 `base_url`/`api_key`，影响自定义 Provider 用户。


## 7. 用户反馈摘要

### 1. 失望与期待
用户 `xRedCrystalx` 在 v0.17.0 后未能等到 Gemma 4 的彻底修复，被迫重新开题，映射出大版本发布中用户对于**重点 Bug 快速修复的高度敏感**。而用户 `dsr-restyn` 在 `#4656` 中提出的零知识代理方案，代表了社区对 Agent 安全的认知正在从"应用层沙盒"升维到"网络层零信任"。

### 2. 环境多样性带来的挑战
大量反馈来自于：
- **MacBook 24GB 本地部署 Gemma 4**
- **Docker + WhatsApp 集成**
- **Windows 复杂 PATH 环境**
- **Signal Cron 定时日报**
这表明 Hermes Agent 正在从纯粹的开发者极客工具向**多元异构生产环境**渗透，对质量保障中的环境覆盖提出了更高要求。

### 3. 贡献者精神高昂
核心贡献者 `stephenschoettler` 在当前队列中独占至少 8 个活跃的修复 PR（MCP 超时、CLI 冻结、Discord Token 读取、Honcho 配置等），展现出极强的模块化发现与独立修复能力。建议项目组通过定向赞助或角色邀请的方式稳定此类高质量贡献者的持续性投入。


## 8. 待处理积压

### ⚠️ PR 审查瓶颈（43 个待合并 PR）

目前项目面临的最大短期风险不是 Bug 数量，而是**高质量 PR 的长时间积压**。以下来自核心贡献者 `stephenschoettler` 的关键 PR 已在队列中滞留数周至数月：

| PR | 主题 | 提交时间 | 备注 |
|---|---|---|---|
| [#17124](https://github.com/NousResearch/hermes-agent/pull/17124) | Honcho 配置回退修复 | 2026-04-28 | 核心记忆插件稳定性 |
| [#24148](https://github.com/NousResearch/hermes-agent/pull/24148) | CLI 目标控制修复 | 2026-05-12 | CLI 重度用户受阻 |
| [#34276](https://github.com/NousResearch/hermes-agent/pull/34276) | MCP 超时修复 | 2026-05-29 | MCP 插件管理 |
| [#34281](https://github.com/NousResearch/hermes-agent/pull/34281) | Discord Token 读取 | 2026-05-29 | 跨平台体验 |
| [#35687](https://github.com/NousResearch/hermes-agent/pull/35687) | CLI 计时器稳定 | 2026-05-31 | 视觉反馈修复 |
| [#34282](https://github.com/NousResearch/hermes-agent/pull/34282) | CLI Context 仪表维护 | 2026-05-29 | 未返回 Usage 时失效 |
| [#43841](https://github.com/NousResearch/hermes-agent/pull/43841) | Discord 读工具授权 | 2026-06-10 | CLI 与网关权限一致性 |
| [#47634](https://github.com/NousResearch/hermes-agent/pull/47634) | Python 3.14 后台 Worker | 2026-06-17 | 新版本兼容性 |

**强烈建议**：在下一轮 HotFix 周期中对上述 PR 进行集中审查与合并，不要等到下一个大版本。

### 悬而未决的核心 Issue

| Issue | 主题 | 创建时间 | 关键词 |
|---|---|---|---|
| [#4656](https://github.com/NousResearch/hermes-agent/issues/4656) | 零知识凭证代理 | 2026-04-02 | **Infra / Security** |
| [#23802](https://github.com/NousResearch/hermes-agent/issues/23802) | CLI 插件过滤破坏 | 2026-05-11 | **Plugin / CLI** |
| [#25106](https://github.com/NousResearch/hermes-agent/issues/25106) | CLI 模型配置持久化 | 2026-05-13 | **Config / CLI** |
| [#33327](https://github.com/NousResearch/hermes-agent/issues/33327) | BlueBubbles Webhook 冲突 | 2026-05-27 | **Gateway / iOS** |
| [#34109](https://github.com/NousResearch/hermes-agent/pull/34109) | Holographic Memory numpy 缺失 | 2026-05-28(PR) | **Memory / PR 积压** |

---

> 总结：Hermes Agent 正处在大版本发布后的高速迭代窗口。社区活力四射、贡献者自愈能力极强，但 **PR 审查瓶颈** 与 **Gemma 4 兼容性** 是当前最影响用户体验和社区协作效率的两大关键风险点。建议维护者利用 v0.17.x 的 HotFix 周期解决上述问题，为 v0.18 的 Projects 架构和桌面端插件系统奠定坚实信任基础。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报｜2026-06-20

## 1. 今日速览

过去 24 小时内，项目收到 **4 条新 Issue**、**7 条 PR 更新**，并发布了最新 Nightly 构建版本。社区互动活跃，暴露了两项高价值线索：中文用户报告的“模型失忆” Bug（#3150）暗示状态管理可能存在的脆弱性；Windows 平台路径兼容性问题（#2472）仍在持续发酵。安全侧，针对 SSRF 绕过的补丁（PR #3143）正在审查。**活跃度评估**：贡献者提交积极，但大量 PR 处于 Stale 待合状态，维护者的批量和合入节奏直接影响社区贡献者的持续投入意愿。

---

## 2. 版本发布

- **Nightly Build：`v0.3.0-nightly.20260620.287853ab`**
  - **变更范围**：自 v0.3.0 稳定版以来的全部 `main` 分支变更。
  - **稳定性警告**：官方标注为不稳定构建，可能存在未暴露的回归问题，仅建议测试环境使用。
  - **迁移注意**：无明确 Breaking Changes 声明，但 diff 可能包含实验性 API 调整，升级生产环境前请仔细比对 [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)。

---

## 3. 项目进展

- **#2956 关闭**（`fix: preserve channel enabled state when merging security.yml`，作者：yuxuan-7814）—— 针对 `config.json` 中 `enabled: true` 被 `.security.yml` 加载过程意外覆盖的修复。该 PR 今日被关闭（状态：stale），虽未追查到合并记录，但暴露了安全配置中心与主配置文件的合并逻辑缺陷，建议开发团队在后续 sprint 中给出明确处理结论。
- **#3143 新提交**（`fix(web): block private IPv4 embeds in ISATAP literals`，作者：lc6464）—— 针对 SSRF 绕过漏洞的直接修复。安全性和正确性均在线，若顺利合并，可消除 `web_fetch` 工具的防御盲区。
- **#2937 持续更新**（`Feat/agent collaboration`，作者：afjcjsbx）—— 大型架构特性 PR，近日仍有更新。引入 Agent 间持久化消息总线，是项目朝分布式多 Agent 演进的关键基石。

> **总结**：项目在 **安全加固** 和 **架构演进** 上保持了良好节奏，但配置管理的合入流程显得稍许混乱，补丁关闭后无外部可追踪的后续状态。

---

## 4. 社区热点

- 🗣️ **#3150「它给自己整失忆了」**[🔗](https://github.com/sipeed/picoclaw/Issues/3150)
  - **作者**：svier0 — 今日创建，2 条评论。
  - **分析**：标题极具传播力，直指 AI Agent 的**记忆可靠性**。虽摘要信息不全，但“失忆”描述在当前大模型应用中是极度严重的用户体验负面信号，建议维护者第一时间联系作者补充环境与复现步骤。

- 👍 **#2472 Windows 路径分隔符问题**[🔗](https://github.com/sipeed/picoclaw/Issues/2472)
  - **作者**：ut2or1 — 6 条评论，1 个赞，持续 2 个月。
  - **分析**：社区对跨平台兼容性的耐心值得肯定。Issue 分析深度极高，直接定位到 Go 标准库 `fs.FS` 与 Windows 原生路径的冲突。该问题若不被根除，Windows 用户的核心文件操作能力将长期被阉割。

- 🧠 **#3114 Telegram 对话类型权限分级控制**[🔗](https://github.com/sipeed/picoclaw/Issues/3114)
  - **作者**：v2up-32mb — 1 个赞。
  - **分析**：用户明确提出了“私聊 vs 群组 vs 频道”的三级权限隔离模型，直指当前 `allow_from` 设计的粗粒度安全缺陷。这反映出社区已不满足于个人工具，开始向**多租户团队生产环境**部署探索。

---

## 5. Bug 与稳定性

（按严重程度降序排列）

| 严重度 | 标题 | 状态 | 关键信息 |
|---|---|---|---|
| 🔴 **安全漏洞** | SSRF 绕过（ISATAP 字面量） | 修复 PR #3143 待合并 | `web_fetch` 防御绕过，可攻击内网 |
| 🟠 **平台阻断** | `list_dir` 在 Windows 上返回 `invalid argument` | 无关联 PR，积压 >2 个月 | 影响 Windows 用户文件能力核心链路 |
| 🟡 **逻辑崩溃** | Agent“失忆”、上下文丢失 | 新报 #3150，待复现 | 严重影响用户对 Agent 可靠性的信任 |
| 🟢 **潜在 Panic** | `openai_compat` Provider 未检查类型断言 (#3091) | PR 已提交待合并 | Non-bool 值静默求值为 `false`，功能异常 |
| 🟢 **潜在 Panic** | `evolution store` `LockStoreFile` 未检查类型断言 (#3053) | PR 已提交待合并 | 类型不匹配直接 Panic |
| 🟢 **配置丢失** | `security.yml` 加载重置 `enabled` 状态 (#2956) | PR 关闭，问题待确认 | 影响多文件配置下的通道启动状态 |

---

## 6. 功能请求与路线图信号

- **🚩 路线图核心：通用附件支持（#348）** [🔗](https://github.com/sipeed/picoclaw/Issues/348)
  - 标签：`[priority: high]` `[type: roadmap]`
  - 信号解读：用户希望 PicoClaw 能处理 IM 消息中的日志、代码、图片等文件附件。这是 Agent **感知能力从纯文本扩展到多媒体**的关键跃升，预计是 v0.4+ 的核心方向。

- **🗳️ 高赞呼声：Telegram 权限分级（#3114）**
  - 信号解读：用户对安全隔离的需求已从“谁能用”（whitelist）升级到“什么场景能用”（context-based）。该功能若落地，可大幅拓展 PicoClaw 在社群运营、团队协作场景的应用边界。

- **🏗️ 架构演进：Agent 协作总线（PR #2937）**
  - 作者：afjcjsbx
  - 信号解读：引入持久化 Agent 间通信基础设施（mailbox， session， structured envelope）。如顺利合并，PicoClaw 将从“单 Agent 工具”蜕变为“多 Agent 操作系统”。该 PR 已 Stale 近 30 天，亟需维护者给出明确反馈方向。

---

## 7. 用户反馈摘要

- **不满意 — Windows 体验断裂**：`list_dir` 完全失效，Go 的 `fs.FS` 路径规范与 Windows 不兼容。用户已给出详尽分析，但 2 个月无进展（Issue #2472）。
- **不满意 — Agent 记忆不可靠**：`svier0` 报告的“失忆”现象（#3150）直击 AI 产品的命门。若无有效的状态持久化保证，用户无法信赖 Agent 的长期任务能力。
- **期望 — 安全控制粒度不足**：用户在 Telegram 群组中对 Bot 权限充满焦虑，强烈要求根据对话类型（私聊/群组/频道）做能力隔离（#3114）。
- **潜在痛点 — 配置文件冲突**：通过 PR #2956 提交背景可得知，`config.json` 与 `.security.yml` 的双文件配置模式在合入时存在 `enabled` 字段互相覆盖的问题，给运维带来困惑。

---

## 8. 待处理积压

以下为超过合理响应窗口或长期无实质性进展的重点条目，建议维护者在下一轮迭代中优先处理：

| 类型 | 编号 | 标题 | 等待时间 | 建议优先级 |
|---|---|---|---|---|
| **Bug** | #2472 | `list_dir` Windows 路径失败 | 2 个月 | 🔴 高（平台阻断） |
| **Bug** | #3045 | Matrix 用户 `allow_from` 失效 | 13 天 | 🟡 中（影响特定渠道用户） |
| **Feature** | #348 | 通用附件支持 | 4 个月 | 🟢 高（Roadmap 核心） |
| **架构 PR** | #2937 | Agent 协作总线 | 27 天 | 🟢 高（大型 PR，极易冲突） |
| **稳定性 PR** | #3091 / #3053 | 类型断言 Panic 修复 | 10-12 天 | 🟢 低（低风险高回报，建议直接合并） |
| **CLI PR** | #3048 | `mcp add` 标志位解析修复 | 13 天 | 🟢 低（但提升 CLI 体验） |
| **悬案** | #2956 | 配置合并 `enabled` 丢失 | — | 🔵 需要确认修复状态并补录记录 |

> **分析师建议**：PR #3091 / #3053 / #3048 改动量小且经过初步 Review，建议批量合并以清理 Stale 队列、提振贡献者士气。PR #2937 规模庞大，应指派一位核心维护者专责跟进，避免架构级贡献因长期搁置而胎死腹中。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 | 2026-06-20

**数据来源：** github.com/nanocoai/nanoclaw
**分析时段：** 2026-06-19 — 2026-06-20

---

## 1. 今日速览

NanoClaw 今日无版本发布和新的 Issue 活动，社区活跃集中体现在开发贡献端。过去 24 小时内共有 **5 个 Pull Request 保持活跃**（全部为待合并状态），涵盖 Apple 原生运行时支持、权限继承架构以及 Discord/审批流程的稳定性修复。总体来看，项目处于**开发活跃但评审合并节奏偏缓**的阶段，高质量的修复和功能增量已准备就绪，但维护者侧的合并动作有所滞后。项目健康度平稳，社区互动数据（评论、点赞）表现为零，亟需维护者加强响应以维持贡献者积极性。

---

## 2. 版本发布

> 本时段无新版本发布。

---

## 3. 项目进展

今日虽无 PR 被正式合并，但待处理的 5 个 PR 展现了项目下一阶段的清晰演进方向：

- **Apple 容器运行时 (PR #2809)**
  由 `hidenwalker` 提交，新增环境变量 `CONTAINER_RUNTIME=container` 支持，使 NanoClaw 可在 macOS / Apple Silicon 平台上原生运行，并新增远程 OneCLI 网关支持。该 PR 完全向后兼容（默认行为不变），是项目向 Apple 生态扩展的关键基建。

- **父子 Agent 权限继承 (PR #2605)**
  由 `guyb1` 贡献，通过 OneCLI 实现父级代理权限向下继承。这是对多租户、企业级权限模型的重要完善，标志着项目在权限治理方面从扁平走向层级化。

- **Discord 消息分片修复 (PR #2812)**
  由 `axnjxn415` 提交，修复 Discord 适配器因未配置 `maxTextLength` 导致超长回复被截断的问题。切换到分片发送逻辑后，用户可以获得完整的对话体验。

- **审批交付目标持久化 (PR #2820)**
  由 `caburi00` 提交，修复了 `requestApproval()` 流程中 `channel_type`、`platform_id` 等字段因时序问题永久为 NULL 的缺陷，确保审批列表和审计记录的功能完整性。

- **安全信誉徽章 (PR #2819)**
  由第三方安全平台 MseeP.ai 主动提交，为仓库添加安全信任徽章，对提升项目的透明度与供应链安全有积极意义。

**整体评估：** 一旦上述 PR 完成合并，项目将同时完成**一次重大平台扩展**（Apple 原生）、**一次架构升级**（权限层级化）和**两项关键稳定性提升**（消息完整性与审批可追溯性）。

---

## 4. 社区热点

根据今日快照数据，所有 5 个活跃 PR 的**评论数均为 `undefined`，点赞数均为 0**，表明 GitHub 渠道上的公开讨论在本时段内接近于零。这一现象值得关注——高质量的开发贡献若得不到及时的 Reviewer 反馈（即使只是简单的 ACK 或 Code Review 排队），容易挫伤社区贡献者的持续投入意愿。

**值得被社区关注的 PR：**
- **PR #2812（Discord 分片）** 直接关系所有 Discord 用户的日常使用，对于使用 NanoClaw 构建聊天助手的小组类用户影响最大。
- **PR #2820（审批持久化）** 涉及审批工作流的核心数据链路，团队协作场景下的用户应重点验证和推动。

---

## 5. Bug 与稳定性

无新的 Issue 报告 Bug。以下稳定性问题是基于 PR 描述反推的现存缺陷：

| 严重程度 | Bug 描述 | 关联 PR | 修复状态 |
|----------|----------|---------|----------|
| **High** | **Discord 回复截断**：适配器未传递 `maxTextLength`，导致 `splitForLimit` 分片逻辑未被触发，超 2000 字符的回复被直接截断。 | #2812 | PR 已提交，待合并 |
| **Medium** | **审批记录字段缺失**：`pending_approvals` 表的 `channel_type`、`platform_id` 等字段因创建于选定审批人之前而永为 NULL，审批列表和通知丢失来源信息。 | #2820 | PR 已提交，待合并 |

> 两项修复均已实现并处于待审状态，建议优先评审合入以消除现有功能缺陷。

---

## 6. 功能请求与路线图信号

虽然本时段无 Issues 提出新功能请求，但已提交的 PR 本身即为有力的路线图信号：

- **Apple 原生容器部署 (PR #2809)**
  标志性功能，开放 `CONTAINER_RUNTIME=container` 环境变量，使得在 macOS 上无需 Docker 即可运行 NanoClaw。同时引入远程 OneCLI 网关，为分布式/异构控制平面铺路。这极有可能被纳入**下一大版本（可能是 v2.x）** 的核心特性。

- **Parent Agent Permissions (PR #2605)**
  权限模型的层级化扩展，通过 OneCLI 实现权限继承。如果当前的顶级权限机制被认为是 v1.0 的形态，那么#2605 定义的继承模式很可能是**即将发布的权限重构**标志。

- **安全生态系统集成 (PR #2819)**
  MseeP.ai 主动提交徽章 PR，暗示社区和第三方安全平台开始关注 NanoClaw 的供应链透明度。如果后续采纳类似的自动安全审查工具，项目可能逐步建立 SBOM 或持续安全审计机制。

---

## 7. 用户反馈摘要

由于今日无新 Issues 且所有 PR 评论数为零，**直接的用户语音文本缺失**。通过分析 PR 描述和修复意图，可以反推出现有用户群体面临的主要痛点：

- **终端用户（Discord 场景）：** 在使用 Agent 对话时遭遇长回复忽然截断，消息不完整，影响决策和交互体验（来源 #2812）。
- **管理员/企业用户（审批场景）：** 审批流程中无法回溯卡片是从哪个平台、哪个消息发起的，审批列表功能失效，严重影响合规审计和工作流追踪（来源 #2820）。
- **开发者/高级用户（部署场景）：** 存在在 macOS 下不依赖 Docker 直接运行 NanoClaw 的需求，现有依赖容器化环境增加了一定配置成本（来源 #2809）。

> 鼓励用户在 GitHub Issues 和 Pull Requests 中积极留言互动，以便项目维护者汇总和响应社区关切。

---

## 8. 待处理积压

> ⚠️ **特别标记：** 本路段数据反映出 PR #2605 已积压长达 27 天，成为当前项目最大的协作风险点。

| 类型 | 编号 | 标题 | 积压天数 | 优先级 | 状态说明 |
|------|------|------|---------|--------|----------|
| **PR** | [#2605](https://github.com/nanocoai/nanoclaw/pull/2605) | feat: inherit parent agent permissions via OneCLI | **27 天** | **Critical** | 作者已遵循贡献指南，功能影响深远，长期无 Reviewer 介入，流失高级贡献者的风险最高。建议维护者立即分配至少一个 Owner 进行初步评审。 |
| **PR** | [#2809](https://github.com/nanocoai/nanoclaw/pull/2809) | feat(apple-container) | 2 天 | High | 大特性，需引入 CI 验证流程，建议设定专门的 Review Period。 |
| **PR** | [#2812](https://github.com/nanocoai/nanoclaw/pull/2812) | fix(discord): chunk replies | 2 天 | High | 影响面广（所有 Discord 用户），修复逻辑清晰，风险低，适合作为近期合入的优先快修。 |
| **PR** | [#2820](https://github.com/nanocoai/nanoclaw/pull/2820) | fix(approvals): persist delivery target | 1 天 | Medium | 修复清晰的字段持久化 bug ，稳定性场景覆盖位。 |
| **PR** | [#2819](https://github.com/nanocoai/nanoclaw/pull/2819) | Add MseeP.ai badge | 1 天 | Low | 低风险快速合并项，可直接 squash merge，鼓励第三方贡献。 |

---

**分析师点评：**
项目今日的开发输入有力而清晰，但 **5 个 PR 零合并 + 零互动** 的数据特征已经敲响了社区运营的警钟。Open Source 项目的生命力不仅在于代码量，更在于 `Review — Merge — Feedback` 的闭环效率。建议维护者：
1. 优先安排 #2605 的初评，降低长积压导致的贡献者流失风险。
2. 将 #2812 和 #2820 作为本周 Hotfix 合并，让社区看到修复时效。
3. 在项目 README 或 DISCUSSIONS 中说明当前评审资源状况，以管理社区预期。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026‑06‑20

---

## 1. 今日速览

过去24小时内，NullClaw 项目共更新 **3 条 Issue**（其中 2 条处于开放/活跃状态，1 条已关闭）和 **1 条 Pull Request**（仍处于待合并状态），无新版本发布。整体活跃度中等，社区主要围绕一个已修复的本地模型响应不完整 Bug 进行收尾确认，同时两项长期存在的问题依然未得到维护者明确回复。项目在 Android/Termux 平台的构建兼容性方面收到一份来自社区的修复 PR，有待维护者审核。

---

## 2. 版本发布

*无新版本发布，此项省略。*

---

## 3. 项目进展

今日无任何 Pull Request 被合并或关闭，项目代码库没有实质性向前推进。值得关注的是，社区贡献者 **vernonstinebaker** 提交了 PR #966，旨在解决 `aarch64-linux-android`（Termux）环境下 `std.http.Client` 因缺少 `/etc/resolv.conf` 而导致的 DNS 解析失败问题。该 PR 通过将 HTTP 请求路由至 libcurl 来规避 Zig stdlib 的限制，一旦合并，将直接惠及 Android 平台用户的使用体验。

📎 https://github.com/nullclaw/nullclaw/pull/966

---

## 4. 社区热点

- **Issue #952（已关闭）** — 是本日最受关注的议题，共产生 3 条评论。报告者使用 Ollama 运行的 Gemma 模型时，Agent 回答总是不完整（截断），并附有截图。该 Issue 在今天被关闭，暗示可能已通过某种方式解决或已被开发者关闭。社区对此类本地模型集成质量关注度高，期待官方的处理说明。

📎 https://github.com/nullclaw/nullclaw/issues/952

- **Issue #484（开放）** — “飞书无法联网查询”自 3 月以来持续开放，同样有 3 条评论，最近更新于昨天。用户反映飞书集成无法进行网络请求，属于功能失效类问题。该 Issue 长期未收到维护者回应，已成为社区隐性痛点。

📎 https://github.com/nullclaw/nullclaw/issues/484

---

## 5. Bug 与稳定性

| 严重程度 | Issue / PR | 描述 | 状态 | 是否有对应修复 PR |
|----------|------------|------|------|------------------|
| **高** | #868 | `zig build` 在 Android/Termux (aarch64) 上因 `options.zig` 链接错误而失败，影响该平台用户自行编译 | **开放**（无维护者回复） | 无直接修复，但 PR #966 针对同一平台做了 HTTP 路由修复，属于间接改进 |
| **中** | #484 | 飞书插件无法联网查询，核心功能受损 | **开放**（长期未解决） | 无 |
| **低** | #952 | 使用 Ollama 本地模型时返回不完整回答，但已关闭 | **已关闭** | 无公开修复记录 |

- **#868** 影响用户自行从源码构建，属于构建系统兼容性问题。报告人提供了详细环境信息和错误日志（`AccessDenied on options.zig linkat`），但尚未有维护者介入。
- **#952** 虽然已关闭，但在缺少修复说明的情况下，可能仍会让其他用户再次遇到类似问题，建议维护者公示解决方法。

📎 #868: https://github.com/nullclaw/nullclaw/issues/868  
📎 #952: https://github.com/nullclaw/nullclaw/issues/952

---

## 6. 功能请求与路线图信号

今日没有任何明确的功能请求（Feature Request）提出。不过，Issue #484 和 #868 属于稳定性/兼容性欠缺，虽非功能请求，却反映出用户对以下能力的期待：

- **国内办公应用（飞书）的稳定集成**（#484）
- **对 Android/Termux 平台的官方构建支持**（#868, #966）

PR #966 的提交表明社区正在主动填补平台支持缺口，这种自下而上的贡献可能影响项目在下一版本的兼容性方向。维护者若积极合并此 PR，将为未来官方支持 Android 构建奠定基础。

---

## 7. 用户反馈摘要

综合本期 Issues 评论中的用户声音，提炼典型痛点：

- **本地模型体验不佳**（#952）：用户 “bloodgroup-cplusplus” 在摘要中明确表示使用 Ollama 拉取的 Gemma 模型无法产出完整句子，且问题可复现。虽然问题已被关闭，但用户对模型输出质量的敏感性值得注意。
- **开发环境受限**（#868）：用户在 Termux 环境下尝试编译失败，反馈了完整的 Zig 版本、设备信息及错误输出，说明其有主动贡献/定制的意愿，却被构建问题阻挡。
- **功能失效长期未处理**（#484）：用户在 3 月就已报告飞书联网查询失败，至今未收到维护者任何回应。这种沉默会削弱社区信任。

整体来看，用户以实际使用场景中的稳定性与集成度为核心诉求，且对平台兼容性有较高期待。

---

## 8. 待处理积压

以下 Issue 和 PR 长期未获得维护者有效响应，建议优先关注：

- **Issue #484（2026‑03‑13 创建）**  
  飞书联网查询问题，3 个月无实质性回复。该问题影响忠实用户日常工作流，亟需维护者确认是否为已知限制或可修复 Bug。  
  📎 https://github.com/nullclaw/nullclaw/issues/484

- **Issue #868（2026‑04‑23 创建）**  
  Android/Termux 构建失败问题，2 个月无维护者介入。已有社区成员提交相关平台的 PR #966，建议将两者关联并给出官方态度。  
  📎 https://github.com/nullclaw/nullclaw/issues/868

- **PR #966（2026‑06‑19 提交）**  
  针对 Android/Termux 平台 HTTP 路由的修复，代码清晰且附有详细问题分析。合并后将直接改善该平台用户的使用体验，同时也是对 #868 反馈的部分间接回应。建议尽快 Code Review 或提供反馈。  
  📎 https://github.com/nullclaw/nullclaw/pull/966

---

**项目健康度评估**：今日社区贡献较为活跃，但维护者响应滞后，长期开放的问题开始积压，可能影响贡献者积极性。若能及时合并 PR #966 并对 #484 和 #868 给出明确答复，项目有望提升迭代效率和社区满意度。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据您提供的 IronClaw 项目数据生成的 2026-06-20 项目动态日报。

---

## IronClaw 项目日报 | 2026-06-20

### 1. 今日速览
过去 24 小时项目活跃度极高，PR 更新达 30 条，其中 12 条已完成合并/关闭。核心团队高强度推进 Reborn 架构迭代，尤其在平台扩展（Slack/Telegram 接入）、基础设施加固（CI 链路优化、QA 固件体系）及核心能力补齐（Projects 全链路完工、并发执行、外部工具调用）上成果显著。Issues 侧有 4 条更新，暴露了 E2E 长期未修复及审批 UI 易用性问题，整体项目处于功能高速推进与稳定性打磨并行的阶段。

### 2. 版本发布
今日无新版本发布。

### 3. 项目进展
今日合并/关闭了大量重要 PR，标志着 Reborn 平台功能框架的基本成型。

- **Projects 模块完整落地**：`#5019` [CLOSED] feat(reborn): light up the Projects page (5/5) 合并，标志着 WebUI v2 下的 Projects 全生命周期管理（CRUD、成员管理）功能正式点亮。相关遗留修复 `#5064` [CLOSED] 也已同步合入。
  - 链接: nearai/ironclaw PR #5019
- **CI 与测试基础设施大规模加固**：
  - `#5090` [CLOSED] perf(ci): extend mold linker 扩展至 E2E 及 replay-gate 任务，预期带来显著编译速度提升。
  - `#5092` [CLOSED] ci(spike): A/B sccache vs rust-cache 完成了实验性对比工作流。
  - `#5095` [CLOSED] / `#5096` [CLOSED] 合入了大量录制型 QA 固件，并将 7 个自动化工作流基准测试导入录制回放体系，显著提升回归测试效率。
  - `#5097` [CLOSED] docs: add Reborn QA guidance to agent rules 补充了跨层测试规范。
  - 链接: nearai/ironclaw PR #5090
- **缺陷修复与体验优化**：
  - `#5078` [CLOSED] 修复了操作审批弹窗在遇到超长 Shell 命令时难以查看详情的问题。
  - `#5087` [OPEN] 实现了 Google OAuth 令牌的主动过期前刷新机制，解决了令牌失效后需手动重连的痛点。
  - 链接: nearai/ironclaw Issue #5078

### 4. 社区热点
尽管 PR 列表未提供详尽的评论数统计，但以下高关注度条目代表了今日社区的核心讨论方向：

- **平台入口之争：Slack vs Telegram 接入**：`#5100` [OPEN] (Telegram Ingress) 与 `#5093` [OPEN] (Slack Ingress) 相继立项。这是社区呼声极高的需求，旨在将 IronClaw 直接投射为即时通讯机器人，实现零壁垒交互。
  - 链接: nearai/ironclaw PR #5100
- **AI Agent 的自我进化**：`#5061` [OPEN] feat(reborn): skill extraction & self-evolution 引入了 Hermes 风格的高阶技能自动萃取与激活机制。该 PR 涉及安全性扫描、作用域写入与上下文注入防护，引发了关于 Agent 自主性边界的深度技术讨论。
  - 链接: nearai/ironclaw PR #5061
- **审批流程的终极博弈**：`#5062` [OPEN] feat(approvals): per-tool permission override model 提出了“始终允许/每次询问/禁用”的三态工具权限模型。这是对 `#5078` (大命令体验差) 和 `#5088` (权限提示不清) 等用户痛点的系统性架构回应，社区反馈积极。
  - 链接: nearai/ironclaw PR #5062
- **易用性谬误**：`#5088` [OPEN] 用户报告 Shell 审批提示误将只读操作标记为需要审批的 `reads` 操作，造成了安全感知上的混乱和疲劳。
  - 链接: nearai/ironclaw Issue #5088

### 5. Bug 与稳定性

- **[严重] Nightly E2E 持续失败**：#4108 `Nightly E2E failed` 自 5 月 27 日开启至今未修复。最新失败报告于 2026-06-19 产生，是目前影响项目回归稳定性的最大风险点。需 Maintainer 介入排查环境或代码层面的回归问题。
  - 链接: nearai/ironclaw Issue #4108
- **[中等] Shell 审批提示误导**：#5088 提示用户审批 `reads` 命令，该命令在系统中并不存在，且在 Shell 执行上下文中具有误导性，降低了用户对安全提示的信任感。
  - 链接: nearai/ironclaw Issue #5088
- **[已修复] 大命令审批弹窗遮盖**：#5078 已关闭，修复了长命令内容覆盖审批按钮与关键细节的 UI 问题。
- **[已改进] OAuth 令牌稳定性**：#5087 虽未合并，但已提供主动刷新方案，降低令牌过期导致的业务中断概率。

### 6. 功能请求与路线图信号

今日的开放 PR/Issue 清晰地勾勒出 IronClaw Reborn 的下一个里程碑方向：

- **迈向生产级部署**：
  - `#5091` [OPEN] 提出建立统一的功能标志（Feature Flag）系统，支持环境动态切换、用户定向与灰度发布。这是大规模企业级部署的基石。
    - 链接: nearai/ironclaw Issue #5091
  - `#5081` [OPEN] 新增 `hosted-single-tenant` Postgres 配置文件，结合现有 SSO 与审批功能，推动 Reborn 从本地开发向托管预览版演进。
    - 链接: nearai/ironclaw PR #5081
- **性能飞跃**：
  - `#5085` [OPEN] 引入 `TurnRunScheduler` 实现并发的对话执行与推理，打破原有严格的串行队列瓶颈，显著提升多会话吞吐量。
    - 链接: nearai/ironclaw PR #5085
- **能力边界拓展**：
  - `#5099` / `#5094` [OPEN] 完善 OpenAI 兼容的 Responses API 工具调用闭环（外部工具注册、调用、结果回传）。
  - `#5065` [OPEN] 支持一次性计划触发器（Once-at），极大拓展了定时任务的灵活性。
    - 链接: nearai/ironclaw PR #5065

### 7. 用户反馈摘要

- **痛点与诉求**：
  - **审批疲劳**：开发者在 `#5078` 和 `#5088` 中反馈，当前审批弹窗在处理复杂 CLI 操作时信息过载，且权限描述模糊（如“reads”），难以快速判断安全性。这直接催生了 `#5062` 的 Per-tool 权限模型。
  - **稳定性焦虑**：`#4108` E2E 长期失败（24 天）可能影响社区贡献者的信新，担心自己的 PR 引入回归。
  - **连接性依赖**：Google OAuth 令牌过期后需要手动重连是高频重复性痛点，`#5087` 的主动刷新机制精准回应了这一需求。
- **满意与期待**：
  - Projects 功能 5/5 栈的完整合并 (`#5019`) 收到了开发者的认可，此功能对于管理复杂工作流至关重要。
  - 社区对 Telegram/ Slack Ingress (`#5100` / `#5093`) 给予了高度期待，认为这是将 AI Agent 融入日常工作流的最后一块拼图。

### 8. 待处理积压

- **`#4108` - Nightly E2E 失败**（持续时间：24 天）
  - 严重性：**高**。E2E 作为质量门禁，长期失败将导致回归风险无法被及时发现。虽然是 BOT 自动报告，但需 Maintainer 立即介入排查。
  - 链接: nearai/ironclaw Issue #4108
- **`#4002` - Dependabot 批量升级**（持续时间：近 1 个月）
  - 严重性：**中**。涉及 16 个 Actions 依赖包的升级（如 `actions/checkout` 大版本跳跃），可能存在破坏性变更或需要解决 CI 冲突，长期未合并将产生技术债务。
  - 链接: nearai/ironclaw PR #4002
- **`#5088` - Shell 审批提示误导**（新开，无维护者回应）
  - 严重性：**中**。作为新报告的可用性 Bug，至今无标签分类或人工回复，建议 Maintainer 尽快确认是否为已知行为或需要修复。
  - 链接: nearai/ironclaw Issue #5088
- **`#4829` - 清理休眠 Workflow**（持续 8 天）
  - 严重性：**低**。虽然内容明确（清理 `reborn-integration.yml`），但处于待合并状态，建议尽快处理以保持 CI 配置整洁。
  - 链接: nearai/ironclaw PR #4829

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

## LobsterAI 项目日报 | 2026-06-20

**分析师观点：** 项目今日处于“战略倾听与积压清洗”阶段。社区贡献者提交了重量级路线图提案，而维护者则通过关闭长期积压的 Issues 来保持项目健康的治理状态。尽管代码层面无变动，但社区能量的跃迁值得关注。

---

### 1. 今日速览

- **整体状态：** 维护与规划主导。项目团队未进行代码合并或版本发布，而是专注于 Issue 追踪器的清理工作。同时，社区中浮现了一个可能重新定义产品方向的宏大功能请求。
- **活跃度评估：** 中等偏下。代码提交与 PR 合并活动停滞，但 Issue 管理活跃（共 4 次更新），且出现了一份内容详实的大型架构提案。
- **关键事件：** 项目执行了 Stale 机制，关闭了 3 个自 4 月起的“僵尸 Issue”；同时，新提交的 **“AI 协作者”功能提案 (#2180)** 成为今日社区最具战略意义的输出。

---

### 2. 版本发布

（本周期内无新版本发布。）

---

### 3. 项目进展

- **代码合入：** 过去 24 小时内**无 Pull Request 被合并或关闭**。项目主干代码库保持稳定，无新功能或修复上线。
- **问题追踪治理：** 维护者通过自动化 Stale 流程关闭了 3 个长期积压的旧 Issue（#1487, #1471, #1472）。这些 Issues 在 2 个多月内因无后续用户响应而被标记关闭。此举有效降低了追踪器噪音，是项目管理健康度的体现，但其中包含的 Bug 并未得到实质修复。

---

### 4. 社区热点

今日社区动态呈现“新旧交替”的格局：

1.  **未来展望（战略聚焦）：[#2180 构建“AI 协作者”表单]**
    - **作者：** @woxinsj
    - **链接：** [Issue #2180](https://github.com/netease-youdao/LobsterAI/issues/2180)
    - **分析：** 虽然该 Issue 刚刚发布且暂无评论互动，但其提交的《OpenClaw AI 协作者提案》内容丰富。提案核心是将 OpenClaw 从低级别工具集升级为面向“懂技术的非精英程序员”的 AI 协作平台，引入自然语言命令栏和跨模型任务调度系统。这是本次报告周期内最重磅的提交，直接触及了项目中长期路线图的根本方向。社区核心用户显然希望项目能承担起更高层次的智能体编排职责。

2.  **旧日回声（生命周期终结）：** 三条此前关于软件 Bug（数据丢失、脚本异常）的报告被关闭。尽管这些 Bug 未引起广泛讨论（共 7 条评论），但它们代表了一部分早期用户在深度使用中遇到的典型障碍，其无疾而终的结局也是对项目 Bug 治理流程的一次检验。

---

### 5. Bug 与稳定性

过去 24 小时内**未收到**新的 Bug 报告。以下是当日因 Stale 而被关闭的遗留 Bug 回顾（按严重程度排列）：

| 严重程度 | Issue | 标题摘要 | 当前状态 | 风险影响 |
|---|---|---|---|---|
| **高 (数据丢失)** | [#1471](https://github.com/netease-youdao/LobsterAI/issues/1471) | 切换视图时输入框草稿因去抖未持久化而丢失 | 已关闭 (Stale) | 用户在写作长文本时，快速切换 Session 或视图会导致未发送内容丢失。 |
| **高 (数据丢失)** | [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472) | 编辑历史消息时静默覆盖当前输入框未发送内容 | 已关闭 (Stale) | 点击历史消息“重新编辑”会直接冲掉当前正在编辑的内容，无任何确认提示。 |
| **中 (功能异常)** | [#1487](https://github.com/netease-youdao/LobsterAI/issues/1487) | 会话中调用 Python 脚本异常（本地 30B 模型） | 已关闭 (Stale) | 特定本地模型下技能执行沙箱存在兼容性问题，弱于 Claude Code CLI。 |

**稳定性评估：** 今日无修复上线。尽管上述 Issue 已被归档，但对应的代码缺陷仍潜藏在当前版本中。对于重度使用 Cowork 功能的用户，数据丢失的风险（#1471, #1472）依然存在，建议在操作中留意手动保存或谨慎点击“重新编辑”。

---

### 6. 功能请求与路线图信号

- **路线图重磅信号：[#2180 “AI 协作者”平台化升级]**
    - **提议核心能力：**
        1.  自然语言命令栏（替代复杂菜单）
        2.  任务分发控制台（跨模型编排）
        3.  项目级持久记忆
    - **战略定位：** 该请求完全跳出了“修改现有 UI 或修复脚下 Bug”的范畴，直接指向了**项目的下一阶段进化形态**。它将 LobsterAI 从一个“附属于 IDE 的脚本执行机”重新定义为“独立的人机协作指挥官”。
    - **目标人群：** 提案明确提出针对“懂技术的非精英程序员”，这是一个非常精准且规模庞大的出海工具用户画像。
    - **纳入版本的可能性分析：** 尽管提案刚提交尚无核心团队回复，但其思路与目前 AI 编程工具向 Agentic（智能体）方向发展的行业趋势高度吻合。如果团队认可此方向，该提案有可能成为 **V2.0 或下一里程碑版本**的核心架构蓝图。

---

### 7. 用户反馈摘要

从今日的动态中，我们可以洞察到几类典型用户的声音：

- **深度工作者的痛诉（@MaoQianTu）：**
    - **场景：** 重度使用 Cowork 输入框编写复杂 Prompt 的技术写作者。
    - **反馈：** 连续两次因 UI 细节（组件卸载防抖失效、静默覆盖）导致丢失大量输入内容。这表明用户对“工作上下文的安全性”极度敏感，当前 UI 的交互模式（未读草稿保护机制）存在明显短板，降低了用户对产品的信任度。

- **横向对比者的批评（@54huige）：**
    - **场景：** 进行多工具对比的技术用户，拥有 30B 本地模型硬件。
    - **反馈：** 明确指出 LobsterAI 的“技能系统在实际执行中不如 Claude Code CLI”。用户将 LobsterAI 与业界公认的顶尖工具进行比较，反映出社区对项目执行层能力的期望很高。技能沙箱的兼容性和稳定性是目前的关键流失点之一。

- **架构师的蓝图（@woxinsj）：**
    - **场景：** 不愿被繁琐低级别 API 操作拖累的独立程序员。
    - **期望：** 要求项目提供高层“思想流”接口（自然语言命令），而非低层“工具流”接口。他不满足于自己做编排，希望工具本身具备协作者级的自主决策与调度能力。

---

### 8. 待处理积压

- **数据安全 Bug 的潜藏风险**
    - **关联 Issue：** #1471, #1472
    - **风险分析：** 虽然这两个 Bug 报告已被 Stale 规则关闭，但代码层面的数据丢失逻辑（debounce 卸载未持久化、编辑覆盖无确认）仍存在于最新代码中。这形成了一个“已归档但未修复”的真空地带。对于每天加入的新用户，只要他们尝试复杂 Prompt 的编写，命中这个 Bug 的概率依然很高。
    - **维护者提醒：** 建议开发团队在内部任务板中补齐这两个 Issue 的修复事项，或至少引入一个草稿 LocalStorage 防御性缓存机制。仅依靠 Issue 追踪器的过期规则来过滤此类高严重性 Bug，可能会损害项目在“数据可靠性”上的声誉。

- **大型 RFC 的初始响应缺口**
    - **关联 Issue：** #2180
    - **提醒：** 该 Issue 目前处于“零回复”状态。提议者提交了如此详细的文档，应获得维护者的初步回应（无论是设定 `needs-design` 标签还是简单的致谢与澄清）。及时的回应对激励高质量社区贡献至关重要，避免热情用户陷入“提交即石沉大海”的负面循环。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，这是根据你提供的 CoPaw (QwenPaw) 项目数据生成的 2026-06-20 项目动态日报。

---

# QwenPaw 项目动态日报 | 2026-06-20

## 1. 今日速览
项目今日迎来社区贡献高峰，24小时内处理了 **11 个 Issues** 和 **17 个 Pull Requests**。社区新面孔贡献显著，最关键的修复之一是长期困扰用户的 ChromaDB 索引膨胀崩溃问题（[#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795)）已通过 [PR #5332](https://github.com/agentscope-ai/QwenPaw/pull/5332) 合并解决。尽管模型兼容性（如 DeepSeek 卡死、智谱连接失败）和 v1.1.12 版本回归问题（如图片发送）带来了短期阵痛，但整个社区响应非常及时，各项修复 PR 均已就位或正在审查中。项目整体活跃度极高，正快速迭代，在稳定性和用户体验上同步改善。

## 2. 版本发布
当前无新版本发布。

## 3. 项目进展

### 漏洞修复与稳定性加固
- **ChromaDB 索引维护**：[PR #5332](https://github.com/agentscope-ai/QwenPaw/pull/5332) 已合并。针对 [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795)，新增了 `compact_index()` 等索引维护功能及超时保护，从根本上解决了索引膨胀至 37G 导致内存搜索崩溃的问题。
- **回复超时保护**：[PR #5242](https://github.com/agentscope-ai/QwenPaw/pull/5242) 已合并。为 `agent.reply()` 调用增加了超时保护，避免 LLM API 无响应时进程冻结。
- **定时任务调度优化**：[PR #5241](https://github.com/agentscope-ai/QwenPaw/pull/5241) 已合并。将默认 `misfire_grace_seconds` 从 60 提升至 3600，防止长任务导致后续定时任务被跳过。
- **多 Agent 协作触发**：[PR #5179](https://github.com/agentscope-ai/QwenPaw/pull/5179) 已合并。补全了触发团队协作模式的关键词，提高了技能识别率。

### API 和框架兼容
- 针对 Zhipu 模型连接失败问题 ([#5330](https://github.com/agentscope-ai/QwenPaw/issues/5330))，社区连开三个 PR ([#5337](https://github.com/agentscope-ai/QwenPaw/pull/5337)、[#5338](https://github.com/agentscope-ai/QwenPaw/pull/5338)、[#5339](https://github.com/agentscope-ai/QwenPaw/pull/5339)) 进行迭代修复，最终方案将消息格式由数组改为纯字符串，适配智谱 API。

**总结**：项目在修复高优稳定性问题上的执行力很强，同时推进了多项 API 兼容性修复，为下一版本的发布扫清了大量障碍。

## 4. 社区热点

### 用户 @bob-geek11 的深度使用反馈
- **Issue [#5328](https://github.com/agentscope-ai/QwenPaw/issues/5328)**：报告 DeepSeek 在 thinking 过程中卡死，严重影响任务连续性。
- **Issue [#5333](https://github.com/agentscope-ai/QwenPaw/issues/5333)**：进一步报告 Agent 提交指令后无响应，且 UI 未正确显示暂停按钮，让用户无法判断运行状态。
- **Issue [#5329](https://github.com/agentscope-ai/QwenPaw/issues/5329)**：提出移动端侧边栏需要切换 Agent 的诉求。
- **分析**：@bob-geek11 的反馈代表了重度用户在多场景（Web/Console/Tauri）使用下的共性痛点。这直接带动了 [PR #5335](https://github.com/agentscope-ai/QwenPaw/pull/5335)（后端异常通知 UI）和 [PR #5334](https://github.com/agentscope-ai/QwenPaw/pull/5334)（侧边栏切换）的迅速产出。

### 版本升级引发的回归讨论
- **Issue [#5320](https://github.com/agentscope-ai/QwenPaw/issues/5320)**：指出 v1.1.12 发布后 `send_file_to_user` 发送图片失败。该问题立即获得了修复 PR（[#5324](https://github.com/agentscope-ai/QwenPaw/pull/5324)），反映出社区对版本稳定性高度敏感，以及维护者介入的及时性。

## 5. Bug 与稳定性

| 严重程度 | Bug 描述 | Issue | 修复状态 |
|---|---|---|---|
| **严重** | DeepSeek 推理卡死，Agent 无响应 | [#5328](https://github.com/agentscope-ai/QwenPaw/issues/5328), [#5333](https://github.com/agentscope-ai/QwenPaw/issues/5333) | 已有修复 PR: [#5335](https://github.com/agentscope-ai/QwenPaw/pull/5335) (异常通知) |
| **严重** | v1.1.12 图片发送功能回归，图片不显示 | [#5320](https://github.com/agentscope-ai/QwenPaw/issues/5320) | 已有修复 PR: [#5324](https://github.com/agentscope-ai/QwenPaw/pull/5324) |
| **严重** | ChromaDB 索引膨胀至 37G 导致崩溃 *(已修复)* | [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795) | **已合并** PR: [#5332](https://github.com/agentscope-ai/QwenPaw/pull/5332) |
| **中等** | 智谱 AI 模型级连接测试全部失败 | [#5330](https://github.com/agentscope-ai/QwenPaw/issues/5330) | 已有修复 PR: [#5339](https://github.com/agentscope-ai/QwenPaw/pull/5339) (审查中) |
| **中等** | 消息计数不匹配 (reasoning vs thinking 类型) | [#5208](https://github.com/agentscope-ai/QwenPaw/issues/5208) | 暂无直接修复，待协议层适配 |
| **低** | Console 通道显示 "Answers have stopped" *(已解决)* | [#5319](https://github.com/agentscope-ai/QwenPaw/issues/5319) | 重装后恢复，根因不明确 |
| **低** | Tauri 端找不到 Python 解释器 | [#5317](https://github.com/agentscope-ai/QwenPaw/issues/5317) | 社区支持讨论中 |

## 6. 功能请求与路线图信号

以下功能请求已有配套 PR，极有可能进入下一版本：
- **UI 易用性**：侧边栏折叠时切换 Agent ([#5329](https://github.com/agentscope-ai/QwenPaw/issues/5329) → [PR #5334](https://github.com/agentscope-ai/QwenPaw/pull/5334))；模型提供商列表自定义排序 ([#5267](https://github.com/agentscope-ai/QwenPaw/issues/5267) → [PR #5336](https://github.com/agentscope-ai/QwenPaw/pull/5336))。
- **桌面端增强**：关闭窗口到系统托盘 ([PR #5326](https://github.com/agentscope-ai/QwenPaw/pull/5326))。
- **通知系统**：Console 通道实时 SSE 推送与提示音 ([PR #5331](https://github.com/agentscope-ai/QwenPaw/pull/5331))。
- **Memory 增强**：Memory search 时效性权重排序 ([PR #5325](https://github.com/agentscope-ai/QwenPaw/pull/5325))。
- **任务规划**：完善 TodoWrite 工具，自动展开计划进度面板 ([PR #5323](https://github.com/agentscope-ai/QwenPaw/pull/5323))。

以下需求尚在初步讨论阶段：
- **智能体办公室互动**：用户建议在 Agent 管理页面直接开启对话 ([#5327](https://github.com/agentscope-ai/QwenPaw/issues/5327))，属于页面架构的较大改动，可能纳入中长期路线图。

## 7. 用户反馈摘要
- **稳定性焦虑**：“升级到 v1.1.12 后，我原来的图片全部都看不到了，发图片也只是显示发送成功”（[#5320](https://github.com/agentscope-ai/QwenPaw/issues/5320)）。版本升级带来的回归问题严重影响用户信任感。
- **交互中断**：“使用 DeepSeek 时，agent 经常在 thinking 的过程中卡死，需要手动点停止继续”（[#5328](https://github.com/agentscope-ai/QwenPaw/issues/5328)）。思考阶段不透明，缺乏进度或状态指示是核心痛点。
- **使用门槛**：“在 Tauri 下找不到 python 了...我写的 skill 都跑不了 python 脚本”（[#5317](https://github.com/agentscope-ai/QwenPaw/issues/5317)）。依赖环境维护对非技术用户仍是较大挑战。
- **积极性反馈**：用户对项目迭代速度表示认可，多个 Issue 提交后数小时内即获得维护者或贡献者响应（如 [#5320](https://github.com/agentscope-ai/QwenPaw/issues/5320) → [#5324](https://github.com/agentscope-ai/QwenPaw/pull/5324)）。社区协作氛围浓厚，如 [#5330](https://github.com/agentscope-ai/QwenPaw/issues/5330) 智谱问题引发了三个修复 PR 的集体攻关。

## 8. 待处理积压
- **Issue [#5328](https://github.com/agentscope-ai/QwenPaw/issues/5328)：DeepSeek 思考阶段卡死根本原因**。当前 [PR #5335](https://github.com/agentscope-ai/QwenPaw/pull/5335) 缓解了 UI 卡死，但 LLM 层面或 Agent 会话逻辑的卡死根因尚未完全定位，需维护者深入研究 DeepSeek 的 Stream 协议处理。
- **Issue [#5208](https://github.com/agentscope-ai/QwenPaw/issues/5208)：Reasoning Block 类型兼容**。该 Issue 讨论 `reasoning` 与 `thinking` 类型的差异，可能导致严格格式要求的模型调用失败。已有 6 条讨论但未有定论，建议在下一版本兼容性改进中优先考虑。
- **Issue [#5317](https://github.com/agentscope-ai/QwenPaw/issues/5317)：Tauri 环境依赖管理**。属于持续的运维体验问题，若无原生内置 Python 的方案，需提供更完善的环境检测与引导文档。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 ZeroClaw 项目 2026 年 6 月 20 日 GitHub 数据生成的零壳项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-20

## 1. 今日速览
在2026年6月20日的报告周期内，ZeroClaw 项目呈现出极高的社区活跃度与技术冲刺态势。24小时内共有 **28 个 Issue** 与 **50 个 Pull Request** 更新。重大功能里程碑（Discord完整交互组件）成功合入，但**严重的构建回归问题（Slack/Discord缺失）**与**安全级 Bug（Agent禁用失效）**引起了社区高度关注，暴露了当前发布质量管控与状态一致性测试的短板。值得注意的是，当前积压了 **47 个待合并 PR**，审查带宽可能成为短期瓶颈。围绕 v0.9.0（OIDC 认证安全架构）与 v0.8.3（MCP 仪表盘）的路线图工作正在同步推进。

## 2. 版本发布
过去24小时内无新版本发布。**（值得警惕：社区对 v0.8.0 预编译包缺失 Slack/Discord 功能的 Bug 反应强烈。）**

## 3. 项目进展
*   **重大功能合并**：
    *   **PR #7965** - `feat(channels/discord): interaction components` — 完成了 Discord 频道交互面的全面升级（按钮、选择菜单、弹窗、带按钮的审批流、自动补全）。这是追踪 Issue #7831（Discord 交互面）的里程碑式合并。
    *   **PR #7868** - `fix(tools/git_operations): include path + recovery hint` — 改进非 Git 目录下的报错信息，包含检查路径与恢复提示。
    *   **PR #7869** - `fix(fill-translations): clear orphaned continuation lines` — 修复翻译填充工具的数据丢失 Bug。
*   **长期 Bug 关闭**：
    *   **Issue #6651** — 矩阵（Matrix）频道因上游 `matrix-rust-sdk` Arc 循环引用导致的约 1MB Pss/次 的内存泄漏问题，在经历月余追踪后正式关闭。
*   **架构推进**：
    *   **Issue #5618** — 推动底层 DaemonSubsystems 重构，使用类型化 Registry API 替代回调函数。
    *   **Issue #6271** — V3 SwarmConfig Schema 定义与运行时实现完成。
*   **今日新特性提交（活跃信号）**：
    *   **PR #8033** (Chat-based onboard) / **#8038** (PATH auto-append) / **#8035** (Session ID for skill tools) 等高质量特性 PR 密集提交，表明社区贡献动力强劲。

## 4. 社区热点
*   **⭐ Issue #7787**：**v0.8.0 构建回归**。当前最热的用户反馈。用户明确指出 v0.8.0 预编译的二进制文件实际上是**不带 Slack 和 Discord 功能**的“残缺版”，回退到 v0.7.5 即刻恢复。此 Issue 有 6 条评论，强烈指向 CI 构建脚本在编译时遗漏了对应 feature flag。
    *   链接: [zeroclaw-labs/zeroclaw Issue #7787](https://github.com/zeroclaw-labs/zeroclaw/issues/7787)
*   **Issue #7141**：**OIDC 认证支持 RFC**。作为 v0.9.0 的核心安全特性，该 Issue 获得了 5 条评论，社区对可插拔认证架构的讨论十分专业且深入。
    *   链接: [zeroclaw-labs/zeroclaw Issue #7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)
*   **Issue #7950**：**Docker 镜像包含文档**。用户希望 Agent 能回答关于 ZeroClaw 自身配置的问题，体现了社区对 Agent“自我认知”与“自举”能力的需求。
    *   链接: [zeroclaw-labs/zeroclaw Issue #7950](https://github.com/zeroclaw-labs/zeroclaw/issues/7950)
*   **Issue #7911**：**Android Termux 支持受阻**。用户反馈在 Termux 上安装 ZeroClaw 时，架构检测脚本识别失败，显示为 `unknown linux aarch64`，表明分发脚本在非标准环境下的兼容性有待加强。

## 5. Bug 与稳定性
*   **严重 (S0 - 数据泄露/安全风险)**：
    *   **Issue #8013**：禁用 Agent 无法可靠停止其绑定的 **Discord 频道**。频道在 Agent 被禁用后仍然在线，存在严重安全风险。**目前无关联修复 PR**。
*   **高危 (S1 - 工作流阻塞)**：
    *   **Issue #7787**：v0.8.0 二进制缺失 Slack/Discord 频道。**非常需要紧急发布热修复补丁。**
    *   **Issue #7907 / #7941**：Agent 重命名/删除操作存在**状态持久化顺序倒置**的 Bug（先改状态后写配置），重启或崩溃后可能导致配置漂移。
*   **中危 (S2 - 功能降级/静默失败)**：
    *   **Issue #7964**：上下文压缩（`context_compression`）的 `summary_model` 配置在共享的运行时配置中，跨 Provider 调用时会产生静默失败。已有修复 PR #7973。
    *   **Issue #8039**：`fill-translations` 工具的修复脚本本身未能清理多行引用，产生**数据丢失**。

## 6. 功能请求与路线图信号
*   **v0.9.0 安全航道锁定**：
    *   **Issue #7141** (OIDC) 与追踪者 **Issue #7432** 表明围绕“认证 - 安全加固 - 破坏性变更”的架构重构已被明确纳入发布计划。
*   **v0.8.3 管理面增强**：
    *   **Issue #7320** 追踪的 MCP（模型上下文协议）仪表盘及 Web/插件管理界面正在稳步推进。
*   **用户强烈诉求**：
    *   **Issue #7952**：发布包含全通道功能的预编译包，从根源解决 #7787 的问题。
    *   **Issue #7929**：统一各端（Web, TUI, Channel）的斜杠命令注册表，避免功能分裂。
    *   **Issue #7996**：为低端存储设备增加可配置的临时文件清理策略。
*   **创新功能孵化**：
    *   **Issue #8034**：提出用“对话式向导”替代废弃的初始化脚本，降低新用户配置门槛。

## 7. 用户反馈摘要
*   **对发布质量的失望**：“I dunno what I'd be without downgrading to the v0.7.5 prebuilt binary restores Slack support” —— Issue #7787 用户对 v0.8.0 正式发布版竟然缺失基础功能表示困惑与失望，强调回归测试的重要性。
*   **对安全边界的担忧**：“disabling an agent does not reliably stop its bound Discord channel from staying online and answering users” —— Issue #8013 用户直接指出了状态管理缺陷可能导致的严重安全后果。
*   **对自举能力的期待**：“ZeroClaw agents often seem unable to answer questions about ZeroClaw features” —— Issue #7950 用户希望 Agent 不仅服务外部，也能解答自身配置，达到真正的“闭环”体验。
*   **对边缘平台兼容性的试探**：“both attempting to install the precompiled binary and compiling on the local device result in the unknown linux aarch64 binary” —— Issue #7911 用户在移动环境（Termux）的尝试受阻，反映出二进制分发脚本对不同 AArch64 环境的检测存在硬编码问题。

## 8. 待处理积压
*   **核心特性-记忆系统阻塞**：
    *   **PR #6693** (Dream Mode 基础PR，自5月16日开启) 与堆叠于此的 **PR #7797** (Per-Agent Dream Mode) 均处于 **needs-author-action** 状态。此特性的长期积压将影响整个 v0.8.x 周期关于“记忆”与“长期上下文”的路线图规划。
*   **配置持久化修复停滞**：
    *   **PR #7973** (修复 Issue #7964 的上下文压缩 Provider 问题) 提交后迅速被打上 `needs-author-action` 标签，作者未及时响应，导致一个 S2 级别的 Bug 悬空。
*   **审查积压预警**：目前有 47 个待合并 PR。社区贡献的轻量级功能增强（如 Wecom/QQ/Telegram 频道的小优化，PRs #8024-#8027）正在排队等待核心维护者的审查，可能影响社区贡献者的积极性。
*   **依赖阻塞**：
    *   **Issue #8012** (技术债务清理-移除旧日志游标) 依赖的 PR #7921 尚未合并，处于 `blocked` 状态。
    *   **Issue #7911** (Termux 支持) 依赖 PR #7916，同样处于 `blocked` 状态。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*