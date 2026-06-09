# OpenClaw 生态日报 2026-06-09

> Issues: 500 | PRs: 473 | 覆盖项目: 13 个 | 生成时间: 2026-06-09 02:49 UTC

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

好的，这是根据 OpenClaw 项目 2026-06-09 的 GitHub 数据生成的日报。

---

# OpenClaw 项目动态日报 | 2026-06-09

## 1. 今日速览

过去 24 小时项目活跃度极高，共产生 **500 条 Issue 更新**（435 新开/活跃）和 **473 条 PR 更新**（144 合并/关闭）。两位 Beta 版本的发布聚焦于 QQ 渠道思维链泄露修复与 MCP 集成强化。然而，**安全注入风险、会话状态混乱、多 Agent 编排不稳定** 等 P1 级 Bug 成为社区讨论的焦点，反映出项目在高速迭代中面临的稳定性压力。整体项目健康度处于 **“功能快速推进，但安全与体验基座亟需夯实”** 的状态。

## 2. 版本发布

今日发布了两个 Beta 版本：

- **[v2026.6.5-beta.3](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5-beta.3)**
- **[v2026.6.5-beta.5](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5-beta.5)**

**核心亮点：**
- **QQ Bot 体验优化：** 修复了模型向 QQ 频道推送回复时，原生通信会泄露原始推理思维链（`<thinking>` 标签）的问题。感谢社区贡献者 @openperf。
- **MCP 工具结果类型强制：** 对 MCP 工具返回的结果进行更严格的类型一致性处理，涵盖了 `resource_link`、`resource`、`audio` 以及格式不正确的图片类型，减少了下游处理时的意外错误。

**迁移建议：** 涉及 QQ 渠道的部署建议立即升级以修复信息泄露隐患。

## 3. 项目进展：今日重要变更

**已合并/关闭的关键 PR（144 条）：**
- **架构与兼容性：**
  - **[`#91551`](https://github.com/openclaw/openclaw/pull/91551):** 修复 `config.patch` 数组替换的显式契约，拒绝未经确认的破坏性负载，增强了配置安全性与 Gateway、iOS 等客户端的兼容性。
  - **[`#90035`](https://github.com/openclaw/openclaw/pull/90035):** 修复 Node.js 23.0–23.10 运行 `openclaw doctor` 时的崩溃问题，扩大了运行时的支持范围。
- **渠道与 UI 修复：**
  - **[`#87474`](https://github.com/openclaw/openclaw/pull/87474):** 修复 Control UI WebChat 在回复结束后仍显示“进行中”状态的假忙问题。
  - **[`#88929`](https://github.com/openclaw/openclaw/issues/88929) 已关闭：** 修复飞书流式卡片模式下的打字效果异常与内容截断。
- **核心引擎修复：**
  - **[`#90856`](https://github.com/openclaw/openclaw/pull/90856):** 修复包含用户图片的会话在首次消息后因 Transcript 错误编辑而永久损坏的问题。
  - **[`#48300`](https://github.com/openclaw/openclaw/issues/48300) 已关闭：** 修复 `memory_search` 混合模式不返回 FTS 全文搜索结果的问题。
  - **[`#91526`](https://github.com/openclaw/openclaw/pull/91526):** 清理废弃的 async Kysely 驱动，简化 SQLite 堆栈。

**待合并/审核中的关键 PR（329 条待合并）：**
- **[`#91566`](https://github.com/openclaw/openclaw/pull/91566):** 修复主会话启动恢复的 Bug，确保守护进程重启后会话已就绪。
- **[`#91557`](https://github.com/openclaw/openclaw/pull/91557):** 大幅优化 iPad/iPhone 控制界面，这是项目向泛移动端体验迈进的重要一步。
- **[`#91500`](https://github.com/openclaw/openclaw/pull/91500):** 引入 QA 评分板分类验证，增强自动化测试的严谨性。
- **[`#90500`](https://github.com/openclaw/openclaw/pull/90500):** 修复移除 Provider 后残留的陈旧会话路由问题。

## 4. 社区热点

以下议题因用户痛点集中或讨论激烈而成为今日热点：

- **[`#90083`](https://github.com/openclaw/openclaw/issues/90083):** **OpenAI gpt-5.4/5.5 接口不兼容（15 条评论，P1）**
  - **诉求：** 升级 2026.6.1 后，调用最新的 OpenAI 模型失败（`invalid_provider_content_type`），直接导致核心推理功能不可用。大量用户被迫回滚或无法使用新模型，暴露了配置迁移流程的脆弱性。
- **[`#50090`](https://github.com/openclaw/openclaw/issues/50090):** **社区技能市场（ClawHub）的现实困境（15 条评论）**
  - **诉求：** 用户尖锐指出 ClawHub “承诺与现实之间存在巨大鸿沟”。当前技能系统缺乏完善的开发者体验、安全审查与分发机制，让期望通过社区生态扩展 Agent 能力的用户感到失望。
- **[`#45740`](https://github.com/openclaw/openclaw/issues/45740):** **gh-issues Skill 提示注入风险（13 条评论）**
  - **诉求：** GitHub Issue 的标题和正文被直接注入子 Agent 提示词，攻击者可通过提交恶意 Issue 控制 Agent 行为。社区对 Skill 安全沙箱的缺失表达了强烈担忧。
- **[`#32296`](https://github.com/openclaw/openclaw/issues/32296):** **Agent 会话上下文错乱（14 条评论，P1）**
  - **诉求：** Agent 总是回复上一条消息而非当前消息，导致对话逻辑彻底错位。这是影响日常使用基础体验的高频 Bug。

## 5. Bug 与稳定性

**严重（P1，影响安全/数据/会话）：**
- **安全注入与信息泄露：**
  - **[`#45740`](https://github.com/openclaw/openclaw/issues/45740):** gh-issues Skill 提示注入攻击。
  - **[`#44905`](https://github.com/openclaw/openclaw/issues/44905):** Discord 渠道泄露内部工具调用详情给普通用户。
  - **[`#49876`](https://github.com/openclaw/openclaw/issues/49876):** Cron 任务在工具失败时产生幻觉输出，构成信任安全问题。
  - **[`#51396`](https://github.com/openclaw/openclaw/issues/51396):** `clearUnboundScopes` 无条件剥离 Operator 权限，导致后端 API 调用失败。
- **会话与数据丢失：**
  - **[`#48573`](https://github.com/openclaw/openclaw/issues/48573)** / **[`#47975`](https://github.com/openclaw/openclaw/issues/47975):** 子 Agent（Subagent）产生僵尸状态或持久残留，导致主会话无响应。
  - **[`#48003`](https://github.com/openclaw/openclaw/issues/48003):** Steer 模式消息注入无效，用户无法干预模型运行中的中间过程。
  - **[`#43367`](https://github.com/openclaw/openclaw/issues/43367):** 多 Agent 编排全面不稳定，包括并发添加覆盖配置、会话锁失败等。

**回归与一般 Bug：**
- **[`#32473`](https://github.com/openclaw/openclaw/issues/32473):** Control UI 要求 HTTPS 安全上下文（Regression，已 Stale 3 个月）。
- **[`#51429`](https://github.com/openclaw/openclaw/issues/51429):** 代码中存在硬编码的工作路径（`/Users/wangtao`），典型代码审查失守案例。
- **[`#43747`](https://github.com/openclaw/openclaw/issues/43747):** 记忆系统管理混乱（不同用户存储位置不一致，更新行为迥异）。
- **[`#45765`](https://github.com/openclaw/openclaw/issues/45765):** 设置 `OPENCLAW_HOME` 环境变量后产生嵌套目录。
- **[`#50442`](https://github.com/openclaw/openclaw/issues/50442):** `backup create` 超时后残留大文件，可能导致磁盘空间耗尽。

**已有 Fix PR 的 Bug：**
- `#90007` (Node 23 兼容) -> `#90035` **已合并**
- `#90760` (图片数据损坏) -> `#90856` **已合并**
- `#91542` (Gemini 工具 Schema) -> `#91559` **审核中**

## 6. 功能请求与路线图信号

以下需求反映了社区对项目未来演进的强烈期待：

- **生态与安全体系完善：**
  - **[`#50090`](https://github.com/openclaw/openclaw/issues/50090):** ClawHub 生态基础设施。
  - **[`#45031`](https://github.com/openclaw/openclaw/issues/45031):** 内置技能安全扫描机制。
  - **[`#43260`](https://github.com/openclaw/openclaw/issues/43260):** 按 Skill 级别路由模型。
  - **[`#50199`](https://github.com/openclaw/openclaw/issues/50199):** 技能优先级配置。
- **Agent 控制力与成本管理：**
  - **[`#42475`](https://github.com/openclaw/openclaw/issues/42475):** Gateway 级别单 Agent 成本预算。
  - **[`#45608`](https://github.com/openclaw/openclaw/issues/45608):** 重置前自动运行 Agentic 内存刷新。
  - **[`#50739`](https://github.com/openclaw/openclaw/issues/50739):** 系统事件旁路队列优先投递。
  - **[`#78441`](https://github.com/openclaw/openclaw/pull/78441):** `sessions_spawn` 支持 `toolsAllow`（已进入审核）。
- **工具与开发体验：**
  - **[`#44431`](https://github.com/openclaw/openclaw/issues/44431):** Browser 工具 7 项改进（含 CSS 选择器支持）。
  - **[`#50291`](https://github.com/openclaw/openclaw/issues/50291):** 插件钩子需要完整的分布式追踪上下文。
  - **[`#42840`](https://github.com/openclaw/openclaw/issues/42840):** Control UI 支持 MathJax/LaTeX 富文本渲染（获赞 5）。
  - **[`#45758`](https://github.com/openclaw/openclaw/issues/45758):** 支持 YAML 配置文件。

## 7. 用户反馈摘要

- **对稳定性与安全性的焦虑：**
  > “After upgrading to OpenClaw 2026.6.1 and running the config/plugin migration, OpenAI/ChatGPT Responses inference fails...” (来自 `#90083`)
  > “Apparently some wangtao hardcode his working space path into the code... who is wangtao?” (来自 `#51429`)
- **对生态建设迟缓的不满：**
  > “The gap between promise and practice is wide right now.” (来自 `#50090`) 用户期望的是“活的 Agent 原语生态系统”，而现实是在使用体验上存在明显落差。
- **对文档与版本脱节的困惑：**
  > “Heartbeat IsolatedSessions is in the live docs but not in the latest version 2026.3.13.” (来自 `#48920`)
- **对渠道适配的肯定：**
  > “QQBot now strips model reasoning/thinking scaffolding...” 社区贡献者 @openperf 的工作获得了明确的致谢，表明社区驱动的渠道改进是深受欢迎的。

## 8. 待处理积压

以下为长期未响应或等待决策的重要议题，建议维护团队关注：

- **长期 Stale 的重要 Issue：**
  - **[`#32473`](https://github.com/openclaw/openclaw/issues/32473)**: Control UI 设备身份问题（Stale 3 个月，影响广泛）。
  - **[`#50090`](https://github.com/openclaw/openclaw/issues/50090)**: ClawHub 社区蓝图（Stale 3 个月，需官方路标回应）。
  - **[`#41744`](https://github.com/openclaw/openclaw/issues/41744)**: 飞书渠道图片丢失（未关闭，P1，Linked PR 待推进）。
  - **[`#42840`](https://github.com/openclaw/openclaw/issues/42840)**: MathJax 公式支持（高赞，等待产品决策）。

- **等待验证或作者响应的 PR：**
  - **[`#85823`](https://github.com/openclaw/openclaw/pull/85823)** / **[`#89034`](https://github.com/openclaw/openclaw/pull/89034)** / **[`#91423`](https://github.com/openclaw/openclaw/pull/91423)**: 均标记为 `needs-real-behavior-proof`，需要社区或 QA 提供实际落地用例验证。
  - **[`#88630`](https://github.com/openclaw/openclaw/pull/88630)**: 修复 Codex 本地模型的 Guardian 审批（等待作者更新）。
  - **[`#91500`](https://github.com/openclaw/openclaw/pull/91500) / [`#91557`](https://github.com/openclaw/openclaw/pull/91557) / [`#91566`](https://github.com/openclaw/openclaw/pull/91566)**: 三位重磅级的大型 PR 已标记为 `ready for maintainer look`，需核心维护者尽快审查以防止代码腐烂。

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析报告

**分析基准**：2026-06-09 社区动态数据  
**数据来源**：OpenClaw、NanoBot、Hermes Agent、PicoClaw、NanoClaw、IronClaw、LobsterAI、TinyClaw、CoPaw、ZeroClaw 等 12 个开源项目  
**声明**：以下分析完全基于各项目公开 GitHub 当日数据，侧重客观事实与数据趋势。

---

## 1. 生态全景

个人 AI 智能体/自主代理开源生态正经历 **爆发式增长与分化**。仅过去 24 小时，头部项目获数百条 Issue 与 PR 更新，功能迭代与安全修复并行。**安全、多 Agent 协作、MCP 标准化、渠道泛化是多数项目的共同攻关方向**，但技术路线已明显分野：部分项目向企业级零信任架构迁移，部分深耕桌面原生体验，亦有专注国内 IM 生态或轻量嵌入式场景的产品。**整体生态正从“单一对话助手”向“可编排、可对抗、可交互的通用数字代理”演进，但安全治理与基础体验仍是全行业短板。**

---

## 2. 各项目活跃度对比（2026-06-09）

| 项目 | Issues 更新（新开/活跃） | PR 更新（合并/关闭－待合并） | 版本发布 | 项目健康度（自评/综合） |
|------|--------------------------|-------------------------------|----------|--------------------------|
| **OpenClaw** | 500（435 新开/活跃） | 473（144 合并－329 待合并） | 2 Beta | 功能快速推进，安全与体验基座亟需夯实 |
| **Hermes Agent** | 50（46 新开/活跃，4 关） | 50（4 合并－46 待合并） | 无 | 严 bug、强功能，桌面/ macOS 问题高发 |
| **IronClaw** | 34（更新） | 50（更新，多合并） | 无 | 高活跃度，Reborn 架构换代攻坚期 |
| **ZeroClaw** | 50（更新） | 50（多重大修复合并） | 无 | 密集迭代与安全加固并行，数据损坏修复 |
| **CoPaw (QwenPaw)** | 38（更新） | 41（22 合并/关闭） | 无 | Bug 修复响应迅速，生态建设步入快车道 |
| **NanoBot** | 7（3 新开，4 关） | 36（16 合并－20 待合并） | 无 | 快速功能集成期，维护者响应高效 |
| **PicoClaw** | <5（热点追踪） | 19（9 合并－10 待合并） | Nightly 1 | 高强度迭代，代码质量攻坚 |
| **LobsterAI** | 0（新开） | 17（17 合并/关闭） | 无 | 代码健康度与功能完成度大幅提升 |
| **NanoClaw** | 1（新开） | 3（2 合并－1 待合并） | 无 | 安全加固落地，核心功能冒烟 |
| **TinyClaw** | 0 | 1（0 合并） | 无 | 维护与基础体验打磨期 |
| **NullClaw / Moltis / ZeptoClaw** | 0 | 0 | 无 | 过去 24h 无活动 |

---

## 3. OpenClaw 在生态中的定位

**社区规模绝对领先**：单日 500+ Issue、470+ PR，远超其他项目，反映出其用户基数与贡献者网络庞大。

### 核心优势
- **渠道覆盖最广**：QQ Bot、飞书、Discord、WebChat 等均有针对性修复，且由社区贡献者高效驱动。
- **MCP 集成深度**：率先强化工具结果类型强制与类型一致，引领 MCP 实践。
- **配置安全创新**：`config.patch` 显式契约、Gateway 无破坏性负载拒绝，体现安全设计前移思路。

### 当前短板
- **稳定性欠账**：P1 级安全注入、会话混淆、多 Agent 编排不稳定等问题集中爆发，用户反馈“升级后核心功能不可用”。
- **生态兑现滞后**：ClawHub 被社区指责“承诺与现实的鸿沟”，开发者体验与安全审查机制缺位。  
- **配置迁移脆弱**：OpenAI 新模型兼容断层暴露配置升级流程缺陷。

### 同类差异化
相较于 NanoBot 偏重语音/跨 Agent 总线、Hermes 偏重桌面原生、CoPaw 偏重国内 IM 与 AgentScope，**OpenClaw 试图做“全能型”平台**，但“全能”也意味技术债面更宽。若能在安全加固与体验一致性上补齐短板，其社区网络效应将产生巨大护城河。

---

## 4. 共同关注的技术方向

从多项目高频议题中提炼出五大交叉热点：

### 🔐 安全治理与沙箱强制
- **OpenClaw** — gh-issues Skill 提示注入（#45740），Discord 泄露工具调用
- **NanoBot** — 符号链接工作空间逃逸修复（#4221），MCP SSRF 风险（#4074）
- **Hermes Agent** —  声明式技能保护策略（#27997），认证路径测试失守（#42130）
- **NanoClaw** — 四项安全修复 PR（#2714），Webhook 默认 0.0.0.0
- **ZeroClaw** — OIDC 认证 RFC（#7141），可插拔安全策略（#7142），高风险命令逐次确认（#7155）

**结论**：安全从“补丁模式”转向 **架构内置与默认安全**，是生态进入生产级的前置条件。

### 🤖 多 Agent 协作与编排
- **OpenClaw** — 多 Agent 全面不稳定（#43367），子 Agent 僵尸状态（#48573）
- **NanoBot** — 跨 Agent 消息总线合并（#3992）
- **Hermes** — `delegate_task` 上下文损坏（#42449）
- **CoPaw** — Subagent 无限轮询（#4873），MCP 进程堆积（#4834）

**结论**：多 Agent 复杂交互的场景需求迫切，但执行模型、共享上下文、生命周期管理仍是系统性难题。

### 🧠 记忆与上下文治理
- **OpenClaw** — `memory_search` 混合模式不返回 FTS（#48300），会话损坏（#90856）
- **Hermes** — 记忆满容量后死循环（#42405），MemoryStore 游标非单调（#4256）
- **CoPaw** — 内存压缩崩溃（#5019）
- **ZeroClaw** —  系统提示词过度强调记忆（#5844）

**结论**：记忆系统从“能不能存”进入 **“怎么准确、高效、可控地使用”** 阶段。

### 🔌 MCP 兼容与扩展
- **OpenClaw** — MCP 工具结果类型强制
- **NanoBot** — MCP HTTP/SSE SSRF 风险（#4074）
- **ZeroClaw** — `tool_filter_groups` 对 MCP 工具无效（#6699）
- **CoPaw** — MCP 工具名含`.`导致 GPT-5.5 调用失败（#4918）

**结论**：MCP 已成为 Agent 与外部工具的事实标准，但各项目对协议细节的理解与实现仍存在碎片化，生态亟需统一兼容性规范。

### 📱 多模态与桌面交互
- **NanoBot** — 文件/图片上传多模态分析需求（#4251）
- **Hermes** — Dashboard 图片粘贴失效（#24860），桌面文件浏览器 PR（#42534）
- **ZeroClaw** — 桌面交互支持 RFC（#6909）
- **CoPaw** — 独立视觉模型配置（#4992）

**结论**：从纯文本对话向 **“看、读、控制”** 的通用 Agent 进化是明确方向，但入口多样、技术栈分散。

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|------------------|
| **OpenClaw** | 全能型 AI 网关，覆盖多 IM、MCP、多Agent | 个人开发者/社区 | 模块化渠道、MCP 严格类型、配置契约 |
| **NanoBot** | 跨 Agent 协作 + 语音转录多提供商 | 多Agent工作流构建者 | 消息总线、转录全局化、OpenAI 兼容 extra_query |
| **Hermes Agent** | 桌面原生体验（macOS/Windows） | 桌面重度用户、设计师 | 原生 Dashboard、LaunchAgent、iMessage 集成 |
| **IronClaw** | 企业级 Reborn 架构迁移 | 企业运营、多租户 | “Reborn”路由层重构、Codex 自动解锁、RBAC 强化 |
| **ZeroClaw** | 安全零信任 + 物联网 | 高安全需求团队、IoT | Egress Lockdown、OIDC/可插拔安全、ESP32 模拟 |
| **CoPaw** | 国内 IM（微信、飞书）+ AgentScope 生态 | 国内开发者 | AgentScope 后端、插件前端扩展、微信深度适配 |
| **PicoClaw** | 轻量 / 边缘 / RISC-V | 嵌入式/边缘硬件用户 | Go 语言、低资源依赖、Nightly 构建 |
| **LobsterAI** | OpenClaw 桌面客户端（Tauri）+ 数据迁移 | OpenClaw 桌面用户 | 本地回环认证、备份迁移、Electron 升级线 |
| **TinyClaw** | 极简安装/最小Agent | 入门学习/轻量场景 | 小型代码库、Node.js + better-sqlite3 单文件部署 |
| **NanoClaw** | 企业安全网络隔离 | DevOps / 安全工程师 | Docker internal 网络、代理出口唯一 |

可以看出，生态已从“通用框架竞争”进入 **“场景垂深 + 架构分层”** 阶段：个人DIY、企业合规、桌面原生、边缘嵌入均有对应项目深耕。

---

## 6. 社区热度与成熟度分层

### 🔥 极高活跃期（日更新 > 30，功能与 Bug 密集交替）
- **OpenClaw, Hermes Agent, IronClaw, ZeroClaw, CoPaw**  
  这些项目吸引了大量贡献者，Issue/PR 吞吐量大，但同时 Bug 爆发频率也高，处于 **“边建边修”** 的快速迭代状态。其中 ZeroClaw 和 IronClaw 有明显重大架构级变更（RFC 与 Reborn），而 Hermes 则表现为桌面场景的精细打磨。

### 📊 中速增长期（日更新 10–30，集成与治理并重）
- **NanoBot, PicoClaw, LobsterAI**  
  NanoBot 功能积累均衡、维护者响应口碑好；PicoClaw 由社区主导代码质量控制；LobsterAI 集中清理技术债，健康度提升显著。三者均处于 **为下一阶段版本发布做质量储备** 的阶段。

### 🐢 低活动/基础巩固期（日更新 < 5）
- **NanoClaw, TinyClaw, NullClaw, Moltis, ZeptoClaw**  
  NanoClaw 虽低活动但合并了关键安全特性；TinyClaw 有单一但重要的安装体验 PR。整体处于 **功能稳定或维护停滞** 状态，但部分项目仍在关键点推进。

---

## 7. 值得关注的趋势信号

### 🛡️ “安全内建”从口号变为默认要求
超过半数项目在当日处理了安全相关议题，包括注入、逃逸、配置泄露、认证缺失。尤其 ZeroClaw 的 OIDC/可插拔安全 RFC 和 OpenClaw 的配置显式契约，标志安全正从补丁走向架构级内置。**AI 智能体开发者须将安全审查纳入 CI/CD 流程，并考虑沙箱设计。**

### 🧩 标准化协议（MCP / ACP / OpenAI API）竞争加速
OpenClaw、NanoBot、ZeroClaw 等都在对齐 MCP 或 OpenAI 兼容 API，但实现细节仍存在歧义。**统一兼容性规范与测试套件将成为生态成熟度的关键基础设施。**

### 📡 边缘/去中心化 Agent 成为新变量
PicoClaw 的 Delta Chat 网关提案、RISC-V 兼容诉求，以及 ZeroClaw 的 ESP32 物联网 Demo，显示 Agent 正在从 x86/ARM 云服务器向边缘设备和去中心化通信网络延伸。**这将带来受限环境下的执行优化与协议适配新课题。**

### 🖥️ 桌面多模态 Agent 成“新战场”
Hermes 的 iMessage 双工、ZeroClaw 的 Computer-use RFC、NanoBot 的文件上传分析需求，都指向 **Agent 获得“看屏幕、操作 UI、处理文件”能力** 的强烈意愿。这将是下一个竞争焦点，但需要突破安全控制与跨平台渲染瓶颈。

### 🔄 Agent 生命周期管理需求爆发
会话恢复、记忆治理、子 Agent 僵尸清理、Cron 任务可靠性（多个项目涉及）——用户期望 Agent 能自愈、可观测、可持续。**长期运行的 Agent 服务不再只是对话缓存问题，而是可管理、可审计的工程系统。**

### 👨‍👩‍👧‍👦 中文社区驱动的本地化 Agent 崛起
CoPaw（与支付宝/微信生态联动）以及 OpenClaw 中 QQ、飞书渠道的活跃贡献，反映国内开发者正在构建符合本土 IM 生态的 AI 助手。**本地化不再只是翻译，而是深度渠道与协议适配。**

---

*本报告基于 2026-06-09 各项目公开 GitHub 数据自动分析与整合。所有外部链接指向对应 Issue/PR 原文，数据因实时采集可能存在 1-2% 浮动。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目日报 (2026-06-09)

## 今日速览
- 过去 24 小时共更新 **7 个 Issue**（新开 3 个，关闭 4 个），处理 **36 个 Pull Request**（16 个合并/关闭，20 个待合并），项目活跃度维持高位。
- 本周无新版本发布，但功能积累密集：**三个语音转录提供商**（Xiaomi MiMo ASR、AssemblyAI、OpenRouter）和**跨 Agent 协作框架**完成合并，核心能力显著扩展。
- 安全与稳定性方面：**符号链接逃逸漏洞修复**、**会话历史孤儿 tool result 清理**等修复已入库；**Telegram 代码块分段错误**和**MemoryStore 游标非单调**等问题已有修复 PR 待合并。
- 社区讨论热点转向 **按会话切换模型**、**文件/图片上传多模态分析**，以及 **UI 版本显示**（已快速实现）。
- 整体看，项目正处于功能快速集成期，维护者响应迅速，测试与安全治理同步推进。

## 版本发布
（无）

## 项目进展
当日合并/关闭的 16 个 PR 中，以下对项目影响最为显著：

| 类别 | PR | 描述 |
|------|----|------|
| 架构 | [#3992](https://github.com/HKUDS/nanobot/pull/3992) （agent-collab） | **跨 Agent 消息总线**：允许多个 Nanobot 实例通过共享消息总线通信，为复杂多 Agent 工作流提供基础。状态：已合并 |
| 语音转录 | [#4224](https://github.com/HKUDS/nanobot/pull/4224) | 添加 **AssemblyAI** 转录提供商，丰富低延迟 STT 选项 |
| | [#4175](https://github.com/HKUDS/nanobot/pull/4175) | 添加 **Xiaomi MiMo ASR** 转录提供商，强化中文语音识别 |
| | [#4113](https://github.com/HKUDS/nanobot/pull/4113) | 添加 **OpenRouter** 转录提供商，可复用已有凭证，支持多模型路由 |
| | [#4232](https://github.com/HKUDS/nanobot/pull/4232) | **共享语音输入**：将 transcription 提升为顶层全局能力，WebUI/桌面/频道统一使用 |
| 提供商增强 | [#4217](https://github.com/HKUDS/nanobot/pull/4217) | 为 OpenAI 兼容提供商添加 `extra_query` 配置，解决 Azure 等网关需 `?api-version=` 参数的问题（Closes [#4204](https://github.com/HKUDS/nanobot/issues/4204)） |
| 安全与稳定性 | [#4221](https://github.com/HKUDS/nanobot/pull/4221) | 修复 `ExecTool` 中相对符号链接可逃逸工作空间的安全漏洞（Closes [#4072](https://github.com/HKUDS/nanobot/issues/4072)） |
| | [#4219](https://github.com/HKUDS/nanobot/pull/4219) | 修复会话历史裁剪后残留孤儿 tool result 的问题（Closes [#4203](https://github.com/HKUDS/nanobot/issues/4203)） |
| UI/UX | [#4235](https://github.com/HKUDS/nanobot/pull/4235) | WebUI **设置概览**增加版本号显示，并附带 PyPI 更新通知（1 小时缓存）（Closes [#4233](https://github.com/HKUDS/nanobot/issues/4233)） |

## 社区热点
根据当日评论与讨论活跃度，以下主题最受社区关注：

1. **按对话切换模型**：[Issue #4253](https://github.com/HKUDS/nanobot/issues/4253) 提出用户需在不同任务中灵活切换在线模型（OpenRouter）与本地模型（llamacpp），仅全局配置无法满足，评论反映了类似场景的普遍需求。目前无对应 PR，社区期待该功能进入路线图。

2. **文件/图片上传与多模态分析**：[Issue #4251](https://github.com/HKUDS/nanobot/issues/4251)（中文）请求在输入框上传图片或 PDF，并由 AI 解析内容（总结、识别等），明确表达了对多模态输入的渴望。虽无对应 PR，但信号较强，可能推动后续多模态支持。

3. **UI 版本显示快速落地**：用户 **[#4233](https://github.com/HKUDS/nanobot/issues/4233)** 提出在 WebUI 显示版本号的建议，同日即被 [#4235](https://github.com/HKUDS/nanobot/pull/4235) 实现并合并，展现了维护者对社区反馈的高效响应，获正面评价。

4. **Telegram 代码块分段错误**：[Issue #4250](https://github.com/HKUDS/nanobot/issues/4250) 报告长消息中包含围栏代码块时，`split_message` 会在代码块内部分割，导致两端格式损坏。修复 PR [#4257](https://github.com/HKUDS/nanobot/pull/4257) 已提交并待合并，社区关注度高。

## Bug 与稳定性
当日活跃的 Bug 相关条目按严重度排列：

| 严重程度 | 编号 | 描述 | 状态 |
|----------|------|------|------|
| **高** | [#4074](https://github.com/HKUDS/nanobot/issues/4074) | MCP HTTP/SSE 配置在 SSRF 拒绝前先尝试回环连接，存在安全风险 | 已关闭（修复已入库） |
| **高** | [#4221](https://github.com/HKUDS/nanobot/pull/4221) | 符号链接工作空间逃逸 | 已合并修复 |
| **中** | [#4250](https://github.com/HKUDS/nanobot/issues/4250) | Telegram 分段破坏围栏代码块渲染 | 修复 PR [#4257](https://github.com/HKUDS/nanobot/pull/4257) 待合并 |
| **中** | [#4219](https://github.com/HKUDS/nanobot/pull/4219) | 会话历史修剪后残留孤儿 tool result | 已合并修复 |
| **中** | [#4256](https://github.com/HKUDS/nanobot/pull/4256) | MemoryStore 游标非单调递增，可能导致历史读取错乱 | 修复 PR open，待合并 |
| **低** | [#4223](https://github.com/HKUDS/nanobot/pull/4223) | 微信 token 过期后死循环，需重新登录 | 修复 PR open，待合并 |
| **低** | [#4053](https://github.com/HKUDS/nanobot/pull/4053) | 只读 extra allowed roots 被写入工具继承 | 修复 PR open，待合并 |

## 功能请求与路线图信号
结合当日 Issue 与未合并 PR，以下方向最可能纳入近期版本：

- **模型切换粒度**（[#4253](https://github.com/HKUDS/nanobot/issues/4253)）： 按对话指定模型预设，支持在线/本地交替使用。暂无 PR，但用户需求强烈，若实现将大幅提升灵活性。
- **多模态上传**（[#4251](https://github.com/HKUDS/nanobot/issues/4251)）： 支持图片/PDF 上传让 AI 分析。目前无直接 PR，但转录系统的统一（[#4232](https://github.com/HKUDS/nanobot/pull/4232)）为多模态输入打下基础设施基础。
- **转录扩展持续**： 今日合并三个提供商，表明转录系统已标准化，未来可能支持更多自定义或本地 STT 模型。
- **电子邮件频道自动化**（[#4170](https://github.com/HKUDS/nanobot/pull/4170)）： 增加 IMAP 后处理动作（已读、移动），面向 Agent 管理邮箱场景，适合下一版本纳入。
- **上下文压力治理**（[#4238](https://github.com/HKUDS/nanobot/pull/4238)）： 通过 ContextGovernor 实现基于上下文压力的微压缩，提升长对话稳定性，已进入审查。
- **内存/会话生命周期测试**： 多个测试用 PR（[#3982](https://github.com/HKUDS/nanobot/pull/3982)、[#3983](https://github.com/HKUDS/nanobot/pull/3983)、[#4193](https://github.com/HKUDS/nanobot/pull/4193)）已开放两周以上，体现团队对质量基础设施的持续投入。

## 用户反馈摘要
从当日 Issue 评论中提炼的真实用户场景与痛点：

- **Azure 兼容门**：使用 Azure 样式 OpenAI 网关的用户因缺少 `?api-version` 参数被迫返回 404，通过 `extra_query` 配置得到解决（[#4204](https://github.com/HKUDS/nanobot/issues/4204)）。
- **模型切换不灵活**：用户同时使用 OpenRouter（快速但需联网）和本地 llama.cpp（私密但慢），希望为不同对话选择不同模型，当前全局设置无法满足（[#4253](https://github.com/HKUDS/nanobot/issues/4253)）。
- **中文用户多模态需求**： 上传图片要求“解析并分析意思”，上传 PDF 要求“总结主要内容”，直接暴露文本/语音之外的多模态缺口（[#4251](https://github.com/HKUDS/nanobot/issues/4251)）。
- **消息格式受损**：Telegram 长消息中嵌入的代码块因分段发送而损坏，影响开发者和技术用户的交流体验（[#4250](https://github.com/HKUDS/nanobot/issues/4250)）。
- **微信频道静默**：token 到期后进入死循环导致频道永久不可用，用户被迫重新扫码，属于较严重的稳定性问题（对应的修复 PR [#4223](https://github.com/HKUDS/nanobot/pull/4223) 等候合并）。

## 待处理积压
以下 Issue/PR 已开放较长时间或长期未获维护者响应，建议优先关注：

| 编号 | 标签 | 创建时间 | 描述 | 建议行动 |
|------|------|----------|------|----------|
| [#3982](https://github.com/HKUDS/nanobot/pull/3982) | test | 2026-05-24 | scripted agent runner harness | 审查并合并，提升测试覆盖率 |
| [#3983](https://github.com/HKUDS/nanobot/pull/3983) | test | 2026-05-24 | runner blocked tool-call finish reasons 测试 | 同上 |
| [#4193](https://github.com/HKUDS/nanobot/pull/4193) | test | 2026-06-04 | memory lifecycle harness | 持续 open，建议给予反馈或合并 |
| [#4053](https://github.com/HKUDS/nanobot/pull/4053) | security | 2026-05-29 | keep read-only roots out of write paths | 重要安全补丁，需加快审查 |
| [#4119](https://github.com/HKUDS/nanobot/pull/4119) | security | 2026-05-31 | block relative symlink workspace escapes（与已合并的 #4221 相似） | 确认是否 superseded，否则合并 | 
| [#4170](https://github.com/HKUDS/nanobot/pull/4170) | feature | 2026-06-03 | email IMAP post-actions | 邮件频道增强，等待维护者评论 |
| [#4223](https://github.com/HKUDS/nanobot/pull/4223) | fix | 2026-06-06 | 微信会话 token 过期后死循环修复 | 用户痛点明显，建议尽快合并 |
| [#4256](https://github.com/HKUDS/nanobot/pull/4256) | fix | 2026-06-08 | MemoryStore 游标单调性修复 | 新提交但关联记忆系统可靠性，需及时审核 |

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报（2026-06-09）

数据来源：[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) 2026-06-09 一次采集

---

## 今日速览

过去 24 小时项目收到 50 条 Issue 更新（新开/活跃 46，关闭 4）和 50 条 PR 更新（待合并 46，合并/关闭 4），社区反馈与贡献保持**极高活跃度**。桌面端、macOS 兼容性、内存系统成为今日问题爆发最集中的领域，同时出现了多项平台级增强 PR（如 iMessage 全双工、Dashboard 文件浏览、延迟工具配置）。无新版本发布，项目处于快速迭代的 **“严 bug、强功能”** 阶段，维护者需优先跟进多项 P1 阻塞问题。

---

## 版本发布

无（过去 24 小时无新 Release）。

---

## 项目进展

今日有 4 个 Issue 和 4 个 PR 进入关闭/合并状态。已关闭 Issue 包括：#42130（OpenRouter 认证未携带 Header）、#42306（Langfuse 追踪缺少 token 用量）等重点阻塞项，表明相应修复已合入基线。在提交的 PR 中，虽然绝大部分仍为 `OPEN`，但多项已具备高质量且指向关键痛点：

- **成本追踪修复** [#42554](https://github.com/NousResearch/hermes-agent/pull/42554)：修正 Gateway 丢弃 token 字段、定价别名及 API 调用成本三大根源，使每周成本报表从 “$0.01/4 次调用” 恢复准确。
- **Telegram 消息截断** [#42523](https://github.com/NousResearch/hermes-agent/pull/42523)：修正 `_split_text_chunks` 在无换行后备分支中以 codepoint 切片代替 UTF-16 编码单位导致的截断偏移。
- **systemd 优雅停止** [#42555](https://github.com/NousResearch/hermes-agent/pull/42555)：在 `ExecStop` 中写入 plan-stop 标记，避免 systemd 误判导致非正常退出。
- **Dashboard 循环认证** [#42546](https://github.com/NousResearch/hermes-agent/pull/42546)：允许桌面客户端自动发现环回 dashboard 的临时令牌并刷新，简化本地连接配置。
- **iMessage 全双向媒体** [#42507](https://github.com/NousResearch/hermes-agent/pull/42507)：补全附件获取、语音消息、点回、已读回执等交互，填补 #42454 的关键缺口。
- **终端侧面板** [#42521](https://github.com/NousResearch/hermes-agent/pull/42521)：在桌面端实现可拖拽调整大小、跟随主题的终端侧栏，提升多面板效率。
- **文件浏览器** [#42534](https://github.com/NousResearch/hermes-agent/pull/42534)：Dashboard 新增文件浏览页，支持上传/下载/删除及拖放。
- **核心工具延迟配置** [#42551](https://github.com/NousResearch/hermes-agent/pull/42551)：让平台可控制核心工具在搜索中是否“渐进披露”，优化工具数量较多的平台体验。
- **Cron 健壮性** [#42552](https://github.com/NousResearch/hermes-agent/pull/42552)：添加 MCP 条件初始化与稳健日期解析，防止远程 MCP 认证失败拖慢纯搜索类 Cron 任务。

这些 PR 一旦合并，将对成本可见性、平台适配、桌面 UX 和告警可靠性带来实质性改进，项目正朝**更加自愈、更跨平台、更富交互**的方向推进。

---

## 社区热点

讨论最热烈、参与度最高的 Issue：

1. **[#27997 – Feature: Declarative Skill Protection Policy](https://github.com/NousResearch/hermes-agent/issues/27997)**（7 条评论）  
   用户指出技能保护规则分散在 6 个文件中且执行不一致，尤其在 `skill_manager_tool.py` 存在高风险缺口。社区深度讨论了集中声明式策略的设计，背后是用户对**统一权限与安全模型**的强烈诉求，尤其在多技能协作场景。

2. **[#24860 – Dashboard Chat: Ctrl+V paste broken, image paste not supported](https://github.com/NousResearch/hermes-agent/issues/24860)**（6 条评论, 1 👍）  
   基础粘贴功能失效，Web/桌面用户普遍感到**日常操作受阻**，图片粘贴缺失进一步影响了多模态交互实验。评论中有用户提供了初步定位（TUI 后端错误读取剪贴板），热度持续。

3. **[#34457 – s6-log lock collision loops endlessly in multi-container gateway + dashboard shared volume setups](https://github.com/NousResearch/hermes-agent/issues/34457)**（6 条评论, 3 👍）  
   日志系统在共享卷 Docker 环境中的死循环锁碰撞，获最高 👍 数。反映**容器化部署用户基群正在扩大**，而对 s6-log 的并发处理有更严格要求，社区在该 issue 中积极贡献 workaround。

4. **[#21549 – fix(gateway): launchd double-spawn triggers infinite restart death spiral](https://github.com/NousResearch/hermes-agent/issues/21549)**（4 条评论）  
   经典 P1 macOS 问题，虽然提交已有月余，但今日仍有用户补充复现环境（显示器唤醒、KeepAlive 重启），持续影响** macOS 主力用户的网关稳定性**。

5. **[#42130 – OpenRouter credential configured but Hermes sends requests without Authentication header](https://github.com/NousResearch/hermes-agent/issues/42130)**（4 条评论，**已关闭**）  
   该问题引发广泛关注后迅速得到修复并关闭，社区对响应速度表示认可，但也反映出认证路径测试覆盖需要加强。

---

## Bug 与稳定性

今日新报告的 Bug 数量多、覆盖面广，按严重程度排列如下（附已有 fix PR 标注）：

### P1（阻塞级）
| ID | 标题 | 说明 | Fix PR？ |
|----|------|------|----------|
| [#42449](https://github.com/NousResearch/hermes-agent/issues/42449) | delegate_task corrupts parent context_length via shared plugin context engine singleton | 子 agent 覆写父 agent 的 `ChatCompressor` 上下文长度，多 agent 委托任务上下文混乱 | 无 |
| [#42524](https://github.com/NousResearch/hermes-agent/issues/42524) | macOS 26: gateway start/restart refreshes LaunchAgent but launchctl exits 5 and falls back to detached process | 新版 macOS 下 `launchctl` 返回 5，网关退化为分离进程，失去服务管理能力 | 无 |
| [#21549](https://github.com/NousResearch/hermes-agent/issues/21549) | launchd double-spawn triggers infinite restart death spiral | 老牌 P1 仍未修复，影响 macOS 用户启动可靠性 | 无 |

### P2（中等影响，多数有临时缓解或正在修复）
| ID | 标题 | 说明 | Fix PR？ |
|----|------|------|----------|
| [#42405](https://github.com/NousResearch/hermes-agent/issues/42405) | Memory at capacity → 'replace' zero-match retry loop → no response | 记忆满容量时替换失败进入死循环，用户得不到任何回复 | 无 |
| [#42120](https://github.com/NousResearch/hermes-agent/issues/42120) | Hermes Desktop: incomplete turn content lost when manually clicking stop/cancel button | 手动停止流式生成导致已生成部分永久丢失 | 无 |
| [#42376](https://github.com/NousResearch/hermes-agent/issues/42376) | hermes gateway restart/install generates plist with LimitLoadToSessionType that breaks launchctl bootstrap on macOS 26.5.1 | macOS Tahoe 新版 plist 兼容问题 | 无 |
| [#41898](https://github.com/NousResearch/hermes-agent/issues/41898) | Desktop assistant response flashes and disappears immediately (provider: NVIDIA NIM) | 桌面端特定提供商下回答闪烁消失，仅后端可见 | 无 |
| [#42533](https://github.com/NousResearch/hermes-agent/issues/42533) | API call failed after 3 retries: HTTP 500 from model cascade | 多模型链式调用中中间模型返回 400 导致整体失败 | 无 |

### P3（低严重度，主要涉及桌面 UI / 非核心路径）
大量问题集中爆发，典型包括：
- [#42431](https://github.com/NousResearch/hermes-agent/issues/42431) 远程模式下 Files 面板使用本地路径导致 `ENOENT`
- [#42468](https://github.com/NousResearch/hermes-agent/issues/42468) 侧栏“Copy ID”因 Radix 菜单嵌套失效
- [#42479](https://github.com/NousResearch/hermes-agent/issues/42479) 停止按钮后 UI 状态未清除，仍显示“运行中”
- [#42433](https://github.com/NousResearch/hermes-agent/issues/42433) Cron 视图不渲染 `no_agent` 任务
- [#42409](https://github.com/NousResearch/hermes-agent/issues/42409) Artifacts 时间戳全部显示 1970-01（epo second 被当 ms）
- [#42422](https://github.com/NousResearch/hermes-agent/issues/42422) 删除 Discord 源会话后自动复活
- [#42401](https://github.com/NousResearch/hermes-agent/issues/42401) 切换页面时未发送的 prompt 丢失
- [#42466](https://github.com/NousResearch/hermes-agent/issues/42466) Cron Hindsight 记忆提供者间歇 “interpreter shutdown” 错误
- [#42505](https://github.com/NousResearch/hermes-agent/issues/42505) Matrix 网关启动时默认日志输出恢复密钥，安全风险

其中部分已有对应修复 PR 在审查中（如 #42543 修复搜索/提取超时，关联 #42360；#42554 修复成本追踪；#42523 修复 Telegram 分割）。

---

## 功能请求与路线图信号

今日新增及活跃的功能请求显示出社区对以下方向的热切期待：

- **技能安全策略集中化**：[#27997](https://github.com/NousResearch/hermes-agent/issues/27997) 要求统一的声明式技能保护。目前已有社区在讨论中提出方案实体，但尚未见对应 PR，是**内部权限治理**的重要信号。
- **多 Profile 支持增强**：[#38357](https://github.com/NousResearch/hermes-agent/issues/38357) 请求桌面侧栏显示所有 profile 的会话，反映出专业用户在**多身份、多 agent 协作**场景下的刚需。
- **Windows 入职体验**：[#41933](https://github.com/NousResearch/hermes-agent/issues/41933) 用户贡献了一个完整的“Windows 环境诊断” skill，说明第一方工具检查流程尚不顺畅，路线图应考虑官方安装引导。
- **记忆提供者生态**：[#42506](https://github.com/NousResearch/hermes-agent/issues/42506) 请求加入 usememos 作为官方记忆提供者，扩展了除原有记忆后端外的轻量选择，预计至少为 P3 级别的后续增强。
- **平台适配深化**：[#38641](https://github.com/NousResearch/hermes-agent/issues/38641) 要求 WeCom 支持流式与消息编辑；[#40259](https://github.com/NousResearch/hermes-agent/issues/40259) 希望 Telegram 的 clarify 按钮使用文字而非序号；[#16675](https://github.com/NousResearch/hermes-agent/issues/16675) 要求 WeCom 消息已读确认。这些构成**平台抽象层打磨**的方向。
- **本地模型默认采样参数**：[#41988](https://github.com/NousResearch/hermes-agent/issues/41988) 指出自定义本地 provider（如 llama.cpp）未发送 temperature 等参数，影响输出质量。

关键 PR 信号：**[#42551](https://github.com/NousResearch/hermes-agent/pull/42551)（核心工具延迟配置）**、**[#42550](https://github.com/NousResearch/hermes-agent/pull/42550)（Web 抽取级联后端）**、**[#42534](https://github.com/NousResearch/hermes-agent/pull/42534)（Dashboard 文件浏览器）**、**[#42507](https://github.com/NousResearch/hermes-agent/pull/42507)（iMessage 全双工）** 等很可能是下一个版本的核心特性；时间线上看有望纳入 v0.17 或后续补丁。

---

## 用户反馈摘要

从今日 Issue 评论与描述中提取真实用户声音：

**“配置了 OpenRouter 但请求没带 Auth Header，每个请求都 401”**（#42130，已感激地确认修复）  
**“每次 Docker 共享卷启动 dashboard 侧车容器，日志就 s6-log 崩溃循环，完全不可用”**（#34457，用户寻求紧急 workaround）  
**“在 Windows 上按照文档装了 node/ffmpeg 等工具，Hermes 还是检测不到——工具在终端可用但软件不认”**（#41933，用户感到困惑且流程断裂）  
**“Mac 上 gateway 重启后进程变成 detached，launchctl 看不到，cron/event 全都掉线”**（#42524，macOS 26 用户首次设置网关即遇挫）  
**“手动停掉生成后，之前已经出来的文字全没了……在别的软件里不是这样的”**（#42120，桌面用户对比竞品表达不满）  
**“记忆满了之后 agent 开始疯狂重试然后 user 收不到任何回应——整个会话就死了”**（#42405，对记忆系统可靠性的严重不信任）  
**“NVIDIA NIM 下回答闪一下就没了，但后端能看到完整输出——Desktop 的渲染有问题”**（#41898，特定提供商回显 bug 影响评测）  
**“Cron 任务明明完成了，Cron 视图里却一片空白，脚本也没显示——我完全不知道它跑没跑”**（#42433，用户失去调度可见性）  
**“Artifacts 里所有时间都显示 1970 年，时间戳单位错了”（**#42409，用户对数据准确性提出质疑）  
**“只要有协 author 用 Telegram，删掉的会话过一会又出现了——好像没删一样”**（#42422，删除持久化 bug 影响用户隐私管理期待）

整体来看，用户对 **桌面端精细化、macOS/Docker 环境稳定性、记忆系统健壮性** 的期望明显高于当前交付质量，但社区对新功能（文件浏览、终端面板、iMessage）的响应积极，表明用户仍然对 Hermes 的未来能力抱有信心。

---

## 待处理积压

以下 Issue 长时间未获得维护者有效响应或修复分配，已超出正常响应周期，需重点排查：

| ID | 创建时间 | 标题 | 严重度 | 说明 |
|----|----------|------|--------|------|
| [#12020](https://github.com/NousResearch/hermes-agent/issues/12020) | 2026-04-18（52 天） | 添加开关控制 `hermes.tool.progress` 事件输出以避免前端解析失败 | ~~P3~~ | 长期未分配，影响 openai 兼容接口前端消费 |
| [#16675](https://github.com/NousResearch/hermes-agent/issues/16675) | 2026-04-27（43 天） | [Feature]: Wecom 收到消息后可立即回复已收确认 | P3 | 1 条用户额外评论，无维护者回复，WeCom 用户处于不确定状态 |
| [#21549](https://github.com/NousResearch/hermes-agent/issues/21549) | 2026-05-07（33 天） | launchd double-spawn 导致无限重启死亡螺旋 | **P1** | macOS 核心稳定性问题，距今已一个月以上，仍无 fix PR，每日仍有新用户遭遇 |
| [#24860](https://github.com/NousResearch/hermes-agent/issues/24860) | 2026-05-13（27 天） | Dashboard 粘贴 Ctrl+V 与图片粘贴失效 | P2 | 高热度（6 评论+1 👍），影响日常使用，尚未确认修复 |
| [#27997](https://github.com/NousResearch/hermes-agent/issues/27997) | 2026-05-18（22 天） | 声明式技能保护策略 | P3（但涉及安全） | 有深度讨论但官方未分配，缺少安全路径时间承诺 |
| [#34457](https://github.com/NousResearch/hermes-agent/issues/34457) | 2026-05-29（11 天） | s6-log 锁碰撞在共享卷多容器中循环 | P2 | 获最高 👍，已有社区 workaround 讨论，仍需根本修复 |

**建议维护团队优先评估 #21549 和 #34457**，前者为长期 P1 影响 macOS 基线，后者是快速增长的 Docker 部署场景的严重阻塞。同时建议重新标记 #12020 的优先级或明确回复规避方案，避免该前端兼容问题持续积累用户不满。

---

*本日报基于 Hermes Agent 公开 GitHub 数据自动生成，部分 PR 评论数未在数据源中提供，未作推算。所有表述以链接对应 Issue/PR 原文为准。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 PicoClaw 项目 2026-06-09 动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-09

## 1. 📈 今日速览

项目今日进入高强度迭代模式，**24 小时内共处理 19 条 Pull Request**，是近期活跃度最高的一次。核心动态为一场由社区贡献者主导的“代码质量攻坚”（约占 PR 总量的 70%），重点修复了类型断言安全、错误包装规范及资源关闭处理等潜在运行时风险。功能层面进展迅速，Telegram 位置消息丢失 Bug 在 24 小时内完成定位并修复。总体来看，项目在快速迭代新功能（如 Delta Chat 网关提案）的同时，正系统性积累技术债，迈向更高稳定性。

## 2. 🚀 版本发布

- **Nightly Build: `v0.2.9-nightly.20260609.46b29a0a`**
  - 这是一个自动化的每日构建版本，可能包含不稳定因素。
  - **更新内容**：包含今日所有已合并的代码质量修复及 Bug 修复。
  - 📎 [查看完整变更日志](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

## 3. ✅ 项目进展（已合并/关闭的 PR）

今日 9 条 PR 完成合并/关闭，主要集中在功能修复与代码健壮性提升：

- **功能性修复**：
  - **Telegram 地理位置支持**（[#3052](https://github.com/sipeed/picoclaw/pull/3052)）：修复 Telegram 频道完全忽略位置消息的 Bug。现在 `message.location` 将被转换为文本并交由 Agent 处理。
  - **健康检查路径修复**（[#3062](https://github.com/sipeed/picoclaw/pull/3062)）：修复了健康检查端点始终返回 `not ready` 的问题。
  - **日志架构升级**（[#3050](https://github.com/sipeed/picoclaw/pull/3050)）：将散落在生产代码中的 `log.Printf`/`fmt.Printf` 全面替换为结构化 Logger，提升可观测性。

- **代码质量控制（贡献者 @chengzhichao-xydt 主导）**：
  - **类型安全**：在 `tools`、`channels`、`config`、`agent` 等核心包中，针对 `interface{}` 类型断言添加了约 20 处 `ok` 检查（[#3056](https://github.com/sipeed/picoclaw/pull/3056)、[#3057](https://github.com/sipeed/picoclaw/pull/3057)、[#3058](https://github.com/sipeed/picoclaw/pull/3058)、[#3018](https://github.com/sipeed/picoclaw/pull/3018) 等）。
  - **错误链保留**：统一将 `%v` 替换为 `%w` 包装错误，确保 `errors.Is`/`errors.As` 链式查询可用（[#3051](https://github.com/sipeed/picoclaw/pull/3051)）。
  - **资源释放规范**：显式忽略并注释了文件关闭、HTTP Body 关闭等错误路径的返回值（[#3059](https://github.com/sipeed/picoclaw/pull/3059)）。

## 4. 🔥 社区热点

- **Delta Chat 网关提案（[#3063](https://github.com/sipeed/picoclaw/pull/3063)）**：来自 @trufae 的 PR 提议增加对 Delta Chat（基于电子邮件协议的去中心化聊天工具）的支持。这引起了社区对“去中心化 AI 网关”方向的热烈讨论，是今日最具前瞻性的功能信号。

- **RISC-V 兼容性困境（[#2887](https://github.com/sipeed/picoclaw/issues/2887)）**：虽然标记为 `stale`，但它是今日评论数最多的 Issue（9 条）。用户对 RISC-V 架构的支持诉求强烈，但问题长期悬而未决，暴露了项目在 x86/ARM 之外的架构测试覆盖上的短板。

- **极速响应赢得口碑（[#3049](https://github.com/sipeed/picoclaw/issues/3049) -> [#3052](https://github.com/sipeed/picoclaw/pull/3052)）**：用户 `terurium` 报告的 Raspberry Pi 下 Telegram 位置消息 Bug，从提报到合入修复仅用了不到 24 小时。这种响应速度显著提升了社区的信任度。

## 5. 🐛 Bug 与稳定性

- **待修复（中危）**：
  - **[[BUG] .deb version on RISC-V is not functional with OpenAI model](https://github.com/sipeed/picoclaw/issues/2887)**：在 RISC-V Debian 环境下，`.deb` 安装包无法正常调用 OpenAI 模型。该问题已存在近一个月，影响 RISC-V 生态用户的基础使用。
  - **[[BUG] QQ Channel Connection Failed After Windows Release Build](https://github.com/sipeed/picoclaw/issues/3015)**：Windows 用户运行 `picoclaw gateway` 时无法获取 QQ 频道令牌，导致该渠道在 Windows 下完全不可用。

- **已修复（低危）**：
  - **[[Bug] Telegram channel ignores location messages](https://github.com/sipeed/picoclaw/issues/3049)** → 已合入主线。

- **稳定性趋势**：
  - 今日无严重崩溃或内存泄漏报告。
  - **大量类型安全检查的合并，有效降低了因上游模型返回 “非常规数据类型” 导致 Agent Panic 的风险。**
  - **风险预警**：PR [#2904](https://github.com/sipeed/picoclaw/pull/2904)（修复 Agent 重载时的 Goroutine 泄漏与 Panic 恢复）已等待核心维护者 Review 长达 20 天，长期未合并可能影响生产环境下实例的稳定运行。

## 6. 💡 功能请求与路线图信号

- **即将进入倒计时的功能**：
  - **Windows 原生体验优化**：PR [#3061](https://github.com/sipeed/picoclaw/pull/3061) 彻底修复了启动 GUI 时后台进程窗口闪烁的问题。
  - **Agent 核心可靠性**：待合并的 [#2904](https://github.com/sipeed/picoclaw/pull/2904) 旨在解决 Agent 重载时的循环稳定性，是通往稳定版 `v0.3.0` 的重要基石。

- **路线图信号**：
  - **协议扩展**：Delta Chat 集成（[#3063](https://github.com/sipeed/picoclaw/pull/3063)）是当下最具差异化的功能。如果推进顺利，PicoClaw 将成为少数同时支持 Matrix、Telegram 和 Delta Chat 的 AI Agent 网关，契合“去中心化 AI”趋势。
  - **“零恐慌”目标**：今日大量针对“类型断言”的修复表明，项目正在向“零运行时恐慌”这一高目标迈进。

## 7. 👂 用户反馈摘要

- **高频痛点**：
  - **“开箱即用”体验受阻**：RISC-V 用户无法使用核心 AI 功能（[#2887](https://github.com/sipeed/picoclaw/issues/2887)），Windows 用户无法使用 QQ 渠道（[#3015](https://github.com/sipeed/picoclaw/issues/3015)）。用户期望对 Release 包进行更完善的架构与平台回归测试。
  - **环境配置门槛**：部分用户对 QQ 频道的 Bot 鉴权流程不熟悉，希望提供更详细的 Windows 环境配置指南。

- **积极信号**：
  - 核心贡献者 `chengzhichao-xydt` 连续发布大量高质量修复 PR，侧面反映了高级社区开发者对项目代码库的认可与持续投入。
  - 针对 Telegram 位置消息的快速响应（24 小时内合入修复），获得了良好反馈。

## 8. 📌 待处理积压

| 类型 | 标题 | 链接 | 待处理时长 | 建议 |
| :--- | :--- | :--- | :--- | :--- |
| **高优** | Fix agent loop reload and panic cleanup stability | [#2904](https://github.com/sipeed/picoclaw/pull/2904) | 20 天 (等待 Review) | 核心稳定性改进，长期阻塞可能影响所有生产用户，建议优先处理。 |
| **高优** | QQ Channel Connection Failed on Windows | [#3015](https://github.com/sipeed/picoclaw/issues/3015) | 3 天 (新阻断) | 完全阻断 QQ 渠道在 Windows 的使用，需确认是网络代理还是 API 兼容性问题。 |
| **中优** | .deb version on RISC-V is not functional | [#2887](https://github.com/sipeed/picoclaw/issues/2887) | 23 天 (Stale) | 需要官方决策是否将 RISC-V 列为一级支持架构。 |
| **中优** | Add DeltaChat Gateway | [#3063](https://github.com/sipeed/picoclaw/pull/3063) | 1 天 (新 PR) | 重大功能扩展，需要核心维护者明确路线图方向并启动 Review。 |

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是根据今日 GitHub 数据生成的 **NanoClaw 项目动态日报**。

---

# NanoClaw 项目动态日报 | 2026-06-09

**分析基准数据**：过去 24 小时。整体活跃度中等偏高，安全基础设施与紧急 Bug 是本日焦点。

## 1. 今日速览

今日 NanoClaw 项目呈现“安全加固推进，核心功能冒烟”的双线状态。一方面，备受关注的**出站流量锁定（Egress Lockdown）特性（PR #2713）已完成合并**，标志着项目在企业级网络隔离方向上迈出坚实一步。另一方面，**严重级 Issue #2715 报告了 WhatsApp 渠道媒体文件接收完全失效的问题**，根源在于 v2 版本容器挂载配置遗漏。与此同时，另一项**安全修复 PR（#2714）正处于开放待审查状态**，等待核心维护者介入。整体来看，项目在快速加入网安新功能的同时，也面临 v2 版本引入的回归性 Bug 修复压力。

## 2. 版本发布

- **无新版本发布。** 今日无 Release 记录。

## 3. 项目进展

今日合并/关闭了 2 个 PR，其中 1 个具有里程碑意义：

- **PR #2713 (Egress Lockdown 特性合并)** [合并]
  - **作者**：@omri-maya
  - **评述**：这是项目安全架构的重要一步。该特性通过让 Agent 容器接入 Docker `--internal` 网络（断开公网路由），并将 OneCLI 网关别名为唯一的出站代理地址，实现了可选的**零信任网络出口控制**。该特性默认关闭，兼顾了老用户的兼容性与新用户的安全性。
  - **影响**：该机制的引入为多租户、金融、医疗等需要对 Agent 出站行为进行严格审计的部署场景扫清了关键障碍。

- **PR #2712 (流程性关闭)** [关闭]
  - 该 PR 无实际代码变更，已关闭。

## 4. 社区热点

- **热点 Issue：#2715 – WhatsApp 媒体文件可见性 [活跃]**
  - **链接**：[nanocoai/nanoclaw Issue #2715](https://github.com/nanocoai/nanoclaw/issues/2715)
  - **热度分析**：虽然发布至今尚未产生评论，但作为今日唯一的**新开且活跃** Issue，其内容直击核心用户体验。用户指出 v2 版本将 WhatsApp 附件下载到了宿主机未挂载的目录，导致 Agent 收到一个在容器内不存在的路径（`/workspace/attachments/...`），导致图片/文档/音频等技能完全无法运作。
  - **背后诉求**：用户期望 v2 版本能够无缝兼容通常的 Docker Compose 或 Kubernetes 部署拓扑，开箱即用地处理媒体渠道。

- **热点 PR：#2714 – 安全缺陷修复 [等待审查]**
  - **链接**：[nanocoai/nanoclaw PR #2714](https://github.com/nanocoai/nanoclaw/pull/2714)
  - **热度分析**：作为当前唯一的开放 PR，社区正在等待维护者的响应。它代表了社区对安全性的自发贡献。

## 5. Bug 与稳定性

| 严重程度 | issue / PR | 状态 | 详情与分析 |
| :--- | :--- | :--- | :--- |
| **严重 (Critical)** | [#2715 WhatsApp 媒体不可达](https://github.com/nanocoai/nanoclaw/issues/2715) | **Open / 无 Fix PR** | **核心渠道功能阻塞**。Agent 在 WhatsApp 渠道中无法访问任何附件，导致所有媒体相关技能（如图像分析、文档OCR、语音转文字）完全不可用。这是一个 v2 版本的回归问题，源于容器卷映射配置缺失。**需要立即响应并修复。** |
| **中 (Medium)** | [#2714 四项安全修复](https://github.com/nanocoai/nanoclaw/pull/2714) | **Open / Fix PR 就绪** | 虽然此 PR 是修复方案，但同时也暴露了代码库中存在的隐患。例如 Webhook 服务默认监听 `0.0.0.0` 可能造成攻击面扩大，以及使用 `Math.random()` 生成审批 ID 存在时序预测漏洞。这些问题属于安全稳定性债务，亟需纳入下一个补丁。 |

## 6. 功能请求与路线图信号

今日无明确的新功能请求 Issue，但从 PR 的合并趋势可以清晰看到信号：

- **企业安全优先：** **PR #2713** 的合并非常明确地传达了项目路线图正在向**零信任网络架构**演进。这种“只有代理能出去，且必须通过网关”的模型，标志着 NanoClaw 正在从个人开发者工具向企业级平台转型。
- **安全债务清理：** **PR #2714** 中针对 Webhook 绑定地址、加密随机数的修改，暗示维护者开始着手清理安全历史债务。预计这部分修复（如使用 `127.0.0.1` 作为默认监听地址）将标配在下一个版本中。

## 7. 用户反馈摘要

- **真实痛点（来自 #2715）：**
  - 用户 @jon-ruth 反馈：“Inbound WhatsApp attachments are downloaded to a host directory that is **not mounted into the agent container**.”
  - **使用场景受阻**：用户在混合部署（Hybrid）或独立部署（Standalone）模式下，尝试让 Agent 读取 WhatsApp 中的图片/文档/音频时失败。
  - **核心诉求**：Agent 不应依赖特定的外部卷挂载配置，而是应通过标准化的共享目录（Session Inbox）进行文件交换，或者安装程序应自动处理挂载逻辑。

## 8. 待处理积压

- **高优先级审查项：[PR #2714](https://github.com/nanocoai/nanoclaw/pull/2714) 安全修复**
  - **状态**：Open，0 条评论，0 个 Approval。
  - **分析**：该 PR 由 @JorellDacasin 提交，修复了 4 个安全点。考虑到 @omri-maya 刚刚合并了安全特性 PR，建议核心团队尽快对此 PR 进行 Code Review 并合入，以消除被暴露的安全窗口。该 PR 长期积压可能引入“修正延迟”风险。

- **新 Issue 分流：[Issue #2715](https://github.com/nanocoai/nanoclaw/issues/2715)**
  - **分析**：虽然是新 Issue，但因其严重影响（渠道核心能力瘫痪），建议维护者立刻将其标记 `bug`、`priority: high` 标签，并分发至负责容器编排或 WhatsApp 渠道的模块负责人。如果不及时分流，该问题可能在下一次周报中变成“高热度积压 Bug”。

---

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据您提供的 IronClaw 项目数据生成的 2026-06-09 项目动态日报。

---

# IronClaw 项目动态日报 (2026-06-09)

## 1. 今日速览

今日项目活跃度极高（更新 Issue 34 条 / PR 50 条），核心开发团队持续高强度推进 **“Reborn” 架构迁移**，这是当前项目的绝对主线。OpenAI 兼容 API 的 Chat/Responses/Streaming 路由层已进入最后的 Code Review 冲刺阶段（`#4495`, `#4546`, `#4552`）。多项底层基础设施已经合入，例如自动化运行历史 UI、Codex 模型解锁、子 Agent 架构重构等。

在稳定性和用户反馈方面，新浮现出几个重要 Bug（Minimax 配置失败、DeepSeek 400 错误），同时 Nightly E2E 持续红屏是一个值得关注的 CI 风险信号。

**项目健康度**：**高活跃度 / 换代攻坚期**。虽然代码更迭速度快、Bug 频发属正常阵痛，但需警惕 Nightly E2E 长期未修复可能导致的回归风险。

## 2. 版本发布

今日 0 个新版本发布。

当前 Release PR (`#3708`) 自 5 月 16 日已开放近一个月，包含 `ironclaw_skills` 的破坏性变更。鉴于 Reborn 核心路由尚未合入，该版本可能被战略性地等待重大功能就绪后再统一发布。

## 3. 项目进展

今日多个关键模块取得了实质性推进，大量 PR 被合并或进入核心审查阶段：

- **Reborn 路由层攻坚 (进行中)**
  - **Chat Completions 路由**: `#4495` (XL, Open) 将非流式 `POST /v1/chat/completions` 路由到 ProductWorkflow。
  - **Responses 路由**: `#4546` (XL, Open) 实现了非流式 Responses 的创建、检索与取消。
  - **Streaming 支持**: `#4552` (XL, Open) 实现了 Projection Stream 向 OpenAI SSE 格式的转换。
- **自动化与触发器 (已合并)**
  - `#4580` 和 `#4581` 已合并，新增了自动化运行历史 UI、作用域外发投递默认值和版本化的偏好写入，显著增强了自动化模块的产品化程度。
- **LLM 与 Codex 增强 (已合并)**
  - `#4566` 解决了 Codex `client_version` 硬编码问题，使得 `gpt-5.5` 等新模型可被自动识别。
  - `#4576` 在 `ToolCall` 中引入了 `arguments_parse_error` 字段，为后续错误处理和兼容性修复铺路。
  - `#4572` 将子 Agent `flavor` 从 `researcher` 重构为 `planner`，并重命名了相关参数。
- **基础设施修复 (已合并)**
  - `#4523` 和 `#4575` 修复了 `ResourceScope` 系统 ID 的 JSON 序列化回环 Bug。
  - `#4578` 修复了 Google Calendar 默认返回最早历史事件的严重 UX 问题。
- **认证与授权**: `#4528` (Slack Host-Beta 状态持久化)、`#4536` (OAuth 用户无法聊天修复)。

**项目里程碑判断**：Reborn 正在从“模块构建”阶段迈向“路由联通”阶段，一旦 Chat/Responses 路由合入，将标志着 Reborn 具备了可对外服务的 API 骨架。

## 4. 社区热点

- **`#3283` (Reborn OpenAI 兼容 API 迁移)**: 该 Epic 虽仅 3 条评论，但作为 Reborn 的“门面”，关联了 10 余个子 Issue 和当前待审的 3 个 XL 级 PR。它是衡量项目进度的核心晴雨表。
  [链接](https://github.com/nearai/ironclaw/issues/3283)
- **`#4175` (Reborn 认证生产就绪)**: 3 条评论，讨论了 Google OAuth 适配、Token 生命周期和 PKCE 安全性。这是 Reborn 能否上生产环境的安全关键节点。
  [链接](https://github.com/nearai/ironclaw/issues/4175)
- **`#4587` (Minimax 提供商配置失败)**: 今日新开 Issue，用户反馈配置后无法聊天，报错指向密钥元数据读取失败。作为即时反馈，吸引了最快的关注。
  [链接](https://github.com/nearai/ironclaw/issues/4587)

## 5. Bug 与稳定性

| 严重程度 | Issue | 现象 | 状态 | 修复 PR |
|---|---|---|---|---|
| **Critical** | `#4557` | 部分 Hosted 代理尽管运行中，却返回 403 错误 | Open | 无 |
| **Critical** | `#4108` | Nightly E2E 持续失败 (自 05-27 起) | Open | 无 |
| **High** | `#4587` | 配置 Minimax 提供商后无法使用 | Open | 无 |
| **High** | `#4548` | DeepSeek API 400 错误 (请求体重复 `model` 字段) | Open | 无 |
| **High** | `#4556` | Telegram 升级 `0.28.2 -> 0.29.1` 后创建新对话 | Open | 无 |
| **Medium** | `#4554` | i18n 翻译器运行时崩溃，国际化覆盖不完整 | Open | 无 |
| **Fixed** | `#4536` | OAuth 用户(GitHub/Google)登录后无法聊天 | Closed | 已在代码中修复 |
| **Fixed** | `#4577` | `google_calendar.list_events` 返回早期历史事件 | Closed | `#4578` |
| **Fixed** | `#4564` | Codex 硬编码版本号隐藏了 `gpt-5.5` 等新模型 | Closed | `#4566` |

## 6. 功能请求与路线图信号

- **Reborn 取代 V1 的最后拼图**: 功能请求 `#4545` (自服务密钥)、`#4543` (运行时服务配置文件)、`#4539` (审批流程对标) 均为 Reborn 达到产品级操作员功能的标准需求。它们与 `#4533` (Operator 诊断) 共同构成了 Reborn 的“运维可观测性”短板。
- **Agent 生态增强**: `#4559` (Trace Commons 自助上链) 和 `#4582` (子 Agent 持久化规范) 表明项目在 Agent 协作和可追溯性上有明确规划。
- **LLM 鲁棒性提升**: `#4583` (NormalizingProvider 装饰器) 旨在屏蔽各家厂商在 `tool_calls` 上的行为差异，对提升多厂商兼容性非常有价值，很可能随下一版本合入。

## 7. 用户反馈摘要

- **配置体验受阻**：用户 @matiasbenary 在配置 Minimax 提供商时遇到阻断性错误，日志提示 API Key 元数据无法读取，导致无法使用 (`#4587`)。
- **升级不兼容抱怨**：用户 @sunglow666 报告 Telegram 集成在从 `0.28.2` 升级到 `0.29.1` 后，旧对话中断并被生成了新的 WebUI 对话，这是典型的版本兼容性痛点 (`#4556`)。
- **供应商兼容性困惑**：用户 @darren2013 报告 DeepSeek API 400 错误，原因是请求体序列化时出现了重复的 `model` 顶层字段，影响了用户使用特定模型 (`#4548`)。
- **生产环境稳定性预警**：用户 @sunglow666 报告生产环境中的 403 幽灵错误——实例状态显示 `RUNNING` 但服务不可达，这是比常规功能 Bug 更严重的可靠性问题 (`#4557`)。
- **正面反馈**：用户 @sunglow666 对 WeCom 信道的新增表示认可，认为核心文本消息流 "mostly stable" (`#4191`)。

## 8. 待处理积压

- **`#4108` (Nightly E2E 失败)**：该工作流自 5 月 27 日以来频繁失败且至今未恢复。这是最重大的**持续集成红灯信号**，可能隐藏了主分支上的潜回归，需维护者优先排查。
  [链接](https://github.com/nearai/ironclaw/issues/4108)
- **`#4191` (WeCom 信道验证报告)**：该报告自 5 月 28 日提交，包含了详细的用户昵称同步、附件支持等改进建议，目前无后续更新。考虑到该信道是新功能，建议尽快排期跟进。
  [链接](https://github.com/nearai/ironclaw/issues/4191)
- **`#3708` (Release PR)**：开放超过 3 周，包含破坏性变更。这一积压表明当前项目管理上倾向于等待 Reborn 核心路由（Chat/Responses）合入后再统一发布，以避免短期内出现两次破坏性变更。
  [链接](https://github.com/nearai/ironclaw/pull/3708)
- **`#3026` (Reborn 生产就绪 Epic)**：作为替代 V1 的总任务，其子任务（如 Postgres 配置 `#4551`、认证完善 `#4175`）仍在积累。虽然进展稳定，但距离总目标达成仍有相当距离。
  [链接](https://github.com/nearai/ironclaw/issues/3026)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，以下是根据您提供的 LobsterAI 项目数据生成的 2026-06-09 项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-06-09

> 数据驱动，客观专业，聚焦项目健康度。

---

## 1. 今日速览

LobsterAI 项目在 2026-06-08 至 2026-06-09 期间经历了爆发式代码变动。虽然社区层面未报告新的 Issue，但开发侧合并/关闭了高达 **17 个 Pull Request**，展现了极高的迭代活力。项目成功落地了 **数据迁移/备份模块** 与 **桌面端认证流程重构** 两大基础能力，并集中清理了 8 个历史遗留的 Stale PR。总体来看，项目代码库健康度与功能完成度大幅提升，正稳步迈向生产级稳定性。

---

## 2. 项目进展

今日项目主干上迎来了多个核心功能节点，整体向前迈进了关键一步。

- **数据迁移与备份模块正式成型**：
  - [#2125](netease-youdao/LobsterAI PR #2125) `feat(data-migration)`: 新增用户数据备份与恢复服务，支持将用户数据打包为 tar 包，通过定时重启实现迁移与回滚。
  - [#2126](netease-youdao/LobsterAI PR #2126) `fix(data-migration)`: 优化恢复逻辑，采用原地替换而非整体重命名，确保运行时锁文件（SingletonLock、Cookie等）被保留，极大增强了迁移可靠性。
  - [#2128](netease-youdao/LobsterAI PR #2128) `fix(data-migration)`: 在备份中排除 Network 目录，避免迁移过程污染系统的网络状态。
- **桌面端认证流程重塑**：
  - [#2122](netease-youdao/LobsterAI PR #2122) `feat(auth)`: 新增基于本地回环地址的回调登录流程，规避浏览器外部应用确认弹窗，提升了登录流畅度。
  - [#2127](netease-youdao/LobsterAI PR #2127) `fix(auth)`: 修复了 Windows 平台认证后主窗口无法自动置前的问题，优化了浏览器登录后的跳转体验。
  - [#2129](netease-youdao/LobsterAI PR #2129) `chore(auth)`: 增加了登录回调的诊断日志输出，便于技术人员排查开发模式下的回调兼容性问题。
- **OpenClaw 网关可视化**：
  - [#2123](netease-youdao/LobsterAI PR #2123) `feat(settings)`: 在设置界面展示 OpenClaw 网关端口与 URL，并添加状态徽章与启动进度条，方便用户集成与排错。
- **历史技术债清理**：合并/关闭了 8 个来自 4 月 7 日的 Stale PR，社区累积的多个 Bug 修复与功能特性终于落地。

---

## 3. 社区热点

今日社区无新增 Issue，所有已关闭 PR 也未产生新评论，讨论相对平静。然而，合并的 8 个历史悠久 PR 无疑是今日的焦点，反映了项目对高频用户痛点的正面回应。

- **修复日志导出超时**（[netease-youdao/LobsterAI PR #1515](netease-youdao/LobsterAI PR #1515)）：此前用户在高配置延迟或大日志量场景下导出按钮常灰掉并提示超时，该项修复已随此次合并解决。
- **动态获取模型列表**（[netease-youdao/LobsterAI PR #1522](netease-youdao/LobsterAI PR #1522)）：用户反馈手动添加新模型极其不便，该特性允许自动拉取 Provider 模型列表，省去了手动配置的繁琐流程，社区呼声极高。

---

## 4. Bug 与稳定性

过去 24 小时内，项目集中修复了 10 余个 Bug，覆盖数据安全、认证、IM 通知、组件稳定性等多个领域，严重等级分布如下：

- **严重（P1）**：
  - **数据迁移数据损坏风险**：`#2126` 修复了恢复过程中锁文件（SingletonLock）被覆盖导致 App 崩溃的风险；`#2128` 排除了 Network 目录对全局网络配置的潜在污染。
  - **定时任务 IM 通知静默失败**（`#1510`）：修复了未选择接收会话时任务能创建但实际不执行的逻辑漏洞。
  - **日志导出功能不可用**（`#1515`）：解决了串行压缩耗时过长及 RPC 时序竞争双重缺陷导致的导出超时。
  - **Copilot OAuth Token 丢失**（`#1517`）：修复了关闭设置面板时后台 OAuth 轮询未取消，导致 Token 在组件卸载后静默丢失的问题。
  - **OpenClaw 网关误重启**（`#1521`）：阻止了技能变更事件触发不必要的网关重启，保证了服务稳定性。
- **中等（P2）**：
  - **Windows 登录窗口失焦**（`#2127`）：优化了浏览器认证回调后主窗口无法自动置前的交互缺陷。
  - **QQ Bot 白名单 UI 缺失**（`#1514`）：补全了群组白名单配置中缺失的添加输入框和按钮，使得白名单功能得以正常使用。

---

## 5. 功能请求与路线图信号

从今日合并的 PR 中可以清晰看出项目下一阶段的产品重心：

- **数据可靠性成为核心优先级**：`Data Migration` 系列（`#2125`, `#2126`, `#2128`）的成功落地，为用户数据的安全备份与跨版本迁移提供了坚实基础，这是走向生产级的必备基础设施。
- **桌面端（尤其 Windows）体验深化**：`feat(auth)` 系列彻底革新了 OAuth 登录流程，专注于解决 Windows 平台的长年历史兼容性问题与用户体验痛点。
- **社区驱动的 UI 功能**：
  - `#1522`：**动态模型获取**预示项目将降低维护成本，同时让用户更快体验到最新 LLM 能力。
  - `#1526`：**会话颜色标注**表明项目开始关注重度用户的信息组织效率。
  - `#1524`：**详细错误信息**展示了团队对用户体验细节的追求。

这些信号表明项目不仅在做功能堆叠，更在积极提升 **稳定性**、**可观测性** 与 **可用性**。

---

## 6. 用户反馈摘要

尽管今日无新增用户 Issue 评论，但被合并的历史 PR 所解决的 Issue 浓缩了用户的多项真实痛点：

- **功能完整性诉求**：用户反馈高度集中在“功能为什么不工作”上。如 `#1514`（白名单 UI 缺失）与 `#1510`（IM 通知失效），这表明用户期望 UI 配置与应用逻辑高度自洽，Bug 会直接导致功能信任度下降。
- **高负载下的稳定性**：`#1515`（日志超时）与 `#2126`（迁移锁竞争）的修复表明，用户在一台机器上长时间、高强度使用后，对 App 的容错能力提出了较高要求，任何静默失败都是不可接受的。
- **对生产力和便利性的追求**：`#1522`（手动添加模型的疲惫感）和 `#1526`（无法区分会话类型的杂乱感）反映了用户希望在工具使用中获得更高效率的普遍倾向。

---

## 7. 待处理积压

目前可见的长期待办事项如下：

- **Electron 依赖版本升级**：[#1277](netease-youdao/LobsterAI PR #1277) `chore(deps-dev): bump the electron group across 1 directory with 2 updates`
  - **状态**：✅ 处于可合并状态（已更新且 CI 应已通过），但尚未被维护者合并。
  - **风险提示**：该 PR 将 Electron 从 `40.2.1` 升级至 `42.3.3`，差异两个主版本。虽由 Dependabot 保持更新，但考虑到 Chromium 内核升级通常带来 **安全补丁**、**API 废弃** 以及 **破坏性变更**，建议维护者尽快组织评审与合并，避免因版本差过大导致未来的升级成本陡增，并填补潜在的安全漏洞窗口。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

好的，这是为您生成的 TinyClaw 项目动态日报。

# TinyClaw 项目动态日报（2026-06-09）

**数据来源：** github.com/TinyAGI/tinyagi
**客观 · 数据驱动 · 聚焦项目健康度**

---

### 1. 今日速览

项目今日整体活跃度较低。过去 24 小时内没有产生新的 Issue，也没有任何 PR 被合入主分支。
- **代码动态**：仅有 1 条新的 Pull Request（#280）提交，目前处于待合并状态。
- **社区动态**：讨论区处于静默状态，无新评论或反馈。
- **健康度评估**：虽然整体静态，但 PR #280 针对的是核心依赖（`better-sqlite3`）的安装体验问题，属于优化开发者体验（DX）的重要信号。项目目前处于**维护与基础体验打磨阶段**。

---

### 2. 版本发布

**无**

（过去 24 小时内无新版本发布通知）

---

### 3. 项目进展

今日无 PR 被合并，项目主干代码没有发生变更。

**重要推进状态**：
- **安装体验优化**：社区开发者提交了 PR #280，尝试通过自动化脚本解决 `better-sqlite3` 的原生模块编译问题。虽然尚未合入，但这标志着项目开始重视“从零开始的安装流畅度”，是向更广泛用户开放使用的必要前置工作。

---

### 4. 社区热点

今日唯一的社区动态来源于一条 Pull Request：

- **[PR #280] fix(install): add postinstall script to auto-rebuild better-sqlite3**
  - **作者**: dsy122
  - **链接**: [TinyAGI/tinyagi PR #280](TinyAGI/tinyagi PR #280)
  - **状态**: 🔴 待合并（0 条评论，0 👍）

- **背后诉求分析**：
  `better-sqlite3` 是 TinyClaw 底层的核心数据库驱动。它是一个原生 C++ 模块，需要在当前 Node.js 环境下编译。在没有正确 `rebuild` 的情况下，新用户执行完 `npm install` 后会立即遭遇**模块找不到**的运行时错误。该 PR 通过添加 `postinstall` 钩子脚本自动化这一步骤，本质上是解决了“项目开箱即用”的最后一公里问题。这是几乎所有使用 native addon 的 Node.js 项目都会遇到的经典痛点，此类 PR 通常代表用户对新手指引和降低门槛的迫切需求。

---

### 5. Bug 与稳定性

今日未收到新的 Bug 报告。

**现存高优先级问题（通过 PR 反推）：**

- **严重程度：高**
- **问题描述**：项目在全新安装（fresh install）后，无法直接启动。因为 `better-sqlite3` 包的预编译二进制文件与本地 Node.js 版本不匹配或缺失，需要用户手动执行 `npm rebuild better-sqlite3`。
- **影响范围**：所有新开发者/用户的首次运行体验。属于**入口阻断型**问题。
- **修复状态**：[PR #280](TinyAGI/tinyagi PR #280) 已提出修复方案（通过 `postinstall` 自动重编译）。该方案风险较低，属于业界标准实践，建议维护者快速审阅合并。

---

### 6. 功能请求与路线图信号

- **新增请求**：今日无。
- **路线图信号**：
  - PR #280 修复的是“安装”过程，而非业务逻辑。这通常不是临时起意的修复，而是**规模化推广的前奏**。
  - 对于 AI Agent 项目，如果无法让用户顺畅体验，功能再强也会流失大量用户。该 PR 表明项目的关注点正在从“功能性”向“可用性/可及性”转移。这通常意味着团队可能在准备一个面向更广泛受众的发布版本。

---

### 7. 用户反馈摘要

今日无显性文字反馈（Issues & PR 评论均为 0）。

**间接用户痛点提取**：
- **核心痛点**：安装步骤繁琐，容易失败。PR #280 的摘要明确指出用户会遇到错误，这表明至少部分核心用户或贡献者（作者 dsy122 本人）在实际使用中被该问题困扰过。
- **关键结论**：**项目的新手上手体验是目前用户体验链路中最薄弱的环节**。该问题如果长期存在，将严重影响项目在 GitHub 上的收藏率和转化率。

---

### 8. 待处理积压

根据现有数据，当前最关键待处理项为：

- **[高优先级] PR #280: 安装自动修复脚本**
  - **活跃时间**：创建于 2026-06-08，已开放 1 天。
  - **链接**: [TinyAGI/tinyagi PR #280](TinyAGI/tinyagi PR #280)
  - **状态**：等待 Code Review。
  - **处理建议**：该 PR 涉及构建流程（`package.json` 的 `scripts`），建议维护者重点确认：1）该脚本是否会增加明显的首次安装耗时；2）是否兼容 Windows/CI 环境；3）是否与现有的 `preinstall` 或 `postinstall` 逻辑冲突。
  - **提醒**：该 PR 直击用户留存命门，建议尽快安排 Review，若方案合理应第一时间合入 `next` 或 `main` 分支。

> 总结：项目今日处于“暴风雨前的宁静”，虽然数据表面波澜不惊，但 #280 的开局暗示着社区正在推动项目向更成熟、更易用的方向进化。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，这是根据 CoPaw (QwenPaw) 实时数据生成的 2026-06-09 项目动态日报。

---

## CoPaw (QwenPaw) 项目动态日报 — 2026-06-09

### 1. 今日速览

项目在过去 24 小时维持着极高的迭代活跃度。共处理 38 个 Issue 和 41 个 Pull Request，关闭/合并了 22 个 PR 与 18 个 Issue。核心进展包括**插件前端扩展框架的合并**（为插件生态奠定基础）以及多项关键 Bug 修复（如**微信定时任务推送失败、Agent 回复重复**）。社区讨论热烈，用户高度认可本地化体验，并围绕 Agent 自主进化（Hermes 学习循环）和后端架构升级（AgentScope 2.0 迁移）提出了极具前瞻性的建议。**健康度评估：高（⭐⭐⭐⭐）**，Bug 修复响应迅速，社区生态建设步入快车道。

### 2. 版本发布

今日无新版本发布。

### 3. 项目进展 — 过去 24 小时核心推进

- **生态基础设施：插件前端扩展框架合并**
  - **[PR #4997](https://github.com/agentscope-ai/QwenPaw/pull/4997) (feat(console): Plugin extension infrastructure)**：已完成合并。该 PR 为插件提供了统一的前端扩展点注册机制（菜单、路由、插槽），标志着 QwenPaw 正式具备标准化的前端插件能力，为即将到来的“插件市场”功能铺平了道路。

- **ACP 协议增强**
  - **[PR #4949](https://github.com/agentscope-ai/QwenPaw/pull/4949) (feat(acp): advertise commands, surface errors...)**：扩展了 Agent Client Protocol，使第三方终端客户端（如 TUI）能够获得更丰富的命令、错误和元数据支持。

- **渠道和核心稳定性修复（已关闭）**
  - **微信 iLink 定时任务失败** ([Issue #4477](https://github.com/agentscope-ai/QwenPaw/issues/4477))：针对 `context_token` 过期无重试、文件发送无日志问题进行修复。
  - **Agent 回复重复** ([Issue #4300](https://github.com/agentscope-ai/QwenPaw/issues/4300))：解决了 Agent 输出以及 Thinking 步骤双重执行的 Bug。
  - **MCP 工具名兼容性** ([Issue #4918](https://github.com/agentscope-ai/QwenPaw/issues/4918))：修复了 MCP 工具名含 `.` 导致 GPT-5.5 模型调用失败的问题。
  - **内存压缩崩溃** ([Issue #5019](https://github.com/agentscope-ai/QwenPaw/issues/5019))：修复了 `pre_reasoning` 钩子中因变量类型假设导致的内存压缩崩溃。

### 4. 社区热点

- **🔥 最热先锋讨论：Agent 学习循环 (Learning Loop)**
  - **[Issue #5017](https://github.com/agentscope-ai/QwenPaw/issues/5017)（7 评论, 2 👍）**：用户 `tecgic` 代表社区发出了深具洞察力的声音，在点赞 QwenPaw “国内用起来特别舒服” 的同时，强烈建议项目关注 Hermes Agent 的 **学习循环** 特性——让 Agent 从自身行为中自动创建并迭代技能。这反映了社区对 Agent 从“被动执行者”进化为“自主学习体”的核心诉求。
- **🔥 最重磅决策讨论：AgentScope 2.0 后端迁移**
  - **[Issue #4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)（6 评论, 2 👍）**：AgentScope 2.0 的发布促使项目开始规划后端架构的重大升级。这是一项 Breaking Change，虽短期有适配成本，但社区普遍认为这是保持技术先进性的必要举措。
- **📊 高关注度 Bug 修复拉动信心：**
  - 微信 iLink 定时任务失败 ([#4477](https://github.com/agentscope-ai/QwenPaw/issues/4477), 15 条评论) 和 Agent 回复重复 ([#4300](https://github.com/agentscope-ai/QwenPaw/issues/4300), 6 条评论) 等顽固 Bug 的关闭，显著提振了社区对项目稳定性的信心。

### 5. Bug 与稳定性

- **严重 ◉ 新增高影响 Bug**
  - **无限图片压缩循环导致幻觉** ([[#4895]](https://github.com/agentscope-ai/QwenPaw/issues/4895))：上传图片后系统陷入“压缩→注入→再压缩”死循环，造成严重输出幻觉。当前无明确修复 PR。
  - **Web Console 多 Agent 不稳定** ([[#5016]](https://github.com/agentscope-ai/QwenPaw/issues/5016), NEW)：自定义/导入的 Agent 会话无法可靠创建和显示。
  - **主动模式微信频道重复回复** ([[#5030]](https://github.com/agentscope-ai/QwenPaw/issues/5030), NEW)：开启后概率性重复回复，需关闭主动模式或重启容器恢复。
  - **Pet 功能严重卡顿/闪退** ([[#5029]](https://github.com/agentscope-ai/QwenPaw/issues/5029), NEW)：体验极差，社区建议标注为实验性功能。
  - **Skill 斜杠命令显示异常** ([[#5031]](https://github.com/agentscope-ai/QwenPaw/issues/5031), NEW)：Console 中调用 Skill 时错误展开显示 SKILL.md 内容。
- **警告 ◍ 已有修复方案或 PR 待合并**
  - **MCP 进程堆积** ([Issue #4834](https://github.com/agentscope-ai/QwenPaw/issues/4834))：重启后 MCP 子进程残留导致系统缓慢。修复 **PR [#5014](https://github.com/agentscope-ai/QwenPaw/pull/5014)** 正在审查。
  - **Subagent 无限轮询** ([Issue #4873](https://github.com/agentscope-ai/QwenPaw/issues/4873))：同时启动两个 Subagent 后台任务会导致主 Agent 高频空转且无法中断。
  - **OneBot 监听端口释放** ([Issue #4926](https://github.com/agentscope-ai/QwenPaw/issues/4926))：热重载时 Websocket 端口未被正确释放，导致插件完全失效。
  - **Windows 桌面端卡顿** ([Issue #5015](https://github.com/agentscope-ai/QwenPaw/issues/5015))：任务执行时前端加载不流畅，CPU激增。

### 6. 功能请求与路线图信号

- **🚩 路线图核心信号**
  - **插件市场 (Plugin Market) 已在路上** ([[PR #5023]](https://github.com/agentscope-ai/QwenPaw/pull/5023))：基于 [#4997](https://github.com/agentscope-ai/QwenPaw/pull/4997) 的框架，该新增 PR 将带来“插件市场”标签页，支持从 AgentScope 平台浏览和安装社区插件。生态构建再加速。
  - **轻量级目标模式 (Goal Mode)** ([[PR #4443]](https://github.com/agentscope-ai/QwenPaw/pull/4443), May 16)：`/goal` 模式功能待合并，可增强 Agent 在执行任务时的导向性。
- **🔥 高赞用户需求**
  - **独立视觉模型配置** ([[#4992]](https://github.com/agentscope-ai/QwenPaw/issues/4992), 1 👍)：纯文本模型通过独立视觉模型获得图片理解能力，场景非常务实。
  - **记忆系统自进化** ([[#4994]](https://github.com/agentscope-ai/QwenPaw/issues/4994), 1 👍)：呼吁引入分层记忆系统，提升长期记忆能力。
  - **工作目录规范化** ([[#4408]](https://github.com/agentscope-ai/QwenPaw/issues/4408))：建议将配置文件统一收纳至隐藏目录，维护工作区整洁。

### 7. 用户反馈摘要

- **😄 满意点**
  - **本地化与易用性深受好评**：用户在 [[#5017]](https://github.com/agentscope-ai/QwenPaw/issues/5017) 中称赞项目“设置清晰无门槛，开箱即用”，这是对产品体验和社区本地化工作的极大肯定。
- **😥 痛点与诉求**
  - **第三方模型/服务整合阵痛**：阿里云 `Code Plan` ([#5003](https://github.com/agentscope-ai/QwenPaw/issues/5003))、九 router ([#5001](https://github.com/agentscope-ai/QwenPaw/issues/5001)) 等模型兼容性问题频发，KimiCode 不显示思考过程([#5013](https://github.com/agentscope-ai/QwenPaw/issues/5013))，第三方生态对接仍需打磨。
  - **交互控制缺失**：用户在 [[#4606]](https://github.com/agentscope-ai/QwenPaw/issues/4606) 中强烈期望能在 Agent 执行任务过程中“中途干预方向”，这是 Agent 可控性的一个核心空白。
  - **可观测性不足**：微信通道静默失败无日志 ([#4477](https://github.com/agentscope-ai/QwenPaw/issues/4477))，普通用户难以自行排查问题。

### 8. 待处理积压

- **⏳ 积压最久的严重 Bug**
  - **GPT-5.x 模型 max_tokens 错误** ([[Issue #2777]](https://github.com/agentscope-ai/QwenPaw/issues/2777))：自 4 月 1 日提出，已搁置超 2 个月。硬编码的模型列表导致所有 GPT-5.x 模型用户受到影响。**强烈建议项目团队优先处理此兼容性问题，或将其明确标记为已知限制。**
- **⏳ 待合并的关键 PR**
  - **DataPaw 商业智能插件** ([[#4622]](https://github.com/agentscope-ai/QwenPaw/pull/4622))：功能完整的 12 项 BI 技能插件，提交近 3 周，等待 Code Review。
  - **Tauri 桌面端自动更新** ([[#4669]](https://github.com/agentscope-ai/QwenPaw/pull/4669))：对桌面用户体验至关重要，积压超 3 周。
  - **可折叠代码块** ([[#4345]](https://github.com/agentscope-ai/QwenPaw/pull/4345))：Console 前端细节优化，已积压近 1 个月。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我已根据您提供的 ZeroClaw 项目数据，生成了以下项目动态日报。

---

# ZeroClaw 开源项目动态日报
**日期:** 2026-06-09
**数据时间窗口:** 2026-06-08 至今

---

### 1. 今日速览

ZeroClaw 项目在过去24小时内呈现出极高的活跃度，Issue 和 PR 的更新数量均达到50条，表明社区和开发者的参与热情高涨。核心开发团队正集中精力解决高优先级（`priority:p1`）和严重性（`S0/S1`）的 Bug，同时积极推动安全架构（OIDC、可插拔安全策略）和基础设施（Gateway 路由、频道隔离）的RFC演进。尽管无新版本发布，但多项重大修复（如 Matrix 频道会话隔离、文件写入损失数据风险）已通过 PR 提交，项目整体健康度健康，正处于密集的功能迭代与稳定性加固阶段。

### 2. 版本发布

**无** - 过去24小时内无新版本发布。

### 3. 项目进展

今日多项重大修复和功能增强的 PR 已关闭或被合并，标志着项目在稳定性和架构上迈出了重要一步。

- **修复了 Matrix 频道的关键数据损坏与身份混淆 Bug**：`PR #7388 (已关闭)` 通过隔离每个 Matrix 实例的会话存储并修复密钥备份，解决了 `Issue #6487` 中报告的“多别名共享同一会话导致账号混淆”的严重（S1）问题。这是一个破坏性变更，需要用户进行会话迁移。
- **修复了 Agent 历史记录被清空的潜在灾难性 Bug**：`PR #7403 (已关闭)` 在 `trim_history` 函数中增加了安全防护，防止因孤儿消息清理级联导致对话历史被完全清空，从而避免了智能体失去上下文的问题。
- **硬件/物联网集成 Demo 取得进展**：`PR #6148 (已关闭)` 和 `PR #7363 (待合并)` 分别完成了基于 Telegram 的智能房间 Demo 和主机端 Telegram ESP32 模拟器框架，标志着 ZeroClaw 向物联网控制领域迈出了实质性一步。
- **Cron 任务重复执行问题得到修复**：`PR #7348 (待合并)` 解决了 `Issue #6037` 中 Cron 任务在守护进程启动后因追赶执行而导致重复触发的 Bug。

### 4. 社区热点

- **`Issue #6909: [RFC] 桌面交互支持（Computer-use）`** (6条评论)
    - **链接**: [Issue #6909](zeroclaw-labs/zeroclaw Issue #6909)
    - **分析**: 该 Issue 获得了社区的广泛关注，讨论热度高。用户核心诉求是为 ZeroClaw 增加类似 OpenAI Codex 的计算机使用能力（截屏、鼠标键盘控制）。这表明社区对 ZeroClaw 从“对话工具”向“自主操作代理”演进的期望很高，是通往通用数字助手的关键能力。
- **`Issue #6699: tool_filter_groups 对 MCP 工具无效`** (7条评论)
    - **链接**: [Issue #6699](zeroclaw-labs/zeroclaw Issue #6699)
    - **分析**: 此 Issue 是今日评论数最多的问题，暴露出 MCP 工具过滤功能完全失效的严重 Bug。社区用户 nick-pape 深入分析了代码，指出了前缀匹配错误和延迟加载集成两个独立 Bug，引发了开发者关于 MCP 工具配置机制的热烈讨论，表明社区对 MCP 集成的正确性和可用性有很高要求。
- **`Issue #5844: [Bug]: 系统提示词过度强调记忆`** (5条评论)
    - **链接**: [Issue #5844](zeroclaw-labs/zeroclaw Issue #5844)
    - **分析**: 这是一个长期存在的核心体验问题。用户抱怨 AI 在生成回复时过度依赖历史记忆，而忽视了当前 Prompt 的指示，尤其影响定时任务等场景。这反映了 Agent 应用中“记忆利用与即时指令”之间的平衡难题，是社区普遍关心的痛点。

### 5. Bug 与稳定性

以下列出了过去24小时内被提及或更新的重要 Bug，按严重程度排列。

- **S0 - 数据丢失/安全风险**:
    - `Issue #4627`: [文件写入工具在 Docker 环境中无声失败](zeroclaw-labs/zeroclaw Issue #4627)。 (`status: in-progress, accepted`)
        - **Fix PR**: `PR #7129` 已提交，旨在通过限制向临时工作区写入来修复此问题，目前处于待合并状态。
- **S1 - 工作流阻塞**:
    - `Issue #6434`: [Shell 工具在 `autonomy level = "full"` 下被拒绝调用](zeroclaw-labs/zeroclaw Issue #6434)。 (`status: in-progress, accepted`)
    - `Issue #6361`: [上下文压缩器删除了工具调用的轨迹，导致 MiniMax 等提供商工具循环](zeroclaw-labs/zeroclaw Issue #6361)。 (`status: in-progress`)
- **S2 - 功能降级**:
    - `Issue #6254`: [WASM 插件安装路径与运行时扫描路径不一致，导致插件不可见](zeroclaw-labs/zeroclaw Issue #6254)。 (`status: accepted`)
    - `Issue #6350`: [WhatsApp Web 通道的白名单过滤对 LID 格式联系人失效](zeroclaw-labs/zeroclaw Issue #6350)。 (`status: in-progress, accepted`)

### 6. 功能请求与路线图信号

- **安全架构升级（v0.9.0 候选特性）**:
    - `Issue #7141`: 提出了对 **OIDC 认证提供商** 支持的 RFC，旨在大幅提升企业级接入的安全性。`PR #7365` 也在进行文档和配置接口的全面重构，可能与新架构版本相关。
    - `Issue #7142`: 提出了将安全实施层暴露为 **可插拔提供商接口** 的 RFC，旨在让用户自定义安全策略。
    - `Issue #7155`: 提出了为高风险 Shell 命令增加 **逐次执行确认** 和策略模式（允许/询问/拒绝），类似于 Claude Code 的安全策略。
- **基础设施与工具链强化**:
    - `Issue #6909`: **桌面交互能力** 的 RFC 是向“通用计算机控制代理”演进的关键信号。
    - `PR #7267`: 实现 `[[mcp.servers]]` 的 **逐字段编辑** 功能，将极大提升 MCP 服务器的管理体验。
    - `PR #7367`: **Gateway 入站 Webhook 路由** 功能，允许为频道别名创建独立端点，是支持多实例部署的关键。

### 7. 用户反馈摘要

- **正面反馈**: 用户对社区和开发者的响应速度表示关注。例如，`Issue #3767` 中关于 TOTP 双因素认证的需求，虽然尚未实现，但维护者已将其状态标记为 `in-progress`，显示了团队对安全需求的重视。
- **核心痛点**:
    - **稳定性问题**: 用户 `Themoonshinesontheriver` 报告了在 WSL2 环境下 **连续 OOM（内存溢出）** 导致进程被内核杀死 (`Issue #5542`)，这是一个严重影响使用的稳定性问题。
    - **集成体验不佳**:
        - 用户 `yaoyunnuo` 反馈 **飞书频道集成后，只调用了 LLM 而不是 Agent** (`Issue #4873`)，导致无法使用工具。
        - 用户 `nrpx` 抱怨 **Gemini CLI OAuth 认证完全无法工作** (`Issue #4879`)，给尝试使用 Gemini 模型的用户造成了很大困扰。
        - 用户 `edgarkech` 报告 **电报频道无法使用提示缓存** (`Issue #6360`)，导致响应变慢且浪费成本。
    - **配置预期不符**: 用户 `perlowja` 指出 `runtime_profiles.*.max_tool_iterations` 配置项不生效，必须设置在 `[agents.*]` 下 (`Issue #6877`)，这给用户配置带来了困扰和认知偏差。

### 8. 待处理积压

以下是在过去24小时中被提及或更新的长期未解决的重要问题，需要维护者持续关注。

- **`Issue #3767`: [Feature]: 跨频道 TOTP 保护关键工具执行** (2026-03-17 创建)
    - **状态**: `status: in-progress, accepted`
    - **链接**: [Issue #3767](zeroclaw-labs/zeroclaw Issue #3767)
    - **提醒**: 自3月以来，该功能请求一直在“进行中”。虽然近期有相关安全问题（如 #7141，#7155）被提出，但此更早期的、综合性的 TOTP 安全门控功能仍需明确的时间表。
- **`Issue #6074`: [审记] 追踪因批量还原而丢失的 153 次提交** (2026-04-24 创建)
    - **状态**: `status: in-progress`
    - **链接**: [Issue #6074](zeroclaw-labs/zeroclaw Issue #6074)
    - **提醒**: 这是代码库的一次较大事故，需要仔细审阅并逐步恢复丢失的特性或修复，否则可能导致回归。目前状态仍在进行中。
- **`PR #6973`: [fix]: 修复 WhatsApp Web 对 LID JID 的处理** (2026-05-27 创建)
    - **状态**: `needs-author-action`
    - **链接**: [PR #6973](zeroclaw-labs/zeroclaw PR #6973)
    - **提醒**: 此 PR 已经提交，但被标记为“需要作者操作”，特别是牵涉到潜在地兼容性问题。考虑到 `Issue #6350` 同样涉及 WhatsApp LID 问题，此 PR 的推进对于修复 WhatsApp 通道至关重要。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*