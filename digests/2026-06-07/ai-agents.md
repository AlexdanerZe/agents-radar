# OpenClaw 生态日报 2026-06-07

> Issues: 296 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-07 03:35 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我已根据您提供的 OpenClaw 项目数据，为您整理出 2026-06-07 的项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-07

## 1. 今日速览

项目今日保持**极高的活跃度**。过去 24 小时内，社区提交了 500 条 Pull Request 更新，Issue 更新达 296 条，同时发布了两个 Beta 版本，表明核心团队正在积极迭代以解决用户反馈的问题。尽管 Issue 关闭率（146条）与新开率（150条）基本持平，但待合并的 PR 积压至 397 条，反映出代码审查与合并流程可能面临较大压力。**当前项目最核心的矛盾集中在 v2026.6.1 引入的 OpenAI ChatGPT Responses 集成回归问题，以及 DeepSeek Prompt Cache 失效导致的成本飙升上**。社区对版本稳定性的诉求明显增强。

## 2. 版本发布

- **v2026.6.5-beta.2 / v2026.6.5-beta.1** (连续发布)

**主要变更亮点：**
1.  **修复 QQBot 推理内容泄露**：现在 QQBot 通道在原生发送消息前会自动剥离模型的推理/思维链内容（`<thinking>` 标签），防止原始推理过程泄露到群聊或频道回复中。（参考 Issues #89913, #90132）感谢贡献者 @openperf。
2.  **强化 MCP 工具结果处理**：更新了 MCP 工具结果的强制转换逻辑，对 `resource_link`、`resource`、`audio` 以及畸形图片等字段进行了规范化处理，提升了对未来扩展的兼容性。

**破坏性变更与迁移注意事项：**
- 本次 Beta 为增量修补，未报告破坏性变更或数据库 Schema 迁移需求。

## 3. 项目进展（重要 PR 合并与推进）

过去 24 小时内，项目在闭合 Bug、优化文档以及重构核心模块方面取得了实质性进展：

- **稳定性修复**：
  - **OpenRouter 费用核算**：PR #91073 已合并，修复了 OpenRouter 流式请求完成后最终成本的核算不准问题。
  - **飞书（Feishu）通道强化**：PR #89659 为飞书 API 增加了请求限流重试逻辑（错误码 230020/230006），提升了因发送频率过高导致失败的场景下的稳定性。
  - **iMessage 通道文档**：PR #91032 已关闭，更新了 macOS 环境下注入 iMessage 所需的 DisableLibraryValidation 条件，明确其在现代 macOS（包含 macOS 26）上的必要性与门控机制。
  - **插件与媒体修复**：修复了 `@openclaw/bluebubbles` 插件在 v2026.5.28/v2026.6.1 上的崩溃问题（#90509）；修复了 `read` 工具无法读取 WebChat 上传媒体文件的问题（#90964）。

- **功能推进**：
  - **记忆核心（Memory Core）重构**：PR #91072（已合并）将记忆维基（Memory Wiki）的源同步状态从 JSON 文件迁移至 SQLite 存储，提升了数据一致性与容量管理能力。
  - **模型运行时公开**：PR #90328 为模型列表增加了 `agentRuntime` 元数据，并在 WebUI 模型选择器中展示非默认运行时标签（例如显示“GPT-5.5 · OpenAI Codex”），这标志着 OpenClaw 在多运行时管理上迈出了重要一步。
  - **子智能体改进**：PR #91076 修复了 v2026.6.1 中 Codex 子智能体回合因孤立 `tool.call` 结果而被标记为 `promptError`，导致回复无法递达的问题。

## 4. 社区热点（高关注度议题）

今日社区讨论热度最高的议题高度集中于 **v2026.6.1 的集成问题群**以及**成本控制**：

1.  **OpenAI ChatGPT Responses 传输层大面积故障（P1 群集）**
    - `#90083`（14 条评论）：升级至 6.1 后，使用 gpt-5.4/5.5 模型直接导致 `invalid_provider_content_type` 错误。这是目前阻碍用户使用最新模型的核心问题。
    - `#90093`（9 条评论）：“原生回放”功能错误发送了加密的推理内容，导致后续回合因 `invalid_encrypted_content` 直接 400 错误，双端对话进程中断。
    - 分析：社区对 OpenAI 新 API 的高度依赖与 6.1 版本的集成成熟度形成了冲突。用户迫切需要一个稳定、无加密异常的 OpenAI Responses 传输实现。

2.  **DeepSeek Prompt Cache 失效（高成本预警）**
    - `#91018`（4 条评论，但获得了“严重警告”标签）：用户反馈从 2026.5.7 升级至 6.1 后，DeepSeek 的 Prompt Cache 完全失效，仅一小时内就烧掉了约 6 美元的成本。这直接触动了用户的“钱袋子”，引发了强烈的升级恐慌。

3.  **Cron 与系统稳定性**
    - `#90991`（7 条评论）：新报告的 P1 级 Bug，Cron 定时触发器会污染全局运行时状态，导致系统范围内间歇性过载。这揭示了调度系统在架构上可能存在深层次的隔离缺陷。

## 5. Bug 与稳定性

根据社区报告的严重程度，以下是过去 24 小时内需要重点关注的 Bug：

| 严重程度 | 问题编号 | 问题描述 | 是否有修复 PR |
| :--- | :--- | :--- | :--- |
| **🔴 P1 / 成本** | `#91018` | 6.1 升级导致 DeepSeek Prompt Cache 失效，成本飙升 | 暂无（仅报告） |
| **🔴 P1 / 功能瘫痪** | `#90083` | OpenAI Responses 传输 `invalid_provider_content_type` 错误 | 暂无 |
| **🔴 P1 / 系统稳定** | `#90991` | Cron 调度器污染全局状态，导致系统过载 | 暂无 |
| **🔴 P1 / 归回归** | `#88312` | Codex app-server 回合完成停滞（Regression of #84076） | 暂无 |
| **🔴 P1** | `#90925` | 子智能体压缩进入 OpenAI API-key 路由导致 OAuth 失败 | 暂无 |
| **🟡 P2** | `#90595` | Cron 失败通知在热加载/重试时频繁发送，导致告警疲劳 | 暂无 |
| **🟡 P2** | `#91042` | 回复上下文截断函数未覆盖所有路径，导致消息体过长 | 暂无 |
| **🟡 P2** | `#88929` | 飞书流式卡片出现异常打字机效果且内容截断 | 暂无（#89659 修复了限流） |
| **🟢 已有修复** | `#90903` | 非默认智能体模型目录未继承，运行时找不到模型 | PR `#90903` 待合并 |
| **🟢 已有修复** | `#90128` | 会话滚动时用户手动 `/model` 覆盖设置被丢弃 | PR `#90128` 待合并 |
| **🟢 已有修复** | `#91076` | Codex 子智能体回复因孤立 tool.call 被抑制 | PR `#91076` 待合并 |
| **🟢 已有修复** | `#89659` | 飞书发送消息超限导致失败 | PR `#89659` 待合并 |

## 6. 功能请求与路线图信号

社区提出的功能需求已经逐渐超越“修修补补”阶段，开始形成清晰的生态建设方向：

1.  **上下文与记忆增强（高优先级）**
    - `#90916` [Feature]：提出“话题-会话家族”概念，允许一个智能体在不同的话题频道（命名上下文）中隔离对话，共享持久记忆。这是对现有扁平化 session 管理的重大升级。
    - `#58818` [Feature]：要求保证智能体上下文中始终保留最近的 N 条原始消息，防止被压缩或日重置删除。结合 `#90354`（预压内存刷写校验），表明用户正在追求更可控且可预测的记忆系统。

2.  **本地模型与隐私（持续走强）**
    - `#89265` [Feature]：提议将本地模型（如 Ollama、LocalAI 等）提升为“一等公民”。随着开源模型质量提升，社区对降低 API 成本和数据隐私的需求正转化为强烈的功能诉求。

3.  **健康与可观测性**
    - `#62615` [Feature]：请求添加网关侧的不健康会话熔断器，避免网关对一个死循环或损坏的 session 进行无休止的无效重试。
    - `#45508` [Feature]：请求将 WebChat 中的 TTS/STT 通过网关路由，支撑自建语音服务的全面集成。

**路线图信号**：PR `#90328`（暴露模型运行时选择器）和 PR `#90101`（运行时自我上下文）的推进，暗示项目正在为更复杂的 Runtime 管理和分层架构做准备，这与社区对“上下文隔离”和“本地模型”的诉求高度契合。

## 7. 用户反馈摘要

- **核心痛点**：升级至 v2026.6.1 带来了显著的回归，这是目前压倒性的负面反馈来源。特别是 OpenAI Responses 和 DeepSeek 集成，直接触及模型兼容性和使用成本两大命脉。**“不降级是损失，降级又缺少新功能”** 是许多用户面临的尴尬处境。
- **满意度亮点**：社区对飞书（Feishu）和 QQ 等垂直通道的修复反应积极。用户对`@openperf`等贡献者快速响应 QQBot 泄思问题的专业度表示赞赏。
- **使用场景多样性**：
    - **硬核开发者**：深度使用 Codex 进行多步骤复杂任务，对会话稳定性和工具结果保真度要求极高。
    - **成本敏感用户**：使用 Proxy/Pool 提供者和 DeepSeek 的用户，对 Fallback 逻辑和缓存策略极其关注。
    - **企业/组织用户**：依赖飞书、iMessage 等通道进行日常协作，期望功能表现稳定且UI/UX无瑕疵。
- **不满情绪**：#90595 提出的“告警疲劳”问题（Cron 框架在重试/热加载时频繁发送失败通知）反映了框架在系统可靠性工程（SRE）方面的用户体验仍有待打磨。

## 8. 待处理积压

以下是一些值得维护者重点关注、长期未解的积压项：

- **P1/P2 级长期 Issue**：
    - `#49603`（3月18日）：网关重启后孤儿锁文件未清理。涉及到进程级状态恢复，架构影响面大，但长期悬而未决。
    - `#59413`（4月2日）：模型回退时逐候选重试次数。该请求直接关系到 API Pool 类提供商的生存质量，但因涉及产品决策和机制变更，一直停留在“需要产品决策”状态。
    - `#43015`（3月11日）：`message.send` Schema 过度暴露高级字段。直接导致 GPT 家族模型随机填充导致校验失败，是典型的“过度开放”引发的副作用。

- **等待作者的大型 PR**：
    - `#78441`（5月6日）：子智能体 `toolsAllow` 白名单转发。XL 级功能，作者已超过一个月没有更新。
    - `#90101`（6月4日）：运行时自我上下文配置与工具。XL 级 PR，是架构级改进的一部分，但作者暂时未响应后续反馈。
    - `#91053`（6月7日）：Zalo 媒体存储重构。XL 级重构，刚提交，处于等待作者响应状态。
    - 这些大型 PR 的长期停滞，反映了社区贡献者驱动的复杂功能开发缺乏核心维护者的直接支持，可能会导致功能碎片化。

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析报告

**报告日期：2026-06-07 | 分析周期：过去 24 小时**  
**数据来源：OpenClaw / NanoBot / Hermes Agent / PicoClaw / NanoClaw / IronClaw / LobsterAI / Moltis / CoPaw / ZeptoClaw / ZeroClaw 等 11 个项目 GitHub 公开动态**

---

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正经历高强度的分化与整合。一线项目保持每日数百次代码变动的迭代节奏，但**版本稳定性与成本控制已成为核心矛盾**——多个项目因缓存失效、回归 Bug 导致用户升级意愿下降。同时，技术方向迅速收敛：**记忆系统向结构化持久化演进，MCP 与 WASM 成为工具扩展的标准化路径，多代理协作正从原型走向产品化**。边缘部署（<7MB 二进制、ARM 原生支持）和本地模型优先的诉求崛起，驱动项目从“重 API 集成”转向“端侧可自持”的架构重设计。社区整体健康度呈两极分化：头部项目在承载巨量贡献的同时面临审查积压，而部分聚焦型项目以工程纪律换取可靠交付，显示出不同的成熟路径。

---

## 2. 各项目活跃度对比

| 项目 | Issues 动态 | PR 动态 | 版本发布 | 健康度评估 |
|------|-------------|---------|----------|------------|
| **OpenClaw** | 296 更新（150 新开 / 146 关闭） | 500 更新（约 103 合并，397 待合并） | 2 个 beta | 极高活跃，但 PR 审查积压严重，稳定性风险突出 |
| **NanoBot** | 7 更新（4 新开 / 3 关闭） | 24 更新（10 合并 / 14 待合并） | 无 | 高度活跃，社区协作闭环快，健康度良好 |
| **Hermes Agent** | 50 更新 | 50 更新（大量安全修复 PR 待合并） | 无 | 极高活跃，安全响应积极，跨平台体验是短板 |
| **PicoClaw** | 12 更新 | 18 更新（16 合并，2 待合并） | 1 个 Nightly | 极高活跃，防御性修复增强健壮性，新领域（ClawTrade）启动 |
| **NanoClaw** | 2 新开（均未关闭） | 14 更新（3 合并 / 11 待合并） | 无 | 中等活跃，入门体验 Bug 影响新用户留存 |
| **IronClaw** | 未披露具体数（以 PR 为主） | 30 更新（10 合并 / 20 待合并） | 无 | 高强度迭代，Nightly E2E 失败阻塞门禁（10+ 天） |
| **LobsterAI** | 6 更新 | 2 合并 | 无 | 中等活跃，长期稳定性 Bug 积压，合并节奏偏慢 |
| **Moltis** | 3 新开（2 Bug / 1 Feature） | 2 个活跃 PR 未合并 | 无 | 社区需求旺盛但代码合并暂缓，Docker Auth 关键 Bug |
| **CoPaw** | 11 更新（2 关闭 / 9 活跃） | 0 | 无 | 社区反馈密集但开发侧静默，回归 Bug 亟待修复 |
| **ZeptoClaw** | 2 更新（1 关闭 / 1 新开） | 1 待合并 | 无 | 中等活跃，聚焦二进制体积门禁，工程纪律性强 |
| **ZeroClaw** | 38 更新 | 50 更新（大量合并 + 45 待合并） | 无（v0.8.x 冲刺） | 极高活跃，安全响应优秀，路线图清晰，生态构建加速 |
| **NullClaw / TinyClaw** | 0 | 0 | 无 | 无活动 |

> **数据说明：** 各项目数据来自过去 24 小时的 GitHub 公开动态。部分项目未细分 Issue 与 PR 的新增/关闭数，故以总更新量表示。健康度评估综合了活跃度、合并效率、Bug 响应、社区反馈及风险敞口。

---

## 3. OpenClaw 在生态中的定位

**绝对体量最大、功能最全的“全能选手”，但也因此承受最高的熵增代价。**

### 核心优势
- **社区规模领先：** 24 小时内 500 PR / 296 Issue 的变动量是第二名 ZeroClaw（50 PR / 38 Issue）的近 10 倍，反映出最广泛的外部贡献者基础和用户群。
- **迭代速度最快：** 1 天内发布 2 个 Beta 版，且合并了 Memory Core 重构（#91072）、模型运行时选择器（#90328）等架构级 PR，功能交付密度高于同类项目。
- **渠道覆盖最广：** 已深度集成 QQBot、飞书、iMessage、WebChat 等 10+ 通道，且针对各通道做了专用修复（QQ 推理泄露、飞书限流重试），广度和深度兼备。
- **技术引领性：** 首先提出“话题-会话家族”（#90916）、公开模型运行时元数据等特性，为多会话上下文隔离和运行时管理树立了参考方向。

### 技术路线差异
- **MCP 工具结果强转：** OpenClaw 对 `resource_link`、`audio`、畸形图片做强制规范化，强调兼容性优先，而 NanoBot 和 ZeroClaw 选择通过 allowFrom / SSRF 控制来保障安全。
- **记忆核心数据层迁移：** 从 JSON 转 SQLite（#91072），相比 NanoBot 的 per-user 目录隔离和 CoPaw 的纯 Prompt 压缩，OpenClaw 更倾向统一存储引擎。
- **子智能体深度绑定 Codex：** 强调多步骤复杂任务的回吐保真度（#91076 修复孤立 tool.call），与 Hermes 的 `/goal` 任务编排形成对照。

### 社区规模对比（粗暴量级）
| 指标 | OpenClaw | ZeroClaw | Hermes Agent | NanoBot |
|------|----------|----------|--------------|---------|
| 日 PR 更新 | ~500 | ~50 | ~50 | ~24 |
| 日 Issue 更新 | ~300 | ~38 | ~50 | ~7 |
| 待合并积压 | ~397 | ~45 | 较多 | ~14 |
| 版本频率 | 2 Beta/天 | 无（冲刺中） | 无 | ~1-2 周 |

**定位总结：** OpenClaw 是生态中的“超级集线器”，适合希望一站式覆盖多模型、多通知渠道的硬核开发者；代价是需要承受频繁的升级回归和配置兼容成本。

---

## 4. 共同关注的技术方向

过去 24 小时内，至少有三个方向在 4 个以上项目中同时涌现，反映出行业共性需求：

### A. 记忆与上下文管理 → 结构化、可隔离、不丢数据
| 项目 | 具体诉求 / 动作 |
|------|----------------|
| OpenClaw | Memory Wiki 源同步从 JSON 迁移至 SQLite（#91072）、“话题-会话家族”提案（#90916）、预压校验（#90354） |
| NanoBot | per-user memory 隔离合并（#2968）、microcompact 破坏 prefix caching（#4222） |
| CoPaw | `/compact` 忽略模型 `max_input_length`（#4937）、v1.1.8 压缩阈值不生效（#4661） |
| Hermes Agent | Honcho 记忆注入网关导致隐私泄露（#40170），已修复 |
| ZeroClaw | 会话复活 Bug（#7252）修复，强调杀死 ACP 后持久化不应复活 |
| Moltis | Cap persisted tool results before rehydration（#1089），防止上下文膨胀 |

**趋势解读：** 记忆不再是纯 Prompt 窗口管理，而是数据库级持续化 + 多租户隔离 + 成本感知的缓存策略。**Prompt Cache 的高效性是降本关键**（OpenClaw #91018 / NanoBot #4222）。

### B. 工具调用与插件生态 → MCP、WASM 成为双轨标准
| 项目 | 具体方向 |
|------|----------|
| OpenClaw | MCP 工具结果强转规范化 |
| NanoBot | MCP `allowFrom` 基于用户组访问控制（#2533）、SSRF 检查（#4123） |
| ZeroClaw | WASM 插件沙箱（资源/网络限制，#7335）、远程插件注册表（#7333）、工具命名空间化（#7337） |
| IronClaw | 工具调用共享解析原语（#4522）、统一审计 |
| NanoClaw | HTTP/SSE MCP 传输扩展（#2208） |
| LobsterAI | 批量导出工具结果（#1529） |

**趋势解读：** MCP 协议成为通道层互操作事实标准，WASM 插件则在 ZeroClaw 中被推向边缘计算与沙箱安全。**两者并存但目标不同：MCP 连接外部服务，WASM 扩展运行时能力。**

### C. 安全与成本 → 从附加特性上升为核心设计原则
- **代价感知：** OpenClaw #91018（DeepSeek Prompt Cache 失效，1 小时烧 $6）、NanoBot #4222（前缀缓存被破坏），**提示缓存有效性直接影响用户钱袋子**。
- **沙箱与权限：** Hermes Agent 修复 RCE（#40939）、注入（#40967）；ZeroClaw 实现 WASM 沙箱 + `#[secret]` 配置脱敏修复；PicoClaw 统一类型断言守卫、防御 nil 解引用；NanoClaw 符号链接逃逸修复（#4221）。
- **多代理安全：** OpenClaw #90925 子智能体压缩 API-key 路由导致 OAuth 失败；Hermes #40863 Telegram 未授权用户时机过晚。

**趋势解读：** Agent 权限模型正从“全有或全无”转向细粒度的作用域控制。**端侧安全（符号链接、配置泄露）与 API 成本管控共同驱动了工具设计的收敛。**

---

## 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 技术架构关键特征 |
|------|----------|----------|------------------|
| **OpenClaw** | 全能个人 AI 助手一站式平台 | 硬核开发者、多模型/多通道重度用户 | 单体+模块化，SQLite 记忆核心，MCP 工具强转，模型运行时选择器 |
| **NanoBot** | 最小化二进制 + 快速上手的通用 Agent | 个人开发者、桌面用户 | 单二进制分發，per-user 目录隔离，MCP 访问控制，强调易部署 |
| **Hermes Agent** | 任务编排型 AI 个人 OS | 自动化重度用户、企业管理 | TUI+Gateway，`/goal` 任务中心，安全审查严格，多代理后台 |
| **PicoClaw** | Go 高性能信道集成 + 量化交易扩展 | 运维部署、量化开发者 | 高并发防御性编码，Slack/飞书/LINE 等信道优先，ClawTrade 子系统 |
| **NanoClaw** | 容器化优先的 OneCLI 智能体 | DevOps、容器化部署用户 | 单实例锁（#2697）、Podman 映射、技能符合性改造 |
| **IronClaw** | 下一代组件化 AI 运行时（Reborn） | API 兼容层开发者 | Reborn 架构重构，OpenAI 协议兼容（chatcmpl-*），CI 隔离 |
| **ZeroClaw** | WASM 插件驱动的安全 Agent | 插件开发者、企业部署 | WASM 沙箱+远程注册表，OIDC 认证路线，`#[secret]` 脱敏，版本追踪 |
| **CoPaw** | 本地模型优先的 Qwen 生态 Agent | 通义模型用户、数据隐私敏感用户 | 上下文压缩/阈值优化，本地千问深度对接 |
| **ZeptoClaw** | 极致轻量的边缘 Agent（<7MB） | 树莓派/Jetson/嵌入式开发者 | 二进制体积门禁，aarch64 优化，工程纪律近乎严苛 |
| **LobsterAI** | 多 Agent 协作与定时任务管理 | 团队协作场景 | 批量导出（#1529）、多 Agent 定时归属（#1530）、cowork 模式 |
| **Moltis** | 跨频道活动观测与管控 | 运维运营、多租户部署 | 活动日志可见性设置（#1093）、Cron 存档管理 |

**关键发现：**
- **OpenClaw 是唯一试图覆盖“一切”的项目**，其余项目均在某个维度做减法（体积、安全、本地模型、容器化）。
- **ZeroClaw 与 NanoBot 在“轻量与插件”上形成对比**：前者用 WASM 做重型扩展，后者用 MCP + per-user 保持极简。
- **CoPaw 与 ZeptoClaw 代表“模型垂直”与“硬件垂直”**，前者绑定 Qwen，后者绑定 ARM 边缘设备。

---

## 6. 社区热度与成熟度分层

### 第一梯队：快速迭代期（每日 ≥20 PR / 高度活跃）
- **OpenClaw**：日变动量远超其他，但频繁回归（OpenAI Responses、DeepSeek Cache）显示**成熟度与迭代速度不匹配**，属于“奔跑中修补”状态。
- **ZeroClaw**：同样日 50 PR，但 S0 漏洞 24 小时内修复、路线图透明、待合并 PR 45 个有序推进，**属于高活跃+高成熟度**。
- **Hermes Agent**：50 PR/50 Issue，安全修复密集，但跨平台体验（Intel Mac、Windows）长期未解决，**安全成熟度高，产品化成熟度中等**。
- **PicoClaw**：16 合并/18 总 PR，以防御性修复为主，新方向 ClawTrade 属于探索期，**健壮性成熟度高，新领域尚在起步**。
- **IronClaw**：30 PR，Reborn 架构重写，但 Nightly E2E 失败 10+ 天，**成熟度受影响**。

### 第二梯队：质量巩固期（中等活跃，侧重稳健性）
- **ZeptoClaw**：每日变动少，但精准聚焦体积门禁，工程纪律强，**成熟度极高**。
- **NanoBot**：日 24 PR，社区反馈到修复的周期短（如 #4228 当天合并），**成熟度高+协作效率高**。
- **LobsterAI**：长期 Bug 积压（#1495、#1496 两月未修复），合并速度偏慢，**成熟度中低**。
- **Moltis**：2 个 Feature PR 等待合并，#1112 认证 Bug 影响 Docker 用户，**成熟度中等偏下**。
- **CoPaw**：开发侧静默（0 PR），3 个回归 Bug 无修复，**成熟度偏低，急需维护者响应**。

### 第三梯队：低活跃或停滞
- **NanoClaw**：虽有 PR 但合并少，入门 Bug（#2703）未回复，**成熟度低**。
- **NullClaw / TinyClaw**：24 小时无任何活动，可能已暂停或维护周期过长。

---

## 7. 值得关注的趋势信号

### 1. Prompt Cache 有效性已成成本生命线
OpenClaw #91018（$6/小时）与 NanoBot #4222（微压缩破坏前缀缓存）同时敲响警钟。**AI Agent 项目的用户留存将越来越依赖缓存命中率——微小的上下文变动就能抵消 API 成本优势。** 开发者应设计“缓存感知的上下文构建器”，避免 session 重置、轮换顺序等操作。

### 2. 记忆系统从“窗口管理”进化到“持久化数据基础设施”
OpenClaw 迁移 SQLite、NanoBot 引入 per-user 目录、CoPaw 用户抱怨压缩配置失效——**记忆不再是简单的对话历史裁剪，而是需要支持隔离、容量、混洗索引的存储层。** 这暗示未来 Agent 框架将内置类 Redis 或 SQLite 的记忆服务。

### 3. 多代理协作从单一能力变为产品化功能
Hermes Agent 的 `/goal` + background delegate（#40946）、OpenClaw 的子智能体改进（#91076）、ZeroClaw 的委托代理子循环（#7307）——**多代理不再只是实验性功能，而是进入“任务编排+安全回吐+资源隔离”的产品化阶段。** 独立的子智能体状态管理、跨代理通信协议将成为下一轮竞争焦点。

### 4. 边缘部署与本地模型形成新增长极
ZeptoClaw 的 7MB aarch64 门禁、PicoClaw 的 ClawTrade 量化扩展、CoPaw 对千问 3.6‑27B 的本地支持——**用户越来越希望 Agent 在无互联网或低成本环境下运行。** 这推动项目从“API 客户端”转向“本地推理调度器”，WASM 沙箱和轻量级运行时成为关键使能技术。

### 5. 安全左移成为项目健康度的核心指标
Hermes Agent 一天内修复 RCE、注入、权限绕过；ZeroClaw 修复会话复活和密钥泄露；PicoClaw 批量合并防御性代码——**安全不再是反应式打补丁，而是被嵌入 CI 门禁（符号链接检查、类型断言守卫、配置脱敏）。** 建议所有 Agent 项目将“工具权限最小化”和“敏感字段自动抹除”作为默认行为。

### 6. MCP 与 WASM 形成“外联 + 内扩”的双轨插件标准
MCP 用于服务间互操作（NanoBot allowFrom、IronClaw 工具审计），WASM 用于运行时能力注入（ZeroClaw 沙箱+远程注册表）。**两者互补关系明确：MCP 连接外部 API 和通道，WASM 安全地扩展 Agent 自身的计算和 I/O 能力。** 未来可能出现统一的“插件市场”同时支持两种格式。

---

*报告基于 2026-06-07 各项目公开数据生成，所有引用链接见原日报。分析建议仅供参考，不构成投资或技术选型建议。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 | 2026-06-07

---

## 今日速览

过去 24 小时内 NanoBot 项目保持高度活跃：共处理 7 条 Issue（**4 条新开 / 活跃，3 条关闭**），PR 更新 24 条（**14 条待合并，10 条已合并 / 关闭**）。社区贡献集中在 **Bug 修复**（`reasoning_content` 保留、图片生成兼容、微信 session 死循环、符号链接逃逸等）和 **功能扩展**（AssemblyAI 转录服务、Cron 静默模式、WhatsApp 桥接增强、桌面端 UI 等）。多位核心贡献者（@franciscomaestre、@yu-xin-c、@michaelxer、@hamb1y 等）提交了关键 PR，项目整体健康度良好，社区协作响应迅速。

---

## 版本发布

*（无新版本发布）*（v0.1.4.post6 为当前最新版本，Release 数据无更新）

---

## 项目进展

今日共有 **9 个 PR 被合并 / 关闭**，覆盖多项重要功能推进和稳定性修复：

### 功能特性
- **#2968 —— per-user memory 隔离**  
  `agents.defaults.per_user_memory` 配置标志，使多用户环境下每个用户拥有独立 `memory/` 目录。  
  [PR #2968](https://github.com/HKUDS/nanobot/pull/2968)（2026-04-09 起，今日合并）
- **#2532 —— 新增 Serper.dev 搜索引擎选项**  
  `web.search` 支持 `provider: 'serper'`，作者 @franciscomaestre。  
  [PR #2532](https://github.com/HKUDS/nanobot/pull/2532)
- **#2533 —— 为 MCP 服务器增加 `allowFrom` 访问控制**  
  敏感工具可按用户组限制调用。  
  [PR #2533](https://github.com/HKUDS/nanobot/pull/2533)
- **#4195 —— 桌面端 Shell 与共享 WebUI 表面打磨**  
  为后续桌面版体验做准备，同时改进聊天/设置界面在桌面端的使用。  
  [PR #4195](https://github.com/HKUDS/nanobot/pull/4195)
- **#2529 —— WhatsApp 桥接：音频消息自动下载转写**  
  将 `audioMessage` 转为临时 `.ogg` 文件供代理转录。  
  [PR #2529](https://github.com/HKUDS/nanobot/pull/2529)

### Bug 修复
- **#4228 —— 修复 `reasoning_content=""` 被错误丢弃（fix #4105）**  
  流式响应解析中保留空字符串而非转换为 `None`，解决 DeepSeek 等 API 的思维链字段消失问题。  
  [PR #4228](https://github.com/HKUDS/nanobot/pull/4228)
- **#4209 —— 允许通过 `null extraBody` 去除默认图像参数（fix #4167）**  
  OpenAI 兼容 API 如拒收 `response_format` 时，用户可显式设为 `null` 绕过。  
  [PR #4209](https://github.com/HKUDS/nanobot/pull/4209)
- **#2555 —— WhatsApp 桥接：新连接时关闭旧客户端**  
  防止重连后消息重复投递。  
  [PR #2555](https://github.com/HKUDS/nanobot/pull/2555)
- **#2528 —— WhatsApp 桥接：丢弃启动前消息**  
  记录启动时间戳，避免重启后回复历史消息。  
  [PR #2528](https://github.com/HKUDS/nanobot/pull/2528)

---

## 社区热点

1. **Issue #2573 —— GitHub Copilot 登录失败（3 条评论，9 👍）**  
  用户报告 `nanobot provider login github-copilot` 出现 `Authorization header is badly formatted` 错误，且指出是 switching to openai 后引发。该 Issue 创建于 3 月 28 日，**今日被关闭**，表明已获得修复。热度最高（9 个赞同），反映较多用户关心 Copilot 集成稳定性。  
  [Issue #2573](https://github.com/HKUDS/nanobot/issues/2573)

2. **Issue/PR 联动：`reasoning_content` 空值处理（#4105 / #4228 / #4227）**  
  社区迅速响应，[@michaelxer](https://github.com/michaelxer) 与 [@Yuxin-Lou](https://github.com/Yuxin-Lou) 在同一天提交了两个修复方案（#4228 已合并，#4227 待合并）。对话显示该问题影响 DeepSeek、Kimi K2.5/2.6 等模型，是当前使用自定义 provider 用户的高频痛点。  
  [Issue #4105](https://github.com/HKUDS/nanobot/issues/4105)  
  [PR #4228](https://github.com/HKUDS/nanobot/pull/4228)  
  [PR #4227](https://github.com/HKUDS/nanobot/pull/4227)

3. **集中贡献者 @franciscomaestre 今日提交 4 条新 PR**  
  涵盖 WhatsApp 桥接增强、Cron 静默模式、AssemblyAI 转录、per-user memory（合并），成为今日最活跃开发者。

---

## Bug 与稳定性

按严重程度排列（*表示已有修复 PR 或已关闭）：

| 严重度 | Issue / PR | 描述 | 状态 |
|--------|------------|------|------|
| **高** | [#4222](https://github.com/HKUDS/nanobot/issues/4222) | `max_messages` 截断 & `microcompact` 持续使前缀/提示缓存失效，**每次请求消息前缀均变化，彻底破坏 prompt caching** | 新开，无 PR |
| **高** | [#4105](https://github.com/HKUDS/nanobot/issues/4105) * | 自定义 provider 因空字符串 `reasoning_content` 被丢弃，导致 DeepSeek 等模型思维链字段缺失 | 已关联 PR #4228（已合并），#4227（待合并） |
| **中** | [#4223](https://github.com/HKUDS/nanobot/pull/4223) * | 微信频道 token 过期后 `_poll_once()` 永久死循环（不重新加载 account.json） | 已有 PR #4223（待合并） |
| **中** | [#4221](https://github.com/HKUDS/nanobot/pull/4221) * | `ExecTool` 中相对路径符号链接可逃逸工作目录（#4072） | 已有 PR #4221（待合并） |
| **中** | [#4167](https://github.com/HKUDS/nanobot/issues/4167) ✔️ | 图片生成 API 不支持 `response_format` 导致 `UnsupportedParamsError` | 已由 #4209 修复（已合并） |
| **低** | [#4211](https://github.com/HKUDS/nanobot/issues/4211) | SDK 嵌入时 stdio MCP 在关闭时引发 `Attempted to exit cancel scope in a different task` | Issue 已关闭（未明确说明修复方式） |
| **低** | [#2573](https://github.com/HKUDS/nanobot/issues/2573) (✔️) | GitHub Copilot OAuth 登录 `Authorization header is badly formatted` | Issue 已关闭 |

> **急需关注**：#4222 没有关联 PR，且直接影响所有使用 prompt caching 的用户，性能衰减严重，建议尽快定位。

---

## 功能请求与路线图信号

### 新提交的增强类 Issue
- **#4220** —— 增加 **GitHub Copilot for Business / Enterprise 支持**，适配不同 API endpoint，适合企业用户。  
  [Issue #4220](https://github.com/HKUDS/nanobot/issues/4220)
- **#4218** —— 为 WebUI 增加 **Cron Job 管理界面**，当前仅 CLI 可操作，缺乏实时反馈。  
  [Issue #4218](https://github.com/HKUDS/nanobot/issues/4218)

### 今日提交的相关功能 PR（未来版本候选）
- **#4225** —— Cron 新增 `silent` 模式与 `lock_recipient`（@franciscomaestre）  
- **#4226** —— WhatsApp 桥接：转发消息检测、启动保护、联系人处理（@franciscomaestre）  
- **#4224** —— 新增 AssemblyAI 转录提供商（@franciscomaestre）  
- **#4033** —— 聊天场景中区分发送者身份（Discord 频道/线程中多人对话）（@hamb1y）  
- **#4094** —— 频道分发持久化与流标识修复（@hamb1y）  
- **#4123** —— MCP URL SSRF 安全检查（@yu-xin-c）  
- **#4229** —— 修复末尾孤立 tool result 导致消息全部丢弃（@michaelxer）

这些 PR 大多处于待合并状态，可能被纳入 v0.1.5 或后续版本。其中 `per-user memory` (#2968) 今日合并，已确认进入主线。

---

## 用户反馈摘要

从 Issue 描述与评论中可提炼出以下真实用户痛点：

- **GitHub Copilot 集成波动**（#2573）：用户明确给出版本 `v0.1.4.post6` 和完整报错，指出替换 litellm 后 `provider login` 损坏，是回归性 Bug。
- **兼容不标准 API 的困难**（#4167）：用户使用小型 OpenAI 兼容图像 API（Agnes AI），因缺少 `response_format` 支持完全无法工作，需通过 `extraBody` 提供逃生口。
- **感知推理内容丢失**（#4105）：用户依赖 DeepSeek 的思维链，自定义 provider 中 `reasoning_content""` 被丢弃导致助手消息属性缺失，影响下游逻辑。
- **SDK 嵌入异常**（#4211）：用户在 Python 脚本中嵌入 NanoBot 时遇到 task 作用域异常，虽功能正常运行但关闭时抛出 `RuntimeError`，有违优雅退出预期。

这些反馈均已被项目维护者快速响应（或在同一天关闭/提交修复 PR），反映出社区反馈循环高效。

---

## 待处理积压

以下 Issue / PR 已开放较久或有较高影响，建议维护者和社区优先关注：

| 条目 | 创建时间 | 最后更新 | 说明 |
|------|----------|----------|------|
| [#4105](https://github.com/HKUDS/nanobot/issues/4105) | 2026-05-30 | 2026-06-06 | 虽已有关联 PR 并合并 #4228，但 Issue 本身仍为 OPEN，需关闭并确认修复范围。 |
| [#4033](https://github.com/HKUDS/nanobot/pull/4033) | 2026-05-28 | 2026-06-06 | 聊天发送者身份识别 PR 已近 10 天未合并，社区有进一步的 review 需求。 |
| [#4094](https://github.com/HKUDS/nanobot/pull/4094) | 2026-05-29 | 2026-06-06 | 频道分发持久化和流标识修复，仍为 OPEN，对应多个 Issue 修复。 |
| [#4123](https://github.com/HKUDS/nanobot/pull/4123) | 2026-05-31 | 2026-06-06 | MCP SSRF 安全检查，安全相关建议尽快 Review。 |
| [#4222](https://github.com/HKUDS/nanobot/issues/4222) | 2026-06-06 | 2026-06-06 | 严重影响 prefix caching 的 Bug，暂无 PR，需社区或维护者认领。 |

> 此外，早期 PR #2555、#2533、#2532、#2529、#2528 均在今日关闭，属于长期延后合并的清理，建议今后对新功能 PR 缩短 Review 周期以避免堆积。

---

*本日报基于 GitHub 项目 [HKUDS/nanobot](https://github.com/HKUDS/nanobot) 截至 2026-06-07 的公开动态自动生成。所有链接均指向原始 Issue 或 PR。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 (2026-06-07)

## 1. 今日速览

Hermes Agent 项目今日活跃度极高，24 小时内产生了 **50 条 Issue** 和 **50 条 PR**，项目正处于密集的 Bug 修复与安全加固周期。社区反馈集中在跨平台兼容性（Intel Mac、WSL、Windows 环境配置）和核心交互稳定性（终端锁死、配置不同步）上。今日出现了多条 **P1 级别的安全修复 PR**（RCE、权限绕过、提示注入），维护团队应对较为迅速，体现了对安全性的高度重视。尽管今日无正式版本发布，但大量 PR 的开放与积压，预示着下一版本将侧重于稳定性和安全加固。

**项目活跃度：极高** | **安全响应：积极** | **跨平台体验：存在短板**

## 2. 版本发布

*（过去 24 小时无新版本发布）*

## 3. 项目进展

项目今日的进展主要体现在高优先级 Bug 的修复关闭上，清理了多个影响基础体验的拦路虎：

- **平台稳定性修复**：[#31193](https://github.com/NousResearch/hermes-agent/issues/31193) 修复了 QQ Bot 适配器在断线重连时陷入死循环导致 CPU 占满的严重资源泄漏问题。
- **终端交互修复**：[#40490](https://github.com/NousResearch/hermes-agent/issues/40490) 修复了 CLI 模式下懒加载依赖（如 Pillow）安装提示弹出导致终端锁死的 P1 级 Bug，解决了“进入假死”的极端用户体验问题。
- **显示与兼容性修复**：[#40296](https://github.com/NousResearch/hermes-agent/issues/40296) 修复了 Nous 提供商下 UI 底部状态栏显示的模型与实际配置不符的问题；[#22961](https://github.com/NousResearch/hermes-agent/issues/22961) 修复了 Dashboard 中 `vision_analyze` 工具结果错误显示为用户消息的问题；[#38358](https://github.com/NousResearch/hermes-agent/issues/38358) 修复了 Windows 多工作区仓库下 `hermes update` 时 Web UI 构建失败的问题。

## 4. 社区热点

讨论最热烈、关注度最高的 Issues 反映出社区对 **开箱即用体验** 的高度关注：

- **[#37505] Intel Mac 兼容性危机（6 条评论）**：用户的强烈不满集中在官方 DMG 发布包仅含 `arm64` 架构，导致 Intel Mac 用户完全无法启动。这是 CI/CD 流程中的产品化疏忽，直接影响近半 Mac 用户群体。
  [查看讨论](https://github.com/NousResearch/hermes-agent/issues/37505)

- **[#38963] Windows 安装环境调试（4 条评论）**：用户反馈 Desktop 安装后在 Win11 上识别不到 `git` 命令，社区成员围绕 Windows 环境变量和安装器检测逻辑进行了讨论，暴露了 Windows 运行环境预检的薄弱环节。
  [查看讨论](https://github.com/NousResearch/hermes-agent/issues/38963)

- **[#27683] Web 工具静默失效（4 条评论）**：社区贡献者 `bradsmithmba` 提供了极其详尽的技术根因分析（`_ensure_plugins_discovered()` 缺失），揭示了 Web 搜索、抓取功能“静默罢工”而非“报错提示”的设计缺陷。这是一个严重的新手引导逻辑 Bug。
  [查看讨论](https://github.com/NousResearch/hermes-agent/issues/27683)

- **[#38989] 侧边栏会话丢失与 [#40820] 路径空格问题** 也获得了较多共鸣，反映了 UI 状态管理的不稳定和 macOS 环境配置的粗糙。

**分析**：社区当下的核心诉求是 **“可靠的基础可用性”**——无论是跨平台运行（Intel Mac, Windows）还是核心功能（Web 工具）的首次使用，任何开箱即用的卡点都会带来极大的负面反馈。

## 5. Bug 与稳定性

**Critical / P1（严重性最高）**：
- **安全性（有 Fix PR 待合并）**：
  - `#36847` TUI Gateway `shell.exec` 存在严重 RCE 漏洞。→ **Fix PR [#40939](https://github.com/NousResearch/hermes-agent/pull/40939)**
  - `#40170` Honcho 记忆模块被无条件注入客户网关（WhatsApp/Telegram）。→ **Fix PR [#40967](https://github.com/NousResearch/hermes-agent/pull/40967)**
  - `#40863` Telegram 未授权用户在消息事件完全构造完毕后才被拒绝。→ **Fix PR [#40941](https://github.com/NousResearch/hermes-agent/pull/40941)**
- **[#40831] macOS 26 更新即退化**：v0.16.0 更新后 `launchd` 域配置错误，Gateway 在 Aqua 桌面会话下无法启动。*（暂无公开 Fix PR）*
- **[#24433] 配置状态割裂**：交互模式无视正确配置，持续报错“No inference provider configured”。*（5月12日创建，暂无公开 Fix PR）*

**P2（中等级别，影响日常使用）**：
- [#40820](https://github.com/NousResearch/hermes-agent/issues/40820) macOS 家目录含空格导致桌面版安装失败。
- [#40250](https://github.com/NousResearch/hermes-agent/issues/40250) 终端转义序列泄漏，每次回复开头被吞字。
- [#34197](https://github.com/NousResearch/hermes-agent/issues/34197) `/goal` 自动延续竞态导致陈旧任务复活。
- [#40801](https://github.com/NousResearch/hermes-agent/issues/40801) Cron 脚本路径守卫误拒默认目录的任务。

**P3（体验问题）**：
- [#37505](https://github.com/NousResearch/hermes-agent/issues/37505) Intel Mac 支持缺位（长期未响应）。
- [#40937](https://github.com/NousResearch/hermes-agent/issues/40937) macOS Dock 图标尺寸过大。
- [#40954](https://github.com/NousResearch/hermes-agent/issues/40954) WSL 下无法使用 Windows 系统输入法。

## 6. 功能请求与路线图信号

**核心演进方向——`/goal` 与任务编排**：
- **[#30577] Goal 结构化元数据**：要求 `gateway /goal` 输出机器可读的结构化状态。
- **[#27777] Goal 生命周期插件钩子**：希望 `on_goal_set/pause/resume/complete` 等事件能暴露给插件系统。
- **[#40940] ScoutGate v2**：提议将 `/goal` 授权与租约和 Manifest 绑定，构建更严谨的安全模型。
- **PR [#40946]**：实现了 `delegate_task(background=true)`，支持异步后台子代理并行工作。

**分析**：`/goal` 正在从简单的“持续对话”进化为 **Hermes 的任务编排与授权核心**。配合后台子代理与看板系统，下一版本极大概率聚焦在复杂多代理工作流的落地。

**集成与自动化方向**：
- [#40917](https://github.com/NousResearch/hermes-agent/issues/40917) **看板级通知订阅**：用户希望摆脱逐个任务订阅的繁琐，支持工作流级别的自动通知，是支撑 Agent 集群自动化的基础需求。
- [#35279](https://github.com/NousResearch/hermes-agent/issues/35279) **Discord 社区 AI 管家**：用户希望用一个 Agent 管理 10 万+ 成员社区的工单和指引，代表了从个人助手到社区 Agent 的跨越需求。
- [#13529](https://github.com/NousResearch/hermes-agent/issues/13529) **Agent 内部状态 API**：请求暴露内部状态（含情绪状态），以便与 Home Assistant 等智能家居深度集成。

**用户体验微优化**：
- **PR [#40942]** 添加了“保持工具调用展开”的 UI 开关，直面用户在 Debug ReAct 循环时的核心痛点。

## 7. 用户反馈摘要

**痛点与不满意（Pain Points）**：
> “The current official macOS Hermes Desktop DMG appears to ship a thin `arm64` installer... app cannot launch and fails with `Bad CPU type in executable`.” —— **#37505**，Intel Mac 用户感觉被排除在外。
> “`hermes config show` confirms provider... interactive chat mode reports 'No inference provider configured' and refuses to send the first message.” —— **#24433**，用户对 CLI 与 TUI 配置状态不一致感到困惑与失望。
> “the terminal becomes completely unresponsive: no keyboard input is accepted, Ctrl-C does nothing” —— **#40490**（已修复），基础交互阻断让用户产生极大不信任感。
> “After updating to Hermes v0.16.0 / current main... incorrectly targets the user/<uid> launchd domain even though the gateway LaunchAgent is loaded and running under gui/<uid>.” —— **#40831**，非兼容的破坏性变更引入回归。

**使用场景亮点（Highlights）**：
> “using Hermes heavily across Telegram, Discord, and Home Assistant” —— **#13529**，用户群体已出现重度跨平台使用者，Hermes 作为 AI 个人 OS 的定位得到验证。
> “Managing a Discord server is a huge challenge for community owners. Many large communities with 100k+ members have to hire staff just to handle support tickets...” —— **#35279**，用户已展现出将 Hermes 从个人助手延伸至商用业务端的强烈意愿。

## 8. 待处理积压

**严重 Bug 长期未响应**：
- **[#6718] 后台进程通知失效（4月9日创建）**：核心 Bot 功能“完成任务后回调 Agent”完全失效，长时间缺乏维护者响应。
- **[#8125] macOS launchd PATH 污染（4月12日创建）**：后台网关服务因 plist 中固化会话级 PATH 导致假性过期，影响服务稳定性。
- **[#24433] P1 推理配置失效（5月12日创建）**：交互模式最关键的通道被堵，严重影响 CLI 重度用户的日常使用。
- **[#27683] P2 Web 工具静默失效（5月18日创建）**：新用户首次体验的致命缺陷，技术根因已分析清晰，等待排期。

**待紧急审查合并的 P1 安全修复 PR**：
- **[PR #40939](https://github.com/NousResearch/hermes-agent/pull/40939)**：修复 TUI Gateway `shell.exec` RCE 漏洞（`#36847`），攻击面最广，优先级最高。
- **[PR #40967](https://github.com/NousResearch/hermes-agent/pull/40967)**：修复 Honcho 记忆被自动注入公共网关的提示词注入漏洞（`#40170`），存在数据泄露风险。
- **[PR #40941](https://github.com/NousResearch/hermes-agent/pull/40941)**：修复 Telegram 用户身份认证过滤时机过晚的问题（`#40863`）。

**值得产品侧回应的长期 Feature Request**：
- **[#27777]（Goal 插件钩子，5月18日创建）**：高度契合插件系统架构，应用场景明确，建议纳入路线图。
- **[#30577]（Goal 结构化元数据，5月22日创建）**：对于第三方 Adapter 集成至关重要，亦应纳入规划。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

## 2026-06-07 PicoClaw 项目日报

### 1. 今日速览
- 项目在过去 24 小时内保持 **极高活跃度**：12 条 Issue 更新、18 条 PR 处理，另发布 1 个 Nightly 版本。  
- **核心基调**：大量防御性代码修复（goroutine 泄漏、nil 解引用、类型断言安全检查）显著提升运行时健壮性，同时 Slack 集成获得实质性改进。  
- **新方向信号**：由社区成员 @jcafeitosa 连开 9 个关于 “ClawTrade” 子系统的任务 Issue（交易所连接、订单簿、风险控制、CI/CD），显示项目正在向 **量化交易/回测** 领域扩展。  
- 整体健康度良好，维护者响应迅速，积压不明显；但仍有一个 Windows‑QQ 信道 Bug 待处理。

---

### 2. 版本发布
**nightly: v0.2.9-nightly.20260607.7d2b0c2a**  
- 自动化每日构建，包含截至 2026‑06‑06 的全部 `main` 分支改动。  
- 可能已集成今日合入的各类修复（goroutine 泄漏、I/O 错误处理、Slack 增强等）。  
- **注意**：Nightly 构建可能不稳定，不建议直接用于生产环境；暂无破坏性变更说明。

[查看对比日志](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

---

### 3. 项目进展
过去 24 小时共有 **16 个 PR 被关闭（绝大多数已合并）**，以下为主要推进方向：

| 方向 | 关键 PR | 贡献者 | 说明 |
|------|---------|--------|------|
| **稳定性/健壮性** | [#3016](https://github.com/sipeed/picoclaw/pull/3016) / [#3014](https://github.com/sipeed/picoclaw/pull/3014)、[#3017](https://github.com/sipeed/picoclaw/pull/3017)、[#3019](https://github.com/sipeed/picoclaw/pull/3019)、[#3021](https://github.com/sipeed/picoclaw/pull/3021)、[#3022](https://github.com/sipeed/picoclaw/pull/3022)、[#3023](https://github.com/sipeed/picoclaw/pull/3023) | @chengzhichao‑xydt | 修复 `Manager.Reload()` 的 goroutine 泄漏；为各信道（Slack、飞书、LINE 等）增加 `sync.Map` 类型断言安全守卫；处理 `io.Copy` 失败后编码器未关闭、解压时文件关闭错误忽略等问题。 |
| **Slack 集成** | [#3020](https://github.com/sipeed/picoclaw/pull/3020) | @bogdanovich | 改进工具反馈追踪与消息格式化；添加频道级别的 allow/ignore 过滤规则，并更新相关测试和文档。 |
| **工作区安全** | [#2965](https://github.com/sipeed/picoclaw/pull/2965) | @maxmilian | 修复开启 `restrict_to_workspace` 后 `exec` 工具误将无 scheme 的 URL（如 `wttr.in/Beijing?T`）当作绝对路径的问题。 |
| **前端兼容** | [#2711](https://github.com/sipeed/picoclaw/pull/2711) | @openapphub | 令复制按钮在非安全（HTTP）环境下自动降级，避免因 `navigator.clipboard` 不可用而报错。 |
| **文档清理** | [#3013](https://github.com/sipeed/picoclaw/pull/3013) | @shenjiecode | 移除技能创建文档中对缺失脚本的引用，提供纯手工步骤。 |
| **其他已关闭（合并/清理）** | [#830](https://github.com/sipeed/picoclaw/pull/830)（Google Chat 信道）、[#1112](https://github.com/sipeed/picoclaw/pull/1112)（DeepSeek 协议支持）、[#2838](https://github.com/sipeed/picoclaw/pull/2838)（工具策略过滤）、[#2662](https://github.com/sipeed/picoclaw/pull/2662)（供应商文档统一）、[#423](https://github.com/sipeed/picoclaw/pull/423)（多代理协作框架） | 多位贡献者 | 这些早期 PR 今日被关闭，说明代码库正在整合先期成果。 |

> 整体上，项目的 **并发安全、错误处理、跨平台兼容性** 均得到实质提升。

---

### 4. 社区热点
- **最活跃 Issue**：[#2625 – Provide compiled builds with WhatsApp support](https://github.com/sipeed/picoclaw/issues/2625)（8 条评论，1 👍）  
  用户表达在树莓派 Zero 2 上需要 WhatsApp 支持，但默认 Arm64 构建未包含此功能，希望官方提供编译标志或预构建版本。该需求虽已关闭，但反映了 **边缘设备用户对开箱即用体验的强烈期望**。

- **方向性讨论**：[#2929 – Add first-class agent‑to‑agent communication](https://github.com/sipeed/picoclaw/issues/2929)（3 条评论，2 👍）  
  提议为多代理建立对等通信层，最终因 stale 关闭。社区或通过现有 `subagent`/`delegate` 机制实现了部分场景，但高级协作需求仍可能在未来重新提出。

- **新系列 Issue（无评论但数量密集）**：@jcafeitosa 创建的 EX‑001～EX‑005、EXM‑001～003、RG‑001（[#3024](https://github.com/sipeed/picoclaw/issues/3024)～[#3032](https://github.com/sipeed/picoclaw/issues/3032)）  
  均为 **ClawTrade** 子系统的实现任务，严格遵循内部架构文档（SDD‑xxx），要求 TDD 与基准测试。这很可能成为下一阶段社区关注焦点。

---

### 5. Bug 与稳定性
**紧急 / 待修复**：

| Issue | 标题 | 影响 | 状态 |
|-------|------|------|------|
| [#3015](https://github.com/sipeed/picoclaw/issues/3015) | QQ 信道在 Windows 下连接失败（token 超时） | Windows 用户无法使用 QQ 频道，Pico 信道正常 | **未修复**，需排查 `bots.qq.com` 超时原因 |

**已合入修复的稳定性问题**（今日关闭的 PR）：

| 问题描述 | 相关 PR |
|----------|---------|
| `Manager.Reload()` 导致 dispatch 协程泄漏 | [#3016](https://github.com/sipeed/picoclaw/pull/3016) / [#3014](https://github.com/sipeed/picoclaw/pull/3014) |
| `GetStartupInfo()` 返回空 map 时 panic | [#3021](https://github.com/sipeed/picoclaw/pull/3021) |
| Slack/飞书/LINE 等场景 `sync.Map` 类型断言缺少 `ok` 检查（潜在 panic） | [#3022](https://github.com/sipeed/picoclaw/pull/3022) |
| 解压时 `Close()` 错误被静默忽略，可能造成截断 | [#3023](https://github.com/sipeed/picoclaw/pull/3023) |
| Base64 编码器在 `io.Copy` 失败后未关闭，输出不完整 | [#3017](https://github.com/sipeed/picoclaw/pull/3017) |
| WhatsApp 信道类型断言冗余；`config` 中 nil guard 缺失 | [#3019](https://github.com/sipeed/picoclaw/pull/3019) |

这些修复均为防御性，不会改变外部行为，但 **显著降低了生产环境下的崩溃风险**。

---

### 6. 功能请求与路线图信号
- **明确路线图推进 – ClawTrade 子系统**  
  今日创建的 [#3032](https://github.com/sipeed/picoclaw/issues/3032)（CLI）、[#3031](https://github.com/sipeed/picoclaw/pull/3031)（CI/CD）、[#3030](https://github.com/sipeed/picoclaw/issues/3030)（消息中心）、[#3029](https://github.com/sipeed/picoclaw/issues/3029)（风险管理）、[#3028](https://github.com/sipeed/picoclaw/issues/3028)（延迟基准）、[#3027](https://github.com/sipeed/picoclaw/issues/3027)（无锁订单簿）、[#3026](https://github.com/sipeed/picoclaw/issues/3026)（Binance REST）、[#3025](https://github.com/sipeed/picoclaw/issues/3025)（Binance WebSocket）、[#3024](https://github.com/sipeed/picoclaw/issues/3024)（Exchange 接口）**组成完整的新功能子项目**。参考 SDD‑001/002/009，预计未来版本将引入交易所连接、回测、风险控制等能力。

- **其他潜在纳入版本的功能**  
  - [PR #2838](https://github.com/sipeed/picoclaw/pull/2838)（工具策略过滤） – 已关闭，应已就绪。  
  - [PR #2935](https://github.com/sipeed/picoclaw/pull/2935)（繁体中文 i18n）– 开放中，若合并将改善非英文用户覆盖。  
  - [Issue #2625](https://github.com/sipeed/picoclaw/issues/2625)（WhatsApp 构建）虽关闭，但用户诉求仍在，维护者可考虑在下个稳定版中新增构建变体。

---

### 7. 用户反馈摘要
（基于 Issue 评论区内容）

- **部署便捷性**（#2625）：用户反馈“使用 PicoClaw on Pi Zero 2，默认可执行文件不含 WhatsApp 支持，导致难以快速更新”。**核心痛点**：预编译包未能覆盖所有信道，用户希望获得包含 WhatsApp 的官方构建或通过编译开关启用。  
- **Windows 兼容性**（#3015）：Windows 环境下 QQ 信道因 token 获取超时而无法启动，而 Pico 信道正常。怀疑是 HTTP 客户端在 Windows 上对 `bots.qq.com` 的处理差异或代理问题，需开发团队验证。  
- **贡献者体验**：今日 PR 贡献者（@chengzhichao‑xydt、@bogdanovich 等）通过提交防御性修复、增强已有集成，显示项目 **代码审查流程健康，社区 PR 被快速合入**。

---

### 8. 待处理积压
- **PR [#2935](https://github.com/sipeed/picoclaw/pull/2935)（繁体中文翻译）**  
  自 2026‑05‑24 开启，标记为 [stale]，至今未合并。可能需要解决冲突或增加维护者 review。  
- **PR [#3018](https://github.com/sipeed/picoclaw/pull/3018)（防御性修复）**  
  包含 LINE 信道、Evolution store 及 `os.Getwd` 错误处理，今日保持 OPEN，尚未合并。  
- **Issue [#3015](https://github.com/sipeed/picoclaw/issues/3015)（QQ 信道 Windows 故障）**  
  新报 Bug，无修复 PR，建议优先确认。若延迟处理将影响 Windows 用户对该信道的采用。  
- **旧 Issue 清理**：`#2625` 与 `#2929` 今日关闭，积压量减小；但大量新开任务（EX‑series）可能需要维护者分配负责人。

---

*报告基于 GitHub 公开数据，统计时段 2026-06-06 00:00 UTC 至 2026-06-07 05:00 UTC。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 2026-06-07

**分析师观点**：项目在24小时内收到2个新Issue、14个活跃PR（其中3个已合入），无版本发布。社区贡献保持活跃，修复与功能改进集中在Signal/Slack适配器、技能可维护性及系统稳定性，但新用户入门路径暴露出关键体验问题，需优先处理。

---

### 1. 今日速览
过去24小时，项目共有2个新Issue（均未关闭）和14个PR变动（3个合并/关闭，11个待合并），无版本发布。社区贡献活跃，修复方向集中于**Signal/Slack适配器**、**技能可维护性统一**及**ID生成/会话重试**等系统稳定性问题。但新用户**推荐的安装流程未正确连接`cli/local`**（#2703），导致首次启动命令超时，提示信息缺失，可能影响新用户留存。整体而言，项目在基础健壮性上持续迭代，但用户体验细节仍需加强。

---

### 3. 项目进展
今日合入的3个PR对项目核心质量有显著提升：
- **#2698 – Skills 符合性改造**：统一技能库的可升级维护标准（最小侵入式reach‑ins、功能性集成测试、幂等REMOVE.md），使技能模块能随核心变更稳定演进。  
  [查看 PR](https://github.com/nanocoai/nanoclaw/pull/2698)
- **#2696 – Dashboard 技能符合性示例**：作为首个符合新模型的技能示例，修复了因核心重构导致的导入漂移问题，并添加了进程内集成测试。  
  [查看 PR](https://github.com/nanocoai/nanoclaw/pull/2696)
- **#2697 – 主机单实例锁**：防止同时运行多个主机进程导致重复消息投递，通过文件锁实现进程互斥，提升生产环境可靠性。  
  [查看 PR](https://github.com/nanocoai/nanoclaw/pull/2697)

此外，还有11个修复性PR处于待合并状态，涉及Signal附件传递、Slack Socket Mode迁移、容器用户映射、MCP传输扩展等，显示出项目在多个集成方向上同步推进。

---

### 4. 社区热点
尽管Issues缺乏评论文档，以下两条新Issue因其影响面可能引发较多讨论：
- **#2703 – 推荐安装路径无法使用`pnpm run chat hi`**：新用户遵循README推荐的步骤后，该命令挂起120秒并超时退出，且未给出任何错误提示。这直击项目入门关键路径，可能对用户第一印象产生负面影响。  
  [查看 Issue](https://github.com/nanocoai/nanoclaw/issues/2703)
- **#2701 – `ncl groups restart --rebuild`在无包时报错**：当`packages_apt`和`packages_npm`均为空时，命令拒绝执行并提示“先用install_packages”，而正常重启却可以正常跳过。用户期望rebuild能自动跳过无包情况。  
  [查看 Issue](https://github.com/nanocoai/nanoclaw/issues/2701)

PR方面，**#2531**（poll‑loop去重）、**#2184**（过期会话立即重试）等长期待合PR虽无新增评论，但作者持续push更新，说明仍在积极讨论。

---

### 5. Bug 与稳定性
按严重程度排列：

| 严重度 | 描述 | 状态 |
|-------|------|------|
| 🔴 **Critical** | **#2703** – 推荐安装后`cli/local`未正确配置，导致`pnpm run chat hi`命令挂起120s后超时，且无任何错误提示。**新用户首次体验严重受损**。 | 新开，无Fix |
| 🟠 **High** | **#2701** – `ncl groups restart --rebuild`在包列表为空时报错，拒绝执行；正常重启却能跳过。rebuild应自动跳过无包安装。 | 新开，无Fix |
| 🟡 **Medium** | **#2695** – Signal附件路径为宿主路径，容器无法读取图片（已有Fix PR） | Fix PR #2695 待合并 |
| 🟢 **Low** | **#2694** – Signal DM因未设置`isMention`/`isGroup`而被路由器丢弃（已有Fix PR） | Fix PR #2694 待合并 |
| | **#2699** – `ncl groups create`生成的ID未以字母开头，导致OneCLI拒绝（已有Fix PR） | Fix PR #2699 待合并 |
| | **#2700/#2702** – Slack适配器仍使用HTTP Webhook模式，但代码中MCP已依赖Socket Mode，需迁移（两Fix PR待合并） | PR #2700, #2702 待合并 |

**关键观察**：新增Bug集中在**入门体验**和**命令容错**上，而Signal/Slack关联的Bug已在PR中修复，需尽快合并以稳定适配器。

---

### 6. 功能请求与路线图信号
- **#2693 – 新增Google Contacts工具（PR）**：提供了OneCLI原生的MCP服务器，与已存在的Gmail、GCal工具形成Google生态系列，表明社区对办公生产力集成的持续需求。  
  [查看 PR](https://github.com/nanocoai/nanoclaw/pull/2693)
- **#2208 – 支持HTTP/SSE MCP服务器传输（待合并）**：扩展MCP传输层，突破当前仅stdio的限制，使MCP服务可跨网络部署。该PR已开放超过一个月，但后续更新说明仍有进展，可能影响下一版本的架构。  
  [查看 PR](https://github.com/nanocoai/nanoclaw/pull/2208)
- **#2697（已合并）** 的“单实例锁”暗示社区实际部署中遇到了多进程冲突问题，该修复提升了生产安全性。
- **Slack Socket Mode迁移（#2700/#2702）**反映了用户对更简易部署方案的需求（无需公开URL），适配主流Slack推荐实践。

**路线图信号**：项目正在向**更标准的技能可维护性**、**更丰富的MCP传输**和**更稳定的集成适配器**演进，Google工具系列可能成为下一个小版本的重点。

---

### 7. 用户反馈摘要
从Issues描述中提炼的真实用户痛点：
- **@bigintersmind**（#2703）：“完全按照README推荐的步骤安装后，`pnpm run chat hi`命令挂起120秒然后退出，没有任何提示。花了好久才发现原来是`cli/local`没有正确连接。”——**痛点：文档与实际配置脱钩，缺乏error提示。**
- **@jtheducation-ctrl**（#2701）：“`ncl groups restart --rebuild`失败，说是必须先安装包。可是我是想重启一个没有包配置的组，正常重启就可以，rebuild却不行。rebuild应该跳过包安装。”——**痛点：命令行为不一致，缺少容错。**
- **@cfis** 提交的多项Signal修复（#2694, #2695）说明Signal渠道用户遇到了**附件无法读取**、**私聊消息被静默丢弃**等问题，影响正常使用。

**总体印象**：用户愿意通过PR贡献修复，但项目在**开箱即用体验**和**命令鲁棒性**上仍有明显短板，新用户引导需优化。

---

### 8. 待处理积压
以下PR/Issue已开放较久（≥30天），仍未合入或关闭，建议维护者评估优先级：

| 条目 | 最后更新 | 现状 | 潜在影响 |
|------|---------|------|---------|
| **#2531** – `fix(poll-loop): suppress duplicate text when send_message fires mid-turn` | 2026-06-06（仍有push） | 待合并 | 回合内消息去重，影响用户体验 |
| **#2184** – `fix(poll-loop): retry immediately on stale session instead of delivering error` | 2026-06-06（更新） | 待合并 | 避免用户看到会话过期错误消息，改为自动重试 |
| **#2230** – `fix(container-runner): map host user via keep-id on rootless podman` | 2026-06-06 | 待合并 | 解决根无权限容器下的权限映射问题 |
| **#2349** – `fix(mount-security): tolerate allowlist entries missing path field` | 2026-06-06 | 待合并 | 增强挂载白名单的容错性 |
| **#2208** – `feat(mcp): support http and sse MCP server transports` | 2026-06-06 | 待合并 | 重要功能扩展，但开放已久 |
| **#2703** – （新Issue） | 2026-06-07 | 新开 | 入门阻塞，需紧急回复但尚无回应 |

**建议**：#2703应第一时间响应，至少告知用户已知问题及临时绕路方案；长期积压的PR若因技术分歧需决定方向，应明确沟通状态，避免贡献者失温。

---

**备注**：本日报基于GitHub公开数据（2026-06-07 UTC）生成，评论数/反应数据未在原始数据中提供，因此社区热点部分以内容影响面推测。所有链接均指向 nanocoai/nanoclaw 仓库。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据 IronClaw 项目 2026-06-06 日的 GitHub 数据生成的 2026-06-07 项目动态日报。

---

## IronClaw 项目动态日报 | 2026-06-07

### 1. 今日速览
昨日（2026-06-06）项目代码库处于**高强度迭代状态**，共计 30 条 Pull Request 被更新，其中 10 条已合并/关闭。核心开发者围绕 **“Reborn” 下一代架构**持续推进，在 Slack 深度集成、OpenAI 兼容层、WebUI 管理能力及 AI 交互循环优化上均有实质性 Commit 落地。CI 方面出现 Nightly E2E 测试失败告警（Issue #4108），但整体代码库稳定性影响可控。项目活跃度极高，社区贡献者也开始活跃（PR #4521），**项目健康度良好，正加速向 RC3/M9 里程碑冲刺**。

### 2. 版本发布
无新版本发布。（对照数据：过去 24 小时新版本发布数为 0）

### 3. 项目进展
昨日合并或关闭的 PR 多于日常，标志着 Reborn 架构拼图与代码质量的同步推进。

- **💻 CI/CD 隔离与提速**：核心贡献者 `henrypark133` 合并了 **PR #4520** (`ci: keep Reborn-only PRs out of legacy tests`)，将 Reborn 分支的测试从旧有测试套件中分离，有效提升 CI 效率。
- **🧠 AI 交互体验优化**：`serrrfirat` 合并了 **PR #4508** (`[codex] Gate repeated-call stops behind warning`)，将重复调用判定从“立刻中止”改为“警告两阶段机制”，显著减少生产环境下的误中断。
- **🔌 渠道集成设施落地**：**PR #4509** (`Slack channel subject routing`) 被合并。该项目建立了频道级的路由规则，是实现多团队/多工作空间 Slack 机器人的关键前置步骤。
- **📐 架构设计夯实**：两份统一设计文档被合并（**PR #4485 / #4486**），涵盖后台子代理（Subagent）、主动上下文压缩、以及 WebUI Run 嵌套架构，为后续开发提供理论依据。

### 4. 社区热点
- **🔥 稳定性焦点：Nightly E2E 持续失败 (Issue #4108)**。此 Issue 由 `github-actions[bot]` 自动创建，报告全功能 E2E 测试失败，失败的 Job 涉及 `E2E (extensions)`。该问题自 5 月底发现以来，昨日再度更新失败记录，已成为阻碍合并门禁的首要风险项，社区期望核心团队尽快排查定位。
    *链接：* `nearai/ironclaw Issue #4108`
- **👋 新贡献者加入**：`Dannye013` 提交了首个独立 PR **#4521** (`Add JSON cleaner for formatting and sanitization`)，虽然功能较为基础，但证明了项目吸引了外部开发者。
- **⚠️ 依赖批量升级**：`dependabot` 提交的 **PR #4002** 试图一次性更新目录下的 16 个 GitHub Actions，其中包含 `actions/checkout` 从 `4.3.1` 到 `6.0.3` 的大跨步升级，维护团队正在谨慎评估兼容性。

### 5. Bug 与稳定性
- **严重 (Critical)：夜间 E2E 故障持续**（Issue #4108）
    - **状态**：Open | **报告时间**：2026-05-27（持续 10 天以上）
    - **影响**：CI 门禁核心环节 Reporting Failure，直接影响代码合并决策。
    - **处理建议**：需紧急查看 `Run: 27052471094` 及关联 Commit `26e41dc` 的构建日志。
    *链接：* `nearai/ironclaw Issue #4108`
- **高 (High)：LLM 设置接口 `service_unavailable`**（PR #4523）
    - **状态**：Open (Fix Ready) | **提交时间**：2026-06-06
    - **原因**：`TenantId`/`UserId` 序列化路径不对称，导致系统内部 Sentinel 值被禁止回环解析。
    - **影响**：`/api/webchat/v2/llm/*` 端点返回 503 错误。
    *链接：* `nearai/ironclaw PR #4523`

### 6. 功能请求与路线图信号
从昨日活跃的 Open PR 来看，项目正稳步向 **M9 / RC3** 里程碑靠拢：

- **🚀 工具调用统一基础设施**：**PR #4522** (`feat(llm): scaffold tool_args.rs shared parsing primitives`) 创建了 Layer 2 共享解析原语，这是实现统一工具调用审计（Audit RC1）和标准化参数解析的基石。
- **🔑 OpenAI 兼容层建设**：**PR #4489** 和 **PR #4495** 正在进行中。前者建立了 `chatcmpl-*` 和 `resp_*` 开头的公开引用系统，后者将 `/v1/chat/completions` 路由由 `ProductWorkflow` 接管，标志着 IronClaw 意图提供对标 OpenAI Agent API 的高版本协议兼容。
- **🖥️ 产品化管理后台**：
    - **PR #4519**：添加 `/api/webchat/v2/session` 端点，用来返回 UI 能力集和权限信息。
    - **PR #4516**：增加 WebChat v2 线程删除接口。
    - **PR #4517**：实现首次启动时自动生成 `config.toml` 文件，显著改善本地开发者体验。
- **🤖 扩展生命周期覆盖**：**PR #4518** 为 Reborn 环境下的扩展（Extension）全生命周期（搜索、安装、激活、卸载）添加了端到端（E2E）测试覆盖。

### 7. 用户反馈摘要
昨日虽无大规模评论浪潮，但从 Issue / PR 内容可提炼出以下用户痛点与诉求：

- **🔴 配置即障碍：LLM 设置不可用**
    - **来源**：PR #4523 修复动机。
    - **痛点**：配置 `/api/webchat/v2/llm/*` 时直接返回 503 报错，极大阻碍了模型接入过程。
- **🔧 数据清洗刚需：JSON 格式不友好**
    - **来源**：新贡献者提交的 PR #4521。
    - **场景**：用户在处理工具调用或外部 API 返回时，频繁遇到含有 `null` 或空字符串的“脏” JSON，需求清晰直接——自动化清洗。
- **🔒 运行时安全关注：敏感信息过滤**
    - **来源**：PR #3981 (test: cover runtime HTTP redaction markers)。
    - **诉求**：用户期望对 HTTP 请求/响应中的敏感 Header（如 Token）进行运行时可视化红化处理，表明社区对“审计可见性”与“安全性”同样敏感。

### 8. 待处理积压
以下 Issue / PR 已存在较长时间，提醒维护者关注：

- **🥇 版本发布发布瓶颈（PR #3708）**：`chore: release` PR 自 5 月 16 日开启，已超过 20 天。该 PR 涉及 `ironclaw_common` 和 `ironclaw_skills` 的 **API Breaking Changes**。此积压会阻塞外部开发者基于最新 Crate 构建上游项目，建议尽快完成 Code Review 并发布。
    *链接：* `nearai/ironclaw PR #3708`
- **🥇 持续集成安全红线（Issue #4108）**：如前文提及，Nightly E2E 失败持续超 10 天，应作为 P0 事件处理。
- **🥈 未决的测试贡献（PR #3981）**：安全贡献者 `failuresmith` 于 5 月 24 日提交的 HTTP 红化测试至今仍未合并，该 PR 虽然风险极低，但长期搁置可能打击外部安全贡献者的积极性。
    *链接：* `nearai/ironclaw PR #3981`
- **🥉 依赖大升级（PR #4002）**：依赖更新 PR 长期存在也会导致其他基于旧 Actions 的 CI 流程面临技术债务风险。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 LobsterAI 项目动态日报。

---

# LobsterAI 项目动态日报 — 2026-06-07

**数据统计周期：** 2026-06-06 ~ 2026-06-07
**数据来源：** GitHub (netease-youdao/LobsterAI)

---

## 1. 今日速览

- **社区活跃度维持中等水平**：过去24小时内，项目有6条Issue更新和2个PR合并，未发布新版本。社区讨论热度主要由几个“stale”标签的旧Issue重新回归活跃，但无新严重Bug紧急上报。
- **核心进展集中在功能迭代收尾**：今日合并的两个PR均为4月初提出的功能，涉及批量会话导出和多Agent定时任务管理，这表明开发团队正在逐步清理长期未合并的功能分支。
- **“配置丢失”类Bug持续引发关注**：由用户MaoQianTu提出的多个关于“未保存确认”的Bug（Agent创建、设置、MCP配置）今日再次获得更新，反映出社区对数据安全与交互体验的要求日益提高，但暂无对应fix提交。
- **项目长期稳定性问题仍是隐忧**：尽管今日未出现新崩溃报告，但两个标记为stale的“任务中断”类Issue（#1495, #1496）仍在更新，提示运行稳定性修复仍是用户核心诉求。

## 2. 项目进展

今日无新功能发布，但合并了两项重要的历史性Pull Request，表明项目推进了以下功能闭环：

- **批量会话导出（PR #1529）**：
  - **功能**：在批量模式下新增“导出”按钮，用户可将选中的多个会话（cowork模式）一键导出为一个结构化JSON文件，包含会话完整信息。
  - **意义**：该功能完成了数据流转的“输出”环节，方便用户备份、迁移或离线分析批量对话数据，显著提升了协作场景下的数据自主权。
  - **贡献者**：MaoQianTu
  - **链接**：[#1529](https://github.com/netease-youdao/LobsterAI/pull/1529)

- **多Agent定时任务归属选择（PR #1530）**：
  - **功能**：当系统启用超过1个Agent时，新建定时任务的界面会显示Agent选择器，允许用户指定任务归属Agent（默认main），解决了此前任务均隐式归属main Agent带来的混乱问题。
  - **意义**：完善了多Agent任务系统的管理基础，使用户在多Agent场景下的定时任务指派变得清晰可控，是任务管理模块走向成熟的重要一步。
  - **贡献者**：gongzhi-netease
  - **链接**：[#1530](https://github.com/netease-youdao/LobsterAI/pull/1530)

**项目健康度判断**：核心功能持续补全，但合并速度略慢于社区期望。今日无新PR提交，开发活跃度偏低。

## 3. 社区热点

今日讨论最活跃/最受关注的Issue主要集中在长期未解决的老问题和新鲜的用户建议上：

1.  **“任务显示完成，但是没有返回” (#1496)**
    - **热度**：该Issue于4月创建，今日有新的评论，共2条评论。
    - **核心诉求**：用户提交的任务在界面上显示“完成”，但实际没有任何结果返回，严重阻塞工作流。用户附带了详细的屏幕截图。
    - **分析**：这是一个典型的“假死”状态，用户体验极差。虽然标记为stale，但仍在引起用户共鸣，说明该问题可能在特定场景下仍未修复或未全面覆盖。
    - **链接**：[#1496](https://github.com/netease-youdao/LobsterAI/issues/1496)

2.  **“建议” (#2120)**
    - **热度**：昨日新创建的Issue，已有1条评论，是今日唯一纯新开的讨论。
    - **核心诉求**：用户提出三项明确的改进建议：
        1.  借鉴 Workbuddy 的**任务预存储**功能，允许在运行当前任务时预输入下一个任务，提高连续性。
        2.  **延长单次任务运行时长**，防止长脚本（如数据抓取）中途因“terminated”被中断。
        3.  **优化技能界面UI**，建议2560*1600分辨率下将双列展示改为三列。
    - **分析**：该用户看起来是中高级使用者，其建议专业且具体，反映了开发型用户对“长时间任务执行策略”和“高分辨率UI适配”的深度需求。这些反馈是提升产品专业度的重要参考。
    - **链接**：[#2120](https://github.com/netease-youdao/LobsterAI/issues/2120)

## 4. Bug 与稳定性

今日未报告新的Bug。但以下三个类别的历史Bug在今日获得了更新，表明它们仍是影响用户体验的长期痛点。按严重程度排列如下：

| 严重程度 | 标题/摘要 | 编号 | 状态 | 关联 Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | **程序无缘无故中断（“terminated”）** <br>用户反映在脚本未完成时，监控进程停止，提示`terminated`，严重影响开发效率。 | [#1495](https://github.com/netease-youdao/LobsterAI/issues/1495) | OPEN (Stale) | 无 |
| **严重** | **任务显示完成但无返回** <br>任务状态显示为完成，但输出为空，属于逻辑或状态机Bug。 | [#1496](https://github.com/netease-youdao/LobsterAI/issues/1496) | OPEN (Stale) | 无 |
| **中等** | **多处表单“未保存确认”缺失** <br>包括创建Agent (`#1468`)、Agent设置面板 (`#1469`)、MCP服务器配置 (`#1470`)三个位置，用户在填写内容后关闭弹窗时，修改会**静默丢失**，无任何确认提示。 | [#1468](https://github.com/netease-youdao/LobsterAI/issues/1468)<br>[#1469](https://github.com/netease-youdao/LobsterAI/issues/1469)<br>[#1470](https://github.com/netease-youdao/LobsterAI/issues/1470) | OPEN (Stale) | 无 |

**分析**：这三个“未保存确认”相关的Bug均由同一用户(MaoQianTu)提出，且创建于同一日（4月4日），但至今未获修复。这一问题反映了产品在交互设计上的基础缺陷，对用户数据安全构成长期威胁。建议维护团队尽快评审并规划修复。

## 5. 功能请求与路线图信号

结合今日的Issue和已合并的PR，可以窥见项目社区的演进方向：

- **高可能性纳入路线图（基于PR合并及社区高频请求）**：
    - **任务管理增强**：PR#1530（多Agent任务归属）和PR#1529（批量导出）已证实团队正在完善任务管理系统。如果结合Issue#2120中“预存储下一个任务”的建议，项目下一阶段可能会探索“任务队列”或“任务编排”功能。
    - **数据导出与互操作性**：批量导出JSON功能的合入（#1529）是重要一步。未来可能延伸出导入/导出标准格式，增强与其他工具的数据流通性。

- **有望在下一个版本得到响应（强用户诉求）**：
    - **长时间任务支持**：Issue #2120和#1495均提到了任务中断问题。这暗示需要引入更长的超时时间、后台守护进程或更清晰的错误分级机制。这是一个阻止用户完成深度任务的“高墙”，修复优先级很高。
    - **UI/UX优化**：Issue #2120的第三点（UI列数调整）和“未保存确认”的Bug群（#1468-#1470）都指向了交互细节的打磨。这通常是中期版本优化的重点。

## 6. 待处理积压

以下Issue长期未获响应或解决，今日虽获更新，但状态仍为OPEN。维护团队可重点审视：

1.  **核心稳定性问题**
    - **#1496 [Stale] 任务显示完成，但是没有返回** - 创建于2个月前的严重Bug，至今无解决方案。建议优先排查状态机或结果处理逻辑。
    - **#1495 [Stale] 无缘无故中断进程** - 与上述问题同属一类，直接影响核心功能可用性。用户等待回复。

2.  **交互设计缺陷**
    - **#1468, #1469, #1470 三元组**：关于“未保存确认”的缺失。这是比较易修复但对用户体验提升显著的改良点，积压2个月未处理略显遗憾。建议安排下次迭代修复。

3.  **高价值社区反馈**
    - **#2120 建议**：虽然刚创建，但其包含的三个建议（任务预存储、长时运行、UI适配）质量很高，建议团队尽快回复用户，说明采纳意向和评估周期，以维护高级用户的贡献热情。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是根据您提供的 Moltis 项目数据生成的 2026-06-07 项目动态日报。

---

### Moltis 项目动态日报 | 2026-06-07

> 数据来源：GitHub (github.com/moltis-org/moltis)
> 覆盖时段：过去24小时

---

#### 1. 今日速览

项目整体呈现出“社区需求旺盛、代码合并暂缓”的状态。过去24小时内，社区提交了3个新 Issue（包含2个 Bug 和1个功能请求），2个活跃 PR 尚未合并，无新版本发布。项目活跃度主要集中于社区反馈层面，核心维护者正集中处理两大待合并 PR（#1089 与 #1093）。**项目健康度总体稳定，但 Bug 报告密度上升，尤其是 Docker 环境下的认证控制失效问题（#1112）值得优先关注。**

---

#### 2. 版本发布

[本日无新版本发布]

---

#### 3. 项目进展

**本日均无 PR 被合并入主分支。** 但以下两个关键活跃 PR 代表了项目当前的重要推进方向：

- **PR #1089 (Cap persisted tool results before rehydration)**
  - **状态：** Open (2026-06-01 创建，2026-06-07 更新)
  - **摘要：** 该 PR 旨在修复历史会话重载时工具结果（tool_result）体积不受控的问题。这直接影响聊天回放、重试、压缩提示及静默记忆等核心流程的稳定性。
  - **项目意义：** 一项重大的底层健壮性优化，防止大上下文溢出。对于长会话用户是刚需。
  - **链接：** [PR #1089](https://github.com/moltis-org/moltis/pull/1089)

- **PR #1093 (Add channel activity log visibility settings)**
  - **状态：** Open (2026-06-03 创建，2026-06-07 更新)
  - **摘要：** 引入细粒度活动日志可见性控制，支持按账户、频道、用户三个维度配置（全部/仅错误/关闭）。
  - **项目意义：** 这是向高级部署运维（多租户、多频道）迈进的关键特性，提升了对活动流的管控能力。
  - **链接：** [PR #1093](https://github.com/moltis-org/moltis/pull/1093)

---

#### 4. 社区热点

- **Issue #1112 “[Bug]: Disabling auth doesn't seem to disable auth (Docker)”**
  - **热度分析：** 昨日唯一获得评论的 Issue（1条评论），是当前社区最关切的问题。
  - **核心诉求：** 用户在 Docker 环境下显式关闭认证功能，但系统仍强制要求认证。这违背了用户的显式配置意图，直接威胁部署的可用性和安全性。
  - **链接：** [Issue #1112](https://github.com/moltis-org/moltis/issues/1112)

---

#### 5. Bug 与稳定性

| 严重程度 | Issue ID | 标题 | 影响范围 | 关联 Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **严重 (P0)** | #1112 | [Bug]: Disabling auth doesn't seem to disable auth (Docker) | 严重影响所有 Docker 用户的认证配置体验。安全策略形同虚设。 | 无 |
| **中等 (P1)** | #1111 | [Bug]: Archiving a cron session has no visible effect | 影响 Cron 模块的核心管理操作，存档功能疑似失效，损害用户信任。 | 无 |

---

#### 6. 功能请求与路线图信号

- **Issue #1110 “[Feature]: A keyword to suppress cron job notifications, like NO_REPLY”**
  - **请求内容：** 希望为一个关键字（如 `NO_REPLY`）用于 Cron 任务，以静默发送通知。
  - **路线图信号：** 此需求与正在推进的 **PR #1093（活动日志可见性）** 高度协同。这表明 **“活动流精细化管控”** 正成为社区对 Moltis 的核心期望。从宏观的频道日志可见性，到微观的特定任务静默，用户的控制需求正在深化。此功能大概率会被考虑纳入下一版本。

- **链接：** [Issue #1110](https://github.com/moltis-org/moltis/issues/1110)

---

#### 7. 用户反馈摘要

根据今日提交的 Issues 及评论，提炼出的真实用户痛点与场景：

- **锚定痛点：** **Docker 部署的可信赖度受到挑战。** 用户（#1112）严格按照要求检查了最新版本和已有 Issues，仍遇到了反直觉的 Auth 逻辑 Bug，这类 Bug 对运营稳定性伤害最大。
- **功能缺失：** **Cron 模块用户满意度较低。** 一位重度 Cron 用户同时提交了存档 Bug（#1111）和通知静默功能请求（#1110）。说明该用户正面临噪音困扰，且基本存档功能无法满足其工作流预期。
- **用户画像：** 反馈用户明显为**高阶运维人员**或**重度自动化用户**，他们正在多频道环境下重度使用 Cron 功能，对配置可靠性和通知粒度有严格要求。

---

#### 8. 待处理积压

以下为当前处于开放状态时间较长的关键 PR，提醒维护者留意：

1.  **PR #1089 (Session 序列化改进)**
    - **已开放天数：** 6 天
    - **风险提示：** 改动涉及历史会话重载、压缩、重试等核心路径，逻辑复杂，建议尽快完成 Code Review 以防后续开发产生严重分支冲突。
    - **链接：** [PR #1089](https://github.com/moltis-org/moltis/pull/1089)

2.  **PR #1093 (日志可见性设置)**
    - **已开放天数：** 4 天
    - **风险提示：** 属于全新的 UI/逻辑特性，影响面较广。鉴于该方向是社区关注焦点（结合 #1110 功能请求），建议加速流程，尽早发布预览版供社区反馈验证。
    - **链接：** [PR #1093](https://github.com/moltis-org/moltis/pull/1093)

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 (2026-06-07)

> 数据来源：GitHub (agentscope-ai/QwenPaw) | 统计时段：过去24小时（截至 2026-06-06）

---

## 1. 今日速览

过去24小时内，项目共收到 **11 条 Issue 更新**，其中 2 条已关闭、9 条仍在活跃讨论；Pull Request 更新数为 0，且无新版本发布。社区反馈密集，集中暴露了版本升级后的配置失效、回归 Bug 以及 Windows 兼容性问题，而开发侧主分支活动暂缓。总体活跃度 **中等偏上**，用户参与积极，但修复节奏需引起关注。

## 2. 版本发布

无（过去24小时无新版本发布）。

## 3. 项目进展

- **无 PR 合并**，过去24小时内没有代码变更被并入主分支，开发侧处于静默期。
- **2 个 Issue 关闭**：
  - [#4661] [已关闭] 上下文压缩阈值与模型配置不符的问题，被标记为关闭（可能已确认为行为正常或已通过其他方式修复）。
  - [#4984] [已关闭] 用户询问审批命令，后确认 `/approval approve` 已支持，属用户未查阅文档所致，关闭并致谢。

尽管无代码推进，Issue 的快速确认与关闭体现了维护者对社区反馈的响应态度。

## 4. 社区热点

| Issue | 标题 | 评论数 | 🔗 |
|-------|------|--------|-----|
| #4661（已关闭） | [Bug] v1.1.8post1模型上下文长度配置，记忆压缩未生效 | 6 | [查看](https://github.com/agentscope-ai/QwenPaw/issues/4661) |
| #4937（开放中） | /compact command ignores model's max_input_length, still uses 128K default | 5 | [查看](https://github.com/agentscope-ai/QwenPaw/issues/4937) |

> **分析**：这两条 Issue 都围绕“上下文压缩阈值与模型 `max_input_length` 配置不匹配”展开，说明该功能在近期版本（v1.1.8~v1.1.10）中存在行为偏差，用户已进行多次试探性配置仍无法生效。由于压缩机制直接影响长对话体验，该话题获得了最多讨论。新报告 #4937 进一步确认 `/compact` 命令完全忽略模型配置，问题尚未解决，是当前最核心的社区诉求。

---

## 5. Bug 与稳定性

按严重程度排列（★为严重性）：

| 严重度 | Issue | 标题 | 说明 |
|--------|-------|------|------|
| ★★★ | [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | 1.1.9 & 1.1.10版本，使用本地千问3.6-27B模型对话无响应 | 回归问题：旧版 (1.1.5.post2) 正常，新版仅显示“转圈”无日志，严重影响使用。无 PR 关联。 |
| ★★★ | [#4988](https://github.com/agentscope-ai/QwenPaw/issues/4988) | Session 文件名重复拼接导致 Windows 路径超限 | 严重兼容问题：Windows 上 session 文件因 ID 重复写入导致 `PathTooLongException`，可能致使会话丢失。 |
| ★★☆ | [#4987](https://github.com/agentscope-ai/QwenPaw/issues/4987) | Coding Mode 下切换会话始终失败 | v1.1.10 引入的回归，v1.1.9 正常，阻断核心交互路径。 |
| ★★☆ | [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | /compact 命令忽略模型配置的 max_input_length | 配置不生效，仍使用 128K 默认值，降低用户对配置系统的信任。 |
| ★★☆ | [#4990](https://github.com/agentscope-ai/QwenPaw/issues/4990) | 企业微信工具调用后返回错误提示 | 渠道层错误，影响企业微信用户正常流程。 |
| ★☆☆ | [#4661](https://github.com/agentscope-ai/QwenPaw/issues/4661) | 上下文压缩大小与配置不符 | 已关闭，但根本原因未公开说明。 |
| ★☆☆ | [#4985](https://github.com/agentscope-ai/QwenPaw/issues/4985) | 删除文件命令显示不换行，需横向滑动 | UI 细节问题，轻微影响可读性。 |

> 另有 [#4986](https://github.com/agentscope-ai/QwenPaw/issues/4986) 为功能请求，不列在此处。

---

## 6. 功能请求与路线图信号

| Issue | 标题 | 用户诉求分析 | 可能纳入路线图？ |
|-------|------|--------------|------------------|
| [#4886](https://github.com/agentscope-ai/QwenPaw/issues/4886) | 添加 MAX Messenger 作为 QwenPaw 通道 | 俄语用户呼声，契合“全渠道”理念 | 若计划加强国际支持，有潜力 |
| [#4971](https://github.com/agentscope-ai/QwenPaw/issues/4971) | 会话管理太麻烦，建议增加侧栏直接切换 | 减少操作步骤，提升 UI 友好度 | 与主流聊天应用看齐，容易被采纳 |
| [#4986](https://github.com/agentscope-ai/QwenPaw/issues/4986) | shell/写文件时需实时交互反馈 | 用户期望类似Cursor/WorkBuddy的流式显示 | 前端动效改进，增强用户掌控感 |
| #4984（已关闭） | 审批命令发现性差 | 用户未找到已有功能，暗示文档或UI入口可优化 | 文档/引导改进 |

**路线图信号**：用户越来越关注“交互实时性”和“频道覆盖度”，这部分需求与项目早期定位匹配，预计后续版本会在 Session 管理和执行反馈上有所增强。

---

## 7. 用户反馈摘要

从各 Issue 评论中提取真实声音：

- **配置体验**：“全局上下文长度不见了，只在模型配置里配置，配置后并没生效。”（#4661）；“确认 compact_threshold_ratio 是 auto-derive，但 /compact 仍按 128K 压缩。”（#4937）
- **升级困扰**：“1.1.9 / 1.1.10 版本用本地千问3.6-27B，提交问题后无响应，后台无日志；1.1.5.post2 正常。”（#4989）
- **平台痛点**：“Session ID 在文件名里重复拼接，导致 Windows 上路径超限，会话无法写入。”（#4988）
- **功能可靠性**：“在 Coding Mode 切换会话总是失败，v1.1.9 正常。”（#4987）
- **渠道问题**：“企业微信调用工具后，返回‘抱歉，我无法回答你的问题’。”（#4990）
- **UI 不满**：“删除文件的请求命令显示不换行，要拖滑块才能看全。”（#4985）
- **积极性**：也有用户主动致谢并关闭 Issue，表明社区愿意与项目合作。

---

## 8. 待处理积压

以下 Issue 对项目健康度影响较大，且尚无关联 PR，建议优先响应：

1. **[#4989] 本地模型无响应（严重回归）**  
   创建于 2026-06-06，无日志、无 PR，影响升级通道。需要开发者快速定位兼容层（可能涉及 `agentscope_runtime` 或 vLLM 对接）。  
   🔗 https://github.com/agentscope-ai/QwenPaw/issues/4989

2. **[#4988] Windows 路径超限**  
   创建于 2026-06-06，可能导致数据丢失，跨平台质量控制薄弱。建议尽早纳入 hotfix。  
   🔗 https://github.com/agentscope-ai/QwenPaw/issues/4988

3. **[#4937] /compact 配置不生效**  
   已存在 4 天，与已关闭的 #4661 反映同一核心问题但尚未修复。配置系统行为需统一修正。  
   🔗 https://github.com/agentscope-ai/QwenPaw/issues/4937

4. **[#4987] Coding Mode 会话切换失败**  
   功能级回归，影响特定用户群，建议快速排查。  
   🔗 https://github.com/agentscope-ai/QwenPaw/issues/4987

5. **[#4886] 添加 MAX Messenger**  
   虽不紧急，但已等待 5 天，至少应由核心维护者回复是否纳入路线图。  
   🔗 https://github.com/agentscope-ai/QwenPaw/issues/4886

> 注意：过去24小时 PR 数为 0，说明开发资源可能集中在其他分支或预发布准备中。上述积压问题的修复进度直接关系到项目在 v1.1.x 系列中的稳定性声誉。

---

*日报生成于 2026-06-07，基于公开 GitHub 数据。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，以下是根据你提供的 ZeptoClaw 项目数据生成的 2026 年 6 月 7 日项目动态日报。

---

# ZeptoClaw 项目日报 | 2026-06-07

## 1. 今日速览
过去 24 小时，ZeptoClaw 项目活动高度聚焦于一个核心工程指标：**二进制体积**。维护者围绕该指标调整了 CI 门禁策略，关闭了一项体积审计 issue 并提出了针对 ARM 架构的新门禁需求。整体来看，项目活跃度中等，但深度极高，反映出项目正从早期快速迭代向工程标准化阶段平稳过渡。虽然无新版本发布，但 CI 基础设施的改进为长期质量奠定了基础。

## 2. 版本发布
无。

## 3. 项目进展
项目在 CI/CD 自动化治理与核心 KPI（二进制大小）控制上迈出了坚实一步。

- **完成体积漂移审计**：**Issue #612** `[CLOSED]` 正式关闭。维护者追溯了从 6.2MB 低水位线到当前 7MB 的约 800KB 体积漂移，并确认将目标门禁从此前的 7.5MB 收紧至 **7MB**。([查看 Issue](qhkm/zeptoclaw Issue #612))
- **推进 PR 门禁合并**：**PR #611** `[OPEN]` 正在等待合并。该 PR 计划取消体积检查任务的运行限制（`if:` guard），使其在**每一次 PR 提交时自动执行**，从根本上防止新功能引入导致的体积无节制膨胀。([查看 PR](qhkm/zeptoclaw PR #611))
- **定义下一目标**：**Issue #629** `[OPEN]` 在昨日开启，明确了 aarch64 架构（树莓派 / Jetson / Apple Silicon）的 7MB 门禁是项目的“**真正的机器人护城河**”（the actual robot moat）。([查看 Issue](qhkm/zeptoclaw Issue #629))

## 4. 社区热点
今日唯一的讨论核心集中于**构建体积门禁系统（Binary Size Gate）**。

- **🏗️ 核心讨论：PR #611 “将体积检查升级为 PR 门禁”**：这是目前最具工程价值的改变。维护者试图将被动监控变为主动防御。虽然该 PR 暂无大量第三方评论，但其“将 7.5MB 设为临时上限，但战略目标必须是 7MB”的策略，体现了极其务实的工程落地哲学。([查看 PR](qhkm/zeptoclaw PR #611))
- **🎯 路线图发声：Issue #629 “增设 aarch64 门禁”**：该 Issue 紧随 x86_64 门禁提出，强烈暗示了项目未来的部署重心。维护者明确指出，x86_64 体积较大（~10.5MB）是链接器决定的现实，而真正的竞争壁垒在于 ARM 生态下的体积控制。

## 5. Bug 与稳定性
本周期内未报告新的程序崩溃或功能性 Bug。但以下项目被标记为 **P2-High（高优先级）**：

- **质量回归风险**：**Issue #612** 揭示了一个重要的回归问题——项目二进制体积脱离了战略目标（曾低至 6.2MB，现已漂移至约 7MB）。对于面向边缘设备的 AI Agent 项目来说，体积失控会直接影响核心卖点和部署场景。
- **临时缓解措施**：当前 **PR #611** 将门禁设为 7.5MB 属临时策略（当前编译后的体积限制在 6.98MB），真正的修复是后续的代码迭代优化。

## 6. 功能请求与路线图信号

- **明确硬件架构路线图**：**Issue #629** 是一个非常强烈的路线图信号。项目团队明确将 **aarch64**（如苹果芯片、树莓派、Jetson）作为目标平台，并为其设定了极为严格的 7MB 体积限制。这暗示未来性能优化和特性开发将优先保障这些平台的体积优势。
- **CI 即规范的文化确立**：**PR #611** 的推进代表项目将“硬性规范”写入 CI 的工程文化。如果该 PR 合并，未来所有贡献者都必须遵守体积限制。对于一个追求 **6-7MB 极大体积极限** 的 AI 助手框架而言，这层纪律保障至关重要。

## 7. 用户反馈摘要
- **维护者深度自省**：从 **Issue #612** 的摘要中，维护者自述当前 darwin-arm64 压缩后大小为 **6.98MB**，距离目标门禁 7MB 仅剩 **21KB** 空间。这种对“20KB左右空间都感到警惕”的态度，反映了维护者对项目核心价值的极度珍视。
- **社区外观望**：本周期内无新用户提交功能请求或 Bug 报告。这通常意味着当前功能集合在稳定性上未引发大量投诉，社区情绪偏向平缓，但也可能反映了当前阶段外部贡献者参与度有限。

## 8. 待处理积压

- **⚠️ 关键路径阻塞：PR #611 (Promote binary-size to PR gate)**
  - **状态**：`OPEN`，待合并。
  - **建议**：该 PR 是整个体积治理体系的基础设施。一旦合并，后续所有的体积优化都有据可依。建议维护者尽快将此 PR 落地。([查看 PR](qhkm/zeptoclaw PR #611))

- **⏳ 待启动规划：Issue #629 (Add aarch64 binary-size gate)**
  - **状态**：`OPEN`，无评论。
  - **建议**：维护者可在此 Issue 中表明学习 x86_64 门禁落地的计划，并具体规划 aarch64 门禁的实现步骤。这有助于社区了解项目宏观节奏。([查看 Issue](qhkm/zeptoclaw Issue #629))

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 | 2026-06-07

## 1. 今日速览

项目在过去 24 小时内活跃度极高，38 个 Issues 更新、50 个 PR 推进，且无新版本发布说明当前正处于 **v0.8.x 冲刺期**。核心主线明确：**安全体系加固（OIDC、工具权限、沙箱隔离）** 与 **WASM 插件生态的初步成型**。多个 S0 级数据安全漏洞（会话复活、密钥泄露）在 24 小时内被迅速修复，体现项目对稳定性的高度重视。待合并 PR 池达 45 个，预示着未来数日将有大量功能汇入主干。项目整体 **健康度优秀**，路线图清晰，社区贡献强劲。


## 2. 版本发布

> 本次数据窗口内无新版本发布。


## 3. 项目进展

### 🧱 WASM 插件系统（里程碑推进）
项目在 v0.8.2 轨道上的插件基础设施取得突破性进展：

| PR | 状态 | 要点 |
|:---|:---|:---|
| [#7335](https://zeroclaw-labs/zeroclaw/pull/7335) | OPEN | **沙箱隔离**：引入资源限制、SSRF 出站防火墙、环境变量作用域——填补了 WASM 插件运行时的安全空白 |
| [#7336](https://zeroclaw-labs/zeroclaw/pull/7336) | OPEN | 调整签名模式默认值，增加签名状态可观测性，优化开发者体验 |
| [#7337](https://zeroclaw-labs/zeroclaw/pull/7337) | OPEN | 插件工具命名空间化（`plugin__tool`），防止名称冲突 |
| [#7333](https://zeroclaw-labs/zeroclaw/pull/7333) | OPEN | **远程插件注册表**：支持 `zeroclaw plugin search` 在线搜索与按名安装，打通插件分发逻辑 |

### 🧩 新插件批量出现（自托管优先）
社区成员 `theonlyhennygod` 在一天内贡献了多条 WASM 插件 PR，构建 **用户自托管、本地优先** 的工具集：

- **Ollama Embed** ([#7324](https://zeroclaw-labs/zeroclaw/pull/7324))：本地嵌入计算
- **Stable Diffusion WebUI** ([#7325](https://zeroclaw-labs/zeroclaw/pull/7325))：本地文生图
- **LanguageTool** ([#7326](https://zeroclaw-labs/zeroclaw/pull/7326))：语法/拼写检查
- **Nominatim** ([#7327](https://zeroclaw-labs/zeroclaw/pull/7327))：地理编码
- **n8n 工作流** ([#7328](https://zeroclaw-labs/zeroclaw/pull/7328))：工作流触发
- **ACE-Step 音乐生成** ([#7331](https://zeroclaw-labs/zeroclaw/pull/7331))：文本到音乐

### 🎯 已合入修复
- [#7297](https://zeroclaw-labs/zeroclaw/pull/7297) (MERGED)：`/webhook` 端点支持 `?agent=` 参数进行按请求分发
- [#7281](https://zeroclaw-labs/zeroclaw/pull/7281) (MERGED)：修复 `forbidden_path_argument` 在 heredoc 体和非路径波浪标记上的误报
- [#7334](https://zeroclaw-labs/zeroclaw/pull/7334) (MERGED)：Telegram 流式编辑零间隔防洪水保护
- [#7307](https://zeroclaw-labs/zeroclaw/pull/7307) (OPEN)：委托代理子循环继承运行时配置

### 📋 管理跟踪
- [#7112](https://zeroclaw-labs/zeroclaw/issues/7112)：v0.8.0 发布队列（配置清理、工具解析器稳定）
- [#6970](https://zeroclaw-labs/zeroclaw/issues/6970)：v0.8.1 集成队列
- [#7314](https://zeroclaw-labs/zeroclaw/issues/7314)：v0.8.2 WASM 插件计划
- [#7320](https://zeroclaw-labs/zeroclaw/issues/7320)：v0.8.3 MCP 仪表盘计划


## 4. 社区热点

### 讨论最活跃的 Issue

| Issue | 评论数 | 核心诉求 |
|:---|:---:|:---|
| [#5601](https://zeroclaw-labs/zeroclaw/issues/5601) — OAuth for 智谱/Kimi/MiniMax | **7** | 用户强烈要求取消静态 API Key 管理，支持订阅制 OAuth。已阻塞 58 天，是企业级和中文市场用户的核心痛处 |
| [#7184](https://zeroclaw-labs/zeroclaw/issues/7184) — i18n 翻译子模块 RFC | **4** | 社区开始讨论非英文翻译文件的治理架构，表明项目国际化加速 |
| [#7141](https://zeroclaw-labs/zeroclaw/issues/7141) — OIDC 认证提供者 | **4** | P1 级追踪 Issue，企业 SSO 需求是 v0.9.0 的主要目标之一 |
| [#6715](https://zeroclaw-labs/zeroclaw/issues/6715) — 清理无效分支 | **4** | 仓库超 200 个分支，贡献者要求清理维护 |

### 分析
社区关注点高度集中在 **安全身份认证拓展（OAuth/OIDC）** 和 **平台治理（分支清理、国际化）** 两方面。新功能讨论多围绕插件生态展开，且情绪积极。


## 5. Bug 与稳定性

### 🚨 已被修复的严重 Bug

| Issue | 严重度 | 摘要 |
|:---|:---:|:---|
| [#7252](https://zeroclaw-labs/zeroclaw/issues/7252) | **S0 — 数据丢失/安全** | 杀死 ACP 会话后，持久化历史记录致会话复活（已修复） |
| [#6978](https://zeroclaw-labs/zeroclaw/issues/6978) | **S0 — 安全风险** | `Vec<T>` 配置中嵌套 `#[secret]` 字段未脱敏（已修复） |
| [#7126](https://zeroclaw-labs/zeroclaw/issues/7126) | **P1 — 功能退化** | Web UI"清除"仅清前端、未清后端会话历史（已修复） |
| [#7068](https://zeroclaw-labs/zeroclaw/issues/7068) | **P1 — 内容泄露** | Telegram 频道错误地将 Codex 内部 scratchpad 发送给用户（已修复） |
| [#6875](https://zeroclaw-labs/zeroclaw/issues/6875) | **P1 — 模型兼容** | 工具调用解析器不支持 `<tool_calls>` 复数标签，Llama 4 静默失败（已修复） |
| [#7151](https://zeroclaw-labs/zeroclaw/issues/7151) | **S2 — 界面污染** | 遥测数据泄漏到聊天 WebSocket，产生悬置的"unknown"工具卡片（已修复） |
| [#7197](https://zeroclaw-labs/zeroclaw/issues/7197) | **S2 — 体验** | Web 工具栏在 Windows 下弹 cmd 窗口、加载缓慢（已修复） |
| [#7332](https://zeroclaw-labs/zeroclaw/issues/7332) | **S2 — 劣化** | Telegram 流编辑接受零间隔、造成洪水编辑（已修复） |
| [#7133](https://zeroclaw-labs/zeroclaw/issues/7133) | **S2 — 行为异常** | 路径策略在引号/heredoc 中对 `~` 标记误报（已修复） |

### ⚠️ 待修复的严重 Bug

| Issue | 严重度 | 摘要 |
|:---|:---:|:---|
| [#7312](https://zeroclaw-labs/zeroclaw/issues/7312) | **S1 — 工作流阻断** | Bedrock Qwen 集成在第二次对话时报错 "unsupported model"。**目前尚无关联修复 PR**，需紧急关注 |

### 总结
昨天的 Bug 修复节奏非常紧凑。`v0.8.0` 锁定前的稳定性冲刺效果显著。唯一突出的未修复 S1 是 [#7312](https://zeroclaw-labs/zeroclaw/issues/7312) Bedrock/Qwen 多轮对话故障。


## 6. 功能请求与路线图信号

### 路线图可见性大幅提升
四个追踪 Issue 使近期路线图透明化：

- **v0.8.0** ([#7112](https://zeroclaw-labs/zeroclaw/issues/7112))：配置清理 + 工具解析器稳定
- **v0.8.1** ([#6970](https://zeroclaw-labs/zeroclaw/issues/6970))：集成/频道/工具/Provider 扩展
- **v0.8.2** ([#7314](https://zeroclaw-labs/zeroclaw/issues/7314))：WASM 插件程序（组件模型、WIT 接口、主机函数）
- **v0.8.3** ([#7320](https://zeroclaw-labs/zeroclaw/issues/7320))：MCP 仪表盘 + Web 管理表面

### 有望纳入下个版本的功能特征

| 能力 | 对应 PR/Issue | 可能性 |
|:---|:---|:---:|
| **WASM 生命周期钩子**（HookRunner 桥接） | [#7338](https://zeroclaw-labs/zeroclaw/issues/7338) RFC | 高（v0.9.0 候选） |
| **OIDC 认证提供者** | [#7141](https://zeroclaw-labs/zeroclaw/issues/7141) | 高（v0.9.0 目标） |
| **订阅制 OAuth 扩展** | [#5601](https://zeroclaw-labs/zeroclaw/issues/5601) | 中等（阻塞中，但呼声极高） |
| **Nix flake 改进** | [#6906](https://zeroclaw-labs/zeroclaw/issues/6906) | 中等（需要贡献者接手） |
| **插件远程注册表** | [#7333](https://zeroclaw-labs/zeroclaw/pull/7333) | 高（已进入 PR） |
| **沙箱隔离**（资源/网络/环境） | [#7335](https://zeroclaw-labs/zeroclaw/pull/7335) | 高（已进入 PR） |


## 7. 用户反馈摘要

### 满意点
- **响应效率认可**：多位用户报告的 S0 级安全漏洞（会话复活、密钥泄露）在 24 小时内关闭，社区对安全问题的响应速度满意。
- **插件方向积极**：开发者社区主动以 PR 形式贡献多种自托管插件，表明 WASM 插件架构对用户有较强吸引力。

### 典型痛点
1. **Windows 体验** ([#7197](https://zeroclaw-labs/zeroclaw/issues/7197) — 已修复)：工具栏加载缓慢、出现 CMD 命令窗口弹窗让 Windows 用户困扰。
2. **中国区 Provider 接入** ([#5601](https://zeroclaw-labs/zeroclaw/issues/5601))：用户对智谱、Kimi、MiniMax 等厂商仅支持 API Key 的方式不满意，期望 OAuth / 订阅制登录。
3. **Bedrock Qwen 无法多轮对话** ([#7312](https://zeroclaw-labs/zeroclaw/issues/7312))：用户报告首次问答正常，第二次提问直接报错，工作流严重受阻。
4. **Nix 开箱体验不佳** ([#6906](https://zeroclaw-labs/zeroclaw/issues/6906))：用户反馈 `flake.nix` 输出的是 toolchain 而非 `zeroclaw` 包和 NixOS Module，与预期不符。


## 8. 待处理积压

### 长期未响应的阻塞 Issue

| Issue | 创建日期 | 阻塞天数 | 类型 |
|:---|:---:|:---:|:---|
| [#5601](https://zeroclaw-labs/zeroclaw/issues/5601) | 2026-04-10 | **58 天** | OAuth 扩展（高风险，高呼声） |
| [#5607](https://zeroclaw-labs/zeroclaw/issues/5607) | 2026-04-10 | **58 天** | Cron 前置钩子（Pre-hook skip gates） |
| [#5775](https://zeroclaw-labs/zeroclaw/issues/5775) | 2026-04-15 | **53 天** | Per-skill 安全权限（Skill 级命令白名单） |
| [#5908](https://zeroclaw-labs/zeroclaw/issues/5908) | 2026-04-19 | **49 天** | Debian 容器镜像 CI/CD |

### 建议维护者关注
- **S1 新 Bug** [#7312](https://zeroclaw-labs/zeroclaw/issues/7312)（Bedrock Qwen 故障，尚无修复 PR）
- **治理类** [#6715](https://zeroclaw-labs/zeroclaw/issues/6715)（清理 200+ 无用分支，22 天，贡献者可自行处理但缺乏决策推动）
- **Nix 体验** [#6906](https://zeroclaw-labs/zeroclaw/issues/6906)（13 天，社区有明确的改进方案和技术能力）

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*