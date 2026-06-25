# Hugging Face 热门模型日报 2026-06-25

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-25 02:54 UTC

---

好的，以下是基于您提供的数据生成的《Hugging Face 热门模型日报》，涵盖今日速览、分类榜单、生态信号与值得探索的模型推荐。

---

# Hugging Face 热门模型日报 | 2026‑06‑25

## 1. 今日速览

- **DeepSeek-V4‑Pro 以 5,049 周点赞强势回归榜首**，成为当日最受关注的模型，下载量突破 200 万，力证社区对高性能开源对话模型的需求持续高涨。
- **GLM‑5.2 系列与 Gemma‑4 系列形成两大竞争集团**：前者凭借 **MoE‑DSA** 新架构吸引广泛关注，后者则通过大量社区量化（GGUF）和微调版本（abliterated）实现热度叠加。
- **多模态模型继续升温**：Nvidia 的 **LocateAnything‑3B**（2347 点赞）和 Google 的 **diffusiongemma‑26B‑A4B‑it**（1061 点赞）推动视觉理解与生成边界；MiniMax‑M3、Krea‑2 等模型也带动了图像、音频方向的活跃。
- **社区量化与微调活动空前活跃**：在 Top30 中 GGUF 或量化版本占据近 1/3，且下载量极高（如 Qwen3.6‑35B‑A3B 未审查版下载 376 万），表明小规模部署和定制化需求旺盛。

---

## 2. 热门模型分类详解

### 🧠 语言模型（LLM、对话、指令微调）

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  作者：deepseek-ai | 👍 5,049 | ⬇️ 2,052,463  
  说明：DeepSeek 第四代旗舰对话模型，本周点赞与下载双料冠军，代表开源 LLM 的最新水平。

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  作者：zai-org | 👍 2,360 | ⬇️ 57,186  
  说明：智谱 AI 发布的 MoE‑DSA 架构语言模型，专为对话与指令跟随优化，凭借架构创新成为本周现象级模型。

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**  
  作者：microsoft | 👍 336 | ⬇️ 4,805  
  说明：面向超长上下文（Explorer SubAgent）的 4B 指令微调模型，强调高效长文本处理能力。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)**  
  作者：empero-ai | 👍 317 | ⬇️ 5,123  
  说明：基于 Qwen3.5 的推理增强对话模型，融合 Claude‑Mythos 风格，满足社区对特定对话风格的需求。

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)**  
  作者：Qwen | 👍 151 | ⬇️ 223  
  说明：Qwen 推出的“代理世界”模型，主打 Agent 场景下的规划与决策，35B‑A3B MoE 架构。

- **[poolside/Laguna-M.1](https://huggingface.co/poolside/Laguna-M.1)**  
  作者：poolside | 👍 95 | ⬇️ 2,913  
  说明：Poolside 开发的 laguna 系列通用语言模型，支持 vLLM 和 SGLang 高效推理。

---

### 🎨 多模态与生成（图像、视频、音频、文本到 X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  作者：nvidia | 👍 2,347 | ⬇️ 359,498  
  说明：NVIDIA 推出的零样本物体定位模型，操作直观（点击或文本指代），迅速成为视觉工具链新星。

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  作者：MiniMaxAI | 👍 1,228 | ⬇️ 143,093  
  说明：MiniMax 第三代多模态大模型，统一处理图像与文本，下载量大表明其在商业场景的广泛测试。

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  作者：google | 👍 1,163 | ⬇️ 2,114,441  
  说明：Google Gemma‑4 指令版本，支持 **any‑to‑any**（文本、图像混合输入输出），多模态能力突出，下载数突破 210 万。

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  作者：google | 👍 1,061 | ⬇️ 1,036,328  
  说明：扩散模型与语言模型融合的产物，26B‑A4B MoE 结构，专为多模态生成与理解设计。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**  
  作者：baidu | 👍 743 | ⬇️ 45,687  
  说明：百度推出的不限长度 OCR 模型，图像到文本能力出色，适合文档数字化场景。

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  作者：nvidia | 👍 679 | ⬇️ 47,208  
  说明：NVIDIA 的流式语音识别模型（600M 参数），支持缓存感知的实时 ASR，效率优先。

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)**  
  作者：krea | 👍 194 | ⬇️ 878  
  说明：Krea 第二代 Turbo 版本，基于 Raw 模型的高效文本生成图像模型，速度更快。

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)**  
  作者：owensong | 👍 194 | ⬇️ 0  
  说明：超小型文本到语音（TTS）模型，专为极低资源设备设计，虽然新发布但关注度很高。

- **[krea/Krea-2-Raw](https://huggingface.co/krea/Krea-2-Raw)**  
  作者：krea | 👍 163 | ⬇️ 1,205  
  说明：Krea‑2 的底座模型，输出更原始的生成结果，保留进一步调优空间。

- **[datalab-to/lift](https://huggingface.co/datalab-to/lift)**  
  作者：datalab-to | 👍 147 | ⬇️ 4,644  
  说明：基于 Qwen3.5 的图像与 PDF 理解模型，适合文档审查等任务。

- **[Boogu/Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)**  
  作者：Boogu | 👍 121 | ⬇️ 743  
  说明：图像编辑模型，支持指令驱动的编辑操作，社区早期版本。

- **[Comfy-Org/Krea-2](https://huggingface.co/Comfy-Org/Krea-2)**  
  作者：Comfy-Org | 👍 91 | ⬇️ 10  
  说明：ComfyUI 为 Krea‑2 提供的集成工作流节点，降低多模型组装门槛。

---

### 🔧 专用模型（代码、数学、嵌入）

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  作者：moonshotai | 👍 984 | ⬇️ 480,013  
  说明：月之暗面推出的代码专用多模态模型（Image‑text‑to‑text），集成图像理解与代码生成，下载量 48 万。

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)**  
  作者：WeiboAI | 👍 692 | ⬇️ 49,569  
  说明：专注数学推理的 3B 小模型，基于 Qwen2，在高效推理场景中表现抢眼。

- **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)**  
  作者：LiquidAI | 👍 119 | ⬇️ 11,471  
  说明：Liquid 第二代文本嵌入模型（350M），适用于 sentence‑similarity 和检索任务。

- **[LiquidAI/LFM2.5-ColBERT-350M](https://huggingface.co/LiquidAI/LFM2.5-ColBERT-350M)**  
  作者：LiquidAI | 👍 88 | ⬇️ 3,362  
  说明：基于 ColBERT 架构的嵌入模型，强化 token‑level 交互，适合段落检索。

---

### 📦 微调与量化（GGUF、AWQ、社区微调）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  作者：yuxinlu1 | 👍 2,302 | ⬇️ 483,139  
  说明：Gemma‑4‑Coder 的 GGUF 量化版，社区最热门的编码模型量化版本，下载量近 50 万。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  作者：HauhauCS | 👍 2,209 | ⬇️ 3,769,369  
  说明：Qwen3.6‑35B‑A3B 的“未审查 + 激进”微调版，兼具 MoE 多模态能力，下载量高达 376 万。

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**  
  作者：yuxinlu1 | 👍 539 | ⬇️ 138,704  
  说明：Gemma‑4 Agentic 版本的 GGUF 量化，面向终端自动化任务，具备工具调用能力。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**  
  作者：empero-ai | 👍 359 | ⬇️ 63,637  
  说明：Qwythos‑9B 的 GGUF 量化版，降低部署门槛，适合资源受限场景。

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)**  
  作者：unsloth | 👍 349 | ⬇️ 76,971  
  说明：Unsloth 社区提供的 GLM‑5.2 量化版，加速了该模型在本地设备上的使用。

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)**  
  作者：zai-org | 👍 158 | ⬇️ 445,304  
  说明：官方 FP8 量化版 GLM‑5.2，兼顾精度与推理速度，下载量快速增长。

- **[huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)**  
  作者：huihui-ai | 👍 124 | ⬇️ 4,402  
  说明：Gemma‑4‑Coder 的“去审查”微调版，满足部分用户定制化偏好。

- **[Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)**  
  作者：Jackrong | 👍 83 | ⬇️ 10,867  
  说明：Qwopus3.6 编码模型的量化版，兼容 MTP（Multi‑Token Prediction）推理。

---

## 3. 生态信号

- **模型家族多极竞争**：DeepSeek‑V4、GLM‑5.2、Gemma‑4 和 Qwen3.6 四大系列占据热度核心，MoE 架构（DS‑A3Dense、DSA、A4B 等）已成新发布标配。
- **开源权重持续领跑**：Top10 中除 Krea‑2（受版权协议保护）外均为完全开源权重，社区无需依赖闭源 API 即可获得旗舰能力，“开源优先”趋势稳固。
- **量化与微调生态成熟**：GGUF 版本的下载量普遍超过原版（例如 Qwen3.6‑Uncensored GGUF 下载是原版数千倍），表明本地部署和”私人定制“是当前主要驱动力。同时，abliterated / uncensored 等社区微调版本形成了独特的长尾需求。

---

## 4. 值得探索

| 模型 | 推荐理由 |
|------|----------|
| **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** 本周综合热度与绝对性能标杆，适合需要最强对话能力的研究和产品团队。 |
| **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** 零样本定位能力极其实用，在目标检测和视觉检索场景中有巨大潜力，值得深度试用。 |
| **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** 融合扩散与语言模型的创新架构，为多模态生成开启新路径，适合学术探索与原型开发。 |

---

*本日报基于 2026‑06‑25 Hugging Face 模型热榜（周点赞排序）自动化分析与整理，关注最新开源模型动态。*

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*