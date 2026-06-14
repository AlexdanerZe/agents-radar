# OpenClaw 生态日报 2026-06-14

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-14 03:41 UTC

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

# OpenClaw 项目动态日报 | 2026-06-14

## 1. 今日速览

今日项目状态为 **高活跃度运行**，24小时内共更新500条Issue与500条PR，并连续发布了两个Beta版本。整体呈现“双速发展”特征：一方面，**严重稳定性问题并发**（P0级内存泄露导致OOM、结构性安全漏洞频出）对生产环境构成明确风险；另一方面，**维护机制趋于成熟**——`@openclaw-clownfish[bot]` 自动修复了多个长期搁置的PR，展现了良好的工程化自愈能力。社区关注焦点集中在**子Agent可靠性**、**渠道安全性**和**跨平台行为一致性**三大方向。

**综合健康度评估：⚠️ 高活跃 / 高压力**。修复速度虽在不断加快，但Bug输入量仍显著高于输出量，尤其是安全类积压问题值得警惕。

---

## 2. 版本发布

### v2026.6.8-beta.1
- **核心增强**：Telegram 渠道全面支持结构化富文本（表格、列表、可展开引用块）；WhatsApp 渠道投递健壮性提升。
- **CLI 后端**：实现了保留Prompt的CLI后端投递模式。
- **清理动作**：废弃了原生草稿迁移机制，并强化了富媒体边界安全。

### v2026.6.7-beta.1
- **渠道统一**：Slack渠道的会话最终回复在Transcript中得到稳定保存；优化了Telegram可展开引用块。
- **媒体响应**：顶级 `image` 消息工具可正常发送附件媒体；静默回复和分页操作结果得到修复。

> **说明**：两版均为Beta，未标注显式的 Breaking Changes。建议用户按 `2026.6.7 → 2026.6.8` 的顺序升级。

---

## 3. 项目进展

### ✅ 今日合并/关闭的重要 PR

| PR | 内容  | 状态信号 |
|---|---|---|
| [#92855](https://github.com/openclaw/openclaw/pull/92855) | 修复 iOS Safari 聊天布局与输入缩放（Clownfish 翻新） | ✅ 已合并 |
| [#92854](https://github.com/openclaw/openclaw/pull/92854) | Slug 生成器拒绝错误 Payload（Clownfish 翻新） | ✅ 已合并 |
| [#92853](https://github.com/openclaw/openclaw/pull/92853) | ACP 服务器接受 MCP 日期式 `protocolVersion` | ✅ 已合并 |
| [#92850](https://github.com/openclaw/openclaw/pull/92850) | `memory-core` 重置 `lastMetaSerialized` 确保 `__meta` 写入 | ✅ 已合并 |
| [#92045](https://github.com/openclaw/openclaw/pull/92045) | 增加 `diagnostics-otel` 插件能力合约测试 | ✅ 已合并 |

### 🔄 当前推进中的关键 PR

- [#92852](https://github.com/openclaw/openclaw/pull/92852)：`[gateway]` 配置热加载在 inotify 耗尽时回退到轮询模式 **（“ready for maintainer look”）**
- [#73958](https://github.com/openclaw/openclaw/pull/73958)：`[feishu]` 彻底修复飞书群话题路由（`root_id` vs `thread_id` 语义分离）
- [#89055](https://github.com/openclaw/openclaw/pull/89055)：修复隔离 Cron 设置超时后无法自动重启的问题
- [#90305](https://github.com/openclaw/openclaw/pull/90305)：Gateway 在执行监督重启时保留 `drain` 状态

**整体迈进步伐**：修复与优化正从“单点修补”转向“系统性覆盖”，而 **Clownfish Bot 对陈旧 PR 的集中翻新是今日最大亮点**——四个已停滞数周甚至数月的PR在同一天被翻新合并，有效降低了技术债。

---

## 4. 社区热点

### 讨论最热的 Issue

| Issue | 评论 | 核心矛盾 |
|---|---|---|
| [#48183](https://github.com/openclaw/openclaw/issues/48183) **飞书内存泄露** | 19 | 停止 Monitor 时 httpServers Map 未及时清理 | 
| [#44925](https://github.com/openclaw/openclaw/issues/44925) **子Agent静默丢失** | 19 | 完成通知失败（E31/E42/E45）后无重试/无通知 |
| [#48788](https://github.com/openclaw/openclaw/issues/48788) **统一文件名编码方案** | 18 | 社区推动架构级解决方案而非单点修补 |
| [#45740](https://github.com/openclaw/openclaw/issues/45740) **gh-issues注入漏洞** | 13 | Issue Body 直接注入 SubAgent Prompt |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) **Steer模式不工作** | 12 | 排队消息无法在当前轮次中注入 |

### 最受期待的 Feature

| Issue | 👍 | 诉求 |
|---|---|---|
| [#42840](https://github.com/openclaw/openclaw/issues/42840) **MathJax/LaTeX 支持** | 6 | 控制台需要渲染数学公式（学术场景信号） |
| [#45608](https://github.com/openclaw/openclaw/issues/45608) **系统重置前自动冲刷记忆** | 4 | `/new` 和每日重置前应执行与 Compaction 相同的记忆冲刷 |
| [#43015](https://github.com/openclaw/openclaw/issues/43015) **`message.send` 模式暴露过多字段** | 3 | GPT 模型会自动填充导致校验失败 |

**分析与洞察**：社区正在将 OpenClaw 定位为 **关键任务基础设施**。用户不仅关心“能不能用”，更关心“出错了怎么恢复”、“丢失了知不知道”。Steer 模式不能工作（Issue #48003）之所以热度高，是因为它在本质上破坏了用户对“实时交互”的信心。

---

## 5. Bug 与稳定性

### 🔴 P0（紧急——需要立即关注）

| Issue | 简述 | 修复状态 |
|---|---|---|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | **Gateway 内存泄露**：RSS 从 350MB 涨至 15.5GB，2-3天内反复 OOM Kill | 🔴 **无修复PR**。这是当前最严重的问题 |

### 🟠 P1（高优先——多数已有分析）

| 类别 | Issue | 简述 | 修复状态 |
|---|---|---|---|
| **安全** | [#45740](https://github.com/openclaw/openclaw/issues/45740) | `gh-issues` 技能注入攻击 | 待安全审查 |
| **安全** | [#44905](https://github.com/openclaw/openclaw/issues/44905) | Discord 泄露 `NO_REPLY`、`to=functions` 等内部追踪 | 待安全审查 |
| **安全** | [#46786](https://github.com/openclaw/openclaw/issues/46786) | `tools.elevated.enabled: true` 导致 Exec 全部路由到网关 | 待审查 |
| **行为** | [#44925](https://github.com/openclaw/openclaw/issues/44925) | 子Agent 完成后静默丢失 | 已定位，无修复PR |
| **行为** | [#48003](https://github.com/openclaw/openclaw/issues/48003) | Steer 模式无法注入当前轮次 | 已定位（`KeyedAsyncQueue` 引入） |
| **渠道** | [#90093](https://github.com/openclaw/openclaw/issues/90093) | `openai-chatgpt-responses` 首轮成功，下一轮 `400 error` | 调查中 |
| **回归** | [#38327](https://github.com/openclaw/openclaw/issues/38327) | `google-vertex/gemini-3.1-pro-preview` “Cannot convert undefined or null to object” | **停滞超100天** |
| **性能** | [#86996](https://github.com/openclaw/openclaw/issues/86996) | Active Memory + Codex 导致大幅延迟和启动中止 | 待产品决策 |

### 🟡 P2（中等——值得跟进）

- [#48788](https://github.com/openclaw/openclaw/issues/48788) 多编码文件名问题（社区推动统一架构）
- [#44993](https://github.com/openclaw/openclaw/issues/44993) Cron/Heartbeat 时间戳不刷新（回归）
- [#45765](https://github.com/openclaw/openclaw/issues/45765) `OPENCLAW_HOME` 导致目录嵌套（回归）

---

## 6. 功能请求与路线图信号

### 高概率纳入下轮迭代

| 功能要求 | 判断依据 |
|---|---|
| [#45608](https://github.com/openclaw/openclaw/issues/45608) **自动记忆冲刷** | 已有 Compaction 冲刷逻辑，扩展成本低，点赞数高（4👍） |
| [#42475](https://github.com/openclaw/openclaw/issues/42475) **Agent 级成本预算** | 运维刚需，技术可行性高（网关层拦截） |
| [#48788](https://github.com/openclaw/openclaw/issues/48788) **集中化文件名编码工具** | PR #48578 已解决 UTF-8 场景，社区要求统一架构 |

### 值得关注的社区呼声

- [#42840](https://github.com/openclaw/openclaw/issues/42840) **LaTeX/MathJax 支持**：6个👍，今日最高，表明学术/科学应用场景正在扩大。
- [#7707](https://github.com/openclaw/openclaw/issues/7707) **内存信任标签**：防止 Web 爬取/第三方技能造成记忆投毒攻击，具有前瞻性。
- [#48874](https://github.com/openclaw/openclaw/issues/48874) **多会话架构 RFC**：共享LLM + 隔离会话 + 公共知识库，架构级升级方向。

---

## 7. 用户反馈摘要

### 满意度信号

- **高质量的 Bug 报告**：大量 Issue 包含完整的复现步骤、环境信息甚至根因分析（如 #44925 提供了 E31/E42/E45 三种失败模式），反映出**用户群体高度技术化且深度投入**。
- **功能参与积极**：#45608（记忆冲刷）和 #42840（LaTeX）等 Feature 的点赞数表明用户愿意投票驱动路线图。

### 主要痛点

- 🚨 **“多Agent编排不靠谱”**（#43367）：“并发添加 Agent 配置被覆盖、子会话锁失败”——这是用户对生产环境稳定性抱怨最强烈的领域。
- 🚨 **“记忆管理太混乱”**（#43747）：“我同事和我三人的 Claw 存储方式完全不同，一个用 SQLite，一个用文件”。跨用户一致性体验出现裂痕。
- 🚨 **“Cron 作业不可靠”**（#40001）：`write` 工具无追加模式导致多 Session 共享工作区文件被静默覆盖。“Isolated cron sessions destroy shared files”。
- 🚨 **“开启某些扩展后系统变慢”**（#86996）：Active Memory + Codex 的组合下，简单 Telegram 消息也出现不可接受的延迟。

### 使用场景画像

> 用户正在将 OpenClaw 部署为 **自动化中枢**：并行编码、跨平台（飞书/Telegram/Discord）群聊、定时记忆归档、浏览器自动化。社区的沉默用户可能更多，而活跃的 Bug 报告者是 OpenClaw 最核心的“深水区用户”。

---

## 8. 待处理积压

### 🆘 长期未响应且影响重大的 Issue（建议维护者优先关注）

| Issue | 时间 | 当前阻塞点 |
|---|---|---|
| [#38327](https://github.com/openclaw/openclaw/issues/38327) **Gemini 回归崩溃** | **2026-03-06**（停滞100天+） | `needs-maintainer-review` + `needs-product-decision` |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) **内存信任标签** | 2026-02-03 | `needs-maintainer-review` + `needs-product-decision` |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) **Write 工具追加模式** | 2026-03-08 | `needs-product-decision`（已有关联 PR） |
| [#42475](https://github.com/openclaw/openclaw/issues/42475) **Agent 成本预算** | 2026-03-10 | `needs-maintainer-review` + `needs-product-decision` |

### 🔒 安全类积压

- [#45740](https://github.com/openclaw/openclaw/issues/45740) Prompt 注入
- [#44905](https://github.com/openclaw/openclaw/issues/44905) Discord 内部信息泄露
- [#46786](https://github.com/openclaw/openclaw/issues/46786) Exec 路由绕过

### 🤖 正面信号：Clownfish Bot 的批量翻新

今日 **四个** 被 Clownfish 翻新的旧 PR 成功合并（#92855 / #92854 / #92853 / #92849）。这是一个极好的趋势——项目方正在通过自动化手段系统性地清理“等待作者响应”状态的积压贡献，建议社区关注这一模式能否持续扩展。

---

*报告生成于 2026-06-14，数据来源于 OpenClaw 公开 GitHub 仓库 [github.com/openclaw/openclaw](https://github.com/openclaw/openclaw)。*

---

## 横向生态对比

# 个人AI助手与自主智能体开源生态横向对比报告
**报告日期**：2026-06-14 ｜ **数据源**：各项目GitHub 24小时公开动态

---

## 1. 生态全景

当前个人AI助手开源生态处于**爆发式增长与基础设施摇摆并存的阶段**。头部项目（OpenClaw、Hermes Agent、ZeroClaw、IronClaw）日均处理数十乃至数百条Issue/PR，用户群体高度技术化，但也暴露出内存泄漏、静默失败、配置混乱等生产环境关键问题。多项目不约而同地将**记忆持久化**、**多Agent编排可靠性**和**跨平台渠道一致性**作为核心攻坚方向。同时，以MCP协议标准化、OAuth流程兼容、本地模型支持为代表的外部集成能力正成为社区诉求的“第二引擎”。整体呈现“功能快速扩展，但稳定性仍滞后于用户预期”的特征。

---

## 2. 各项目活跃度对比

| 项目 | Issues动态（新开/更新） | PR动态（新开/更新） | 合并/关闭PR | 版本发布 | 健康度评估 |
|------|------------------------|---------------------|-------------|----------|-----------|
| **OpenClaw** | 500条更新 | 500条更新 | 5个合并 | 2个Beta（v2026.6.7、v2026.6.8） | ⚠️ 高活跃/高压力 |
| **Hermes Agent** | 50条更新（2关闭） | 50条更新（2合并/关闭） | 2个合并 | 无 | ⚠️ 活跃，但合并滞后 |
| **ZeroClaw** | 42条更新（26新开，16关闭） | 50条更新（45待合并，5合并） | 5个合并 | 无 | ✅ 极高活跃，响应积极 |
| **IronClaw** | 未单独统计（24条PR动态） | 24条PR动态 | 7个合并 | 无 | ✅ 极高活跃，架构迭代 |
| **NanoBot** | 未提供精确数字 | 18个PR（13开启，5合并） | 5个合并 | 无 | ✅ 极高活跃，研发密集 |
| **NanoClaw** | 1条（已关闭误操作） | 6个PR（4合并，2待合并） | 4个合并 | 无 | ✅ 高活跃，正向并行 |
| **CoPaw（QwenPaw）** | 8条 | 8个PR | 1个合并 | 无 | ✅ 较高活跃，外部贡献亮眼 |
| **PicoClaw** | 未提供精确数字 | 5个PR合并 | 5个合并 | `nightly v0.2.9-nightly` | ✅ 中等偏上，稳定性推进 |
| **NullClaw** | 1个活跃Bug | 1个修复PR（#954） | 0合并 | 无 | ⚠️ 中等，核心功能亮黄灯 |
| **Moltis** | 1个Bug报告（#1119） | 3个PR（均待合并） | 0合并 | 无 | ✅ 活跃，快速响应 |
| **LobsterAI** | 0新（4个旧Issue被标记Stale） | 2个PR合并 | 2个合并 | 无 | ⚠️ 低活跃维护期，积压严重 |
| **TinyClaw** | 无活动 | 无活动 | — | — | 💤 休眠 |
| **ZeptoClaw** | 无活动 | 无活动 | — | — | 💤 休眠 |

> **说明**：OpenClaw与Hermes Agent的“500/50”为总更新数（含评论、标签变更等）；部分项目未独立统计Issue数，以“—”标记。健康度评估基于日报原文与数据推断。

---

## 3. OpenClaw在生态中的定位

OpenClaw 是该生态**用户规模最大、功能覆盖最全的核心参照项目**。其日均500+ Issue/PR的流量远超同类（第二名Hermes Agent约为50），社区从“能不能用”转向“出错了怎么恢复”的生产环境要求，具备最高的成熟度期待。

**核心优势**：
- **渠道广度**：Telegram、Slack、WhatsApp、Discord、飞书等全渠道支持，并持续改进富文本与跨平台一致性；
- **工程自愈能力**：`@openclaw-clownfish[bot]` 自动翻新停滞PR，一天内合并4个长期积压，展现了自动化运维资产；
- **生态沉淀最深**：CLI后端、Gateway内存管理、MCP、ACP等基础设施完善，适合作为企业级部署基线。

**技术路线差异**：
- 相较ZeroClaw的“Dream Mode（记忆反思）”与IronClaw的“附件文本抽取管线”，OpenClaw更强调**渠道安全性与多Agent编排的稳健性**，而非激进的新能力注入；
- 其子Agent可靠性（E31/E42/E45失败模式）、Steer模式不能工作等实际痛点，反映了项目在复杂交互场景下面临的**后摩尔定律式稳定性挑战**。

**社区规模对比**：OpenClaw Issue/PR数量级是其余各项目的5~10倍，但Bug输入量大于输出量，安全类积压堆积明显，整体属于“高活跃高负债”状态。

---

## 4. 共同关注的技术方向

### ① 子Agent/多Agent编排可靠性
- **OpenClaw** #44925 子Agent静默丢失（E31/E42/E45无重试）
- **Hermes Agent** #31155 `delegation.model`被忽略
- **CoPaw** #5172 对话挂起导致Agent死亡
- **ZeroClaw** MCP工具权限/委托风险配置
- **NanoBot** PR #4291 子代理模型可配置探索

### ② 记忆管理与长期一致性
- **OpenClaw** #45608 系统重置前自动冲刷记忆
- **NanoBot** #4326 idleCompact压缩修复
- **Hermes Agent** #10771 Auto Dream自动记忆整合
- **ZeroClaw** #5849 Dream Mode（5阶段引擎）
- **PicoClaw** #3012 Evolution模式token持续消耗（隐含记忆循环）

### ③ 跨平台消息渠道兼容与新平台适配
- **Telegram 10.1富消息**：Hermes (#44428)、OpenClaw（已发布支持）
- **中国渠道**：ZeroClaw (#7531 流式卡片)、CoPaw (#5168 Zalo)
- **WhatsApp**：Hermes (#45935 消息模板)、ZeroClaw (#7518 消息反应)
- **Web UI缺失/退化**：Hermes (#501 Web UI)、ZeroClaw (#7523 Dashboard空白)

### ④ 配置易用性与环境变量处理
- **NanoBot** (#4323/#4324/#4325) 环境变量未解析导致静默失败
- **Hermes Agent** (#44666/#43586) `api_key_env`/`key_env`混淆
- **OpenClaw** #48788 统一文件名编码方案
- **ZeroClaw** #7591 无效alias无验证导致用户输入丢失

### ⑤ 安全与注入防御
- **OpenClaw** #45740 gh-issues注入、#44905 Discord内部泄露、#46786 Exec路由绕过
- **NanoBot** #4098 exec符号链接逃逸修复
- **Hermes Agent** #45681 SSL损坏检测、#21774 Google Workspace OAuth加固
- **IronClaw** Slack重新审批循环（身份泄露风险）

### ⑥ 可观测性与调试能力
- **OpenClaw** #92045 diagnostics-otel测试
- **ZeroClaw** #7570 OTel GenAI spans（记录prompt/completion）
- **IronClaw** #4836 运行时上下文感知（让模型知道当前渠道）
- **NullClaw** 严重日志缺失（失败任务标记为成功）

### ⑦ 本地模型与API兼容性
- **NanoBot** #193 Ollama支持（长期诉求）
- **Hermes Agent** #45813 GitHub Copilot provider 400错误
- **Moltis** #1119 MCP OAuth兼容（Notion/Linear）
- **CoPaw** #5156 Kimi-for-Coding / uv白名单
- **ZeroClaw** #7539 llama.cpp快速模型切换

---

## 5. 差异化定位分析

| 维度 | OpenClaw | ZeroClaw | Hermes Agent | IronClaw | NanoBot | PicoClaw | CoPaw | NullClaw | Moltis | LobsterAI |
|------|----------|----------|--------------|----------|---------|----------|-------|----------|--------|-----------|
| **功能侧重** | 全渠道Agent网关 | 长期记忆+插件化 | 多IM集成+社区Mega PR | 企业Slack+附件管线 | CLI/TUI优先+配置重构 | 多模型路由+图像压缩 | 中文IM+跨平台Hub | 定时任务可靠性 | MCP集成标准化 | CoWork+技能系统 |
| **目标用户** | 企业/运维/重度自动化 | 开发者/记忆力强依赖 | Telegram高频/尝鲜者 | Slack企业团队 | 本地模型/开发者 | 资源敏感/嵌入式 | 东南亚/中国IM用户 | 自动化工作流用户 | MCP服务生态用户 | 团队协作（停滞） |
| **技术架构** | Golang? 多语言混合 | Rust? Agent引擎统一 | Rust+OpenTUI | Rust（独立crate） | Python（FastAPI?) | Go? | Python（Tauri桌面） | Go? | Rust? | Python |
| **迭代阶段** | 功能扩展+安全修补 | 能力跃迁（Dream/Obs） | 社区贡献堆积→整合 | 深度重构（附件/提取） | 底层重构+WebUI加速 | 稳定性+国际化 | 亚洲支付/IM适配 | 核心Bug攻坚 | OAuth兼容性 | 濒临停滞 |

注：部分项目语言为推断，以实际仓库为准。

**关键差异**：
- **OpenClaw** vs **ZeroClaw**：前者稳守渠道与安全，后者押注长期记忆与可观测性，是“运维第一”与“智能第一”的路线分化。
- **Hermes Agent**：社区开放度最高，86个PR集成Mega bundle；但维护者合并速度慢，依赖社区自愈。
- **IronClaw**：最具“企业产品感”，附件文本抽取独立crate、Slack审批循环修复系列，工程严谨度高。
- **NanoBot**：更贴近“开发者个人助手”，TUI、WebUI、子代理可配置，轻灵但缺少大型部署案例。
- **CoPaw**：唯一明确瞄准越南/中文渠道的项目，但核心对话挂起Bug成为致命伤。

---

## 6. 社区热度与成熟度分层

### 第一梯队：极高活跃（日均Issue/PR >40 或 PR合并 >5）
- **OpenClaw**：社区规模最大，但压力最高；**快速迭代+安全修补并行的双速模式**
- **Hermes Agent**：Issue/PR数量大，合并率极低（2/50），**“提交海啸”与“审查瓶颈”矛盾突出**
- **ZeroClaw**：合并5个PR，同时清理16个Issue；**功能扩张与积压清理同步**
- **IronClaw**：7个PR合并，Epic管线合龙；**架构重构驱动，处于质量巩固前夜**

### 第二梯队：高活跃（日均10~40条动态）
- **NanoBot**：18个PR提交5个合并；**底层重构期（配置/执行环境/WebUI）**
- **NanoClaw**：4个PR合并，Provider能力跃迁；**小步快跑，功能性交付**
- **CoPaw**：8+8动态，1个PR合并（国际化）；**外部贡献活跃，核心待稳定**

### 第三梯队：中等活跃
- **PicoClaw**：5个PR合并，Nightly发布；**稳定性与多模型兼容稳步推进**
- **NullClaw**：1个关键修复PR提交；**处于“单点突破”状态**
- **Moltis**：1个Bug + 3个PR，修复OAuth并发；**响应快但规模小**

### 第四梯队：低活跃/休眠
- **LobsterAI**：0新Issue/PR，Stale Bot批量标记；**已陷入维护停滞**
- **TinyClaw / ZeptoClaw**：连续24小时无活动；**无开发信号**

---

## 7. 值得关注的趋势信号

### ① 学术/教育场景驱动功能需求
- OpenClaw #42840（MathJax/LaTeX）获得当日最多6个👍；Hermes Agent Telegram 10.1富消息同样包含LaTeX渲染。
- **信号**：个人AI助手正从“编程辅助”向“科研论文/教育场景”渗透，公式渲染、图表支持成为下一个必备特性。

### ② 本地模型部署需求持续升温
- NanoBot #193（Ollama）长踞热门；ZeroClaw #7539（llama.cpp切换）；Hermes Agent #45813（Custom provider）。
- **信号**：用户对成本、隐私、离线可用性敏感，项目必须在OpenAI兼容API之外提供对本地推理的**一等公民支持**。

### ③ 多Agent编排的“信任危机”
- OpenClaw #43367（“多Agent编排不靠谱”）、CoPaw #5172（“聊天一直等待”）、NullClaw #941（“Agent定时任务静默失败”）。
- **信号**：多Agent/子Agent的可靠性已成为影响生产力信心的核心瓶颈，而非功能丰富度。行业需要**事务性保证、可观测的重试/补偿机制**。

### ④ 记忆管理从“存储”走向“智能巩固”
- ZeroClaw的Dream Mode（5阶段引擎）、Hermes Agent的Auto Dream、OpenClaw的冲刷提议。
- **信号**：单纯的记忆存取已不满足用户，项目正在探索**LLM辅助的去重、压缩、反思**，使记忆具备自主维护能力。

### ⑤ 渠道安全与权限治理成为必备基础设施
- OpenClaw三件安全漏洞（注入、泄露、绕过）；Hermes OAuth修复；NanoBot exec符号链接逃逸；IronClaw Slack审批循环。
- **信号**：安全不再是“加分项”，而是生产部署的前提。社区期待统一的权限分层（工具级、渠道级、模型级）、深度防御机制。

### ⑥ MCP协议标准化进入“互操作性攻坚期”
- Moltis #1119（WWW-Authenticate兼容）、ZeroClaw #6876（MCP工具权限）、OpenClaw #92853（MCP日期式protocolVersion）。
- **信号**：MCP成为事实上插件标准，但不同实现间的OAuth、能力声明、资源元数据解析存在碎片化。**下一次爆发将取决于各项目对MCP规范的精确兼容。**

### ⑦ 跨项目代码与基础设施复用趋势浮现
- OpenClaw的Clownfish Bot自动化翻新、IronClaw将提取逻辑抽离为独立crate、NanoClaw引入Provider能力注册表。
- **信号**：头部项目开始进行**模块化拆解与平台化思维**，这为衍生项目（如PicoClaw基于OpenClaw？）提供了复用基础，生态分化的速度可能加快。

---

**总结**：个人AI助手开源生态正处于“能力大爆炸”与“稳定性焦虑”并行的窗口期。对技术决策者而言，选择**OpenClaw**意味着更成熟的渠道网络与更高的运维门槛，**ZeroClaw**代表更先进的记忆架构但仍在早期，**IronClaw**则在企业级工程质量上领先。最核心的建议是：**在拥抱功能创新的同时，优先投资于可观测性、事务性补偿与安全治理——这三者将决定谁能从“有趣的原型”进化为“可信的基础设施”。**

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，根据您提供的 HKUDS/nanobot GitHub 项目数据，我为您生成了**2026年6月14日**的 NanoBot 项目动态日报。

---

### NanoBot 项目动态日报 | 2026年6月14日

#### 1. 今日速览

今日项目活跃度**极高**，尤其是在代码贡献方面。过去24小时内，项目经历了 18 个 Pull Requests (PRs) 的密集处理，其中大部分 (13个) 仍处于开启/待合并状态，表明核心开发者正在进行大规模的功能开发和重构工作。Bug 修复和功能请求在社区中讨论热烈，焦点集中在**API兼容性**、**环境变量处理**和**WebUI体验优化**上。尽管合并率有待提升，但整体项目健康度良好，维护者响应积极。

#### 2. 版本发布

（无）

---

#### 3. 项目进展

今日有5个PR被成功合并或关闭，涵盖了代码重构、关键Bug修复和功能增强，显示了项目在稳定性与基础设施方面的稳步前进。核心进展如下：

-   **打破工具配置导入循环**：**PR #4314** 成功合并，通过引入 `nanobot.config_base` 模块，解决了工具配置中的循环依赖问题。这是一个重要的底层重构，为未来添加更多工具类型扫清了障碍，提升了代码的可维护性。
-   **修复内存压缩Bug**：**PR #4326** 修复了 `idleCompact` 功能的一个关键逻辑错误。该Bug导致在对话压缩时，模型纠正错误的正确结论可能被忽略，现在压缩算法会利用完整的会话历史，显著提升了长期对话的记忆准确性。
-   **优化WebUI启动性能**：**PR #4327** 解决了 WebUI 启动时因网关路由缓慢导致的阻塞问题。通过将耗时操作异步化，并优化侧边栏的会话读取逻辑，大幅提升了用户首次加载界面的体验。
-   **增强配置与界面一致性**：**PR #4313** 为WebUI设置面板新增了温度参数、工具限制、Dream功能等多个与 `config.json` 对应的写入接口，显著缩小了界面配置与直接修改配置文件之间的功能差距，提升了用户体验。
-   **修复执行环境安全性**：**PR #4098** 成功关闭，解决了执行工作区的符号链接逃逸漏洞，并修正了 `pathAppend` 的路径优先级问题，增强了 `exec` 工具的安全性。

**项目动态**: 代码库正经历高频次的更新与重构，基础架构（如配置系统）和安全性得到加强，WebUI功能快速迭代，研发效率较高。

---

#### 4. 社区热点

今日社区讨论焦点明确，技术讨论深入：

-   **新TUI交互界面的巨大反响**：**PR #4329** 提出为 `nanobot agent` 添加一个全新的内联交互式 TUI，替代现有的 Rich-Live 循环。该PR改动量大，新增了命令面板、多模态输入等丰富功能，评论区和社区关注度极高。这反映出用户对更现代、更高效命令行交互方式的强烈渴望。
    -   [PR #4329: Nanobot TUI](https://github.com/HKUDS/nanobot/pull/4329)

-   **Ollama API 支持呼声已久**：**Issue #193** 虽然早已关闭，但积累了15条评论，是历史讨论热点。用户迫切希望 NanoBot 除了支持 vLLM 外，也能支持 Ollama 等更轻量、更流行的本地推理方案，这代表了社区对部署便捷性和多样性的核心诉求。
    -   [Issue #193: Ollama api support?](https://github.com/HKUDS/nanobot/issues/193)

-   **Anthropic API兼容性问题引发关注**：**Issue #4333** 报告了一个直接影响用户使用的问题：项目向较新的 `claude-opus-4-8` 模型发送了已废弃的 `temperature` 参数。由于这会导致API直接返回400错误，引起了受影响的用户高度关注。随后立刻有修复PR提交，体现了社区快速响应和协作的能力。
    -   [Issue #4333: Anthropic provider sends deprecated temperature to opus-4-8](https://github.com/HKUDS/nanobot/issues/4333)

---

#### 5. Bug 与稳定性

今日报告的Bug主要集中在API兼容性和配置处理上，严重程度不一，但都有相应的修复PR跟进。

-   **高严重性：API请求被拒 (400错误)**
    -   **现象**：向 `claude-opus-4-8` 及 Fable 模型发送请求时，因携带了已废弃的 `temperature` 参数而失败。
    -   **状态**：已报告，**已有修复PR (#4334)**。
    -   [Issue #4333](https://github.com/HKUDS/nanobot/issues/4333)  | [PR #4334](https://github.com/HKUDS/nanobot/pull/4334)

-   **高严重性：MCP Server崩溃**
    -   **现象**：当 `streamableHttp` 类型的 MCP server 会话终止并重连时，进程会因为 `asyncio` 任务作用域错误而崩溃。
    -   **状态**：已报告，**已有修复PR (#4303)**。
    -   [PR #4303](https://github.com/HKUDS/nanobot/pull/4303)

-   **中严重性：合并代码导致启动崩溃**
    -   **现象**：合并分支后，因 `session_key` 变量未定义，导致 Agent 在启动时直接崩溃（NameError）。
    -   **状态**：已报告，待解决。 [Issue #4322](https://github.com/HKUDS/nanobot/issues/4322)

-   **中严重性：环境变量未解析导致的静默失败**
    -   **现象**：在**转录配置** (`#4323`) 和 **WebUI设置读写** (`#4325`, `#4324`) 等多个代码路径中，`load_config()` 返回的包含 `${VAR}` 格式的环境变量未被解析，导致API密钥无法被识别，进而使功能静默失败。这影响面较广，可能影响所有依赖环境变量配置的用户。
    -   **状态**：已报告，**每个问题均有修复PR**。 [PR #4323](https://github.com/HKUDS/nanobot/pull/4323)，[PR #4325](https://github.com/HKUDS/nanobot/pull/4325)，[PR #4324](https://github.com/HKUDS/nanobot/pull/4324)

---

#### 6. 功能请求与路线图信号

今日社区提出的功能请求指向性明确，部分已进入开发阶段：

-   **更细粒度的工具控制**：**PR #4138** 希望为内置的文件系统工具组添加 `enable` 开关，与现有的 `exec`、`web` 工具组保持一致。这反映了用户希望在**安全沙箱**场景下，精确控制模型工具使用权限的需求，极可能被纳入后续版本。
    -   [PR #4138: Add tools.file.enable to toggle built-in filesystem tools](https://github.com/HKUDS/nanobot/pull/4138)

-   **子代理模型可配置**：**PR #4291** 允许子代理使用与父代理不同的模型预设。这标志着用户对**复杂多Agent协作**场景的探索，希望通过更智能的模型调度来平衡成本与性能。预计将成为 Agent 功能的下一个重要扩展点。
    -   [PR #4291: feat(spawn): allow subagents to use configurable model presets](https://github.com/HKUDS/nanobot/pull/4291)

-   **WebUI自动化管理**：**PR #4330** 提出为 WebUI 增加对“自动化”功能的管理界面，包括列出、过滤、暂停/恢复和删除自动化任务。这表明项目在**从“会话工具”向“平台”演进**的路线图上又迈进了一步，将高级功能可视化管理。
    -   [PR #4330: feat(webui): add automation management view](https://github.com/HKUDS/nanobot/pull/4330)

-   **反向代理支持**：**PR #4328** 旨在解决 WebUI 在反向代理或子路径下部署时，资源路径和API请求错误的问题。这是**企业级部署**的必要功能，表明项目正在吸引更多需要定制化部署环境的用户。
    -   [PR #4328: webui: serve correctly under a path prefix](https://github.com/HKUDS/nanobot/pull/4328)

---

#### 7. 用户反馈摘要

-   **集成广度**：从社区对 `#193` (Ollama) 的长期关注和对 `#4333` (Anthropic新版API) 的迅速反应看，用户对 **接入更多、更新的大模型后端** 有着持续的、强烈的需求。任何API兼容性问题都会立刻影响用户体验。
-   **控制权与透明度**：`#4083` (路径优先级) 和 `#4138` (文件工具开关) 等议题凸显了用户对 **更精细控制** 的渴望，尤其是在安全相关的执行环境和权限管理上。用户希望工具行为是可预测和可配置的。
-   **数据完整性**：`#4264` (idleCompact Bug) 的投诉表明，用户对 **Agent的“记忆”准确性** 非常敏感。错误的压缩逻辑可能导致对话历史中“学到的纠正”丢失，这会严重损害用户对Agent能力的信任。
-   **易用性**：`#4329` (新TUI) 的成功，以及 `#4327` (WebUI启动优化) 的合并，都反映出用户对 **更流畅、更现代的操作体验** 的追求，不管是命令行还是图形界面。

---

#### 8. 待处理积压

-   **关于执行环境路径问题的长期Issue**：**Issue #4083** 报告了 `pathAppend` 优先级问题，自创建以来 (5月29日) 直到今天才有关联PR (#4098) 合并。类似的基础设施和配置细节问题，虽然是小众场景，但容易长期等待。虽然本次已解决，仍需提醒维护者关注类似“影响面窄但危害大”的积压问题。
    -   [Issue #4083: Bug: pathAppend does not take executable lookup precedence](https://github.com/HKUDS/nanobot/issues/4083)

-   **文件系统工具开关PR**：**PR #4138** 已开启近两周，仍处于待合并状态。此功能能显著增强平台安全性，并满足高级用户需求，建议维护者尽快审阅并决策，以避免社区贡献积压。
    -   [PR #4138: Add tools.file.enable to toggle built-in filesystem tools](https://github.com/HKUDS/nanobot/pull/4138)

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-06-14

## 1. 今日速览

项目在过去 24 小时保持极高的社区活跃度：共产生 50 条 Issue 更新（新开/活跃 48，关闭 2）和 50 条 PR 更新（待合并 48，合并/关闭 2）。海量涌入的 Issue/PR 表明项目正处于密集的功能请求、Bug 报告与社区贡献阶段，但合并/关闭速度相对滞后，仅各有 2 项完结。讨论焦点集中在 **Telegram Bot API 10.1 富消息支持**、**Web UI 缺失**、**长期运行的内存自动优化**以及 **Windows/中文环境的编码与轮询问题**。总体来看项目健康度良好，迭代势头迅猛，但维护者需加快审查与合并节奏以消化积压。

## 2. 版本发布

**无。** 过去 24 小时内未发布新版本。

## 3. 项目进展

根据数据概览，今日有 **2 个 PR 被合并/关闭** 以及 **2 个 Issue 被关闭**，具体条目未进入评论数最多的列表，但值得注意的里程碑包括：

- **Issue #501** *[CLOSED] Web UI Gateway* 历经 3 个多月讨论后被关闭，社区呼声极高的浏览器界面需求可能已被决定暂不推进或已形成替代方案。
- **Issue #44927** *[CLOSED] streaming auto-follow* 重复 Issue 被关闭，表明该功能可能已有内部实现或协议。

在 **未合并但开发中** 的重要 PR 方面，项目正在大步前进：

- **Mega bundle PR #45925** 将 86 个开放 PR 整合至同一分支，试图解决大量 PR 积压导致的合并冲突与集成测试问题，是一次大规模协作尝试。
- **PR #42922** 基于 OpenTUI 构建全新的终端界面，若合并将彻底替换当前的 Ink TUI。
- **PR #45681** 增加了 SSL 证书损坏的预先检测，提升 provider 调用可靠性。
- **PR #45937** 修复了 dashboard 在 GBK 环境下的编码问题。
- **PR #45934** 解决了 WeChat (Weixin) 网关轮询因传输错误挂起的问题。

这些 PR 虽尚未合并，但已清晰展示了项目接下来的改进方向。

## 4. 社区热点

| 条目 | 类型 | 热度指标 | 核心诉求 |
|------|------|----------|----------|
| [#501 Web UI Gateway](https://github.com/NousResearch/hermes-agent/issues/501) | Issue (CLOSED) | 14 条评论，👍1 | 社区长期呼声最高的本地浏览器界面，对标 Claude Artifacts；虽已关闭但讨论热度高 |
| [#10771 Auto Dream 自动内存整合](https://github.com/NousResearch/hermes-agent/issues/10771) | Issue (OPEN) | 8 条评论，👍5 | 借鉴 Claude Code 的 Auto Dream 机制，定期清理、去重、优化记忆文件，用户痛点明显 |
| [#44428 Telegram Bot API 10.1 富消息](https://github.com/NousResearch/hermes-agent/issues/44428) | Issue (OPEN) | 5 条评论，👍3 | 要求支持新发布的 Telegram 富消息（标题、表格、LaTeX、折叠块等），已有重复 Issue #45864、#45854 |
| [#42366 Desktop 不自动滚动且输入框消失](https://github.com/NouResearch/hermes-agent/issues/42366) | Issue (OPEN) | 2 条评论，👍3 | 虽然评论少但点赞多，是影响日常使用的高频痛点 |
| [#44927 streaming auto-follow 设置](https://github.com/NousResearch/hermes-agent/issues/44927) | Issue (CLOSED, duplicate) | 2 条评论，👍3 | 用户渴望恢复/增加“流式输出自动跟随”的开关，且默认关闭 |

**分析：** 社区目前最活跃的诉求集中在 **Web UI 缺失**、**长期记忆碎片化**和 **新平台 API（Telegram 10.1）适配** 上。虽然 Web UI Issue 已关闭，但社区仍在期待替代方案；Telegram 富消息相关的重复 Issue 激增，表明用户已开始大量使用新 API，适配需求紧迫。

## 5. Bug 与稳定性

过去 24 小时报告的 Bug 涵盖多个平台和严重程度，按 P2 (重要) 到 P3 (一般) 排列。多数已有对应的修复 PR，但仍处于开放状态：

### P2 级别（重要）

| Issue | 描述 | 备注 |
|-------|------|------|
| [#23975](https://github.com/NousResearch/hermes-agent/issues/23975) | 上下文压缩被网关消息中断，导致降级摘要标记 | — |
| [#44666](https://github.com/NousResearch/hermes-agent/issues/44666) | `providers:` 中 `api_key_env` 别名被静默忽略，实际发送 `no-key-required` | |
| [#31155](https://github.com/NousResearch/hermes-agent/issues/31155) | `delegation.model` 配置被忽略，子代理总是继承父模型 | |
| [#43586](https://github.com/NousResearch/hermes-agent/issues/43586) | 裸 `provider: custom` + `key_env` 不读取 API Key，导致 401 | 与 #44666 同类型 |
| [#42405](https://github.com/NousResearch/hermes-agent/issues/42405) | 记忆达到容量上限后 `replace` 零匹配进入重试循环，最终静默无响应 | |
| [#19245](https://github.com/NousResearch/hermes-agent/issues/19245) | 崩溃后 `session_search` 返回空，孤立 session JSON 无法恢复 | |
| [#33907](https://github.com/NousResearch/hermes-agent/issues/33907) | 上下文压缩产生孤立 session，未写入 state.db | duplicate |
| [#45783](https://github.com/NousResearch/hermes-agent/issues/45783) | 会话恢复时重放所有待处理工具调用，导致大量 API 费用尖峰（581+ 调用） | |
| [#45860](https://github.com/NousResearch/hermes-agent/issues/45860) | Windows 安装三个 Bug（中断后 hermes.exe 缺失、重试报错、pip 失败） | |
| [#45813](https://github.com/NousResearch/hermes-agent/issues/45813) | GitHub Copilot (非 ACP) provider 始终返回 400 Bad Request | |
| [#45674](https://github.com/NousResearch/hermes-agent/issues/45674) | `hermes mcp list` 因 string 类型的 server 条目直接崩溃 | |
| [#45792](https://github.com/NousResearch/hermes-agent/issues/45792) | Docker 容器内不理解自身环境，无法正确配置 | |
| [#42188](https://github.com/NousResearch/hermes-agent/issues/42228) | 桌面/TUI 压缩会话因 cwd 未继承而进入 "No workspace" 分组 | |
| [#40187](https://github.com/NousResearch/hermes-agent/issues/40187) | macOS 下 `hermes desktop` 编译 Electron 应用失败 | |

### P3 级别（一般）

- **平台相关**: Matrix 线程初始消息丢失 ([#45493](https://github.com/NousResearch/hermes-agent/issues/45493)), WeChat 轮询挂起 + GBK 编码问题 ([#45931](https://github.com/NousResearch/hermes-agent/issues/45931)), 消息网关 GBK 解码错误 ([#45932](https://github.com/NousResearch/hermes-agent/issues/45932))
- **TUI**: 目录太多时工作区选择按钮消失 ([#45921](https://github.com/NousResearch/hermes-agent/issues/45921)), 重复 patch 文件被应用两次 ([#45834](https://github.com/NousResearch/hermes-agent/issues/45834))
- **功能受限**: Cron 后台审查阻止 read_file 等只读工具 ([#45877](https://github.com/NousResearch/hermes-agent/issues/45877))

**已有修复 PR**:  
- [#45937](https://github.com/NousResearch/hermes-agent/pull/45937) → GBK dashboard 编码  
- [#45934](https://github.com/NousResearch/hermes-agent/pull/45934) → Weixin 轮询传输错误  
- [#45681](https://github.com/NousResearch/hermes-agent/pull/45681) → SSL CA 损坏检测  
- [#45936](https://github.com/NousResearch/hermes-agent/pull/45936) → 桌面模型切换回滚  
- [#45938](https://github.com/NousResearch/hermes-agent/pull/45938) → 流式溢出块可编辑性  
- [#24395](https://github.com/NousResearch/hermes-agent/pull/24395) → auth remove 误杀同源凭据  
- [#45868](https://github.com/NousResearch/hermes-agent/pull/45868) → skills 区分引用与变更  
- [#37027](https://github.com/NousResearch/hermes-agent/pull/37027) → TTS 语音气泡 ContextVar 修复  
- [#21774](https://github.com/NousResearch/hermes-agent/pull/21774) → Google Workspace OAuth 加固  
- [#17480](https://github.com/NousResearch/hermes-agent/pull/17480) → Codex usage 凭据从 auth fallback 解析  

**评价**: 今日 Bug 报告密集，尤其是配置系统（key_env 别名、delegation.model 忽略）和记忆子系统（容量循环、孤儿 session）暴露出较为严重的稳定性问题。大量 PR 已经瞄准修复，但尚未合并，建议维护者优先处理这些影响核心体验的 P2 错误。

## 6. 功能请求与路线图信号

新涌现的功能请求与已有 PR 所体现的方向如下：

### 高优先级（社区呼声强且有对应 PR 实现）

- **Telegram 10.1 富消息支持**: #44428、#45864、#45854 三个 Issue 外加 [#45863](https://github.com/NousResearch/hermes-agent/pull/45863) (WhatsApp Calling) 和 [#45800](https://github.com/NousResearch/hermes-agent/pull/45800) (WhatsApp Opus 语音) 显示团队正在全力加强消息平台能力。已有一个 PR [#45933](https://github.com/NousResearch/hermes-agent/pull/45933) 将 Telegram 富消息设为 opt-in，平衡新功能与兼容性。
- **自动记忆整合 (Auto Dream)**: [#10771](https://github.com/NousResearch/hermes-agent/issues/10771) 获得 5 个 👍，目前尚无 PR，但记忆相关 Bug 高发（#42405、#19245、#33907）已构成业务驱动，预计很快会有实现。
- **WhatsApp 消息模板**: [#45935](https://github.com/NousResearch/hermes-agent/issues/45935) 来自生产用户需求，用于突破 24h 会话窗口。
- **原生 OpenTUI 界面**: [#42922](https://github.com/NousResearch/hermes-agent/pull/42922) 几乎是一个全新 TUI 的重写，如果合并将成为下一版本默认交互界面。

### 中期潜力

- **规划顾问 /consult**: [#19344](https://github.com/NousResearch/hermes-agent/issues/19344) 允许低成本模型遇到复杂问题时委托给前沿模型，反映用户对多模型混合使用的需求。
- **桌面完成音效**: [#42480](https://github.com/NousResearch/hermes-agent/pull/42480) 增加了 Web Audio 合成提示音，提升交互反馈。
- **自动跟随滚动 opt-in**: 虽然 #44927 已关闭，但诉求仍在，可能以更完善的设置重新出现。

### 路线图信号

今日的 Mega bundle [#45925](https://github.com/NousResearch/hermes-agent/pull/45925) 集成 86 个开放 PR，表明维护者意识到积压问题并试图通过大规模整合测试来加速合并。这暗示下一阶段将重点清理存量贡献并发布一个稳定性/特性集中更新版本。

## 7. 用户反馈摘要

从 Issue 评论和 Bug 描述提炼出以下真实用户反馈：

- **Web UI 是最大期待**: 尽管 #501 已关闭，用户仍在吐槽 CLI 和现有接入方式无法替代浏览器界面的便利性，尤其是预览制品和富文本。
- **长期运行后体验急剧下降**: 用户报告运行数小时或跨天会话后，记忆文件臃肿（#42405）、上下文压缩产生孤儿会话（#33907）、恢复时会话搜索为空（#19245），严重依赖 Auto Dream 类机制。
- **配置系统令人困惑**: 多个用户遇到 `api_key_env` / `key_env` 字段名混淆、自定义 provider 认证失败的陷阱（#44666、#43586），表明文档与实际实现存在偏差，且错误提示不明确（仅返回 `no-key-required`）。
- **多模型/子代理管控不足**: 用户期望为子代理配置不同模型以节省成本或分配任务，但 `delegation.model` 被忽略（#31155），导致部署受限。
- **中文环境用户受挫**: Windows GBK 编码问题（#45932、#45931）导致 WeChat 网关和 dashboard 启动失败，英文用户同样抱怨 Docker 环境感知（#45792）、macOS 编译（#40187）等非功能性问题。
- **Telegram 用户期待最新 API**: 多个用户急切要求支持 6月11日发布的 Telegram Bot API 10.1 富消息，因现有 MarkdownV2 方式无法渲染新格式，且官方 Telegram Web 尚未完美支持，社区已有 opt-in PR 作为折中。
- **桌面 TUI 基础体验亟待提升**: 自动滚动、输入框保留（#42366）、工作区选择（#45921）是高频小问题，严重影响日常使用满意度。

## 8. 待处理积压

以下 Issue/PR 开放时间较长且无最近维护者响应，或具有重要影响但缺少进展：

| 条目 | 创建时间 | 简介 | 备注 |
|------|----------|------|------|
| [#10771](https://github.com/NousResearch/hermes-agent/issues/10771) | 2026-04-16 | 自动记忆整合 Auto Dream | 已有 5 个 👍，至今无 PR 或分配 |
| [#19245](https://github.com/NousResearch/hermes-agent/issues/19245) | 2026-05-03 | 崩溃后 session_search 空结果 | 严重影响恢复能力 |
| [#19344](https://github.com/NousResearch/hermes-agent/issues/19344) | 2026-05-03 | 规划顾问 /consult | 有价值的混合模型需求 |
| [#22417](https://github.com/NousResearch/hermes-agent/issues/22417) | 2026-05-09 | 紫鸾场域健康引擎（社区展示） | 用户自研集成，未获官方回应 |
| [#22532](https://github.com/NousResearch/hermes-agent/pull/22532) | 2026-05-09 | Telegram clarify prompts | PR 开放一个多月，无 review |
| [#23975](https://github.com/NousResearch/hermes-agent/issues/23975) | 2026-05-11 | 上下文压缩被中断导致降级 | P2 稳定性 Bug |
| [#31155](https://github.com/NousResearch/hermes-agent/issues/31155) | 2026-05-23 | delegation.model 被忽略 | P2 配置错误 |
| [#33907](https://github.com/NousResearch/hermes-agent/issues/33907) | 2026-05-28 | 压缩后孤儿 session 问题 | 重复问题，但无 root cause 修复 |
| [#17480](https://github.com/NousResearch/hermes-agent/pull/17480) | 2026-04-29 | Codex usage 从 auth fallback 解析凭据 | 重要修复 PR 搁置超过 45 天 |
| [#21774](https://github.com/NousResearch/hermes-agent/pull/21774) | 2026-05-08 | Google Workspace OAuth 加固 | 类似情况 |

**建议**: 维护者应关注以上积压，特别是从 4 月就已开放的 #10771（记忆整合）和 #17480（认证修复），它们直接关联用户反馈中反复出现的记忆碎片化和配置混淆问题。同时，#22417 这样的社区分支展示也可以给予认可或指导意见，增强社区活力。

---

*本日报基于 NousResearch/hermes-agent 2026-06-14 公开数据生成，所有链接均可直接访问。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 — 2026-06-14

## 1. 今日速览

过去 24 小时内，项目合并/关闭了 5 个 PR，涵盖核心 bug 修复、TTS 增强、代码清理及中文文档贡献；同时发布了一个 nightly 自动构建版本。社区活跃度中等偏上，关键 bug（图像描述幻觉 #3108）已由 #3117 修复，但较严重的 token 持续消耗问题（#3012）仍在讨论中，尚无修复 PR。整体来看，项目在稳定性和多模型兼容性上稳步推进，但需关注尚未解决的成本优化问题。

## 2. 版本发布

**nightly: v0.2.9-nightly.20260614.cf67dd38**  
自动构建版本，可能包含不稳定变更，请谨慎使用。  
本次 nightly 涵盖自 v0.2.9 以来的合并内容（包括今日关闭的 #3117、#3119 等修复与功能）。无破坏性变更说明及特殊迁移注意事项。  
[Release 链接](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

## 3. 项目进展

今日合并/关闭的 PR 对项目有显著推进：

- **#3117** `fix(agent): route media turns to image models`（已合并）  
  修复了当活动模型不支持视觉时图像描述请求产生幻觉的 bug。该 PR 将媒体轮次和 `load_image` 后续强制路由到配置的图像模型，是今日最重要的修复。  
  [PR #3117](https://github.com/sipeed/picoclaw/pull/3117)

- **#3119** `fix(tts): support OpenRouter voice overrides and fallback`（已合并）  
  支持通过 `extra_body` 字段覆盖 OpenAI TTS 的 `voice`/`response_format`，并在失败时自动降级重试，增强了 TTS 在多供应商下的兼容性。  
  [PR #3119](https://github.com/sipeed/picoclaw/pull/3119)

- **#3065 & #3066** `fix: explicitly ignore Close() errors on ... failure paths`（均合并）  
  清理了 `pkg/seahorse`、`pkg/tools` 等模块中未检查的 `Close()` 错误，提升代码健壮性。  
  [PR #3065](https://github.com/sipeed/picoclaw/pull/3065) | [PR #3066](https://github.com/sipeed/picoclaw/pull/3066)

- **#2935** `docs(i18n): add Traditional Chinese (zh-TW) locale and READMEs`（已合并）  
  社区贡献者添加了繁体中文的 README、贡献指南及前端 i18n 资源，有助于项目在国际市场的接纳。  
  [PR #2935](https://github.com/sipeed/picoclaw/pull/2935)

以上变更使项目在**多模型路由正确性、语音合成灵活性、代码质量及国际化**方面均向前迈进。

## 4. 社区热点

- **#3012** `[BUG] Continuous consumption of tokens every minutes when evolution is enabled`  
  自 6 月 5 日开启至今已收获 3 条评论，用户报告：在 FreeBSD 环境下使用 MiniMax 模型、开启 Evolution Draft 模式时，每分钟持续消耗大量 token。该问题直接影响使用成本，社区关注度较高，但目前尚无指派或修复 PR。  
  [Issue #3012](https://github.com/sipeed/picoclaw/issues/3012)

- **#2964** `Feat/image input compression`  
  该 PR 虽未合并，但涉及图像预处理功能的重大扩展（可配置的多级压缩策略），评论中有一定讨论，社区对改善视觉管道效率有较高期待。  
  [PR #2964](https://github.com/sipeed/picoclaw/pull/2964)

## 5. Bug 与稳定性

| 严重程度 | Issue | 状态 | 说明 |
|----------|-------|------|------|
| **高** | #3108 图像描述请求产生幻觉 | 已关闭（#3117 修复） | 当活动模型为 `deepseek/deepseek-v4-flash`（文本模型）时，图像描述输出与内容无关。现已路由至图像模型修复。 |
| **中高** | #3012 Evolution 模式下持续消耗 token | 开放中，无修复 PR | 影响使用 Evolution 功能的所有用户，可能产生额外费用。暂未分配。 |
| **低** | #3065 / #3066 未检查的 Close() 错误 | 已修复 | 潜在静默失败路径，需手动忽略错误。 |

所有今日关闭的 bug 均有对应修复 PR，项目对稳定性反馈响应及时。

## 6. 功能请求与路线图信号

- **#3118** `Add remote Pico WebSocket mode to picoclaw agent`（打开，未合并）  
  为 agent 新增远程模式，支持 `--remote ws://...`，便于外部系统通过 WebSocket 调用 agent。该需求若落地将显著扩展 PicoClaw 的集成能力。  
  [PR #3118](https://github.com/sipeed/picoclaw/pull/3118)

- **#2964** 图像输入压缩（打开，未合并）  
  解决大尺寸图片占用过高的问题，通过可配置策略压缩后送入模型，对资源敏感场景有很大价值，可能纳入下一 minor 版本。

- **#3119** TTS 多供应商回退与参数覆盖（今日合并）  
  已合入主线，代表项目在**语音输出灵活性**上的持续投入。

综合以上信号，项目下一阶段的路线图可能围绕**多模态管道优化、外部集成扩展**展开。

## 7. 用户反馈摘要

- **@xpader**（#3012）详细描述在 FreeBSD / MiniMax 环境下启用 Evolution Draft 后 token 消耗异常，每分钟持续扣费。用户建议关闭 Evolution 临时规避，但期望官方修复。该反馈凸显模型供应商计费模式与客户端逻辑交互的潜在缺陷。

- **@afjcjsbx** 提交了 #3108 以及对应的修复 PR #3117，同时在 #2964 中贡献了图像压缩的实现。扮演了“发现问题、解决问题”的积极角色，表明有一定开发能力的用户正深度参与项目改进。

## 8. 待处理积压

| 项目 | 标题 | 创建 | 天数 | 状态 |
|------|------|------|------|------|
| #3012 | Continuous consumption of tokens when evolution enabled | 2026-06-05 | 9 天 | 无 assignee、无 PR，持续活跃但无进展 |
| #2964 | Feat/image input compression | 2026-05-28 | 17 天 | 已至 PR 阶段，等待维护者 Review / Merge |

以上两条长期未解决的重要议题需要维护者重点关注，尤其是 #3012 直接关系到用户成本和信任。建议为 #3012 分配负责人并制定修复计划。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 —— 2026-06-14

> 数据来源：GitHub (nanocoai/nanoclaw) | 统计区间：2026-06-13 ~ 2026-06-14

---

## 1. 今日速览

截至 2026 年 6 月 14 日，NanoClaw 在 24 小时内保持了强劲的开发活跃度。**核心团队合入了 4 个架构级功能 PR**，涵盖 Provider Hook 扩展、SDK 大版本升级、能力注册表与持久化内存支架，显著推进了项目在 Provider 可扩展性路线图上的落地。修复方面，**2 个高优先级稳定性 PR 正在等待审核合并**，分别针对容器异常杀死后的数据库日志恢复（#2750）及系统级健康审计加固（#2732）。社区互动侧当日无新增实质性功能讨论，唯一一条 Issue 为误操作删除帖。项目整体处于**功能快速交付与基础设施硬化的正向并行期**。

- **过去 24h Issues 更新**: 1 条（已关闭，误发删除）
- **过去 24h PR 更新**: 6 条（待合并 2，已合并/关闭 4）
- **新版本发布**: 无

---

## 2. 版本发布

（无）

---

## 3. 项目进展

今日合并/关闭的 PR 集中于 **Provider 体系的能力跃迁**与 **开发工具链升级**，合计入库 4 笔核心改动：

### 3.1 Provider 体系功能性飞跃
- **交互完成钩子与指令打断**
  PR [#2754](https://github.com/nanocoai/nanoclaw/pull/2754) `feat(runner): onExchangeComplete provider hook + slash-command interruption`
  为 Provider 运行时增加了 `onExchangeComplete` 可选钩子与斜杠命令打断能力。核心源码层改动，覆盖了 Agent 交互闭环的最后一个关键回调接缝，是构建复杂工单流与用户干预界面的基础设施。

- **Provider 能力注册表**
  PR [#2746](https://github.com/nanocoai/nanoclaw/pull/2746) `feat(providers): agent-surfaces capability seam`
  引入了宿主侧能力注册表，Provider 可以对外声明自身支持的 Capability 面。这为宿主编排多 Provider 组合场景提供了可查询的契约基础，提升了系统松耦合程度。

- **可选的持久化内存脚手架**
  PR [#2745](https://github.com/nanocoai/nanoclaw/pull/2745) `feat(memory): opt-in persistent memory scaffold for providers`
  为 Provider 增加了 `usesMemoryScaffold` 能力标记与配套容器运行时支持，实现跨 Session 的状态持久化。这一改动将记忆能力从硬编码变为 Provider 的可声明特性。

### 3.2 开发工具链与安全升级
- **SDK 升级与凭证管理**
  PR [#2747](https://github.com/nanocoai/nanoclaw/pull/2747) `feat(onecli): SDK 2.2.1 — credential-stub mounts + machine-checkable pins`
  完成 `@onecli-sh/sdk` 0.5.0 → 2.2.1 大版本升级，引入凭证存根挂载机制与可机器验证的 PIN 体系。该 PR 直接增强了命令行工具在 CI/CD 与多环境部署场景下的安全性与配置一致性。

**小结**: 今日合并更改覆盖了 Provider 生命周期、能力声明与状态持久化三大接缝，项目在 **Provider 生态抽象层**上的完整度显著提升。

---

## 4. 社区热点

尽管当前社区评论区活跃度不高（当日无新增讨论楼层），但以下两笔开放 PR 因其**技术深度与生产环境关键性**成为社区关注焦点：

- **#2750 — 容器日志脏数据修复**
  [查看 PR](https://github.com/nanocoai/nanoclaw/pull/2750)
  `fix: recover stale outbound.db journals after container kills; classify hot-journal poll races`
  该 PR 直接承接了用户报告的 **#2516** 和 **#2640** 两个历史 BUG，试图一次性解决容器 SIGKILL 后 `outbound.db` 日志陈旧与轮询竞争条件两个隐秘问题。PR 描述充分追溯了根因，展示了开发团队对社区反馈的主动兜底态度，是目前仓库中技术讨论价值最高的 PR。

- **#2732 — 宿主与 Agent Runner 加固**
  [查看 PR](https://github.com/nanocoai/nanoclaw/pull/2732)
  `Harden host + agent-runner from health audit findings`
  虽然零评论，但其改动范围（容器生命周期、断路器、并发限制、Runner 重连）覆盖了生产环境下最常见的崩溃场景，实际潜在影响面使得它成为维护者与深度用户重点关注的目标。

---

## 5. Bug 与稳定性

### 5.1 [严重] 容器异常杀死后 Outbound 数据库日志损坏（Stale Journal）
- **关联问题**: [#2516](https://github.com/nanocoai/nanoclaw/issues/2516)、[#2640](https://github.com/nanocoai/nanoclaw/issues/2640)
- **修复 PR**: [#2750](https://github.com/nanocoai/nanoclaw/pull/2750)（**待合并**）
- **影响面**: 当容器因 `SIGKILL` 或上限触发被杀后，宿主持有的只读 `outbound.db` 句柄无法正确识别已写入日志与脏页之间的边界，导致数据库进入不一致状态。修复方案以认领/阻塞机制解决了轮询竞争条件。
- **严重程度**: 高——直接影响数据持久化可靠性。

### 5.2 [严重] 多主机 Agent 健康审计发现的安全与稳定性漏洞
- **修复 PR**: [#2732](https://github.com/nanocoai/nanoclaw/pull/2732)（**待合并**）
- **修复范围**:
  - `container-lifecycle`: Docker Desktop drvfs 绑定挂载源导致 `exit 127` 崩溃（Windows 用户敏感）；
  - `spawn` 阶段添加断路器防止崩溃空转；
  - 强制 `MAX_CONCURRENT_CONTAINERS` 上限守卫；
  - 进程级别 `docker kill` 回退兜底；
  - `agent-runner`: 无认证泄露时的自动重连机制。
- **严重程度**: 高——此为对抗性健康审计输出的整改合辑，未加固前宿主层存在多处崩溃与安全暴露面。

### 5.3 [低] 误操作 Issue 清理
- [#2755](https://github.com/nanocoai/nanoclaw/issues/2755) 已关闭，用户误将 Issue 提交至本仓库，已及时删除。无实质内容影响。

---

## 6. 功能请求与路线图信号

当日合并的 PR 清晰揭示了 NanoClaw 短中期路线图的**两个核心信令**：

### 信令一：Provider 生态化（高优先级信号）
`onExchangeComplete`（#2754）+ `agent-surfaces capability seam`（#2746）+ `persistent memory scaffold`（#2745）的密集落地，表明项目正在**从单体 Agent 运行时向高度可插拔的 Provider 体系跃迁**。下一版本极有可能围绕 Provider 能力声明接口（Capability Seam）、持久化上下文传递（Memory Scaffold）以及原生跨 Provider 编排协议展开标准化工作。

### 信令二：安全与治理增强
#2747 的 SDK 凭证挂载更新 + #2732 的 `MAX_CONCURRENT_CONTAINERS` 强制限流，表明项目正在主动向**企业级部署安全性与资源治理**靠拢。这对于持有大规模容器集群的用户是明确的利好信号。

---

## 7. 用户反馈摘要

当日无长篇用户反馈或新 Feature 请求。有限的互动线索如下：

- **隐式反馈（Bug 回追）**：PR #2750 精确关联了 #2516 与 #2640 两个由用户报告的 BUG。从 PR 描述看，用户面对的场景是容器被强杀后 Session 数据丢失且无法自动恢复。修复方案证明了该问题在过去一段时间内有稳定复现路径，且根因定位难度大。开发团队对此类隐秘技术债务的追查态度值得肯定。
- **操作路径提示**：Issue #2755 用户将 Issue 误发至本仓库，尽管是个例，但可能暗示用户在跨仓库或跨组织提报时的路由提示仍有优化空间。

---

## 8. 待处理积压

以下为**当前等待审核或合并的高优先级 PR**，建议维护团队关注。

### 8.1 [极高] PR #2732 — 健康审计加固
- 创建于 2026-06-11，已等待 3 天
- 涉及：`container-lifecycle` 级 `drvfs` 修复、强制 `MAX_CONCURRENT_CONTAINERS`、Runner 重连等多项变更
- [查看 PR](https://github.com/nanocoai/nanoclaw/pull/2732)
- **建议**：该 PR 改动量大且跨多个子系统，需进行细粒度的 Code Review，但建议优先合并以覆盖已暴露的攻击面与稳定性风险。如规模过大，可考虑拆分为容器生命周期与 Runner 两部分分别合并。

### 8.2 [高] PR #2750 — Outbound 数据库日志恢复
- 创建于 2026-06-12，已等待 2 天
- 关联两个历史 Issue（#2516、#2640），修复逻辑清晰且通过单元验证
- [查看 PR](https://github.com/nanocoai/nanoclaw/pull/2750)
- **建议**：在 #2732 合并后应尽快推进此 PR。由于修复方向与现有 BUG 完全对应且描述详尽，审核门槛较低，可优先合并以恢复数据一致性保障。

---

**报告结语**：NanoClaw 在 2026-06-14 的活跃度处于**高位区间**。开发交付能力强（4 PR 合并），稳定性投入深（2 笔高复杂度加固），路线图方向明确（Provider 生态化）。当日无社区负面情绪信号，项目健康度良好。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为您的专属 AI 智能体与个人 AI 助手领域开源项目分析师，这是基于 NullClaw 项目最新 GitHub 数据生成的 2026-06-14 项目动态日报。

---

# NullClaw 项目日报 | 2026-06-14

## 1. 今日速览

项目今日整体活跃度**中等，属于高价值的集中式维护**。虽然过去 24 小时内无新版本发布或 PR 合并，但核心开发团队针对社区反馈最严重的 `Agent` 类型定时任务静默失败问题做出了快速响应，提交了修复补丁。目前项目的“日程执行”核心链路处于被社区挑战的脆弱状态，但开发者的响应积极，项目健康度呈现 **“核心功能亮黄灯，但治理响应亮绿灯”** 的局面。

## 2. 版本发布

无（无新版本发布）

## 3. 项目进展

- **今日无 PR 被合并或关闭。** 项目的重大推进体现在 **PR #954 的提交**，它直接针对社区最活跃的 Issue #941 提供了修复补丁。
    - **PR #954**：[OPEN] [Fix: one-shot cron jobs silently fail to deliver messages (use-after-free in OutboundMessage.channel)](https://github.com/nullclaw/nullclaw/pull/954)
    - **摘要**：该 PR 指出了 `OutboundMessage.channel` 属性存在 **“use-after-free”**（释放后使用）内存错误，导致一次性定时任务在尝试输出消息时崩溃，但系统错误地将任务标记为“已完成”。
    - **影响**：如果该 PR 被合并，将直接修复 Agent 定时任务通过 Telegram/Mattermost 等渠道静默失败的严重 BUG，是整个项目在稳定性上的一大步。

## 4. 社区热点

今日讨论的热点完全集中在 **Issue #941** 上。

- **话题热榜**：[#941 [OPEN] Agent-type cron jobs don't spawn a subprocess — Telegram delivery never happens](https://github.com/nullclaw/nullclaw/issues/941)
- **热度分析**：该 Issue 由用户 `weissfl` 提出，过去 24 小时内虽无新增评论，但 **PR #954 的及时提交**表明该 Issue 已被维护者深度关注并进入了解决流程。
- **背后诉求**：社区正在要求 **“AI Agent 作为独立定时工作流”的绝对可靠性**。用户期望 `schedule` + `agent` + `telegram` 这一组合能够像 Unix 的 cron 服务一样健壮。失败后没有任何报错（静默失败）是用户最不能容忍的，这破坏了 AI 助手作为“自主执行者”的核心信任基础。

## 5. Bug 与稳定性

今日仅报告了 **1 个 BUG**，但性质极为严重。

- **[严重] BUG #941（Agent 定时任务静默失败）**
    - **现象**：使用 `schedule` 创建 `job_type: "agent"` 的任务并配置 `delivery_mode: "always"` 和 `delivery_channel: "telegram"` 后，任务被错误标记为“完成”，但 Agent 子进程实际上从未启动，消息也从未送达 Telegram。
    - **严重等级**：**最高级**。这是一个典型的静默数据丢失问题，对自动化场景是致命的。
    - **诊断的根因**：PR #954 指出根因在于 `OutboundMessage.channel` 的 **use-after-free** 错误，导致消息发送线程访问了已被释放的内存，任务进程退出。
    - **Fix 状态**：已有 **PR #954** 待审核合并。

## 6. 功能请求与路线图信号

今日无明确的功能请求提交。

- **路线图信号**：鉴于 Issue #941 的严重性，**“Agent 定时任务执行链路”的加固**已成为项目的最高优先级路线图信号。这可能预示着在后续版本中，项目会引入：
    1.  Agent 任务执行日志的增强（即使 Job 失败，也应记录失败原因）。
    2.  `cron.json` 中删除任务前的事务性保证（避免任务未执行就被移除）。
    3.  对 `OutboundMessage` 和子进程管理模块的全面审查，防止类似的内存安全问题。

## 7. 用户反馈摘要

主要来自 Issue #941 的创建者 `weissfl`：

- **使用场景**：用户试图构建一个定时自动化的 Agent，在特定时间执行任务并通过 Telegram 推送结果——这是 AI 个人助理最典型的高频使用场景。
- **满意点**：无（用户正处于发现问题后的不满状态）。
- **不满意点 / 痛点**：
    1.  **反馈缺失（最大的痛点）**：系统没有给出任何错误提示，甚至将失败任务标记为完成，这是一种“欺骗性”的用户体验。
    2.  **配置信任度下降**：用户质疑 `delivery_mode` 和 `delivery_channel` 等参数的组合是否可靠。
    3.  **调试困难**：没有日志指明 Agent 子进程为何没有 spawned，用户只能通过“消息没收到”来逆向判断故障（PR #954 提交后才明确了根因）。

## 8. 待处理积压

目前关键的积压项集中在同一个修复链路上：

- **[待合并] PR #954**：[Fix: use-after-free in OutboundMessage.channel](https://github.com/nullclaw/nullclaw/pull/954)
    - **状态**：自昨日（2026-06-13）提交后，仍在等待 Code Review 和合并。
    - **提醒关注**：对于修复“静默失败”这种严重 BUG 的 PR，建议维护者**加速审核**，并在合并后进行充分的回归测试，特别是对一次性（`once`）和计划性（`cron`）任务的全面测试。

- **[待关闭] Issue #941**：[Agent-type cron jobs fail silently](https://github.com/nullclaw/nullclaw/issues/941)
    - **状态**：已存在约 2 周（2026-05-31 创建），是 PR #954 的直接动因。
    - **提醒关注**：解决问题只是第一步，建议维护者在修复后回应该 Issue，并考虑是否需要发布一个热修复版本（hotfix）。

---
*数据来源：GitHub nullclaw/nullclaw | 分析周期：2026-06-13 ~ 2026-06-14*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 | 2026-06-14

## 1. 今日速览
过去 24 小时 IronClaw 开发热度极高，共产生 24 条 Pull Request 动态，其中 7 条成功合并/关闭。核心开发组双线并行作战：一是大规模 **“附件文本抽取与模型可见”** 功能管线（Epic #4644）的基础设施宣告合龙，二是密集攻关 **Slack 重新审批循环** 这一严重的用户侧体验 Bug（连发 #4839/#4843/#4844 三个 Fix PR）。此外，仍在开放中的 17 条 PR 中有多条属 XL/大型重构，体现项目正处于深度架构迭代期。需关注的是，Nightly E2E 持续故障（#4108）已接近三周无有效行动，存在严重的 CI 积压风险。

## 2. 版本发布
过去 24 小时无正式版本发布。Release PR `#3708`（`ironclaw 0.29.1`）自 5 月 16 日起开放，至今未合并。

## 3. 项目进展

### 里程碑合龙：附件文本抽取与持久化管线
Epic `#4644`（Attachments: Extract document text on inbound / Bring text into model context）的一系列基础建设 PR 于今日集中完成合并，标志着从**字节落地 → 文本提取 → 转录持久化**的完整链路已建成：

- **[#4655](https://github.com/nearai/ironclaw/pull/4655)（已合并）**：Reborn Transcript 记事本契约扩展 `AttachmentRef`，附件引用在 `accept` → 重启过程中不再丢失。
- **[#4668](https://github.com/nearai/ironclaw/pull/4668)（已合并）**：基于 MountView 的字节存储落地 crate，为附件提供持久化后端。
- **[#4670](https://github.com/nearai/ironclaw/pull/4670)（已合并）**：桥接落地字节与 Trans cript `AttachmentRef`，完成 Track 2 → Track 3 的连接。
- **[#4675](https://github.com/nearai/ironclaw/pull/4675)（已合并）**：将 `byte→text` 抽取逻辑抽离为独立内库 `ironclaw_extractors`，供后续复用。
- **[#4672](https://github.com/nearai/ironclaw/pull/4672)（已合并）**：WebChat v2 发送路径接入 `land_inbound_attachments`，浏览器上传文件正式全链路打通。

### 依赖安全修复
- **[#4242](https://github.com/nearai/ironclaw/pull/4242)（已合并）**：`tar` 库版本 0.4.45 → 0.4.46，修复 PAX 头部符号链接遍历漏洞。

### 整体评估
项目模块化进度显著推进（提取器独立 crate、字节存储独立 crate），为未来支持更多文件类型和跨能力复用奠定了基础。

## 4. 社区热点

- **🔥 Slack 重新审批循环修复系列**
  核心开发者 `henrypark133` 针对一个 Slack QA 中的严重 Bug（单次调用需 4 次授权确认）连发三条 PR，条分缕析地拆解问题域：
  - **[#4839](https://github.com/nearai/ironclaw/pull/4839)**：在审批网关重分发时保留调用身份，避免身份丢失导致重新要求授权。
  - **[#4843](https://github.com/nearai/ironclaw/pull/4843)**：对同一个 `run_id` 的网关送达做单例处理（single-flight），防止 Ack 扇出造成冗余。
  - **[#4844](https://github.com/nearai/ironclaw/pull/4844)**：修复网关筛选函数底层逻辑，将 `fn(&GateRef)` 改为 `fn(&str)`，消除遍历分支带来的分类混乱。
  这三条 PR 代表了 IronClaw 团队面对深层状态机缺陷时典型的 **“模块化解耦 + 分层修复”** 风格，是当前社区最核心的关注焦点。

- **🆕 模型运行时上下文感知**
  **[#4836](https://github.com/nearai/ironclaw/pull/4836)** 实现 #4828：向模型暴露当前连接通道、出站投递目标、运行来源。这一改动赋予模型运行时的 **“自我状态认知”**，是 Agent 透明性上的重要提升，回应了用户长久以来“模型不知道为什么连接不上”的痛点。

## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 简述 | 状态 |
|---|---|---|---|
| 🔴 严重 | [#4108](https://github.com/nearai/ironclaw/issues/4108) | Nightly E2E 持续失败（5月27日起），无修复 PR 关联。 | 开放/未分配 |
| 🔴 严重 | [#4839](https://github.com/nearai/ironclaw/pull/4839) / [#4843](https://github.com/nearai/ironclaw/pull/4843) / [#4844](https://github.com/nearai/ironclaw/pull/4844) | Slack 重新审批循环，单次操作需要多次授权确认。 | 有 Fix PR，待合并 |
| 🟠 高 | [#4841](https://github.com/nearai/ironclaw/pull/4841) | Reborn 运行器“闪崩”：遇到 `HostUnavailable` 或协议错误时直接杀死进程并返回不透明错误码。 | 有 Fix PR，开放中 |
| 🟠 高 | [#4838](https://github.com/nearai/ironclaw/pull/4838) | 繁忙线程处 理：替换之前 Buggy 的 defer-and-drain 模型，改为明确拒绝并告知用户重试。 | 有 Fix PR，开放中 |
| 🟡 中 | [#4846](https://github.com/nearai/ironclaw/pull/4846) | 裸 `workspace/` 工具路径被错误嵌套为 `/workspace/workspace/`。 | 有 Fix PR，开放中 |

## 6. 功能请求与路线图信号

- **⛳ 运行时上下文透明化（#4828 → #4836）**：已由核心团队落地实现。此功能将作为未来 Agent “自我修正” 的基础设施。
- **⛳ Routine REST API 端点（#4264）**：新贡献者 `wcc945` 提交的 `POST /api/routines` 端点 PR。虽然已两周未获维护者评论，但这清晰地反映了社区对程序化管理 Routine 的强烈诉求，是未来 Web 平台化的关键拼图。
- **⛳ Slack 状态持久化与出站引导（#4777 / #4780）**：两个 PR 旨在解决 Slack 集成中的状态同步问题（WebUI 总是显示 Slack 离线）和模型出站投递的决策指导（让模型知道投递目标后不再误报“Slack 不可用”）。这属于 Slack 接入稳定化的最后环节。

## 7. 用户反馈摘要
本期数据采集范围内，Issue 评论区呈现零交互状态，直接的文字反馈缺失。但 IronClaw 团队在 PR 描述中撰写了详尽的上下文，我们可以从中逆向解析当下用户的真实痛点：

- **重复授权地狱**：PR #4839 观察到用户通过 Slack 触发 `gmail.get_message` 时，因同时需要一次性审批和 OAuth 凭据，导致单次逻辑调用在重启循环中需经历多达 **4 个审批关口**。此问题已成为高层级用户在实际工作流中的最大阻塞点。
- **失败即死**：PR #4841 描述当前状态：“一个遇到 `HostUnavailable` 的 run 会带着不透明错误码直接死亡，无恢复路径。” 这表明用户在面对短暂网络或后端波动时毫无容错空间，这是被频繁投诉的场景。
- **系统状态黑盒**：PR #4777 和 #4836 指出，直到现在模型在每轮循环启动时仍然不知道哪个通道是连接的、出站投递指向哪里。用户典型的困惑是“我明明配置了 Slack，为什么模型说它无法访问 Slack？”。
- **附件静默丢失**：整个 Epic #4644 的反面，是用户上传的文档在过去被转录层静默丢弃（text-only contract），这一重大体验坍塌正在被系统性修复。

## 8. 待处理积压

- **⚠️ 紧急积压：Nightly E2E 持续失败（[#4108](https://github.com/nearai/ironclaw/issues/4108)）**
  自 5 月 27 日首次报出，已 19 天无任何回复、暂未标记责任人，亦无关联修复 PR。持续的红灯将严重影响 CI 置信度和发布节奏。
- **⚠️ 发布阻塞：Release 0.29.1（[#3708](https://github.com/nearai/ironclaw/pull/3708)）**
  核心发布 PR 停滞 29 天，内含 `ironclaw_common` 和 `ironclaw_skills` 的 Breaking Changes。阻塞可能导致下游依赖方无法同步修复。
- **⚠️ 社区健康风险：新贡献者 PR 搁置（[#4264](https://github.com/nearai/ironclaw/pull/4264)）**
  `wcc945` 的 Routine 端点 PR 持续两周无维护者评论。这种沉默对开源社区贡献热情的侵蚀不容忽视，建议至少给予初步人工反馈或 CI 触发说明。
- **🕒 等待合并：附件管线残留 PR**
  [#4676](https://github.com/nearai/ironclaw/pull/4676) 与 [#4677](https://github.com/nearai/ironclaw/pull/4677) 已完成功能开发，属于管线后半段（文本抽取、模型上下文折叠），风险较低，建议尽快 Review 合并以完结 Epic #4644。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是根据 LobsterAI 项目 2026-06-14 前24小时数据生成的项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-06-14

## 1. 今日速览
项目过去24小时内**未产生新的 Issue 或 PR**，活跃度降至近期低点。主要动态为机器人（Stale Bot）标记了4个旧Issue和5个旧PR，同时对2个小型平台体验修复PR进行了合并。整体处于**低活跃维护期**。尽管有代码合入，但社区贡献者提交的重大功能（如 Artifacts 预览管线 #1441）和关键的兼容性缺陷（OpenCLAW 升级 #1443）已长时间无人问津。积压问题数量未见减少，项目需要在未来迅速回应社区诉求，以维持健康度和贡献者活跃度。

## 2. 版本发布
**无**。

## 3. 项目进展
过去24小时内成功合并/关闭了 **2 个 Pull Requests**，均为针对用户体验的细节打磨：

- **\[已合并\] MCP 弹窗交互优化** `#1466` ([Details](https://github.com/netease-youdao/LobsterAI/pull/1466)): 修复了 MCP Server 配置弹窗内容过长时，底部“取消”按钮被遮挡无法点击的问题，提升了表单的可访问性。
- **\[已合并\] macOS 快捷键适配** `#1467` ([Details](https://github.com/netease-youdao/LobsterAI/pull/1467)): 修复了在 macOS 系统下设置页面快捷键图标仍显示 `Ctrl` 的问题，现已针对平台正确显示 `⌘（Cmd）`，完善了跨平台细节。

**评估：** 项目推进节奏较慢，主要体现在修复了细碎的体验缺陷。但仍有 **3 个从 4 月初就提交的关键 PR**（技能系统重构、Artifacts管线）迟迟未能合入，版本迭代趋缓。

## 4. 社区热点
尽管没有增量讨论，以下几个议题因长期悬而未决，构成了社区最核心的关注点：

- **OpenCLAW 兼容性危机 (Issue #1443)**: 用户因无法适配 OpenCLAW v2026.3.24 的 Breaking Change 导致服务崩溃。这是 **直接影响项目可用性** 的核心依赖问题，用户长时间未收到官方回复，仅被机器人标注为 stale。这是社区最大的焦虑来源。 [查看详情](https://github.com/netease-youdao/LobsterAI/issues/1443)
- **Artifacts 巨型 PR (PR #1441)**: 该 PR 解决了 10 个冲突文件并修复了 5 个 Bug，试图为 CoWork 引入 HTML/React/Mermaid 的扩展预览管线。该功能极具前瞻性，但长时间缺乏 Code Review，贡献者的动力正在被持续消耗。 [查看详情](https://github.com/netease-youdao/LobsterAI/pull/1441)
- **Agent 技能系统设计博弈 (Issue #1442 / PR #1440)**: 用户对 “Agent 选择技能后的交互逻辑” 提出根本性质疑，认为当前写法不符合直觉。社区贡献者也提交了 UI 重构方案（#1440）试图解决视觉与交互层的不一致性。 [查看详情](https://github.com/netease-youdao/LobsterAI/issues/1442)

## 5. Bug 与稳定性
以下为当前跟踪的 Bug，按严重程度排列：

- **\[严重\] 禁用技能仍可被调用** (`#1439`): “关闭技能”的开关形同虚设，用户通过对话关键词仍能触发。这可能导致大模型路由混乱，存在稳定性和安全性隐患。**尚无关联修复 PR。** [查看详情](https://github.com/netease-youdao/LobsterAI/issues/1439)
- **\[严重\] 创建不重复任务按钮无响应** (`#1437`): 选择“不重复”计划后，点击“创建任务”无任何 UI 反馈或报错。这是典型的静默错误，阻塞了任务创建的核心流程。**尚无关联修复 PR。** [查看详情](https://github.com/netease-youdao/LobsterAI/issues/1437)
- **\[中等\] Agent 技能引用状态错乱** (`#1442`): 用户选择技能进入对话，对话后技能标签消失，且用户对“技能选择”这一行为本身的设计目标感到困惑。PR `#1440` 尝试进行修复。 [查看详情](https://github.com/netease-youdao/LobsterAI/issues/1442)
- **\[已修复\] MCP 配置弹窗按钮不可达** (`#1466`): 已合并。
- **\[已修复\] macOS 快捷键图标错乱** (`#1467`): 已合并。

## 6. 功能请求与路线图信号
基于数据，社区正在强烈暗示以下路线图方向：

- **核心依赖升级（紧急）**: `#1443` 请求适配 OpenCLAW 新版本。这是维持项目在线运行的头号刚需，若不解决，将直接阻碍用户留存。
- **高级渲染能力（重大特性）**: `#1441` 的 Artifacts 管线证明了用户期望 LobsterAI 成为一个更强的 AI 工作空间（AI Workspace），具备复杂的页面渲染与预览能力。
- **技能编排系统重构（高优先）**: `#1440` / `#1445` 表明当前技能系统无论是 UI 展示还是稳定性校验（重复导入）都存在严重不足，社区希望看到一个更健壮、交互更合理的技能系统。
- **MCP Server 精细打磨**: 随着 MCP 功能的深度使用，其弹窗交互等问题开始显现，精细化体验是必然趋势。

## 7. 用户反馈摘要
- **“升级就崩，不知所措”** (`#1443`): “之前升级到openclaw v2026.3.24，官方的release说明有breaking change，我本地尝试了会报错，拉不起来。我们有计划适配openclaw新版本吗？” —— 这是典型的**生态依赖断裂**，用户非常焦虑。
- **“功能 Work，但逻辑不通”** (`#1439`, `#1442`): 用户报告“关闭技能，在对话中使用技能关键字”，以及质疑“agent选择技能的作用是什么？” 这说明功能的实现细节未能达到用户的心理模型预期，存在设计沟通鸿沟。
- **“无反馈，硬崩溃”** (`#1437`): 用户面对静默按钮（点击无反应）感到受挫，这损害了软件的可信度。
- **贡献者反馈（隐式）**: 从 PR `#1440/1441` 长期未被处理来看，社区贡献者正在经历“提交即石沉大海”的周期，这是 OSS 项目最危险的信号之一。

## 8. 待处理积压
以下 Issue 和 PR 已被 Stale Bot 标记（更新于 2026-06-13），即将被机器人自动关闭。**强烈建议维护者优先审阅**，以免核心贡献付诸东流。

**核心高危积压：**

| 编号 | 类型 | 标题 | 状态 | 最后活跃 | 链接 |
|:---|:---|:---|:---|:---|:---|
| #1443 | Issue | 有计划支持新版本的openclaw吗？ | **Stale** | 2026-06-13 | [查看](https://github.com/netease-youdao/LobsterAI/issues/1443) |
| #1437 | Issue | 创建定时任务按钮无响应 | **Stale** | 2026-06-13 | [查看](https://github.com/netease-youdao/LobsterAI/issues/1437) |
| #1439 | Issue | 上传技能已停用，对话中仍然可以调用 | **Stale** | 2026-06-13 | [查看](https://github.com/netease-youdao/LobsterAI/issues/1439) |
| #1442 | Issue | Agent添加技能，对话后引用的技能不展示 | **Stale** | 2026-06-13 | [查看](https://github.com/netease-youdao/LobsterAI/issues/1442) |
| #1441 | PR | Artifacts 扩展预览管线 | **Stale** | 2026-06-13 | [查看](https://github.com/netease-youdao/LobsterAI/pull/1441) |
| #1440 | PR | 技能标签UI移至输入框内顶部 | **Stale** | 2026-06-13 | [查看](https://github.com/netease-youdao/LobsterAI/pull/1440) |
| #1445 | PR | 技能重复导入校验及修复 | **Stale** | 2026-06-13 | [查看](https://github.com/netease-youdao/LobsterAI/pull/1445) |

**总结：** 项目正处于一个关键的 **“沟通与清理”窗口期**。大量的历史债务（尤其是 OpenCLAW 兼容性和 Artifacts 巨型 PR）处理得当将极大提振社区士气；处理不当则可能导致社区生态萎缩。建议尽快针对 4 月的积压发起一轮集中的打版冲刺。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是根据您提供的 Moltis GitHub 数据生成的 2026-06-14 项目动态日报。

---

# Moltis 项目动态日报 | 2026-06-14

## 1. 今日速览

今日 Moltis 项目呈现出快速的“问题发现-修复响应”闭环，活跃度维持在较高水平。社区报告了一个影响主流 MCP 服务集成的严重 OAuth Bug，并由同一贡献者在短时间内提交了修复 PR，展现了社区极高的参与度和响应效率。与此同时，项目在 Docker 部署健壮性及前端构建依赖方面也有持续的清理和自动化更新。整体来看，项目核心开发方向明确，工程维护质量稳定，健康状况良好。

## 2. 项目进展

今日项目虽无 PR 被正式合并，但 3 个开放的 PR 清晰指明了当前核心推进方向：

-  **核心 Bug 修复**：针对阻塞用户接入 Notion/Linear 等服务的 OAuth 故障，贡献者已提交具体的解决方案，等待代码审查与合并。
-  **Docker 部署优化**：修复了 Dockerfile 中 `VOLUME` 指令与宿主机目录挂载冲突的“病理”现象，提升了容器化部署的体验。
-  **依赖自动化维护**：由 Dependabot 发起的例行依赖更新提升了项目的工程安全性。

## 3. 社区热点

今日社区讨论高度集中。唯一的 Bug 报告 **Issue [#1119](moltis-org/moltis Issue #1119)** 承担了全部的关注热度。

-   **热度分析**：该链接了外界认为最活跃的两个 MCP 服务商（Notion, Linear），用户对这写服务的集成诉求非常迫切。该 Issue 在数小时内即获得了开发者的跟进，并迅速有对应的修复 PR (#1120) 提出，这说明项目团队对阻碍核心体验的优先级判断非常明确。
-   **用户诉求**：用户期望 Moltis 能无痛兼容所有标准的第三方 MCP 服务，尤其是在处理非标准的 `WWW-Authenticate` 头部参数时，流程需要足够健壮。

## 4. Bug 与稳定性

今日报告了一个严重 Bug，但已有修复 PR 跟进。

-   **[严重] MCP OAuth 认证失败（Notion/Linear）**
    -   **问题描述**：Issue [#1119](moltis-org/moltis Issue #1119) 指出，当 MCP 服务器（如 Notion、Linear）在 OAuth 流程的 `WWW-Authenticate` 响应头中包含 `resource_metadata` 属性时，Moltis 的 `discover_and_register()` 流程会将此 URL 传递给 `fetch_resource_metadata()` 函数，导致浏览器端 OAuth 授权失败，抛出 `invalid_target` 错误。这属于一个 OAuth 流程中的边缘情况兼容问题。
    -   **影响范围**：严重。直接导致用户无法添加 Notion、Linear 等主流 MCP 服务器。
    -   **修复状态**：**已有 Fix PR**。同一用户（@xzavrel）提交了 PR [#1120](moltis-org/moltis PR #1120)，策略是调整对 `resource_metadata` URL 的处理方式，直接进行 fetch 而非依赖于当前的解析逻辑。该 PR 目前等待合并。

## 5. 功能请求与路线图信号

今日数据中未包含明确的新功能请求信号。

不过，**PR [#1122](moltis-org/moltis PR #1122)** 是一个值得关注的工程改进信号。该 PR 专门修复了 Docker 部署中 `VOLUME` 指令导致宿主机绑定的宿主目录被“遮蔽”（shadow）的问题。这表明项目正在关注更为精细的**部署与运维体验**。对于面向个人的 AI 助手项目，降低自部署难度和解决生产环境问题是提升用户满意度的重要环节，这很可能成为下一阶段稳定性的关注点。

## 6. 用户反馈摘要

-   **用户画像**：来自 Issue [#1119](moltis-org/moltis Issue #1119) 的用户 @xzavrel 属于典型的“贡献型用户”。
-   **核心痛点**：“特定（且非常常用的）MCP 服务器在 OAuth 添加流程中完全不可用”，浏览器出现了具体的错误 JSON 提示。
-   **行为反馈**：该用户不仅详细报告了 Bug 发生的具体步骤和错误信息，还直接动手编写了修复代码并提交了 PR。这种行为代表了社区中最具生产力的用户群体，他们对项目的期望很高，同时也愿意投入精力改善项目。

## 7. 待处理积压

根据过去 24 小时的数据快照进行分析，所有活跃的 Issue (#1119) 和 PR (#1120, #1121, #1122) 均处于新建或被快速更新状态。

-   **Issue #1119（创建于 2026-06-13）**：已于 14 日被修复 PR 跟进，响应周期不足 24 小时，无积压风险。
-   **PRs 状态**：均为创建于 13 日或 14 日的新 PR，处于等待审查状态，属于正常的开发周期流转。

综上所述，今日数据中未发现长期未响应、需要特别提醒维护者关注的积压项。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，这是根据 CoPaw（QwenPaw）项目 2026-06-13 至 2026-06-14 数据生成的每日项目分析日报。

---

# CoPaw / QwenPaw 项目动态日报 | 2026-06-14

## 1. 今日速览
项目 24 小时内活跃度较高，共产生 **16 条** 有效更新（8 Issues + 8 PRs）。社区贡献者 `ly-wang19` 成为今日亮点，持续提交了针对边缘 Case 的系统级 Bug 修复 PR，展现了良好的外部贡献生态。不过，核心稳定性挑战依然严峻：**对话挂起（Task Hang）** 和 **桌面端性能退化** 成为用户集中吐槽的两个痛点，项目正处于 **功能多元化扩展** 与 **核心稳定性修复** 并重的阶段。

## 2. 版本发布
今日无新版本发布。

## 3. 项目进展
今日有 **1 个长期 PR** 完成合并关闭：

- **PR #2498 - `fix(agents): use console language when creating agent and fallback unsupported langs`**
  - **状态**：已合并/关闭（从 2026-03-29 开放至 2026-06-13）
  - **贡献者**：`Alneys`
  - **分析**：该 PR 解决了 Agent 创建时语言选择的硬编码问题。此前新建 Agent 会默认使用英语/中文，忽略用户的 UI 语言偏好。现在 Agent 创建时会正确读取控制台语言设置，并对不支持的语言进行优雅降级（fallback to English）。这是项目国际化（i18n）的一项重要基础设施完善。
  [查看 PR](agentscope-ai/QwenPaw PR #2498)

## 4. 社区热点
- **最大情绪爆发点：Issue #5172** “聊天总出现问完问题没反应一直等待”
  - 用户情绪明显沮丧，指出该 Bug（对话挂起）长期存在且影响极广。一旦聊完间隔一段时间再提问，模型会永久等待，必须手动点击“停止”。用户特别强调，在 QQ/微信渠道上无法点击停止，直接导致 Agent “死亡”。该问题触及 **核心对话流的可用性**，虽评论数不多，但严重性极高。
  [查看 Issue](agentscope-ai/QwenPaw Issue #5172)

- **最高效贡献者焦点：`ly-wang19`**
  - 该贡献者今日提交并持续活跃了 6 个 PR，覆盖了 `local_models`、`crons`、`config`、`backup`、`context`、`agents` 模块。这种系统性扫除 Bug 的行为是项目健康状况的强心剂，但目前这些 PR 均处于“待审核”状态，审核速度和效率成为社区关注的潜在瓶颈。
  [查看系列 PR](agentscope-ai/QwenPaw PR #5035) | [#5040](agentscope-ai/QwenPaw PR #5040) | [#5037](agentscope-ai/QwenPaw PR #5037) | [#5041](agentscope-ai/QwenPaw PR #5041) | [#5038](agentscope-ai/QwenPaw PR #5038) | [#5170](agentscope-ai/QwenPaw PR #5170)

- **新兴区域市场需求：越南语界面 & Zalo 机器人**
  - **Issues #5169** 和 **#5168** 分别提出添加 **越南语（vi）界面** 和 **Zalo Bot 官方渠道支持**。两位发起人均来自越南社区。这表明 CoPaw 在东南亚（尤其越南）拥有活跃的潜在用户群，并且该社区正在积极寻求本地化落地。
  [查看 Issue #5169](agentscope-ai/QwenPaw Issue #5169) | [Issue #5168](agentscope-ai/QwenPaw Issue #5168)

## 5. Bug 与稳定性
按严重程度排列今日修复与报告：

| 严重度 | Issue / PR | 描述 | 是否有修复 PR |
| :--- | :--- | :--- | :--- |
| **🔴 致命** | **#5172** | **对话挂起/等待**：核心通信线程阻塞，需手动干预。直接导致非 GUI 渠道（QQ/WeChat）不可用。 | 否（紧急待办） |
| **🔴 致命** | **#5171** | **上下文压缩导致信息完全丢失**：当人设文件超过 Token 阈值时，压缩算法将所有上下文清空，导致 Agent 失忆、任务中断。 | 否 |
| **🟠 高** | **#5047** | **Windows Tauri 桌面端启动极慢**：启动时间从原本的 1-2 分钟退化到 10-20 分钟，且经常无响应。严重影响 Windows 用户体验。 | 否 |
| **🟠 高** | **#5174** | **Cron/心跳机制缺陷**：Cron Agent 无法执行 `write_file`和 `spawn_subagent`，导致无法自动化执行知识文件生成等复杂任务。 | 否 |
| **🟢 中/低** | **PR #5035** | Llama.cpp 版本号硬编码切片已修复 | 是（待合并） |
| **🟢 中/低** | **PR #5037** | Linux 浏览器检测空行 `IndexError` 已修复 | 是（待合并） |
| **🟢 中/低** | **PR #5038** | 空消息列表引发的 `IndexError` 已修复 | 是（待合并） |
| **🟢 中/低** | **PR #5040** | 单个 Cron 错误导致全部任务失败已修复 | 是（待合并） |
| **🟢 中/低** | **PR #5041** | 不可读文件导致全备份失败已修复 | 是（待合并） |

## 6. 功能请求与路线图信号
- **极高概率纳入（社区已PR）**：**越南语界面 (#5169)**。
  - 同主题的 **PR #5175** 已由 `nguyenthanhthe` 提交。基于成熟的 i18n 框架，只要无重大文本冲突，预计很快可合并。
- **高价值路线参考**：**Kimi-for-Coding / uv 白名单 (#5156)**。
  - 用户希望将已付费的 Kimi Coding 订阅直接接入，并希望加入 uv 白名单。这释放了一个强烈信号：**用户希望将个人付费的高级模型能力直接“搬进” CoPaw**。团队可能需要评估非官方 API 集成的合规性风险与社区需求之间的平衡。
- **值得关注的生态扩展**：**Zalo Bot 支持 (#5168)**。
  - 若采纳，CoPaw 将成为越南市场第一个大型开源 Agent 平台，具有显著的先发优势。

## 7. 用户反馈摘要
- **核心痛点**：
  - **稳定性信仰危机**：用户 `kfrtiamo` 对 #5172 表达的强烈不满（“这么严重问题竟然一直存在”），说明核心聊天稳定性正在消耗用户的耐心。
  - **性能退化**：Windows 用户抱怨 Tauri 迁移带来的巨大性能回退，有用户表示从“能用”变为“几乎无法使用”（#5047）。
- **使用场景**：
  - **生产级自动化**：用户正在尝试利用 Cron/心跳机制执行真实的文件合并和知识产出的工作流（#5174）。
  - **跨平台 Hub**：用户希望 CoPaw 能作为统一后端，同时对接 QQ、微信、Zalo 等不同平台。
- **满意点**：
  - 贡献者 `ly-wang19` 的系列高质量修复 PR 获得了社区默认的认可（无负面反馈即是认可），说明项目代码质量趋势向上。用户对项目“被积极维护”有信心。

## 8. 待处理积压
- **⚠️ 紧急关注（Bug 响应）**：
  - **#5172** 对话挂起：这是最高优先级的告警，建议维护者立即组织复现和热修复（Hotfix）。
  - **#5047** Tauri 启动慢：建议成立专项组，排查是文件系统 IO 还是框架初始化问题。
- **⏳ 长期待办（社区贡献审核）**：
  - `ly-wang19` 的 **5 个修复 PR**（#5035、#5037、#5038、#5040、#5041）自 **2026-06-09** 起就已提交并标记为 “Under Review” 及 “First Time Contributor”。**至今已等待 5 天且无任何交互**。这极有可能打击一个高产新贡献者的热情。建议核心维护者尽快安排 Code Review，合并其中明显正确的修复。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目日报 — 2026-06-14

---

## 今日速览

过去 24 小时，ZeroClaw 维持了**极高活跃度**：共处理 42 条 Issue 更新（26 条新开/活跃，16 条关闭）和 50 条 PR 更新（45 条待合并，5 条已合并/关闭）。社区讨论集中在 **Dream Mode 记忆巩固**、**MCP 工具权限设计**、**Web 多会话支持**以及**可观测性增强**等方向；多个严重 Bug（如 WS 通道 `ask_user`失效、canvas 回归）已有或正在提交修复。项目本周未发布正式版本，但架构类 RFC（统一 Agent 引擎）已完成执行，整体处在功能密集开发与积压清理并行的阶段。

---

## 版本发布

无新版本发布（Releases 列表为空）。

---

## 项目进展

过去 24 小时内共有 **5 个 PR 被合并或关闭**（具体列表未在热点条目中体现），同时多个与之关联的 Issue 被标记为已关闭，标志着以下功能或修复已落地：

- **统一 Agent 三个 turn 引擎** —— RFC [#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) 已执行，对应合并 PR #7540 完成，三个 agent 执行路径（`run_tool_call_loop` + `turn_streamed` + `Agent::turn`）整合为单一流程，降低了后续维护成本。
- **MCP 工具权限设计澄清** —— [#6876](https://github.com/zeroclaw-labs/zeroclaw/issues/6876) 已关闭，`risk_profile.allowed_tools` 对 MCP 工具的约束行为现在通过文档明确为“默认不限制”，同时修复 PR [#7547](https://github.com/zeroclaw-labs/zeroclaw/pull/7547) 提供了自动包含的选项。
- **WhatsApp Web 渠道修复** —— Bug [#6223](https://github.com/zeroclaw-labs/zeroclaw/issues/6223)（`web_fetch` 不可用）已关闭，渠道集成稳定性提升。
- **Zerocode TUI 体验修复** —— [#7378](https://github.com/zeroclaw-labs/zeroclaw/issues/7378)（Cmd-C 误触退出）和 [#7377](https://github.com/zeroclaw-labs/zeroclaw/issues/7377)（暗色主题可读性）均已关闭，终端用户交互更友好。
- **自动测试与 Quickstart 健壮性** —— [#7509](https://github.com/zeroclaw-labs/zeroclaw/issues/7509)（Windows 自测失败）和 [#7507](https://github.com/zeroclaw-labs/zeroclaw/issues/7507)（非 TTY 无限重绘）被关闭。

此外，**多个大型功能 PR 仍在积极推进**，如 Dream Mode ([#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693))、OTel 可观测性 ([#7570](https://github.com/zeroclaw-labs/zeroclaw/pull/7570))、多数据库会话后端 ([#6893](https://github.com/zeroclaw-labs/zeroclaw/pull/6893)) 等，项目整体处于功能扩展区间。

---

## 社区热点

#### 讨论最活跃的 Issues

| Issue | 标题 | 评论数 | 关注点 |
|-------|------|--------|--------|
| [#5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849) | Dream Mode — Periodic Memory Consolidation & Reflective Learning | **18** |  社区对长期记忆机制高度关注，讨论从架构设计到实现细节（5 阶段引擎、LLM 辅助反思），是实现持续学习能力的核心需求。 |
| [#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) | RFC: Unify the three agent turn engines | 5 |  尽管已关闭，前期积累了大量关于 agent 执行路径统一的设计讨论，最终以单 PR 执行，体现了社区对架构简化的认同。 |
| [#5470](https://github.com/zeroclaw-labs/zeroclaw/issues/5470) / [#5570](https://github.com/zeroclaw-labs/zeroclaw/issues/5570) | 运行时安全 / SQLite 向量搜索加速 | 5+5 |  曾有多轮技术讨论，用户对 S2 级别的退化行为和 O(n) 搜索性能提出改进要求，现均已关闭（部分因长期无响应）。 |

#### 持续活跃的 Pull Requests

- **Dream Mode** ([#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693))：与 #5849 对应，已积压近一月，最新更新在 06-14，显示作者仍在推动。
- **OTel 内存操作插桩** ([#7570](https://github.com/zeroclaw-labs/zeroclaw/pull/7570))：06-13 新开，替代冲突的 #6190，立即获得社区关注，有望增强运行时可观测性。
- **每轮输出路由与语音修复** ([#7361](https://github.com/zeroclaw-labs/zeroclaw/pull/7361))：影响 Slack、Telegram、Discord 等多渠道，评论热度高，是集成层面的重要改进。
- **修复 MCP 工具自动包含** ([#7547](https://github.com/zeroclaw-labs/zeroclaw/pull/7547))：与 #6876 直接相关，解决了用户配置后工具不可见的痛点。

**诉求分析**：社区当前最迫切的需求集中在**记忆持久化**、**渠道体验一致性**、**调试与监控能力**三个方向，且对架构统一（如 agent 引擎、插件系统）抱有期待。

---

## Bug 与稳定性

过去 24 小时报告的 Bug 按严重程度排列：

| 严重度 | Issue | 描述 | 状态 |
|--------|-------|------|------|
| **S1 – 工作流阻塞** | [#7563](https://github.com/zeroclaw-labs/zeroclaw/issues/7563) | canvas-store 回归：Web UI `/canvas` 页面在 WS 聊天后变为空白，关联 #6986 | OPEN，暂无修复 PR |
| | [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) | `ask_user` 在网关 WebSocket 会话中立即失败“Channel closed” | OPEN，**已有修复 PR [#7588](https://github.com/zeroclaw-labs/zeroclaw/pull/7588)** |
| | [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | macOS app 无法检测权限，窗口消失 | OPEN，blocked |
| | [#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523) | Web Dashboard 不可用（0.8.0 brew 安装） | OPEN，需构建前端 |
| **S2 – 降级行为** | [#7591](https://github.com/zeroclaw-labs/zeroclaw/issues/7591) | 无效 agent 别名未在 quickstart 中验证，导致用户输入丢失 | OPEN（今天新开） |
| | [#7521](https://github.com/zeroclaw-labs/zeroclaw/issues/7521) | `file_read` 无法解码非 UTF-8 文本，返回乱码 | OPEN |
| | [#7377](https://github.com/zeroclaw-labs/zeroclaw/issues/7377) | 暗色主题可能在浅色终端下不可读（已关闭） | ✅ CLOSED |
| **S3 – 小问题** | [#7509](https://github.com/zeroclaw-labs/zeroclaw/issues/7509) | 自测在 Windows 主机失败（已关闭） | ✅ CLOSED |

**值得注意的修复进展**：  
- [#7588](https://github.com/zeroclaw-labs/zeroclaw/pull/7588) 和 [#7587](https://github.com/zeroclaw-labs/zeroclaw/pull/7587) 直接定位 #7542 和 #7551，两个 PR 均在 06-14 提交，显示维护者对 WS 审批通道问题响应迅速。
- [#7547](https://github.com/zeroclaw-labs/zeroclaw/pull/7547) 针对 #6876 的设计 gap 提供了自动包含 MCP 工具的机制，虽不是纯 bug 修复，但解决了实际配置困扰。

---

## 功能请求与路线图信号

以下新提出的增强需求（标记 `enhancement`）反映了社区对下一版本的期待，部分已有对应 PR 或 RFC：

| Issue / PR | 功能描述 | 实现状态 | 纳入可能性 |
|------------|----------|----------|------------|
| [#5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849) / [#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693) | Dream Mode：周期性记忆巩固与反思学习 | PR 开放中，需作者更新 | 🟡 高（v0.8.1 候选） |
| [#7543](https://github.com/zeroclaw-labs/zeroclaw/issues/7543) | Web 聊天多会话支持（侧边栏增删改） | 仅 Issue，无 PR | 🟡 中（UI 层刚需） |
| [#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531) | 为中国渠道（QQ/钉钉/微信/飞书）增加流式卡片消息 | 仅 Issue | 🟢 可能被纳入集成队列 (Tracker #6970) |
| [#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539) | llama.cpp 模型快速切换路由 | 仅 Issue | 🟡 中（local 模型用户呼声高） |
| [#7521](https://github.com/zeroclaw-labs/zeroclaw/issues/7521) | `file_read` 自动编码检测（cp1251/Shift-JIS 等） | 仅 Issue | 🟢 容易实现，依赖 charset 库 |
| [#7518](https://github.com/zeroclaw-labs/zeroclaw/issues/7518) | WhatsApp 添加消息反应支持（`ack_reactions`） | 仅 Issue | 🟢 与其他渠道对齐 |
| [#7514](https://github.com/zeroclaw-labs/zeroclaw/issues/7514) | 允许 delegate 工具使用不同风险配置的子 agent | 已接受，无 PR | 🟡 中（安全架构增强） |
| [#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497) | RFC：OCI 容器注册表作为 WASM 插件存储 | RFC 待维护者审核 | 🟡 长期架构方向 |
| [#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420) | RFC：原生动态库插件系统 | RFC 待维护者审核 | 🟡 长期架构方向 |
| [#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289) | 提示用户安装缺失技能/插件 | 已接受 | 🟢 提升发现性 |
| [#7570](https://github.com/zeroclaw-labs/zeroclaw/pull/7570) | OTel GenAI spans 记录 prompt/completion 内容 | PR 开放 | 🟢 调试利器，预计合并 |
| [#6893](https://github.com/zeroclaw-labs/zeroclaw/pull/6893) | 多数据库会话后端（Postgres/Oracle/MySQL/Db2） | PR 开放 | 🟡 面向多机部署 |

**路线图信号**：短期内可观测性（#7570， #6966）和渠道体验补齐（#7518, #7531）最可能被优先合并；架构层面，**插件存储与发现机制**（#7497, #7420）正在形成 RFC 讨论，可能为 v0.9 铺垫。

---

## 用户反馈摘要

从过去 24 小时的 Issue 描述与标签中提炼出以下真实用户声音：

- **对本地模型友好**：“llama.cpp 在小任务上非常有用，但模型固定在默认配置，希望能快速切换不同模型。”（#7539）
- **Web UI 易用性待改进**：“Dashboard 一片空白，构建前端太复杂；多会话管理缺失，每次只能一个对话。”（#7523, #7543）
- **macOS 原生支持急需**：“安装后窗口消失，权限检测失败，无法使用。”（#7527）
- **文档与实际行为不符**：“`allowed_tools` 配置对 MCP 无效，必须改设计还是文档漏了？”（#6876）
- **Quickstart 流程折磨**：“只是输错一个别名就要从头再来，太浪费时间。”（#7591）
- **文件读取硬伤**：“读取 Windows-1251 编码的文本全是乱码，这个工具对非英语用户基本不能用。”（#7521）
- **中国渠道用户等待焦虑**：“QQ/钉钉发送卡片消息时用户要等很久，没有流式反馈。”（#7531）

正面反馈方面，用户对 **Dream Mode**（#5849）表现出浓厚兴趣，认为“这正是 AI 助手需要的自主学习能力”；**OTel 可观测性**的改进（#7570）也获得好评，认为“终于能看清 prompt 和 response 了”。

---

## 待处理积压

以下 Issue/PR 长期未获得回应或处于停滞状态，提醒维护者关注：

#### 需要作者操作（needs-author-action / stale-candidate）
| 编号 | 标题 | 等待时间 | 备注 |
|------|------|----------|------|
| [#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693) | feat(memory): dream mode | 自 2026-05-16 开放，近 30 天 | 与 #5849 对应，作者需回应 review |
| [#5779](https://github.com/zeroclaw-labs/zeroclaw/pull/5779) | feat(security): TOTP gate for shell (phase 1) | 自 2026-04-15 开放，超 60 天 | 安全增强，被多次催促 |
| [#6190](https://github.com/zeroclaw-labs/zeroclaw/pull/6190) | feat(obs): instrument runtime memory ops with OTel | 自 2026-04-28，被 #7570 取代 | 建议关闭或标记 superseded |
| [#5892](https://github.com/zeroclaw-labs/zeroclaw/pull/5892) | fix(providers,runtime): three production blockers | 自 2026-04-19，stale-candidate | 涉及 vLLM 兼容性，需跟进 |
| [#6966](https://github.com/zeroclaw-labs/zeroclaw/pull/6966) | feat(obs): capture prompt/completion content | 自 2026-05-27，needs-author-action | 与 #7570 有重叠 |

#### 需要维护者审核（needs-maintainer-review）
| 编号 | 标题 | 提交时间 | 内容 |
|------|------|----------|------|
| [#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420) | RFC: Native Dynamic-Library Plugin System | 2026-06-09 | 微内核架构升级方案 |
| [#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497) | RFC: OCI-Compliant Container Registries as Plugin Storage | 2026-06-11 | WASM 插件分发机制 |

#### Blocked / 长期停滞
| 编号 | 标题 | 阻塞原因 |
|------|------|----------|
| [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | macOS app not work | 缺复现步骤，标记 blocked |
| [#5470](https://github.com/zeroclaw-labs/zeroclaw/issues/5470) | Multiple issues when running safely | 已关闭，但曾因缺复现信息 blocked 30+ 天 |

#### 持续关注的长期议题（no-stale）
- [#5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849) Dream Mode
- [#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289) 提示安装缺失技能
- [#6823](https://github.com/zeroclaw-labs/zeroclaw/issues/6823) / [#6826](https://github.com/zeroclaw-labs/zeroclaw/issues/6826) / [#6825](https://github.com/zeroclaw-labs/zeroclaw/issues/6825) Zerocode TUI 系列 Tracker

这些议题已持续活跃超过两周，社区期待维护者给出明确的时间表或决策。

---

**总结**：ZeroClaw 在 2026-06-14 依旧保持快速迭代节奏，Bug 响应积极（尤其是 WS 审批通道和 MCP 配置问题），功能需求多样且带有强烈的实际部署导向。下一步需关注 Dream Mode 等大型 PR 的合并进度，并清理一批长期搁置的作者依赖项。项目健康度良好，但 macOS 与 Web Dashboard 的可用性问题若持续未解决，可能影响新用户留存。

*数据来源：ZeroClaw GitHub 仓库 (`github.com/zeroclaw-labs/zeroclaw`)，统计区间 2026-06-13 ~ 2026-06-14。*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*