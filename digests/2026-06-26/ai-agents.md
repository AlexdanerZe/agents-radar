# OpenClaw 生态日报 2026-06-26

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-26 03:23 UTC

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

好的，这是根据您提供的 OpenClaw 项目 GitHub 数据生成的 2026-06-26 项目动态日报。

---

# OpenClaw 项目动态日报 (2026-06-26)

## 1. 今日速览
过去 24 小时内，OpenClaw 项目活跃度极高，共涉及 **500 条 Issue 更新**和 **500 条 PR 更新**。虽然合并/关闭率（Issues 4.6%，PRs 18.8%）暗示着庞大的积压量带来的维护压力，但极高的更新量也证明了社区强劲的参与热情和开发团队的持续高强度投入。当前社区的两大核心关注点集中在 **内存/会话状态治理** 与 **全面安全加固** 上。Agent 执行可靠性依然是用户热议的痛点。

## 2. 版本发布
今日无新版本发布。

## 3. 项目进展
今日有 94 个 PR 被合并或关闭，重要进展包括：
- **Mattermost 频道交互修复** ([PR #72513] - 已合并)：修复了在 Mattermost 中编辑消息追加 @提及无法唤醒 Agent 的 Root Cause，提升了群聊响应可靠性。
- **自动化基础设施** ([PR #68936] - 已合并)：合入了基于 Claude Agent SDK 的 PR 审查自动修复流水线和 Windows 后台守护进程，显著提升了项目 DevOps 效率。
- **频道入口稳定性修复** ([PR #96912] - 新提交)：针对高优 Bug [#90945]，提出了 Gateway 重启后频道 Ingress 断言恢复机制，旨在解决 Telegram 等频道消息卡死问题。
- **安全边界大规模加固**：社区积极响应安全号召，提交了多个针对外部服务（如 Anthropic OAuth、Fal AI、Google Media）的 JSON 响应边界读取修复 PR（#96917, #96886, #96920, #96904），防范不可信端点攻击。

## 4. 社区热点
- **Agent 承诺一致性** ([Issue #58450] - 评论数: 15, 👍: 3)：
  用户强烈反映 Agent 经常在对话结尾承诺“我会查一下稍后回复”，但实际并未启动任何后台任务。这是涉及用户体验信任度的核心 P2 问题，社区讨论热烈，认为这是项目从“能跑”到“能靠谱”的关键门槛。
- **ClawHub 生态落地反思** ([Issue #50090] - 评论数: 15, 👍: 2)：
  用户系统性地剖析了社区技能（Skill）生态 ClawHub 当前“愿景美好，落地骨感”的尴尬现状。讨论涉及开发工具链（Driftnet）不完善、安装体验差等问题，属于对项目长期发展的深度关切。
- **模型兼容性断层** ([Issue #63918] - 评论数: 17)：
  Cron Agent Turn 在调用 OpenAI 新模型（gpt-5-nano）时硬编码了不支持的 `thinking` 参数，导致任务失败。该 Issue 暴露了功能开发与最新模型 spec 之间的适配滞后问题。
- **功能回归之痛** ([Issue #53599] - 评论数: 6, 👍: 5)：
  关于“Chrome 扩展浏览器中继被移除”的 Issue 虽然评论不多，但获得了 **5 个 👍**，是本期数据中 Reaction 最高的。用户表示该功能对托管服务商至关重要，当前替代方案无法跨机器工作，情绪较为不满。

## 5. Bug 与稳定性
稳定性问题是今日的重灾区，大量 P1 级 Bug 集中在内存管理和状态损毁上：

| 严重程度 | Issue ID | 摘要 | 状态 | 影响范围 |
| :--- | :--- | :--- | :--- | :--- |
| **严重 (P1)** | [#63216](openclaw/openclaw Issue #63216) | 高`reserveTokensFloor`下仍反复硬重置；重试循环注入引导上下文 | 待 Live Repro | 会话状态、消息丢失 |
| **严重 (P1)** | [#55334](openclaw/openclaw Issue #55334) | Gateway 内存泄漏（4天 389MB→14.7GB），`sessions.json` 无边界增长 | 待 Live Repro | 宕机、崩溃循环 |
| **严重 (P1)** | [#65161](openclaw/openclaw Issue #65161) | 心跳隔离模式多项回归：节奏停止、事件标签错乱、状态写入缺失 | 待 Live Repro | 会话状态、诊断混乱 |
| **严重 (P1)** | [#51396](openclaw/openclaw Issue #51396) | 权限剥离回归：`clearUnboundScopes`无条件移除操作员权限 | 需安全审查 | 安全、认证 |
| **高 (P1)** | [#53599](openclaw/openclaw Issue #53599) | Chrome 扩展中继被移除，无跨机器替代方案 | 需产品决策 | 功能回归（+5 👍） |
| **高 (P1)** | [#66443](openclaw/openclaw Issue #66443) | 上下文溢出恢复导致用户消息重复，放大转录体积 | 已有链接 PR | 会话状态、消息丢失 |

**已有 Fix PR 待合并：**
- **Provider 配额熔断** ([PR #64127])：针对 Provider 每日/每周配额耗尽后的重试风暴，已提交持久退避机制修复。
- **配置文件写失败** ([PR #67077])：修复 Windows 下 auth-profiles.json 被热加载锁定导致 EPERM 崩溃的问题。

## 6. 功能请求与路线图信号
路线图信号已从功能堆叠转向 **“架构升级与企业级安全”**：
- **多会话架构** ([Issue #48874] - RFC)：提出共享 LLM + 隔离会话的架构，旨在大幅降低资源消耗，是支持多租户的基础设计。
- **多索引嵌入记忆** ([Issue #63990] - P2)：提议支持多向量索引，实现模型感知的故障转移，避免语义空间污染。
- **语境溯源** ([Issue #54373] - 讨论中)：要求在注入上下文中添加来源/易失性元数据，帮助 Agent 区分“你现在知道的”和“你刚查到的”。
- **不可绕过的出站策略** ([Issue #56349] - P2)：企业级安全需求，要求对 Agent 发出的每一条消息进行强制预校验，防止合规绕过。
- **敏感数据脱敏** ([Issue #64046] - P1)：用户对 openclaw.json 中 API Key 明文存储及 UI 中明文展示表达了极大不安，该功能呼声很高。

## 7. 用户反馈摘要
用户反馈呈现出深度使用后的细腻痛点：
- **信任危机**：“Agent 承诺会去做某事，结果什么都没干，这严重破坏了我的信任。”（源自 #58450）
- **资源浪费**：“每轮对话把 6 个 Markdown 文件重新注入，20%-30% 的 Token 都浪费了，能不能缓存一下？”（源自 #67419）
- **安全焦虑**：“所有 API Key 明文写在 JSON 里，这是等着被泄漏吗？”（源自 #64046）
- **生态质疑**：“ClawHub 听起来很美好，但实际开发体验（Driftnet）和安装体验太差了，感觉像半成品。”（源自 #50090）
- **正向信号**：尽管抱怨颇多，但用户愿意花费精力撰写包含 Root Cause 分析的深度 Bug Report（如 #63216, #65161），甚至提交高质量 Fix PR，表明社区技术实力雄厚且对项目期望极高。

## 8. 待处理积压
多个高优问题长期悬而未决，急需维护者关注：
- **战略级积压**：[Issue #50090] (ClawHub 生态建设)：P2 但已 stale，若持续缺乏推进，将严重打击社区生态建设的信心。
- **信任与安全积压**：[Issue #49876] (Cron 会话发送幻觉输出)：P1 级别，3 月提出已标记 stale。工具调用失败时 LLM 会编造结果，这是重大的信任与安全问题。
- **长期 Live Repro 阻塞**：[Issue #63216] (硬重置) 与 [Issue #55334] (OOM)：作为核心稳定性杀手，长期处于 `needs-live-repro` 状态，急需维护者介入调试。
- **等待作者更新的 PR**：大量重要 PR 处于 `waiting on author` 状态，例如 [PR #89569] (预授权工作流)、[PR #67080] (网关路由加载)、[PR #67077] (配置文件修复)，建议维护者主动推进。

---

## 横向生态对比

好的，作为资深技术分析师，以下是基于您提供的 2026-06-26 各项目动态数据生成的横向对比分析报告。

---

### 个人 AI 智能体开源生态横向分析报告 (2026-06-26)

#### 1. 生态全景

个人 AI 智能体开源生态正处于 **“繁荣与阵痛并存”** 的关键分化期。虽然社区贡献热情极高（多个项目单日 PR/Issue 过百），但生态整体正经历从“功能堆叠”向“生产可靠性”的艰难转型。核心痛点高度集中在 **Agent 承诺一致性、内存/会话状态治理、以及多智能体协作中的审批信任机制**。与此同时，以 **供应链安全（WASM/SLSA）** 和 **企业级多租户架构（Capability Policy）** 为代表的未来方向已获得社区实质性的 RFC 和代码投入，表明行业正在为下一代企业级自主智能体准备基础设施。

---

#### 2. 各项目活跃度对比

| 项目 | 过去24h Issues | 过去24h PRs | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 更新 | 500 更新 | 无 | 极高活跃 / 维护压力巨大 / 信任危机凸显 |
| **NanoBot** | 25 (6新/19关) | 40 (25新/15关) | 无 | 极高活跃 / 安全审计风暴 / 响应敏捷 |
| **Hermes Agent** | 50 (14关) | 50 (48开) | 无 | 极高活跃 / 桌面端高频迭代 / 稳定性承压 |
| **IronClaw** | 50 (17关) | 50 (18关) | 无 | 极高活跃 / 架构重构期 / 核心功能断裂（审批流）|
| **ZeroClaw** | 43 (30新/13关) | 50 (4合/46开) | 无 (v0.8.2冲刺) | 极高活跃 / 发版冲刺 / 安全补丁及时 / 技术债遗留 |
| **CoPaw** | 25 (10关) | 50 (21合) | 无 | 高活跃 / 修复效率高 / 特性管线饱满 |
| **NanoClaw** | 1 (新开) | 16 (11合) | 无 | 高活跃 / 健康稳定 / 功能与安全并行 |
| **LobsterAI** | 0 新 (1 陈旧) | 8 (8 合) | 无 | 中高活跃 / 质量打磨期 / 无积压PR |
| **PicoClaw** | 3 | 19 (6合) | 无 | 中等活跃 / 技术债务偿还 / 安全库替换停滞 |
| **NullClaw** | 无活动 | 无活动 | - | 静止 |
| **TinyClaw** | 无活动 | 无活动 | - | 静止 |
| **Moltis** | 无活动 | 无活动 | - | 静止 |
| **ZeptoClaw** | 无活动 | 无活动 | - | 静止 |

---

#### 3. OpenClaw 在生态中的定位

OpenClaw 凭借 **500 Issue/PR 的量级**，稳居生态讨论度和贡献量的**绝对核心**，但其“核心参照”地位正受到严峻挑战。

*   **优势**：拥有最庞大的社区参与度，涵盖核心架构（多会话）、生态平台（ClawHub）和全面安全加固，是行业技术趋势的“晴雨表”。其厚重的架构设计使其成为企业级深度定制的首选参照。
*   **技术路线差异**：相比于 **NanoBot** 的“小而锐”（聚焦安全审计的快速响应）和 **IronClaw** 的“大而快”（高频率推进 Reborn 架构），OpenClaw 更像一个“重装航母”，致力于解决最底层、最通用的基础设施问题（如内存泄漏、会话状态一致）。但这种“大而全”也导致维护负荷极高（单日 500 更新），积压问题修复速度慢于专注型的项目。
*   **社区规模对比**：从绝对数值看，OpenClaw 社区规模远超其它。但用户反馈的 **“信任危机”（Issue #58450 - 承诺不执行）** 和 **“生态落地骨感”（Issue #50090 - ClawHub）** 问题揭示了社区期望与实际交付之间的巨大鸿沟，构成了 OpenClaw 当前最大的脆弱性。

---

#### 4. 共同关注的技术方向

| 共同技术方向 | 涉及项目 | 具体诉求与表现 |
| :--- | :--- | :--- |
| **Agent 执行可靠性** | **OpenClaw**, **IronClaw**, **CoPaw** | Agent “承诺查一下”但不执行(OpenClaw #58450)；审批拒绝后继续弹窗/批准不持久(IronClaw #5192)；对话思考死锁(CoPaw #5162)。 |
| **内存/状态治理** | **OpenClaw**, **CoPaw**, **ZeroClaw** | 会话历史无限增长/硬重置(OpenClaw #63216)；大会话前端崩溃(CoPaw #5479)；图片 Token 计算错误导致资源浪费(ZeroClaw #8327)。 |
| **安全架构与供应链** | **NanoBot**, **ZeroClaw**, **Hermes** | MCP 作用域逃逸(NanoBot #4519)；SubAgent 绕过工具白名单(ZeroClaw #8279 - S0级)；Email 伪造攻击(Hermes #52801)；硬件 PGP/SLSA 签名的强烈诉求(ZeroClaw #8177)。 |
| **多智能体协作/审批** | **LobsterAI**, **IronClaw**, **NanoClaw** | 多智能体消息泄漏/重复(LobsterAI #2204)；审批流程系统性 Bug(IronClaw)；多管理员/CLI 审批支持(NanoClaw #2857)。 |
| **平台兼容性（Windows）** | **NanoBot**, **Hermes**, **CoPaw** | 系统服务重启冲突(NanoBot #4513)；桌面端 OTA 更新直接崩溃(Hermes #52735)；安装即报 Internal Server Error(CoPaw #5379)。 |

---

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构特征 | 当前核心短板 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 企业级状态管理、ClawHub 生态、通用 Agent | 核心开发者、深度定制团队 | 重架构，强会话抽象，多 Provider 支持 | 信任危机、维护负荷、决策缓慢 |
| **NanoBot** | 安全边界 Audit、多 IM 渠道、敏捷部署 | 安全研究者、快速验证、中小企业 | 插件化 MCP，强沙箱，多网关入口 | Windows 服务化部署体验差 |
| **Hermes Agent** | TUI/桌面原生体验、开发者工具链 | 资深开发者、DevOps 工程师 | 强桌面集成(Electron/TUI)，强 SSH 适配 | 桌面端发布管线脆弱，原生依赖管理差 |
| **IronClaw** | 多租户权限、企业级可观测性、自动化 | 企业平台运维、多角色团队 | Reborn 架构、Capability Policy、Dogfooding | 新架构稳定性 Bug 冲击核心功能（审批流）|
| **ZeroClaw** | WASM 边缘计算、供应链安全、Rust 化 | 边缘计算/嵌入式、安全合规团队 | WASM 沙箱、轻量核心、强国际化(v0.8.2) | 长期 MCP 泄漏未修复、关键设计决策悬停 |
| **CoPaw** | 国产模型兼容(GLM/DeepSeek)、桌面自动化 | 中文用户、教育科研、数据分析 | AgentScope 深度绑定, 强中文生态, 框架演进 | Windows 安装与复杂 UI 场景下的稳定性 |

---

#### 6. 社区热度与成熟度分层

*   **第一梯队（高速迭代/架构驱动）：** **IronClaw、ZeroClaw**
    *   **特征**：正在经历宏大的架构升级（Reborn、WASM化），社区讨论热度最高，方向感最强，但处于“先开枪再瞄准”的阶段，稳定性 Bug 密集爆发。
*   **第二梯队（高频冲刺/安全驱动）：** **NanoBot、Hermes Agent**
    *   **特征**：社区响应速度极快（小时级修复），活力和弹性最好的群体。问题集中在安全审计风暴和桌面端体验突破上，是生态中最“敏捷”的代表。
*   **第三梯队（稳健增长/质量巩固）：** **CoPaw、LobsterAI、NanoClaw、OpenClaw**
    *   **特征**：OpenClaw 体量虽大，但正从“野蛮生长”转向“负重前行”，处于巩固期。CoPaw 和 LobsterAI 修复效率极高，处于功能打磨的成熟阶段。NanoClaw 则是小而美的健康案例。
*   **第四梯队（停滞）：** **NullClaw、Moltis、TinyClaw、ZeptoClaw**
    *   **特征**：24小时内无任何活动。反映出 AI Agent 赛道极高的失败率与竞争壁垒，仅有少数头部项目能维持持续迭代。

---

#### 7. 值得关注的趋势信号

1.  **审批即界面（Approval is the Interface）：** **IronClaw** 审批流的全线崩溃（拒绝无效、批准不持久）和 **NanoClaw** 多管理员审批的 RFE，揭示了 **“人机协作的信任断裂点”** 。未来的 Agent 平台之争，核心可能是谁家的审批交互设计得更优雅、更可靠。
2.  **模型生态碎片化加剧：** **CoPaw** 专门修复 GLM 的 tool call schema 不兼容，**OpenClaw** 适配 gpt-5-nano 而报错，**IronClaw** 的 Clawbench 运行特定模型失败。**“通用兼容性”** 正在成为一个几乎无法完成的任务，深度绑定特定模型生态（如 CoPaw 绑定 AgentScope/国产模型）或将成为一个差异化生存策略。
3.  **供应链安全债显性化：** **ZeroClaw** 的 SLSA/RFC（#8177）与 **NanoBot** 的 PyPI 恶意代码事件（#2439）形成鲜明对比。上游一个依赖（如 libolm）的不安全就可能导致整条链路崩盘（PicoClaw #3088）。**WASM 沙箱** 和 **可复现构建** 将不再是可选项，而是进入企业市场的硬性门槛。
4.  **“瘦”上下文需求崭露头角：** **Hermes Agent** 的用户要求移除 70KB 的 AGENTS.md 文件（#52821），**OpenClaw** 的用户抱怨令牌浪费在 Markdown 文件重注入上（#67419），**CoPaw** 提交了 Scroll Context Manager（#5321）。这标志着用户对**细粒度的上下文成本控制**和**按需检索**的需求已非常迫切，传统的“全量压缩”策略正在被社区抛弃。
5.  **Windows 是“财富洼地”：** 几乎每一个跨平台项目的 Windows 端都在苦苦挣扎（安装崩溃、路径问题、服务化冲突）。这既是巨大的维护成本，也意味着 **“谁先搞定 Windows 一等公民体验，谁就能收割大规模桌面用户市场”**。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是根据您提供的 NanoBot 项目 GitHub 数据生成的 2026-06-26 项目动态日报。

---

### NanoBot 项目动态日报 | 2026-06-26

---

### 1. 今日速览

过去 24 小时，NanoBot 项目经历了一次高强度“安全审计风暴”。共计处理 **25 条 Issue 更新**（新开 6 条，关闭 19 条），**40 条 PR 更新**（新开 25 条，合入/关闭 15 条），活跃度评估为**极高**。核心动因是安全研究员 `YLChen-007` 集中披露了涉及 `exec` 工具白名单绕过、MCP 作用域逃逸及登录 Shell 环境变量泄露等 **7 个高危安全漏洞**。项目维护者响应极快，在报告当天即提交了多条针对性修复 PR，社区协作呈现出“高危漏洞主动披露、代码响应小时级更新”的良性生态。尽管安全债集中显现，但项目的迭代活力与社区信任度在快速修复中得到了巩固。

---

### 3. 版本发布

*（今日无新版本发布）*

---

### 4. 项目进展

今日项目关闭了 15 个 Pull Request，完成了多项安全加固与功能修复，并有大量关键功能 PR 进入待合并阶段。

**安全架构紧急加固：**

- **MCP 作用域逃逸修复**：修复 PR [#4524](https://github.com/HKUDS/nanobot/pull/4524) 成功关闭了 #4519 等系列问题。将 `enabledTools` 的过滤逻辑从仅仅过滤工具调用延伸至资源和提示词注册，修补了核心逻辑漏洞。
- **Shell 执行沙箱加固**：合并修复链包括防止链式命令 (shell-chain) 绕过 [#4526](https://github.com/HKUDS/nanobot/pull/4526)、关闭默认的 Login Shell 执行以隔离环境变量泄露 [#4525](https://github.com/HKUDS/nanobot/pull/4525)，极大增强了 `exec` 工具的安全性。
- **文件系统权限收敛**：修复 PR [#4099](https://github.com/HKUDS/nanobot/pull/4099) 解决了 `extra_allowed_dirs` 意外可写的问题，关闭了长期悬而未决的安全 ISSUE #4073 和 #143。

**平台集成与稳定性修复：**

- **小米 MiMo ASR 兼容**：修复 PR [#4493](https://github.com/HKUDS/nanobot/pull/4493) 合入，解决了前端 WebM 录音格式与后端 WAV 需求不匹配的问题。
- **钉钉 IM 增强**：合并了针对钉钉渠道的修复 Issue [#4497](https://github.com/HKUDS/nanobot/issues/4497)，支持了富文本格式与 HTTP 超时设定。
- **代码健壮性提升**：合入了针对非流式推理工具 ID 去重 (PR [#4530](https://github.com/HKUDS/nanobot/pull/4530))、Session 键冲突 (PR [#4533](https://github.com/HKUDS/nanobot/pull/4533))、Anthropic 内容块类型校验 (PR [#4532](https://github.com/HKUDS/nanobot/pull/4532)) 及无效工具调用过滤 (PR [#4510](https://github.com/HKUDS/nanobot/pull/4510)) 等多项稳定性修复。

**关键能力蓄势待发（待合入 PR）：**

- **Gateway Webhook 引擎**：PR [#4502](https://github.com/HKUDS/nanobot/pull/4502) 重构了网关层入口，支持通用与 GitHub Webhook 事件路由，是走向平台化的重要一步。
- **Agent 可靠性层**：PR [#4534](https://github.com/HKUDS/nanobot/pull/4534) 提出了一套通用容错机制与验证门，意在解决 Agent 生产环境中的瞬态故障难题。
- **MCP 空闲超时管理**：PR [#4506](https://github.com/HKUDS/nanobot/pull/4506) 引入了空闲自动杀死机制，防止 MCP 子进程成为僵尸进程。

---

### 5. 社区热点

今日社区讨论聚焦于 **安全漏洞的全链条高效处理** 及 **Windows 平台的深层部署困境**。

**热点一：高密度安全漏洞披露与敏捷修复闭环**

- **事件背景**：安全研究员 `YLChen-007` 在 24 小时内系统性地测出了涉及 `exec` 工具正则绕过 (shell chain, comment tail) 和 MCP 作用域逃逸的多个漏洞。
- **社区诉求与反馈**：社区成员高度关注攻击向量的技术细节，并见证了“报告 → 确认 → 修复 PR 提交 → 问题关闭”的完整闭环。这种透明、高效的协作模式极大提升了社区对项目长期安全治理能力的信任分。
- **[查看系列 Issue](https://github.com/HKUDS/nanobot/issues?q=is%3Aissue+author%3AYLChen-007+created%3A2026-06-25+)**

**热点二：Windows 平台代理部署的“最后一公里”挑战**

- **事件背景**：用户 `Quincy-Zh` 提交的两条 Bug 报告 (`#4511`, `#4513`) 详细描述了将 `nanobot gateway` 通过 `nssm` 设置为 Windows 系统服务后遇到的进程管理与重启逻辑冲突。
- **社区痛点**：此类报告直接暴露了 NanoBot 在作为持续运行的后台服务时，对 Windows 服务生命周期规范（如端口释放、进程保活）的适配尚不完善，是桌面环境被阻塞的关键痛点。
- **[Issue #4513 - NSSM 服务重启异常](https://github.com/HKUDS/nanobot/issues/4513)**

---

### 6. Bug 与稳定性

**已修复并关闭的高/严重 Bug：**

- **Critical：PyPI 包恶意代码事件** ([#2439](https://github.com/HKUDS/nanobot/issues/2439)) —— 彻底调查并完成清理，今日关闭。
- **Critical：MCP `enabledTools` 绕过** ([#4519](https://github.com/HKUDS/nanobot/issues/4519), [#4434](https://github.com/HKUDS/nanobot/issues/4434)) —— 今日合入修复 PR #4524 解决。
- **Critical：Exec `allowPatterns` 绕过** ([#4514](https://github.com/HKUDS/nanobot/issues/4514), [#4515](https://github.com/HKUDS/nanobot/issues/4515), [#4520](https://github.com/HKUDS/nanobot/issues/4520), [#4521](https://github.com/HKUDS/nanobot/issues/4521)) —— 今日提交修复 PR #4526 解决。
- **High：文件系统权限配置不生效** ([#4073](https://github.com/HKUDS/nanobot/issues/4073), [#143](https://github.com/HKUDS/nanobot/issues/143)) —— 今日合入修复 PR #4099 解决。
- **High：Login Shell 泄露环境变量** ([#4518](https://github.com/HKUDS/nanobot/issues/4518)) —— 今日提交修复 PR #4525 解决。

**待处理的 Bug（暂无明确修复 PR）：**

- **Windows `--background` 模式状态不同步** ([#4511](https://github.com/HKUDS/nanobot/issues/4511))：重启后进程状态记录文件与实际情况不符。
- **NSSM 系统服务重启异常** ([#4513](https://github.com/HKUDS/nanobot/issues/4513))：存在端口占用与服务停止不一致的场景。

---

### 7. 功能请求与路线图信号

**高概率纳入下个版本的功能：**

- **WebUI 移动端体验跃升** ([PR #4494](https://github.com/HKUDS/nanobot/pull/4494))：PWA 支持与侧边栏滑动手势。React 社区标准实践，低风险高回报，预计快速合并。
- **技能目录组织优化** ([PR #4504](https://github.com/HKUDS/nanobot/pull/4504))：支持子目录收纳技能，解决技能数量增长后的管理混乱。
- **Gateway Webhook 能力** ([PR #4502](https://github.com/HKUDS/nanobot/pull/4502))：统一 Webhook 入口，是平台化能力的关键一步。

**路线图关键信号（中期规划）：**

- **Agent 交互范式升维**：[Issue #4508](https://github.com/HKUDS/nanobot/issues/4508) 提议的 `ask_clarification`（主动追问澄清）工具，代表了从“纯工具调用”向“协作式交互”的进化，是 Agent 智能提升的关键方向。
- **Agent 可靠性工程**：[PR #4534](https://github.com/HKUDS/nanobot/pull/4534) 引入的验证门与 Provider 恢复机制，标志着项目开始系统性应对“AI 幻觉/故障”在生产环境中的容错挑战。

---

### 8. 用户反馈摘要

- **安全建设透明化获认可**：研究员在多个 Issue 中指出 “nanobot exposes a high-impact exec tool...”，这种零信任的白盒测试风格得到了项目组的严肃对待和快速修复，成熟的开源治理模式可见一斑。
- **Windows 服务化部署体验需打磨**：用户反馈“服务显示‘已停止’，但实际 nanobot 却是在运行”，这种进程感知的脱节感是当前 Windows 环境下运维体验的明显短板。
- **集成细节存在摩擦**：钉钉连接超时、小米 ASR 格式不支持、Telegram Web 富文本显示异常，这些集成细节的反馈暴露出多模态输入和 IM 渠道适配中的兼容性挑战。

---

### 9. 待处理积压

- **Windows 服务相关问题积压**：`#4511` 和 `#4513` 目前没有明确的修复 PR，对于希望在 Windows 生产环境部署的团队属于阻塞项，建议维护者优先关注。
- **功能 PR 等待 Code Review**：`#4402` (Eager Memory Consolidation) 和 `#4404` (bwrap Bind Roots) 等 PR 由外部贡献者提交，工作量大且对核心能力有深远影响。为避免贡献者等待过久，需要维护者安排重点评审。
- **历史 Issue 清理建议**：长期 Issue `#1710` (模型无回答时的处理逻辑) 在关闭时无任何维护者评论。建议维护者在关闭此类 Issue 时留下 “By design” 或 “已在某版本修复” 等明确说明，避免外部贡献者产生反馈被忽视的负面感受。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 | 2026-06-26

## 1. 今日速览

- **活跃度极高**：过去 24 小时共产生 50 条 Issue 更新（**14 条已关闭**）与 50 条 PR 更新（**48 条开放中**），社区贡献与维护者响应保持高强度同步。
- **桌面端稳定性警报**：`hermes update` 后因 `simple-git` 模块未被打包导致桌面端启动崩溃引发用户集中报修（#52735 系列），暴露出 OTA 更新管线的依赖管理盲区。
- **安全与状态一致性攻坚**：多个 P1 级网关状态泄露/死锁 Bug 于本日关闭，同时出现了 P0 级会话恢复缓存失效修复 (#52813) 与 Email 网关防伪造安全补丁 (#52801)，显示了项目对稳定性底线的积极态度。
- **项目健康度判断**：社区活跃度极佳，Bug 反馈及时，修复力度大，但快速迭代对集成测试与构建流程带来的压力已开始显性化。

---

## 3. 项目进展

今日项目在**稳定性修复**与**平台兼容性**方面均取得实质进展：

**🔧 已合并/关闭的重要 PR**
- **TUI 状态栏修复**：PR #3291 正式合并，解决了 SSH 环境下因终端宽度探测不准确导致状态栏溢出、重复的长期问题。
- **一系列 P1 级 Bug 被关闭**：Discord 网关事件循环阻塞 (#52197)、Web/微信会话历史泄露 (#49106)、Telegram 轮询静默死亡 (#48495)、Windows Docker 后端路径泄漏 (#48137) 等困扰社区多日的问题均在本日被修复关闭。

**🆕 新提出的关键 PR**
- **P0 修复 — 会话缓存 100% 失效** (#52813)：社区贡献者 sailieri 定位并修复了 `resume/cron` 路径下发送陈旧数据库字段导致 Prompt Cache 完全失效的严重回归。
- **P1 安全修复 — Email 防伪造** (#52801)：合入了 SPF/DKIM/DMARC 验证，关闭了 GHSA-rxqh-5572-8m77 安全公告。
- **P1 修复 — sessions.json 残影** (#52808)：Gateway Crash 后重启会丢失消息路由，该 PR 通过启动时剪枝解决。
- **基础设施优化**（0disoft 系列）：#52438 (认证 Store 复用)、#52433 (Profile 轻量级列表)、#52435 (Windows venv 适配)、#52425 (更新过程耗时显示)，展现了系统化的性能与开发体验改进。
- **Provider 生态拓展**：Vertex AI 支持 (#8427)、自定义 Provider Header 转发 (#52413) 均在持续推进。

---

## 4. 社区热点

| 话题 | Issue / PR | 热度信号 | 核心诉求 |
|---|---|---|---|
| **桌面端更新崩溃** | #52735 / #52753 / #52764 | 跨平台报修，9+ 条评论，多个 Duplicate | “`hermes update` 破坏了桌面端”——新加的 `simple-git` 依赖未被正确打包进 Electron asar 包，启动即崩溃。社区要求修复 OTA 流程中的依赖同步问题。 |
| **技能管理进程误归档** | #29912 | **P1**、连续 1 个月无人修复 | “我一觉醒来 10 个活跃技能被归档了”——管理进程（Curator）在合并不具备完整验证证据的技能时，会误标记并归档正在运营的技能，且无回滚机制。 |
| **Slack Block Kit 支持** | #8552 | **9 👍**、8 条评论、活跃 2 个月 | 社区不再满足于遗留的 `mrkdwn` 格式，要求原生支持表格、列表、块级排版。这与飞书平台希望用 Card 替代 Markdown 降级的诉求（#46470）形成了跨平台 Markdown 改进的强烈信号。 |
| **工具级输出压缩** | #39691 | **10 👍**、8 条评论 | 用户对当前全上下文 LLM 压缩的高成本不满，希望引入头罗 (Headroom) 式细粒度的工具输出压缩，只压缩工具结果而非整个对话窗口。 |

---

## 5. Bug 与稳定性

| 严重度 | Bug | 状态 | 摘要 |
|---|---|---|---|
| **P0** | **#52813** — Resume/Cron 提示缓存 100% 失败 | ✅ 已有修复 PR | `repair_message_sequence` 迭代 JSON 字符串导致 `tool_calls` 空集合，回放的第一轮必定 Miss Cache。 |
| **P1** | **#52804 / #52808** — Gateway 崩溃后会话路由错误 | ✅ 已有修复 PR | Crash 跳过正常关闭，`sessions.json` 残留过期会话指针，所有新消息路由到死会话。 |
| **P1** | **GHSA-rxqh-5572-8m77 / #52801** — Email 网关 From 地址伪造 | ✅ 已有修复 PR | 仅依赖 `From` 头鉴权，可被伪造授权。已加入 SPF/DKIM/DMARC。 |
| **P1** | **#29912** — 管理进程归档活跃技能 | ❌ **待定** | 自 5 月 21 日至今未有明确修复，是当前最危急的未处理 Bug。 |
| **P2** | **#52735 #52753 #52764** — 桌面端 OTA 更新崩溃 | ❌ **待定** | `simple-git` 未打包，构建流程缺少依赖审计。 |
| **P2** | **#51646** — Gateway Memory Loss | ❌ **待定** | INSERT 遗漏 `active` 列，持久化框架默认为 NULL，导致筛选过滤全量历史。 |
| **P2** | **#36658** — Dashboard 聊天 UI 炸裂 | ❌ **待定** | React 最小化错误 #301，生产环境难以排查。 |
| **P2** | **#46260** — Windows 安装器失败 | ❌ **待定** | `npm install` 安装桌面依赖时退出，阻断 Windows 用户入门。 |

---

## 6. 功能请求与路线图信号

新提交的功能请求与活跃中的 PR 共同揭示了接下来的发展方向：

**🖥️ 桌面端「原生感」补全**
- **#52787** (最小化到托盘)、**#52769** (自动创建 `.desktop`) 代表用户希望 Hermes Desktop 成为一个有原生体验的桌面应用，而非一个跑在终端上的壳。

**📊 Agent 运营可观测性**
- **#52815 / PR #52822** (TUI 状态栏显示 Cron 状态)：社区不满足于“它能工作”，需要实时知道 Cron 是否还活着。这是 Agent 从“玩具”走向“生产工具”的必由之路。
- **#48843** (TUI 批量归档会话)：用户侧工作流效率提升。

**🧠 上下文窗口优化**
- **#52821** (从会话上下文中移除 70KB 的 AGENTS.md)：一个新思路，将大文件从系统 Prompt 改为按需加载或 RAG 式检索，极大节省 Token。此 Feature 很有希望被纳入短中期路线图。

**🌉 平台适配持续深化**
- 飞书 (Feishu) 社区的产能很高，PR #51269 (Bot to Bot 互动) 和 #46470 (统一 Card 渲染) 均在推进。
- Slack 的 Block Kit (#8552) 呼声持续高涨。

---

## 7. 用户反馈摘要

- **“更新后我失去了我的 Agent”** (#52735, #52753, #52764)：从 CLI 到 Desktop 的更新流程没有做好依赖传递，导致 Electron 主进程直接崩溃。**更新流程的健壮性是当前 UX 最大短板。**
- **“我的 Agent 失忆了”** (#51646, #49106)：用户反馈 Agent 不记得几轮前的对话，或者 Web 端和微信端的对话互相“穿越”。**会话状态的强一致性是交互式 Agent 的生命线。**
- **“我想要看到它在跑”** (#52815, PR #52822)：高级用户用代码投票，直接提交了能显示 Cron 健康状态的功能。这说明用户群已进入深度运营阶段，需要系统内建的可观测性机制。
- **“OS 的支持差距需要弥合”**：从 Docker 路径 (#48137) 到 NW.js 的 Windows 安装器 (#46260) 再到 WSL2 剪贴板 (#52819)，**Windows 端的体验虽然被积极补课，但积累的缺口依然明显。**
- **“飞书用户是最活跃的平台贡献者”**：围绕着飞书 Bot 的渲染和互动，用户提交了大量高质量的 Issue 和 PR (#46470, #51269, #27922, #52786)。

---

## 8. 待处理积压

| 类型 | 编号 | 期限/严重度 | 摘要 | 建议行动 |
|---|---|---|---|---|
| **Bug** | **#29912** (Curator 技能误归档) | **P1 / 5月21日** | 管理进程可在未完成验证的情况下归档活跃技能，过程无法回滚。 | **⚠️ 高优先级**：维护者应优先评估此 Bug 的修复方案，或临时降级 Curator 的合并力度。 |
| **Feature** | **#4656** (凭证代理守护进程) | **P3 / 4月2日** (11 评论) | 零知识 HTTP/HTTPS 代理，用于隔离 Agent 凭证。架构复杂，讨论已趋于成熟。 | 维护者给出官方设计反馈或接受/拒绝信号，避免社区贡献者做无用功。 |
| **Bot Report** | **#38240** (技能索引陈旧) | **P3 / 6月3日** | 被监控机器人持续标记 Index 为 Degraded，`github: 0 < 30`。 | 需人工确认是索引构建 CI 故障还是缓存策略问题，长期 Degraded 会削弱技能生态可信度。 |
| **PR** | **#27922** (飞书 Markdown 表格渲染) | **P2 / 5月18日** | 移除 `_MARKDOWN_TABLE_RE` 降级逻辑，使表格走原生飞书渲染管线。 | 等待 Review 与合并，这是飞书平台用户等待最久的修复之一。 |

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

## 2026-06-26 PicoClaw 项目动态日报

### 1. 今日速览
过去24小时项目活跃度较高，共更新 19 条 PR 和 3 条 Issue。核心贡献者持续发力，重点围绕资源泄漏修复、类型断言安全强化以及依赖项自动批量升级（Dependabot）展开工作。代码库合并了多个关键的 Bug 修复，包括进化模式 Token 消耗异常和 OpenAI 兼容层的构建错误。一个标记为 **高优先级** 的功能请求（[#3088](sipeed/picoclaw Issue #3088)——使用 vodozemac 替代 libolm）已滞留17天未获得指派，值得维护团队关注。整体来看，项目正处于一个积极的 **技术债务偿还与稳定性加固周期**。

### 2. 版本发布
过去24小时内无新版本发布。

### 3. 项目进展
今日共合并/关闭 6 个 PR，主要集中在 Bug 修复与工程质量提升：

*   **进化模式修复**：`#3169` ([sipeed/picoclaw PR #3169](https://github.com/sipeed/picoclaw/pull/3169)) 成功修复了进化模式在心跳检测（Heartbeat）时错误进入冷启动路径消耗 Token 的问题，直接回应了社区用户报告的 Token 泄漏 Bug（#3012）。新增了回归测试。
*   **构建与错误处理**：`#3166` ([sipeed/picoclaw PR #3166](https://github.com/sipeed/picoclaw/pull/3166)) 修复了 OpenAI 兼容提供商中因误用 `log.Printf` 导致的编译错误；`#3168` ([sipeed/picoclaw PR #3168](https://github.com/sipeed/picoclaw/pull/3168)) 改进了模型列表获取失败时的错误提示可读性。
*   **类型安全与兼容性**：`#3092` ([sipeed/picoclaw PR #3092](https://github.com/sipeed/picoclaw/pull/3092)) 修复了 `skills_install` 中类型断言未检查 `ok` 的问题；`#3045` ([sipeed/picoclaw PR #3045](https://github.com/sipeed/picoclaw/pull/3045)) 修复了 Matrix 用户 ID 中的冒号导致 `allow_from` 规则失效的问题。
*   **依赖升级**：`#3145` ([sipeed/picoclaw PR #3145](https://github.com/sipeed/picoclaw/pull/3145)) 将 `github.com/github/copilot-sdk/go` 从 v0.2.0 升级至 v1.0.2。

### 4. 社区热点
今日讨论最活跃的议题集中在已修复的和待推进的重大变更上：

*   **定时任务故障帖**：`#1757` ([sipeed/picoclaw Issue #1757](https://github.com/sipeed/picoclaw/issues/1757)) 获得了 **10 条评论**，用户 `dhensen` 报告在树莓派 Zero W 上配置每小时执行任务时遭遇 Channel 报错。该 Issue 现已关闭，表明问题已得到处理。
*   **安全库替换争议**：`#3088` ([sipeed/picoclaw Issue #3088](https://github.com/sipeed/picoclaw/issues/3088)) 是唯一一个处于开放状态的活跃 Issue，获得 **2 个点赞**。社区核心诉求是弃用不再维护且存在安全隐患的 `libolm` 库，迁移到官方替代品 `vodozemac`。尽管被标记为“高优先级”和“寻求贡献者”，但长期未获得维护者直接参与，社区对此有一定焦虑。

### 5. Bug 与稳定性
今日处理的 Bug 按严重程度排列如下：

*   **【已修复-严重】** `#3012`：进化模式每分钟固定消耗 Token。该问题通过合并 `#3169` 已彻底解决。
*   **【已修复-严重】** `#3166`：OpenAI 兼容模式构建失败，导致开发者无法正常编译代码。已合并修复。
*   **【待修复-严重】** `#3115` ([sipeed/picoclaw PR #3115](https://github.com/sipeed/picoclaw/pull/3115))：会话历史损坏 Bug。当通用工具（如 `read_file`）输出内联 Base64 图片数据时，系统会错误地将其视为附件，导致会话上下文错乱。已有修复 PR 等待合并。
*   **【待修复-中等】** `#3171` ([sipeed/picoclaw PR #3171](https://github.com/sipeed/picoclaw/pull/3171))：LINE 消息渠道的 `Send` 方法中存在因缺少类型断言检查导致的 **Panic 风险**。
*   **【待修复-中等】** `#3170` ([sipeed/picoclaw PR #3170](https://github.com/sipeed/picoclaw/pull/3170))：Agent 模块中 Base64 编码器在 `io.Copy` 失败时未关闭，造成 **资源泄漏**。
*   **【待修复-低优】** `#3172` ([sipeed/picoclaw PR #3172](https://github.com/sipeed/picoclaw/pull/3172))：多个文件中存在未处理 Body 关闭错误的代码，已有批量修复 PR。

### 6. 功能请求与路线图信号
今日观察到的功能需求与未来方向信号：

*   **高优需求（安全）**：`#3088` ([sipeed/picoclaw Issue #3088](https://github.com/sipeed/picoclaw/pull/3088)) 强烈建议用 `vodozemac` 替换 `libolm`。如果采纳，这将大幅增强 Matrix 协议下的安全性，但可能会带来编译选项和代码依赖的调整。
*   **通讯协议扩展**：`#3063` ([sipeed/picoclaw PR #3063](https://github.com/sipeed/picoclaw/pull/3063)) 新增 **DeltaChat 网关**，这表明项目正在积极拓宽去中心化消息渠道的支持范围。
*   **远程控制 Agent**：`#3118` ([sipeed/picoclaw PR #3118](https://github.com/sipeed/picoclaw/pull/3118)) 为 `picoclaw agent` 命令引入 **WebSocket 远程工作模式**，这可能是向微服务架构和 IDE 集成迈出的重要一步。

### 7. 用户反馈摘要
从今日活跃的 Issue 中可以提炼出以下用户呼声：

*   **硬件兼容性**：用户 `dhensen` 在 **Raspberry Pi Zero W**（低配ARM设备）上遇到了定时任务报错问题，尽管已经修复，但提示项目应持续关注边缘设备的测试覆盖。
*   **资源消耗敏感**：用户 `xpader` 在 **FreeBSD** 环境下反馈进化模式的 Token 持续消耗问题。这表明不同操作系统下的资源调度逻辑需要更细致的验证。
*   **供应链安全意识强**：`#3088` 请求者 `pbsds` 明确表示“`libolm` 未维护且不安全”，展现了社区对底层安全依赖的极高警惕性。这种呼声往往影响到企业级用户的选择。

### 8. 待处理积压
提醒维护者关注的长期未响应或重要积压项目：

*   **【高优-停滞】`#3088`** ([sipeed/picoclaw Issue #3088](https://github.com/sipeed/picoclaw/issues/3088))：状态为 [OPEN, help wanted, priority: high, stale]。尽管获得高优先级标签，但无人认领，已停滞17天。建议维护者明确是否接纳此功能，或授权社区贡献者。
*   **【功能-等待Review】`#3063`** ([sipeed/picoclaw PR #3063](https://github.com/sipeed/picoclaw/pull/3063)) 与 **`#3118`** ([sipeed/picoclaw PR #3118](https://github.com/sipeed/picoclaw/pull/3118))：这两个功能型 PR 已提交超过 10 天，目前没有新增 Review 进展，长期搁置可能导致与主线的冲突风险增加。
*   **【Bug-悬而未决】`#3142`** ([sipeed/picoclaw PR #3142](https://github.com/sipeed/picoclaw/pull/3142))：修复 Spawn 子流程中重复消息的 Bug 已与 `#3142` 关联，该 PR 已标记为 `stale`，需尽快评估是否继续。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-06-26

---

## 今日速览

- 过去 24 小时 **1 个新 Issue** 开启，**16 个 PR 有活动**（其中 11 个已合并/关闭，5 个仍开放），**无新版本发布**。
- 项目开发活跃度极高：大量 PR 被合并，涵盖**安全加固、认证机制改进、新技能添加、平台兼容性修复**等多个维度。
- 社区新 Issue 聚焦**审批机制的多管理员支持与 CLI 批准**，与刚合并的“拒绝带原因”功能形成延续，可能成为下阶段重点。
- 多个历史遗留下来的 Bug（macOS 证书问题、服务残留注册、UTF-8 计数错误）在本日得到修复，项目整体稳定性提升。

---

## 版本发布

无（今日无新版本发布）。

---

## 项目进展

今日共有 **11 个 PR 被合并/关闭**，以下为关键推进（按重要程度排列）：

- **安全加固**：[PR #2817](https://github.com/nanocoai/nanoclaw/pull/2817) `fix(security): confine send_file reads to workspace` —— 使用 `realpath` 严格校验路径，防止符号链接逃逸工作区，已附带回归测试。
- **认证降级机制**：[PR #2855](https://github.com/nanocoai/nanoclaw/pull/2855) `feat(auth): subscription-primary credential posture with API-key failover` —— 使 Claude 订阅（OAuth）成为首选，API Key 作为热备自动降级，并触发运维告警。
- **审批增强**：[PR #2832](https://github.com/nanocoai/nanoclaw/pull/2832) `feat(approvals): reject with reason` —— 审批卡片增加“拒绝并附原因”按钮，拒绝理由会回传给请求 agent，使其能据此调整行为。
- **新技能**：[PR #2843](https://github.com/nanocoai/nanoclaw/pull/2843) `feat: add /learn skill` —— 新增 `/learn` 技能，可从目录、URL、剪贴板等来源提炼并生成可复用的技能文件。
- **容器资源限制**：[PR #2856](https://github.com/nanocoai/nanoclaw/pull/2856) `feat(container): per-container CPU/memory limits (opt-in)` —— 通过环境变量 `CONTAINER_CPU_LIMIT` / `CONTAINER_MEMORY_LIMIT` 对每个 agent 容器做资源上限设置。
- **macOS 证书修复**：[PR #2854](https://github.com/nanocoai/nanoclaw/pull/2854) `fix(onecli): redirect TMPDIR so gateway CA mounts into containers on macOS` —— 解决 Rancher Desktop 下自签名证书导致的 API 连接失败。
- **服务残留清理**：[PR #2830](https://github.com/nanocoai/nanoclaw/pull/2830) `fix(setup): reap dead peer service registrations whose binary is gone` —— 自动检测并移除已删除项目残留的 launchd/systemd 注册。
- **CLI 响应计数**：[PR #2813](https://github.com/nanocoai/nanoclaw/pull/2813) `fix(cli): count socket response cap by bytes` —— 将响应截断由字符数改为字节数，修复 UTF-8 多字节字符导致的误判。
- **Router 修复**：[PR #2815](https://github.com/nanocoai/nanoclaw/pull/2815) `fix(router): guard safeParseContent against primitive JSON` —— 修复 JSON 基本类型/数组被错误解析为对象而导致路由规则失效的问题。
- **Per-thread 会话功能（最终关闭）**：[PR #2471](https://github.com/nanocoai/nanoclaw/pull/2471) 和 [PR #2472](https://github.com/nanocoai/nanoclaw/pull/2472) 完成 Router 层与 Slack 适配器的 per-thread 支持，优化 Slack 私信中的会话管理。

这些合并标志着项目在**安全性、稳定性、功能完整度**上均有扎实进展。

---

## 社区热点

今日未出现评论数极高的讨论，但以下项目值得关注：

- **[Issue #2857](https://github.com/nanocoai/nanoclaw/issues/2857)** `approval should support multi admins and terminal cli approvals` —— 当前唯一新开 Issue，提出两个诉求：1) agent 可重新向其他管理员请求批准；2) 拥有机器访问权限的 owner 可通过 CLI 直接批准。该 Issue 与刚合并的 PR #2832（拒绝带理由）直接关联，表明审批流程是社区当前关注的焦点。
- **[PR #2843](https://github.com/nanocoai/nanoclaw/pull/2843)** `/learn skill` —— 虽已合并，但在合并前可能引发关于技能生成最佳实践的讨论，且其描述中提及“从任何来源提炼技能”，对开发者效率提升显著。
- **[PR #2855](https://github.com/nanocoai/nanoclaw/pull/2855)** 认证降级机制 —— 直接关系到用户在生产环境中的可用性，尤其适合拥有企业订阅同时使用 API Key 作为备用的场景。

由于平台数据未提供评论/反应计数，上述分析主要基于内容本身的影响面。

---

## Bug 与稳定性

今日修复和暴露的 Bug 按严重程度排列：

| 严重程度 | 问题描述 | 状态 |
|----------|----------|------|
| **高** | macOS 上 Rancher Desktop 下所有 agent API 调用因自签名证书失败（网关 CA 未挂载到容器） | ✅ 已修复 [PR #2854](https://github.com/nanocoai/nanoclaw/pull/2854) |
| **中** | v2 迁移脚本在旧版 v1.1.0 数据库上因缺少 `is_main` 列而崩溃，导致整个 v2 数据无法创建 | 🔴 仍有未合并修复 [PR #2859](https://github.com/nanocoai/nanoclaw/pull/2859) |
| **中** | 依赖库 `libsignal` 在每次会话开闭时输出密钥材料到 console.info，造成日志噪音及潜在信息泄露 | 🔴 修复中 [PR #2860](https://github.com/nanocoai/nanoclaw/pull/2860) |
| **低** | socket 响应字符数限制在 UTF-8 多字节字符下不能正确截断，可能导致服务端误判 | ✅ 已修复 [PR #2813](https://github.com/nanocoai/nanoclaw/pull/2813) |
| **低** | `safeParseContent` 将 JSON 字符串/数组当作对象解析，导致这些内容无法匹配路由规则 | ✅ 已修复 [PR #2815](https://github.com/nanocoai/nanoclaw/pull/2815) |
| **低** | `send_file` 路径验证可被符号链接绕过，读取工作区外的文件 | ✅ 已修复 [PR #2817](https://github.com/nanocoai/nanoclaw/pull/2817) |
| **低** | 删除项目后系统残留的 launchd/systemd 注册持续尝试启动已不存在的入口文件，积累无用进程 | ✅ 已修复 [PR #2830](https://github.com/nanocoai/nanoclaw/pull/2830) |

总体来看，今日无严重新 Bug 报告，多个低中危问题已通过合并解决，项目稳定性趋势向好。

---

## 功能请求与路线图信号

- **多管理员审批 & CLI 批准**（[Issue #2857](https://github.com/nanocoai/nanoclaw/issues/2857)）—— 与已合并的“拒绝带理由”形成闭环，很可能被纳入下一个小版本。
- **/add-clidash 技能**（[PR #2795](https://github.com/nanocoai/nanoclaw/pull/2795) 及替代版 [PR #2858](https://github.com/nanocoai/nanoclaw/pull/2858)）—— 社区贡献的只读 CLI 仪表板技能，目前有新版 PR 等待审查。
- **移除过时的 Global Memory 指令**（[PR #2824](https://github.com/nanocoai/nanoclaw/pull/2824)）—— 清理默认 system prompt 中的遗留内容，影响所有新建会话，建议尽快纳入主线。
- **libsignal 日志静默**（[PR #2860](https://github.com/nanocoai/nanoclaw/pull/2860)）—— 虽标记为 chore，但涉及密钥材料输出，安全敏感，应优先合并。
- **v2 迁移兼容性修复**（[PR #2859](https://github.com/nanocoai/nanoclaw/pull/2859)）—— 确保旧版 v1 用户顺利完成升级，直接影响升级路径的可用性。

结合已合并的 per-thread 会话功能和容器资源限制，下一版本可能侧重**审批流程完善、系统提示清理、以及安装/迁移体验优化**。

---

## 用户反馈摘要

今日无直接 Issue 评论提供用户反馈，但从修复的 PR 描述中可以提炼出以下真实用户痛点：

- **macOS 用户使用 Rancher Desktop** 时所有 agent API 请求因自签名证书失败，需手动干预（[PR #2854](https://github.com/nanocoai/nanoclaw/pull/2854)）。
- **从 v1 升级到 v2** 时若旧版本为 1.1.0，迁移脚本会因列缺失而直接崩溃，无法完成升级（[PR #2859](https://github.com/nanocoai/nanoclaw/pull/2859)）。
- **删除项目后未运行卸载程序**导致 launchd/systemd 无限重试、堆积大量僵尸注册（[PR #2830](https://github.com/nanocoai/nanoclaw/pull/2830)）。
- **审批流程不灵活**：当单一管理员不可用，其他管理员无法介入，期望支持多管理员与 CLI 批准（[Issue #2857](https://github.com/nanocoai/nanoclaw/issues/2857)）。
- **希望从现有工作流中快速提炼技能**：/learn 技能的提出表明社区有将已有代码/对话转化为标准化技能的迫切需求（[PR #2843](https://github.com/nanocoai/nanoclaw/pull/2843)）。

---

## 待处理积压

以下开放 PR 或 Issue 持续时间较长或涉及关键功能，建议维护者优先关注：

| 项目 | 描述 | 开启时间 | 建议 |
|------|------|----------|------|
| [PR #2795](https://github.com/nanocoai/nanoclaw/pull/2795) `feat: add /add-clidash` | 社区贡献的技能，已有替代改进 PR #2858，原 PR 未关闭 | 2026-06-17 | 关闭原 PR 并推动 #2858 合并 |
| [PR #2858](https://github.com/nanocoai/nanoclaw/pull/2858) `fix(add-clidash): apply install and engine fixes` | 替代 #2795，已根据审查意见修正，需审核 | 2026-06-25 | 审查并合并，以完成技能发布 |
| [PR #2824](https://github.com/nanocoai/nanoclaw/pull/2824) `fix: drop stale "Global Memory" instruction` | 清理 prompt 中过时指令，影响所有用户且改动简单，已悬停近一周 | 2026-06-20 | 尽快审查合并 |
| [PR #2859](https://github.com/nanocoai/nanoclaw/pull/2859) `fix(migrate-v2): don't SELECT is_main from v1` | 修复旧版 v1 用户升级时崩溃，阻塞升级通道 | 2026-06-25 | 必须合并，否则部分用户无法迁移 |
| [PR #2860](https://github.com/nanocoai/nanoclaw/pull/2860) `chore(logging): silence libsignal session debug spam` | 静默密钥材料输出，安全风险，虽有风险但属于低风险合并 | 2026-06-26 | 尽快合并以防止可能的信息泄露 |
| [Issue #2857](https://github.com/nanocoai/nanoclaw/issues/2857) `approval support multi admins` | 新功能需求，暂无回复 | 2026-06-25 | 标记为下个里程碑，结合已合并的 #2832 考虑实现 |

---

*日报由AI辅助生成，数据截止时间为 2026-06-26 14:00 UTC。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 | 2026-06-26

## 📊 今日速览

今日 IronClaw 维持极高的开发活跃度，过去 24 小时内产生 50 条 Issues 和 50 条 PR。项目主线集中在 **Reborn 架构** 的 **Capability Policy（能力策略/多租户权限系统）** 和 **Memory 2.0（扩展清单与记忆系统）** 两大特性推进上。然而，高强度开发也暴露了 Reborn 核心流程的信任危机：**工具审批流出现系统性 Bug**（拒绝后仍弹窗、批准后不持久、重复授权循环），**自动化定时任务因 "No Thread Attached" 完全失效（#5276）**。尽管团队响应迅速（重试死循环、UI 体验、性能回归等修复均已有对应 PR 在途），Stability 仍是当前项目最突出的健康度短板。

---

## 🚀 版本发布

今日无新版本发布。

---

## ✅ 项目进展

过去 24 小时内，项目共关闭 Issues **17** 条，合并/关闭 PR **18** 个。主要进展集中在修复 Reborn 遗留 Bug 和优化基础设施性能：

### 已合并/关闭的重要 PR

| PR / Issue | 描述 | 类型 |
|---|---|---|
| [#5278](https://github.com/nearai/ironclaw/issues/5278) | 修复 WebUI v2 Logs 页面无法滚动的问题 | 🪲 Bug |
| [#5255](https://github.com/nearai/ironclaw/issues/5255) | 将 Postgres CAS `put` 的路径预检从 **3 轮查询合并为 1 轮**，显著降低写延迟 | ⚡ 性能 |
| [#5210](https://github.com/nearai/ironclaw/issues/5210) | 修复审批弹窗未关闭时发送新消息导致的消息状态丢失 | 🪲 Bug |
| [#5211](https://github.com/nearai/ironclaw/issues/5211) | 修复新响应未自动滚动到视图的问题 | 🪲 Bug |
| [#5208](https://github.com/nearai/ironclaw/issues/5208) | 修复等待 Agent 回复时输入框被锁定的问题 | 🪲 Bug |
| [#5212](https://github.com/nearai/ironclaw/issues/5212) | 对话中消息时间戳显示一致性修复 | 🪲 UX |
| [#5242](https://github.com/nearai/ironclaw/issues/5242) | 修复 Settings > Tools 页面错误显示 Operator-only 权限错误 | 🪲 Bug |
| [#5243](https://github.com/nearai/ironclaw/issues/5243) | 修复 "Approve & always allow" 未持久化到 Settings | 🪲 Bug |

### 关键开放 PR（代表项目前进方向）

- **Capability Policy 系列**：[#5288](https://github.com/nearai/ironclaw/issues/5288)（Delta Store + PolicyResolver）、[#5286](https://github.com/nearai/ironclaw/issues/5286)（多用户本地认证）、[#5277](https://github.com/nearai/ironclaw/issues/5277)（可用性解析器）
- **稳定性修复**：[#5287](https://github.com/nearai/ironclaw/issues/5287) / [#5285](https://github.com/nearai/ironclaw/issues/5285)（打破 Agent 重试死循环，root cause 明确）
- **Trace Commons 可观测性**：[#5280](https://github.com/nearai/ironclaw/issues/5280)（实例级注册与用户 profile）
- **事件日志批量写入**：[#5257](https://github.com/nearai/ironclaw/issues/5257)（write-behind coalescing 性能优化）

**项目整体向前迈进的信号**：Capability Policy 的特性已经进入后端存储与调度层的具体实现阶段，标志着 IronClaw 正在从「个人助手」向「可运营的企业级 Agent 平台」演进。大量 UI 遗留 Bug 的关闭也说明 Reborn 的 Dogfooding 机制（#5119）正在高效运转。

---

## 🔥 社区热点

### 1. 工具审批流程系统性故障（信任危机）

这是今日社区反映最集中、影响最严重的 Bug 集群：

- [#5192](https://github.com/nearai/ironclaw/issues/5192)：**拒绝工具审批后，AI 仍会继续发出审批请求**，拒绝形同虚设
- [#5196](https://github.com/nearai/ironclaw/issues/5196)：**“Ask each time” 批准后触发授权错误**，进入双重审批循环
- [#5243](https://github.com/nearai/ironclaw/issues/5243) / [#5283](https://github.com/nearai/ironclaw/issues/5283)：**"Approve & always allow" 不生效**，设置不持久化
- [#5129](https://github.com/nearai/ironclaw/issues/5129)：`outbound_delivery_target_set` 场景下的 Always approve 完全失效

**背后诉求**：用户对 Agent 安全机制产生根本性质疑。工具的审批是自主 Agent *信任底座* 的核心环节，当前状态严重破坏了产品体验的基础保障。

### 2. 自动化任务 100% 失败

- [#5276](https://github.com/nearai/ironclaw/issues/5276)：定时自动化（Daily PR Digest）每次运行均报 `No thread attached`，成功率 **0%**。任务记录创建后无法关联到对话线程，直接空输出。

**背后诉求**：自动化为高阶用户的日常必备能力，该 Bug 完全堵塞了依赖自动化工作流的用户场景。

---

## 🐛 Bug 与稳定性（按严重程度排列）

| 严重程度 | Issue / PR | 描述 | Fix 状态 |
|---|---|---|---|
| 🔴 **严重** | [#5276](https://github.com/nearai/ironclaw/issues/5276) | 定时自动化因 "No Thread Attached" 成功率 0% | **无 Fix PR** |
| 🔴 **严重** | [#5289](https://github.com/nearai/ironclaw/issues/5289) | `builtin.json` 的 `invalid_input` 被掩盖为通用 "driver protocol error"，用户无法诊断 | **无 Fix PR** |
| 🔴 **严重** | [#5196](https://github.com/nearai/ironclaw/issues/5196) / [#5243](https://github.com/nearai/ironclaw/issues/5243) / [#5283](https://github.com/nearai/ironclaw/issues/5283) | 工具审批/授权流程全线故障（批准不持久、拒绝后仍请求） | **无 Fix PR** |
| 🟠 **高** | [#5192](https://github.com/nearai/ironclaw/issues/5192) | 拒绝工具审批无法终止 AI 后续的审批请求 | **无 Fix PR** |
| 🟠 **高** | [#5210](https://github.com/nearai/ironclaw/issues/5210) | 审批打开时发新消息导致消息状态丢失 | ✅ **已关闭** |
| 🟠 **高** | [#5191](https://github.com/nearai/ironclaw/issues/5191) | 内部技能编排消息暴露在用户对话界面 | **无 Fix PR** |
| 🟠 **高** | [#5287](https://github.com/nearai/ironclaw/issues/5287) / [#5285](https://github.com/nearai/ironclaw/issues/5285) | Agent 面对同一失败卡住不响应（sys-005 超时） | ✅ **Fix PR** #5287 / #5285 开放中 |
| 🟠 **高** | [#5275](https://github.com/nearai/ironclaw/issues/5275) | Logs 链接路径 `/v2/v2/logs` 重复拼接导致死链 | ✅ **Fix PR** #5275 开放中 |
| 🟡 **中** | [#5282](https://github.com/nearai/ironclaw/issues/5282) | Agent 运行时，"Logs" 条目出现在消息输入框内 | ✅ **Fix PR** #5284 开放中 |
| 🟡 **中** | [#5242](https://github.com/nearai/ironclaw/issues/5242) | 普通用户打开 Settings > Tools 页面误报 Operator 权限错误 | ✅ **已关闭** |
| 🟡 **中** | [#4980](https://github.com/nearai/ironclaw/issues/4980) | Automations 空状态缺少创建引导（无按钮、无提示） | ✅ **已关闭** |

---

## 🧭 功能请求与路线图信号

### 1. 【确定性信号】Capability Policy —— 下一版本的核心功能

这是目前投入开发资源最多的特性，**极有可能纳入下一版本**。

- **Epic**：[#5261](https://github.com/nearai/ironclaw/issues/5261) *Reborn Capability Policy: Admin-shared tools with per-user auth*
- 今日推进的子任务：
  - [#5288](https://github.com/nearai/ironclaw/issues/5288)：**Delta Store + PolicyResolver 存储层**（PR 开放）
  - [#5286](https://github.com/nearai/ironclaw/issues/5286)：**多用户本地认证**，支持同一 operator 模拟不同身份（PR 开放）
  - [#5277](https://github.com/nearai/ironclaw/issues/5277)：**可用性解析器**，将授权结果真正绑定到模型可见的工具列表（PR 开放）
  - [#5272](https://github.com/nearai/ironclaw/issues/5272) / [#5273](https://github.com/nearai/ironclaw/issues/5273)：用户 Token → Role 映射、四维策略（配置/身份/审批）执行层

**信号解读**：一个公司运行一个 IronClaw 实例、管理员分配权限、不同角色看到不同工具的能力链路已经闭环。**这标志着 IronClaw 正在从「个人单机助手」向「企业多租户平台」转型。**

### 2. 【中等信号】Memory 2.0 —— 扩展清单 V2 + 语义搜索

- **Epic**：[#3537](https://github.com/nearai/ironclaw/issues/3537) / [#5260](https://github.com/nearai/ironclaw/issues/5260)
- PR [#5205](https://github.com/nearai/ironclaw/issues/5205)（size: XL）已开放，作者设计了全新的 Extension Manifest V2 架构、源感知信任体系、以及始终在线的原生文档存储

### 3. 【微弱信号】OpenAI 兼容 API 接口

- PR [#5094](https://github.com/nearai/ironclaw/issues/5094)（/v1/models, model validation, external-tool gate）已开放多日等待后续执行器重调度工作

---

## 💬 用户反馈摘要

从今日 Issues 评论区提取的真实用户痛点场景：

### 信任与安全
> “点击 **Approve** 后不生效，点击 **Deny** 后继续弹窗。审批系统像是坏掉了。”
> — 引自 #5192、#5243、#5283 多位用户

### 自动化不可靠
> “我的 Daily PR Digest 自动化 0% 成功率，没有任何有用报错，完全不可用。”
> — 引自 #5276

### 错误信息不透明
> “我只看到 `The operation stopped before responding due to a driver protocol error`，完全不知道底层是 `invalid_input` 的错。”
> — 引自 #5289

### 用户体验粗糙
> “运行过程中输入框被锁、Logs 居然跑到输入框里、长回复不自动滚屏……Reborn UI 的实时状态管理还有很长的路要走。”
> — 引自 #5208、#5282、#5211 等多条反馈

### 积极信号
> “虽然 Bug 很多，但修 Bug 的速度也很快。Dogfooding 的沟通很透明。”
> — 引自 #5119 Dogfooding 跟踪 Issue

---

## 📥 待处理积压

以下为需要维护者重点关注、但当前尚无明确 Fix 在途的积压事项：

| Item | 类型 | 积压天数 | 风险 |
|---|---|---|---|
| [#5276](https://github.com/nearai/ironclaw/issues/5276) 自动化“No Thread Attached”全量失败 | 🐛 **Critical Bug** | 1 天 | 🔴 产品核心功能断裂 |
| [#5192](https://github.com/nearai/ironclaw/issues/5192) 拒绝后仍弹窗（审批状态机设计缺陷） | 🐛 **Critical Bug** | 2 天 | 🔴 安全/信任屏障失效 |
| [#5289](https://github.com/nearai/ironclaw/issues/5289) 通用 Driver Protocol Error 掩盖根因 | 🐛 **Critical Bug** | 1 天 | 🔴 使用户无法自助排查 |
| [#5173](https://github.com/nearai/ironclaw/issues/5173) Clawbench 失败分类（deepseek-v4-flash） | 🧪 **内部分类** | 2 天 | 🟠 模型/基准质量积压 |
| [#5094](https://github.com/nearai/ironclaw/issues/5094) OpenAI /v1/models API 兼容 PR | 🚀 **Feature PR** | 7 天 | 🟡 阻塞外部生态系统集成 |
| [#5234](https://github.com/nearai/ironclaw/issues/5234) 移除每个 Record 的锁并发（CAS 迁移） | ⚡ **Perf PR** | 1 天 | 🟡 多线程性能风险 |

---

**总结**：IronClaw 正处于一场大胆的重构期。Capability Policy 和 Memory System 让人对产品的未来架构充满期待，但当前 Reborn 稳定性的缺口——尤其是审批流的信任链条断裂（#5192, #5196, #5243）和自动化底层故障（#5276）——需要优先止血。社区的积极参与和团队的高响应速度是项目健康的资产负债表中最有价值的部分。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是根据今日 LobsterAI GitHub 数据生成的 2026-06-26 项目动态日报。

---

## LobsterAI 项目动态日报 | 2026-06-26

### 1. 今日速览

项目今日无新版本发布，但代码开发节奏极为紧凑，24小时内共合并了 **8 个 Pull Requests**，且无任何待合并 PR 积压。今日修复工作全面围绕 **Cowork（协作模式）** 与 **OpenClaw（插件扩展系统）** 两大核心模块展开，重点解决了多智能体协作过程中的消息一致性与插件加载健壮性问题。Issues 侧相对平静，但存在一条长期未响应的用户 Bug 报告。

### 2. 版本发布

今日无新版本发布。

### 3. 项目进展

今日合并的 8 个 PR 标志着项目正从功能迭代转向深度稳定性打磨，具体推进如下：

**协作模式（Cowork）稳定性增强**
- **修复规划模式消息泄漏与重复**：解决了 GLM 规划模式下标签文本溢出到聊天框（[#2204](https://github.com/netease-youdao/LobsterAI/pull/2204)），以及 Qwen 规划模式下因流抖动导致重复规划消息的问题（[#2200](https://github.com/netease-youdao/LobsterAI/pull/2200)）。
- **修复子智能体断连**：修复父会话结束后子智能体轮询丢失的问题，现在支持在父任务完成后继续等待子任务运行最多 5 分钟再获得最终结果（[#2199](https://github.com/netease-youdao/LobsterAI/pull/2199)）。
- **UI 细节优化**：更新了规划模式的应用图标，使其更好地适配主题 SVG（[#2205](https://github.com/netease-youdao/LobsterAI/pull/2205)）。

**插件系统（OpenClaw）健壮性提升**
- **修复扩展加载与白名单**：修复了预编译本地扩展入口文件加载失败的问题，并将内置浏览器插件强制加入允许列表，确保安全策略下浏览器控制功能不受影响（[#2203](https://github.com/netease-youdao/LobsterAI/pull/2203)，[#2202](https://github.com/netease-youdao/LobsterAI/pull/2202)）。
- **历史同步去重**：修复了对话“yield”后最终同步导致助手回复重复写入的缺陷（[#2201](https://github.com/netease-youdao/LobsterAI/pull/2201)）。

**系统设置修复**
- **启动项同步**：修复了“开机自启”设置与操作系统实际状态不同步的问题，增加了校验逻辑和诊断日志（[#2206](https://github.com/netease-youdao/LobsterAI/pull/2206)）。

### 4. 社区热点

今日社区讨论热度较低，唯一有动态的 Issue 是 **[#1392：定时任务开关点击无反应](https://github.com/netease-youdao/LobsterAI/issues/1392)**。

该 Issue 创建于 4 月初，尽管已被标记为 `[stale]`，但在今日被系统自动更新。用户反映设置定时任务后，部分任务的开关无法点击关闭，且配图描述了现状。
**分析**：该 Issue 长期未被标记或分配，反映出“部分场景下的偶现 UI 交互失效”在优先级上低于核心架构修复。用户对于“开关”这种基础控件在部分场景下失效的情况存在较强的挫败感，建议维护团队给予关注和回应。

### 5. Bug 与稳定性

| 严重程度 | 描述 | 状态 | 链接 |
| :--- | :--- | :--- | :--- |
| **严重** | **定时任务开关部分失效**：用户无法关闭已设定的部分定时任务，影响核心定时功能正常使用。 | 开放（无指派） | [#1392](https://github.com/netease-youdao/LobsterAI/issues/1392) |
| **已修复** | **协作模式消息重复/丢失**：因流抖动和小助手同步逻辑缺陷导致的多条消息重复问题。 | 已合并 | [#2200](https://github.com/netease-youdao/LobsterAI/pull/2200)，[#2201](https://github.com/netease-youdao/LobsterAI/pull/2201) |
| **已修复** | **子智能体断连**：父会话结束后，子智能体运行状态丢失，无法返回最终结果。 | 已合并 | [#2199](https://github.com/netease-youdao/LobsterAI/pull/2199) |
| **已修复** | **开机自启状态不同步**：设置界面显示与实际操作系统状态不一致。 | 已合并 | [#2206](https://github.com/netease-youdao/LobsterAI/pull/2206) |
| **已修复** | **插件加载异常**：预编译扩展与浏览器插件在特殊配置下无法正常加载或保持开启。 | 已合并 | [#2203](https://github.com/netease-youdao/LobsterAI/pull/2203)，[#2202](https://github.com/netease-youdao/LobsterAI/pull/2202) |

### 6. 功能请求与路线图信号

今日未收到新的功能请求。

**路线图信号**：从今日合并的 PR 可以明显看出，项目当前的开发重点完全聚焦于 **Cowork 多智能体场景的数据一致性** 与 **OpenClaw 插件系统的工程健壮性**。这表明项目目前处于 **“核心能力打磨期”**，正在为未来可能的大版本发布或更开放的第三方插件生态夯实基础。

### 7. 用户反馈摘要

主要反馈来自 Issue [#1392](https://github.com/netease-youdao/LobsterAI/issues/1392)：
- **痛点**：用户 `zqgittest` 报告，设置定时任务后，**部分**任务的开关无法点击关闭。虽然用户表述为“大部分正常”，但偶现的控件失效严重影响了用户对任务模块的控制感和信任度。该反馈未获得官方回复。

### 8. 待处理积压

目前仅有一条长期未响应的积压 Issue：

- **[Issue #1392] 定时任务开关点击无反应，无法关闭**
  - **创建于**：2026-04-03（距今 84 天）
  - **最近更新**：2026-06-25（自动化 stale 标记更新）
  - **状态**：Open（未被分配）
  - **链接**：[netease-youdao/LobsterAI #1392](https://github.com/netease-youdao/LobsterAI/issues/1392)
  - **建议**：该 Issue 虽然已被自动化标记为 `[stale]`，但核心功能缺陷不应随之沉寂。建议项目维护者在当前密集的架构优化周期之余，将该问题列入排期，至少给予用户初步的排查方向回复，以缓解因长时间沉默带来的社区信任度流失。

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

## CoPaw 项目动态日报 — 2026-06-26

### 1. 今日速览

过去 24 小时项目活跃度维持高位：共处理 **25 条 Issue**（新开/活跃 15 条，关闭 10 条）和 **50 条 PR**（待合并 29 条，合并/关闭 21 条）。多个阻塞性 Bug（如 GLM 模型兼容性、前端排版错乱、Token 页面空状态）通过合入 PR 得到修复；未发布新版本，但 Windows 桌面自动化、记忆系统重构、沙箱等大型特性 PR 仍在积极开发中。整体来看，项目修复效率高、特性管线饱满，社区反馈响应及时。

---

### 2. 版本发布

本日无新版本发布。

---

### 3. 项目进展

今日合并/关闭了多项关键 PR，主要涵盖以下方面：

| PR | 说明 | 关联 Issue |
|----|------|------------|
| [#5496](https://github.com/agentscope-ai/QwenPaw/pull/5496) | 内联工具参数 schema 中的 `$ref/$defs`，修复 GLM-5.x 通过 OpenCode Go 调用时的 `json_schema_converter.cc` 失败 | fix [#5472](https://github.com/agentscope-ai/QwenPaw/issues/5472) |
| [#5538](https://github.com/agentscope-ai/QwenPaw/pull/5538) | 保留 Assistant Markdown 消息中的换行符，解决长消息排版错乱 | fix [#5480](https://github.com/agentscope-ai/QwenPaw/issues/5480) |
| [#5457](https://github.com/agentscope-ai/QwenPaw/pull/5457) | 对 `send_file_to_user` 增加文件大小上限，防止资源滥用 | 提升健壮性 |
| [#5471](https://github.com/agentscope-ai/QwenPaw/pull/5471) | 泛化 Governance 匹配模式，为策略系统奠定基础 | 框架演进 |
| [#5443](https://github.com/agentscope-ai/QwenPaw/pull/5443) | 恢复 AgentScope 2.0 迁移后的 TUI ACP 命令与内联审批功能 | 修复回归 |
| [#5380](https://github.com/agentscope-ai/QwenPaw/pull/5380) | 新增 Langfuse 可观测性 Docker 部署与配置文档 | 文档完善 |
| [#5544](https://github.com/agentscope-ai/QwenPaw/pull/5544) | 修复 TokenUsage 页面缺失的 `emptyState` / `emptyIcon` 样式 | 前端体验 |

此外，[#5540](https://github.com/agentscope-ai/QwenPaw/pull/5540)（基于 turn 标记重构自动记忆系统）和 [#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187)（Windows 桌面 GUI 自动化）等大型特性 PR 仍在持续更新中，标志着项目在跨平台自动化与智能记忆方向稳步推进。

---

### 4. 社区热点

- **[#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345)（8 条评论）**：用户报告 OMLX 等自定义 OpenAI 兼容提供商无法使用 function calling，而 Ollama 正常工作。该 Issue 虽已关闭，但反映了社区对企业级/自建模型集成原生工具调用能力的高度关注。
- **[#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379)（6 条评论）**：Windows 用户通过 pip 安装后启动即报 `Internal Server Error`，日志指向 `get_remote_addr(transport)` 错误。该问题严重阻碍新用户上手，社区正协助分析日志，目前尚无修复 PR。
- **[#5480](https://github.com/agentscope-ai/QwenPaw/issues/5480)（5 条评论）**：Console 前端接收长消息时排版完全错乱，切换选项卡后恢复。被多位用户标记为严重的 UI 缺陷，已于当日通过 [#5538](https://github.com/agentscope-ai/QwenPaw/pull/5538) 合入修复。

---

### 5. Bug 与稳定性

以下按严重程度排列今日活跃的 Bug，并标注是否有对应修复 PR。

| 严重程度 | Issue | 描述 | 状态 | Fix PR |
|----------|-------|------|------|--------|
| 🔴 严重 | [#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379) | 安装后启动报 `Internal Server Error`，影响 Windows 用户 | OPEN | 无 |
| 🔴 严重 | [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) | 对话思考逻辑进入死循环，Agent 不可用（已开放 2 周） | OPEN | 无 |
| 🟠 中高 | [#5520](https://github.com/agentscope-ai/QwenPaw/issues/5520) | `browser_use stop()` 未清理 Chrome 渲染进程，内存泄漏（#2733 回归） | OPEN | [#5536](https://github.com/agentscope-ai/QwenPaw/pull/5536)（待合入）|
| 🟠 中高 | [#5505](https://github.com/agentscope-ai/QwenPaw/issues/5505) | MiniMax-M3 安全审核错误被缓存为 `rejects_media=True`，后续图片请求被错误剥离 | OPEN | 无 |
| 🟡 中等 | [#5479](https://github.com/agentscope-ai/QwenPaw/issues/5479) | 大会话文件（>500KB）打开时前端崩溃 | OPEN | 无 |
| 🟡 中等 | [#5543](https://github.com/agentscope-ai/QwenPaw/issues/5543) | Function Declaration 中 `type: "null"` 导致第三方代理请求失败 | OPEN | [#5545](https://github.com/agentscope-ai/QwenPaw/pull/5545)（待合入）|
| 🟢 中低 | [#5528](https://github.com/agentscope-ai/QwenPaw/issues/5528) | Linux 桌面下默认浏览器被 IME 包装导致 `browser_use` 超时 | OPEN | 无 |
| 🟢 中低 | [#5539](https://github.com/agentscope-ai/QwenPaw/issues/5539) | Heartbeat 任务 120s 硬超时导致复杂任务被误打断 | OPEN | 无 |
| ✅ 已修复 | [#5480](https://github.com/agentscope-ai/QwenPaw/issues/5480) | 前端长消息排版错乱 | CLOSED | [#5538](https://github.com/agentscope-ai/QwenPaw/pull/5538) |
| ✅ 已修复 | [#5472](https://github.com/agentscope-ai/QwenPaw/issues/5472) | GLM 系列模型调用报错 | CLOSED | [#5496](https://github.com/agentscope-ai/QwenPaw/pull/5496) |
| ✅ 已修复 | [#5501](https://github.com/agentscope-ai/QwenPaw/issues/5501) | 宽屏模式发送按钮对齐 | CLOSED | 无（直接关闭） |

---

### 6. 功能请求与路线图信号

- **工具结果大小硬上限（[#5342](https://github.com/agentscope-ai/QwenPaw/issues/5342)）**：建议在执行层设置工具结果大小硬限制，作为上下文爆炸的纵深防御。社区讨论积极，暂无 PR 实现，但路线图价值高。
- **AgentScope 2.0 动态模型切换（[#5527](https://github.com/agentscope-ai/QwenPaw/issues/5527)）**：用户希望在模型限流或不可用时自动切换到备用模型，避免任务中断。该能力依赖底层框架升级，可能进入中期规划。
- **Windows 桌面自动化（[#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187)）**：通过 UIA + Tauri Control Mode 实现 Agent 驱动 Windows 桌面，是该方向的重要补充。
- **Windows 原生沙箱（[#5525](https://github.com/agentscope-ai/QwenPaw/pull/5525)）**：为代码执行提供隔离环境，配合上游 feature，推进跨平台沙箱覆盖。
- **Scroll Context Manager（[#5321](https://github.com/agentscope-ai/QwenPaw/pull/5321)）**：基于 SQLite 持久化完整对话历史，通过 REPL 按需召回，替代简单的压缩策略。
- **DataPaw 数据分析插件（[#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)）**：12 个 BI 技能的数据分析插件，丰富工具生态。
- **TUI 项目级代码会话（[#5448](https://github.com/agentscope-ai/QwenPaw/pull/5448)）**：支持 `qwenpaw .` 绑定 Coding Mode 项目目录，提升开发场景体验。

以上 PR 大多处于 Open 或 Under Review 状态，有望在未来 1-2 个版本中逐步合入。

---

### 7. 用户反馈摘要

从 Issue 描述与评论中可提炼出以下真实用户反馈：

- **集成兼容性**：用户对非标准 OpenAI 提供商（OMLX）及国产模型（GLM）的适配存在痛点，建议增强兼容性测试（[#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345)、[#5472](https://github.com/agentscope-ai/QwenPaw/issues/5472)）。
- **Windows 稳定性**：安装即崩溃（[#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379)）、文件预览 404（[#5508](https://github.com/agentscope-ai/QwenPaw/issues/5508)），影响本地部署信心。
- **前端性能**：大会话崩溃（[#5479](https://github.com/agentscope-ai/QwenPaw/issues/5479)）、长消息排版问题（已修复 [#5480](https://github.com/agentscope-ai/QwenPaw/issues/5480)），高频用户对 UI 稳健性要求较高。
- **自动化资源清理**：Chrome 进程残留（[#5520](https://github.com/agentscope-ai/QwenPaw/issues/5520)）导致内存泄漏，表明 Playwright 集成仍需健壮性增强。
- **会话与权限**：希望在 tool 中获得 `sessionId` 用于下游权限管控（[#5547](https://github.com/agentscope-ai/QwenPaw/issues/5547)），反映了实际部署中的企业级需求。
- **命令冲突**：内建 `/new` 与自定义 skill 前缀冲突（[#5529](https://github.com/agentscope-ai/QwenPaw/issues/5529)），用户体验细节待打磨。

总体而言，用户对功能广度认可，但对 Windows 与复杂场景下的稳定性期待更高。

---

### 8. 待处理积压

- **[#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162)（对话死循环）**：创建于 2026-06-12，已开放 2 周，未分配或给出修复时间线。作为致命 Bug 应优先排查。
- **[#5523](https://github.com/agentscope-ai/QwenPaw/issues/5523)（spawn_subagent 在 Runtime 2.0 注册缺失）**：标记出 4 个迁移回归，阻碍依赖子 Agent 的工作流，PR 尚未关联。
- **PR 长期积压**：
  - [#4041](https://github.com/agentscope-ai/QwenPaw/pull/4041)（Tauri 托盘行为，2026-05-05 创建，Under Review）
  - [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)（DataPaw 插件，2026-05-22 创建，Under Review）

以上两项 PR 等待核心维护者审核/同步，建议尽快推进以避免分支冲突加剧。同时，AgentScope 2.0 迁移后遗留的兼容性问题（如 [#5523](https://github.com/agentscope-ai/QwenPaw/issues/5523)）需要集中梳理。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是根据您提供的 ZeroClaw GitHub 项目数据生成的 2026-06-26 项目动态日报。

---

# ZeroClaw 项目动态日报 (2026-06-26)

## 1. 今日速览
过去 24 小时，ZeroClaw 项目保持 **极高活跃度**，项目更新呈井喷状。共处理 43 条 Issues（新开 30 条，关闭 13 条），更新 50 条 PR（待合并 46 条，合并/关闭 4 条）。核心进展集中在 **v0.8.2 版本发布启动**、**严重安全漏洞修复**以及面向未来的 **WASM/安全架构 RFC** 讨论。社区层面，治理工作流与供应链安全议题成为最热讨论焦点。虽然项目在安全和版本发布上迈出了坚实一步，但挂起数月的 **MCP 子进程泄漏 Bug (#5903)** 仍未得到实质性解决，构成运维风险。

## 2. 版本发布
**无。** 尽管 v0.8.2 的发布准备工作已全面启动（见下文“项目进展”），但过去 24 小时内未有正式的版本对外发布。

## 3. 项目进展
项目整体朝 **v0.8.2 里程碑** 大步迈进，同时清理了运行时的关键稳定性缺陷和紧急安全问题。

- **🚀 v0.8.2 发布通道开启：** `singlerider` 合并了里程碑式 PR **[#8234](https://github.com/zeroclaw-labs/zeroclaw/pull/8234)**，将工作区版本号从 v0.8.1 提升至 v0.8.2，并同步生成了更新日志（Changelog）。同时，**[#8332](https://github.com/zeroclaw-labs/zeroclaw/pull/8332)** 完成了 v0.8.2 的多语言文档翻译同步。这意味着 v0.8.2 的正式发布已进入倒计时。
- **🔒 紧急安全修复：** Issue **[#8279](https://github.com/zeroclaw-labs/zeroclaw/issues/8279)**（子代理通过 delegate 工具绕过父级工具白名单，S0 级数据泄露风险）已被标记为已关闭。该严重危害已通过对应的 PR 修复并合并，保障了多智能体协作时的安全边界。
- **⚙️ 运行时稳定性提升：**
    - PR **[#8218](https://github.com/zeroclaw-labs/zeroclaw/pull/8218)** 已合入，修复了 Agent 历史记录修剪逻辑中因整形溢出（Underflow）导致的运行时 Panic。
    - PR **[#8265](https://github.com/zeroclaw-labs/zeroclaw/pull/8265)** 为新增的 Matrix 房间管理工具补充了多国语言翻译，完善了国际化体验。
- **🔧 Bug 修复进行时：** 针对昨日反馈的图片 Token 消耗异常 Bug（[#8327](https://github.com/zeroclaw-labs/zeroclaw/issues/8327)），贡献者 `OmkumarSolanki` 已提交修复性 PR **[#8339](https://github.com/zeroclaw-labs/zeroclaw/pull/8339)**，将 Native Tool Calling 中的图片标记正确解析为结构化数据。

## 4. 社区热点
- **讨论焦点：治理与代码规范（#6808）**：获得 **11条评论** 的 [Issue #6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) 正在就“工作泳道（Work Lanes）、看板自动化和标签清理”进行社区治理 RFC 讨论。这反映了核心贡献者们正在积极优化项目内部的协作与任务路由机制，意图建立更高效的大型开源项目协作范式。
- **安全社区活跃（#8177）**：由 `ConYel` 提出的 **[#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)**（关于硬件 PGP、SLSA 供应链签名）获得了 8 条评论。该项目提议将供应链安全提升到工业级标准，表明用户和贡献者对于金融级安全基线的强烈诉求。
- **架构方向之争（#6165）**：**[#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)**（主张通过外部集成实现轻量化核心）仍在持续发酵。社区围绕“内建功能”与“外部技能”之间的平衡展开了深入辩论，这会直接影响 ZeroClaw 后续的插件和模块化生态。

## 5. Bug 与稳定性
- **已解决的严重威胁：** **Issue #8279**（S0级，已关闭）是最重要的安全修复，解决了 delegation 模式下的权限逃逸问题。
- **高危顽疾亟待解决：**
    - **MCP Stdio 子进程泄漏（Issue [#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903)）**：此 Bug 已存在超过两个月（自4月19日），每次心跳（默认30分钟）都会产生一个孤儿进程。尽管昨日仍有讨论，但尚无明确的修复 PR 提交。这已构成运行时可靠性隐患。
    - **Telegram 图片刷屏（Issue [#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514)）**：尽管相关的 Tracker Issue #7873 已关闭，但主 Bug 仍处于打开状态，Telegram 频道发送多图仍会导致 Agent 反复输出多条重复回复。
- **新报告的 Bug：**
    - **Token 浪费漏洞（Issue [#8327](https://github.com/zeroclaw-labs/zeroclaw/issues/8327)）**：在进行 Native Tool Calling 时，工具返回的图片数据被当做纯文本发送，导致大模型错误地巨额计费 Token。**目前已有修复 PR #8339。**
    - **CLI 命令断裂（Issue [#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334)）**：`skills install` 等 CLI 命令在最新的多 Agent 架构下目标路径错误，导致“拉取并安装技能”的核心工作流彻底失效。
    - **翻译泄漏残留（Issue [#8312](https://github.com/zeroclaw-labs/zeroclaw/issues/8312)）**：修复了数据路径后，旧的翻译映射表未被清理，可能通过其他路径再次引发数据泄漏。

## 6. 功能请求与路线图信号
- **短期纳入可能性极高（下一个 Patch 版本）：**
    - **一键升级（Issue [#8170](https://github.com/zeroclaw-labs/zeroclaw/issues/8170)）**：从 Web 仪表盘直接检测、下载并重启更新。对应的功能 PR [#8173](https://github.com/zeroclaw-labs/zeroclaw/pull/8173) 已处于待合并状态。
    - **目标模式（Issue [#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)）**：RFC 已获接受，旨在引入"目标模式"，让 Agent 能自主执行一个目标直到完成或失败。这是补全 Agent 交互范式的重要拼图。
- **中长期路线图（v0.9.0 或更远）：**
    - **WASM 化转型（Issues [#8132](https://github.com/zeroclaw-labs/zeroclaw/issues/8132), [#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135)）**：社区正在密集讨论将前端 UI 和插件运行时全面转向 Rust/WASM 体系，以彻底摆脱对 Node.js 的依赖并提升安全性和跨平台能力。
    - **硬件接口支持（Issue [#8187](https://github.com/zeroclaw-labs/zeroclaw/issues/8187)）**：提出为 WASM 插件增加 GPIO、I2C 等硬件访问能力，这预示着 ZeroClaw 向边缘计算和硬件自动化领域的扩张野心。
    - **OpenRouter 故障切换（Issue [#8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138)）**：强烈的高可用需求信号，用户 `vinitasher` 请求增加模型 Fallback 配置。

## 7. 用户反馈摘要
- **🙁 核心工作流受挫：**
    - `JordanTheJet` 在 **[#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334)** 中反馈“拉取技能即用”的流程在多 Agent 部署中直接崩溃，暗示了新架构与遗留 CLI 接口之间的适配问题严重。
    - `rordd` 在 **[#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903)** 中详细描述了 MCP 进程泄漏对生产环境的长期侵蚀，显示运维团队对运行时资源管理的关切。
- **🙂 高质量贡献：**
    - `ConYel` 连续提交了关于供应链安全（#8177）和 WASM 运行时（#8135）的深度 RFC，展示了社区中具备深厚安全设计和系统架构能力的贡献者生态。
    - `vrurg` 对于“独立代表权模式”（#8238）和“目标模式”（#8303）的设计思考，体现出用户群体正在探索更复杂的多智能体协作范式。

## 8. 待处理积压
以下主要问题长期未获得有效介入，提醒维护者重点关注：
- **高危性能 Bug - MCP Stdio 泄漏（[Issue #5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903)）**：自 2026-04-19 起打开，严重威胁后台守护进程的长期稳定运行。维护者暂未表态或指派。
- **功能断裂 - CLI 技能管理（[Issue #8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334)）**：虽然提出不久，但直接破坏了核心用户体验，亟待修复。
- **悬而未决的架构决策 - 轻量化核心（[Issue #6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)）**：一个多月过去，维护者对于是否将 Jira、Github 等内置集成外迁至技能系统的决策尚无定论，建议尽快给出维护者（Maintainer）评论以引导后续开发。
- **功能遗产处置 - SkillForge（[Issue #8309](https://github.com/zeroclaw-labs/zeroclaw/issues/8309)）**：半年前合并的自动技能发现引擎至今无法被任何运行时加载。如果团队无意短期激活，建议明确标注“Deprecated”或计划移除，避免增加新贡献者的困惑。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*