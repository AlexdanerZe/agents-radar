# Hugging Face 热门模型日报 2026-06-26

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-26 03:23 UTC

---

# Hugging Face 热门模型日报 (2026-06-26)

## 今日速览
- **DeepSeek-V4 Pro** 以 5,063 周点赞登顶，成为本周最瞩目的开源 MoE 对话模型，标志国产大模型在推理与对话能力上再上台阶。
- **Gemma4** 与 **Qwen3.x** 系列的社区微调/量化活动白热化：abliterated、GGUF、NVFP4 等变体收割百万级下载，用户对本地部署、特定能力（代码/Agent）和“去审查”的需求极其强烈。
- 多模态赛道持续拓宽：**Google Gemma4-12B-it** 官方多模态版本、**MiniMax-M3** 及 **NVIDIA LocateAnything-3B** 分别站稳通用理解、专业定位等细分方向。
- 模型小型化与边缘部署趋势明显：**LiquidAI LFM2.5-230M**、**Inflect-Nano-v1** (TTS) 等极小模型入榜，表明垂直场景与资源受限设备正成为新战场。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）
- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — *deepseek-ai* | 👍 5,063 | ⬇️ 1,878,217  
  深度求索最新旗舰 MoE 对话模型，推理与生成能力全面升级，是本周社区关注度最高的开源模型。
- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — *zai-org* | 👍 2,488 | ⬇️ 67,107  
  智谱AI 第五代 GLM MoE 模型，中英文对话表现优异，是中文开源社区的核心关注点。
- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — *Qwen* | 👍 249 | ⬇️ 3,389  
  阿里千问团队针对智能体（Agent）场景设计的混合专家模型，以极低激活参数实现世界建模。
- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — *microsoft* | 👍 345 | ⬇️ 5,276  
  微软推出的长上下文优化模型，基于 Qwen3 架构，擅长高效处理大规模文本。
- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** — *LiquidAI* | 👍 76 | ⬇️ 7,334  
  仅 230M 参数的语言模型，专为边缘端与低算力场景设计，是轻量化路线的代表。

### 🎨 多模态与生成（图像、视频、音频、文本到X）
- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — *google* | 👍 1,179 | ⬇️ 2,187,644  
  Google 官方指令微调多模态模型，支持任意模态输入输出，是通用多模态的标杆。
- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — *MiniMaxAI* | 👍 1,241 | ⬇️ 154,350  
  MiniMax 新一代多模态模型，图文理解能力强，社区反馈积极。
- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — *krea* | 👍 245 | ⬇️ 2,996  
  对 Krea-2-Raw 蒸馏优化的文生图模型，生成速度快，适合创意生产。
- **[krea/Krea-2-Raw](https://huggingface.co/krea/Krea-2-Raw)** — *krea* | 👍 185 | ⬇️ 5,113  
  Krea-2 的原始权重版，为社区微调和研究提供基础。
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — *nvidia* | 👍 695 | ⬇️ 50,553  
  NVIDIA 流式语音识别模型，低延迟实时转写，面向对话式 AI 部署。
- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** — *owensong* | 👍 201 | ⬇️ 0  
  超轻量语音合成模型（TTS），适合在弱算力设备上运行。
- **[datalab-to/lift](https://huggingface.co/datalab-to/lift)** — *datalab-to* | 👍 152 | ⬇️ 5,189  
  基于 Qwen3.5 的 PDF 文档理解模型，可提取结构化信息。
- **[Boogu/Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)** — *Boogu* | 👍 124 | ⬇️ 824  
  指令驱动的图像编辑扩散模型，Boogu 首秀，支持局部修改。
- **[Comfy-Org/Krea-2](https://huggingface.co/Comfy-Org/Krea-2)** — *Comfy-Org* | 👍 121 | ⬇️ 10  
  ComfyUI 对 Krea-2 的工作流节点，方便在 ComfyUI 中使用图像生成能力。

### 🔧 专用模型（代码、数学、医疗、嵌入）
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — *baidu* | 👍 900 | ⬇️ 70,743  
  百度推出的通用 OCR 模型，支持多语言场景下的文字识别任务。
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia* | 👍 2,365 | ⬇️ 407,838  
  NVIDIA 定位专用模型，可按描述在图像中精准定位目标，驱动多模态交互新思路。
- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — *WeiboAI* | 👍 716 | ⬇️ 51,717  
  基于 Qwen2 的 3B 数学推理模型，以极小尺寸实现接近大模型的推理性能。
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — *moonshotai* | 👍 992 | ⬇️ 502,106  
  月之暗面 Kimi 的代码专用版本，支持图像与文字联合上下文，编程能力突出。
- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** — *Chunjiang-Intelligence* | 👍 94 | ⬇️ 646  
  基于 DeepSeek-v4 的安全模型，专注于网络安全分析与威胁检测。

### 📦 微调与量化（社区微调、GGUF、AWQ）
- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — *yuxinlu1* | 👍 2,367 | ⬇️ 495,813  
  Gemma4 代码微调版的 GGUF 量化，可本地高效运行，下载量极高。
- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — *yuxinlu1* | 👍 622 | ⬇️ 165,187  
  Gemma4 Agent 能力量化的 GGUF 版，适合终端与工具调用场景。
- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — *unsloth* | 👍 387 | ⬇️ 88,915  
  GLM-5.2 官方量化版 (Unsloth)，便于消费级硬件部署。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — *empero-ai* | 👍 495 | ⬇️ 134,294  
  Qwen3.5 混合 Claude 风格微调后的 GGUF 量化版，本地玩家热门选择。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — *empero-ai* | 👍 394 | ⬇️ 10,160  
  同一微调模型的非量化原版，保留完整精度。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* | 👍 2,239 | ⬇️ 3,520,206  
  社区对 Qwen3.6 MoE 视觉模型进行去审查 + GGUF 量化，暴风级下载反映用户对“无限制”模型的强烈需求。
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — *nvidia* | 👍 343 | ⬇️ 4,602,255  
  NVIDIA 使用 NVFP4 格式压缩的 Qwen3.6，效率极高，下载量超 460 万，领跑量化格式。
- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — *deepreinforce-ai* | 👍 100 | ⬇️ 0  
  35B 大模型的 GGUF 量化版，降低大模型在消费级 GPU 上的使用门槛。
- **[huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)** — *huihui-ai* | 👍 127 | ⬇️ 4,874  
  对 Gemma4 coder 进行“消限”(abliterated) 微调，去除了安全抑制层，面向特定研究场景。
- **[HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)** — *HauhauCS* | 👍 83 | ⬇️ 15,128  
  Gemma4 的 QAT 量化 + 去审查版，平衡性能与容量。
- **[Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)** — *Jackrong* | 👍 89 | ⬇️ 19,382  
  基于 Qwen3.6 的 27B 代码模型 GGUF 版，利用 MTP 压缩降低显存占用。

## 生态信号
本周模型生态呈现 **“巨头引领、社区疯狂”** 的局面。**DeepSeek-v4**、**GLM-5.2** 和 **Gemma4** 三大家族占据流量上游，尤其是 Gemma4 的微调变体（代码、Agent、abliterated）数量暴增，反映了社区对“即用型”本地模型的渴求。**Qwen3.x** 系列在 MoE 量化（NVFP4、GGUF）上也已成为社区标杆。**开源权重模式**继续主导——几乎所有热门模型都提供了开放权重，而闭源模型通过开源参数参与竞争。**量化活动**格外活跃：GGUF 仍是主流，但 NVIDIA 的 NVFP4 在特定硬件（Hopper 架构）上展现出高效优势，未来量化标准仍有变数。同时，去审查（Uncensored/Abliterated）微调成为一股不容忽视的力量，用户对模型自由度要求日益强烈。

## 值得探索
1. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 本周最重磅发布，性能与对话体验极佳，适合对比测试当前开源 LLM 的顶线能力。
2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 开创性的定位模型，将多模态理解从“识别”延伸到“指代”，是 Prompt 工程与多模态应用研究的绝佳案例。
3. **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — 直接可用的本地代码助手，GGUF 量化后显存友好，是开发者提升编码效率的实用选择。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*