# AI 开源趋势日报 2026-05-29

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-05-29 02:54 UTC

---

### 第一步：AI 相关性筛选
从 **Trending 榜单（16 个仓库）** 中剔除 `DigitalPlatDev/FreeDomain`（免费域名）、`byoungd/English-level-up-tips`（英语学习指南）、`microsoft/markitdown`（文档格式转换，无 AI 属性）、`codecrafters-io/build-your-own-x`（编程实操项目），保留 12 个明确 AI/ML 相关仓库。  
**主题搜索（80 个仓库）** 均带有 AI 标签，全部保留。  
去重后得到 **91 个独立项目**（如 `affaan-m/ECC` 同时出现在两个来源，合并统计）。

---

## 《AI 开源趋势日报》

### 1. 今日速览
- **Agent 技能生态迎来爆发：** Anthropic 官方发布 `skills` 仓库，配合 `ECC`、`Superpowers`、`taste-skill` 等第三方技能框架，推动 Agent 插件化开发范式快速成型，今日 Trending 中该类项目占据近半席位。
- **AI 视频生成持续吸星：** `MoneyPrinterTurbo` 单日新增近 5k stars，仍是内容创作领域最热开源工具。
- **代码知识图谱工具走红：** `Understand-Anything` 上线即获 3.7k+ stars，将任意代码库转化为可交互知识图谱，支持自然语言问答。
- **开源语音模型家族登场：** MOSI.AI 与 OpenMOSS 团队发布 `MOSS-TTS`，覆盖长文、多说话人、实时流式等场景，降低语音 AI 门槛。
- **RAG 存储效率革命：** `LEANN` 提出 97% 存储压缩方案，向量数据库赛道进一步向轻量、私有化演进。

---

### 2. 各维度热门项目

#### 🔧 AI 基础工具（框架、SDK、推理引擎、开发 CLI）
| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [ollama/ollama](https://github.com/ollama/ollama) | 172,542 | 主流本地大模型运行工具，支持 DeepSeek、Qwen 等最新架构 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 81,307 | 高吞吐、低延迟的 LLM 推理引擎，已被广泛用于模型部署 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 137,906 | 最流行的 LLM 应用开发框架，Agent/RAG 核心基建 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,030 | 统一模型定义与训练框架，覆盖文本/视觉/多模态 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 125,812 | 专为 AI Agent 设计的网页爬虫与检索 API |
| [unclecode/crawl4ai](https://github.com/unclecode/crawl4ai) | 0（+154 today） | LLM 友好的开源爬虫，可结构化提取内容供大模型使用 |
| [gradio-app/gradio](https://github.com/gradio-app/gradio) | 42,747 | 快速构建 ML 演示界面的 Python 库 |

#### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体协作）
| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 171,716 | 自成长型智能体框架，强调记忆与持续演进能力 |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | 197,413（+1,385 today） | 统一 Agent 性能优化系统，支持 Claude Code、Codex 等主流 harness |
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 63,341 | 从零实现 mini Claude Code agent harness 的教学项目 |
| [obra/superpowers](https://github.com/obra/superpowers) | 0（+1,730 today） | Agent 技能框架与软件开发方法论，定义领域专属团队 |
| [anthropics/skills](https://github.com/anthropics/skills) | 0（+718 today） | Anthropic 官方 Agent 技能仓库，规范技能文件格式 |
| [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | 0（+2,234 today） | 赋予 AI “品味”，防止生成枯燥套话的技能文件 |
| [Lum1104/Understand-Anything](https://github.com/Lum1104/Understand-Anything) | 0（+3,776 today） | 将代码/文档转化为交互式知识图谱，支持搜索与问答 |
| [langgenius/dify](https://github.com/langgenius/dify) | 143,018 | 企业级可视化 Agentic Workflow 开发平台，内置 RAG 与工具调用 |

#### 📦 AI 应用（具体产品、垂直场景解决方案）
| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | 0（+4,698 today） | 利用 AI 大模型一键生成高清短视频，内容创作者利器 |
| [OpenMOSS/MOSS-TTS](https://github.com/OpenMOSS/MOSS-TTS) | 0（+71 today） | 全场景开源语音生成模型家族，支持长文、对话、音效与实时流式 |
| [twentyhq/twenty](https://github.com/twentyhq/twenty) | 0（+493 today） | 原生 AI 设计的新型 CRM，替代 Salesforce 的开源方案 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 46,508 | AI 生产力工作室，集成 300+ 助手、自主 Agent 与前沿 LLM |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 139,091 | 用户友好的 LLM 交互界面，支持 Ollama 与 OpenAI API |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 22,155 | 从任意文档 AI 生成原生 PPTX，支持动画与图形 |
| [OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) | 68,217 | 面向金融分析师和 AI Agent 的开源数据平台 |

#### 🧠 大模型 / 训练（模型权重、训练框架、微调、评估）
| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 96,200 | 从零实现 ChatGPT 类似 LLM 的 PyTorch 教程，极客必修 |
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | 71,684 | 统一高效微调 100+ LLM/VLM，ACL 2024 官方认可 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,044 | 大规模 LLM 评测平台，支持 100+ 数据集 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 236 | 可靠、可扩展的基础模型预训练库，聚焦世界模型 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,215 | 在 Apple Silicon 上学习 LLM 推理服务的课程型项目 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | 311 | 设备端 LLM 推理库，主打 X-Bit 量化与低功耗 |

#### 🔍 RAG / 知识库（向量数据库、检索增强、记忆、知识管理）
| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 81,462 | 领先的开源 RAG 引擎，融合 Agent 能力实现深度文档理解 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 57,008 | AI Agent 通用记忆层，跨会话持久化上下文 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,516 | 高性能云原生向量数据库，大规模 ANN 搜索标准 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 31,644 | Rust 编写的下一代向量搜索引擎，云服务已上线 |
| [NirDiamant/RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques) | 27,613 | 一站式 RAG 技术教程库，包含多篇 Notebook 实战 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | 78,888 | 高精度 OCR 工具，将 PDF/图片转为结构化数据供 LLM 使用 |
| [yichuan-w/LEANN](https://github.com/yichuan-w/LEANN) | 11,806 | 97% 存储压缩的轻量 RAG 方案，全私有部署 |

---

### 3. 趋势信号分析
**Agent 技能生态化是今日最显著信号。** `anthropics/skills` 首次以官方身份定义技能文件规范，`ECC`、`Superpowers`、`taste-skill` 等第三方技能框架集中登榜，标志 AI Agent 正从“手动编码”走向“插件式组合”，类似早期 VSCode/Obsidian 的插件爆发前夜。同时，**代码理解与知识图谱结合**成为新热点：`Understand-Anything` 一天获得 3.7k+ stars，反映开发者在 AI 生成代码之外，更迫切需求“理解代码”的工具——将仓库自动转为可交互图谱并支持自然语言查询，直击大型项目协作痛点。  
**RAG 赛道进入深水区**：`LEANN` 提出 97% 存储压缩，`PageIndex` 采用“无向量推理”范式，表明社区不再满足于传统向量数据库，开始追求极致的存储效率与隐私性。  
**多模态生成继续分化**：`MoneyPrinterTurbo`（视频）与 `MOSS-TTS`（语音）分别在两个垂直方向保持高热度，预示 AIGC 正从“文本/图像”向“动态内容”全面扩散。  
**事件关联**：MOSS-TTS 由 MOSI.AI 与 OpenMOSS 团队发布，其命名与复旦 MOSS 大模型一脉相承，暗示国内开源多模态模型的第二波浪潮正在酝酿。

---

### 4. 社区关注热点
- **🧩 Agent Skills 生态**：`anthropics/skills` + `ECC` 定义了可复用、可组合的 Agent 技能文件格式，建议关注其规范演进与商业化插件市场雏形。
- **📚 代码知识图谱——Understand-Anything**：首个将“代码→知识图谱→问答”完整打通的开源工具，适合需求文档沉淀、代码审查与团队协作场景。
- **♻️ 极致 RAG：LEANN 与 PageIndex**：两者分别从存储压缩和取消向量化入手，打破对传统向量数据库的依赖，为端侧 RAG 提供新思路。
- **🔊 开源语音全家桶：MOSS-TTS**：从长文到实时流式的一次性覆盖，未来可集成进智能客服、有声读物、虚拟人等应用。
- **🏢 AI 原生商业软件：twenty（CRM）与 JeecgBoot（低代码）**：二十 CRM 在 UI 层面重构客户管理流程，JeecgBoot 则用 AI 加速 Java 开发，表明现成软件正被重新定义。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*