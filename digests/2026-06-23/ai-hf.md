# Hugging Face 热门模型日报 2026-06-23

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-23 02:54 UTC

---

# Hugging Face 热门模型日报（2026-06-23）

## 今日速览
本周 Hugging Face 热门榜多重重磅模型同时发力。DeepSeek V4 Pro 以 5,013 点赞登顶第一，继续引领开源 LLM 竞争；智谱 AI 的 GLM‑5.2 发布后迅速带动社区量化版，MoE 架构成为热点；Google Gemma‑4 系列成为本周衍生模型最多的家族，多款 code/agentic GGUF 版本跻身前列。多模态方面，NVIDIA LocateAnything‑3B、MiniMax‑M3 与 Google DiffusionGemma 表现抢眼。整体来看，大规模混合专家模型、社区量化（尤其是 GGUF）以及多模态统一模型是本周的核心关键词。

## 热门模型

### 🧠 语言模型
- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – deepseek-ai | 点赞 5,013 | 下载 2,421,858  
  新一代旗舰 LLM，采用高效 MoE 架构并在多项基准上刷新记录，开放权重吸引大量评测与试用。

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** – zai-org | 点赞 2,044 | 下载 33,589  
  智谱 AI 的最新 MoE 大模型，在中文理解和通用任务上表现出色，成为本周社区讨论焦点。

- **[FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** – microsoft | 点赞 289 | 下载 3,498  
  微软出品的小参数长上下文模型，专为推理加速与子代理场景设计，受到效率研究者的关注。

- **[Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)** – lordx64 | 点赞 162 | 下载 3,733  
  基于 Qwen 架构的社区微调版，融合 MoE 与多模态能力（任务标注为文本生成），吸引大小型模型爱好者。

- **[Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** – empero-ai | 点赞 131 | 下载 842  
  利用 Claude 输出合成数据微调的 9B 模型，采用 Qwen3.5 基础，实验性质强但社区讨论度不低。

- **[Laguna-M.1](https://huggingface.co/poolside/Laguna-M.1)** – poolside | 点赞 91 | 下载 2,707  
  poolside 推出的软件开发基础模型，原生支持 vLLM/SGLang 部署，引起开发者社区关注。

### 🎨 多模态与生成
- **[LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – nvidia | 点赞 2,294 | 下载 247,517  
  NVIDIA 发布的开放词汇目标定位模型，可在图像中自由指定目标进行检测，多模态理解新标杆。

- **[MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** – MiniMaxAI | 点赞 1,209 | 下载 119,967  
  国内 MiniMax 的多模态大模型，同时支持视觉理解与内容生成，获得广泛试用反馈。

- **[DiffusionGemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** – google | 点赞 1,050 | 下载 874,368  
  Google 结合扩散架构的视觉语言模型，在图像对话与理解任务上表现突出，开放权重带动大量部署。

- **[Gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** – google | 点赞 1,139 | 下载 1,912,198  
  Google 的统一多模态模型，支持 any‑to‑any 任务（图像、文本、音频），实用性极强。

- **[Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** – moonshotai | 点赞 964 | 下载 412,778  
  月之暗面的多模态代码模型，可接受图像与文本输入进行编程，结合了视觉与代码理解。

- **[Nemotron-3.5-ASR-Streaming-0.6B](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** – nvidia | 点赞 631 | 下载 34,860  
  NVIDIA 的轻量流式语音识别模型，专为实时场景优化，低延迟是其主要亮点。

- **[Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** – baidu | 点赞 192 | 下载 47  
  百度推出的通用 OCR 模型，号称可识别任意场景下文字，尽管刚发布，已引起行业兴趣。

- **[Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** – owensong | 点赞 167 | 下载 0  
  超小型文本到语音模型，适用于边缘设备，模型体积极小但点赞数暗示社区期待。

- **[Lift](https://huggingface.co/datalab-to/lift)** – datalab-to | 点赞 125 | 下载 1,821  
  基于 Qwen3.5 的轻量 PDF/文档理解模型，擅长处理长文本与排版融合场景。

- **[Ideogram_4_Turbotime_LoRA](https://huggingface.co/ostris/ideogram_4_turbotime_lora)** – ostris | 点赞 102 | 下载 3,244  
  为 Ideogram 4 设计的 LoRA 适配器，社区可快速自定义图像生成风格。

- **[Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)** – Boogu | 点赞 101 | 下载 473  
  基于 Diffusers 的图像编辑模型，强调修改自然度，吸引初探图像生成的用户。

### 🔧 专用模型
- **[VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** – WeiboAI | 点赞 615 | 下载 32,385  
  专注于数学推理的 3B 小模型，基于 Qwen2 架构，以少参数实现强推理性能，受到科研社区欢迎。

- **[North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** – CohereLabs | 点赞 481 | 下载 21,078  
  Cohere 的轻量代码生成 MoE 模型，在保持生成质量的同时降低了计算门槛。

- **[LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)** – LiquidAI | 点赞 101 | 下载 8,822  
  Liquid 的最新一代嵌入模型，用于文本检索与 RAG，表示能力出色。

- **[LFM2.5-ColBERT-350M](https://huggingface.co/LiquidAI/LFM2.5-ColBERT-350M)** – LiquidAI | 点赞 79 | 下载 2,202  
  基于 ColBERT 策略的检索模型，在语义搜索中兼顾效率与精度。

### 📦 微调与量化
- **[gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** – yuxinlu1 | 点赞 2,175 | 下载 414,734  
  Gemma‑4 的代码专项 GGUF 量化版，性能‑大小平衡佳，成为开发者的首选量化方案。

- **[Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – HauhauCS | 点赞 2,118 | 下载 4,078,305  
  基于 Qwen3.6 的未经审查版量化模型，下载量超过 400 万，反映社区对宽松内容策略的强烈需求。

- **[gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** – yuxinlu1 | 点赞 388 | 下载 50,314  
  专为智能代理场景量化的 Gemma‑4 版本，适用于终端自动交互与工具调用。

- **[Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** – Jackrong | 点赞 282 | 下载 214,630  
  Qwen3.6 的代码量化版，集成多令牌预测（MTP）以加速解码，下载量领先。

- **[GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** – unsloth | 点赞 257 | 下载 41,846  
  unsloth 社区将 GLM‑5.2 转换为 GGUF 格式，极大降低了本地运行门槛。

- **[Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** – empero-ai | 点赞 140 | 下载 6,633  
  Qwythos 的 GGUF 量化版，方便用户在显存受限设备上运行合成微调模型。

- **[GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** – zai-org | 点赞 133 | 下载 334,716  
  官方提供的 FP8 精度版 GLM‑5.2，在保持质量的同时进一步压缩模型大小。

- **[Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)** – Mia-AiLab | 点赞 125 | 下载 23,958  
  Qwen3.6 的社区量化版，多格式支持（Transformers + GGUF），覆盖更多部署环境。

- **[Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)** – bytkim | 点赞 107 | 下载 52,774  
  同样采用 MTP 优化的量化版本，重点提升长序列生成时的吞吐量。

## 生态信号
本周模型生态呈现出三个关键信号：一是 **MoE 家族势头最强** —— DeepSeek V4、GLM‑5.2、Gemma‑4 以及 Qwen3.6 衍生的多个模型均采用混合专家设计，大模型趋向稀疏激活；二是 **开源权重仍是主流**，榜单前五全为开源模型，DeepSeek、GLM 等厂商继续推动开放生态，寡头闭源模型暂时缺席；三是 **量化活动极度活跃**，GGUF 格式占据量化类主力，GLM‑5.2 还获得了 FP8 官方版本，表明社区既追求性能又渴望低门槛运行。此外，针对代码和智能代理的量化版明显增多，说明用户场景正从“能用”向“好用”转移。

## 值得探索
1. **DeepSeek-V4-Pro** – 本周最炙手可热的模型，无论从评分还是讨论度都代表当前开源 LLM 的最高水平，适合作为基础模型进行各项评测与应用开发。  
2. **nvidia/LocateAnything-3B** – 它将定位任务与开放词汇结合，在多模态理解领域提出了新颖的思路，对工业目标检测和视觉问答有直接参考价值。  
3. **HauhauCS/Qwen3.6-35B-A3B-Uncensored** – 下载量超过 400 万的量化版，不仅反映社区对无审查模型的渴望，也证明了大规模量化（A3B）在保持能力下依然具备极高实用性，值得研究者分析其量化策略与效果。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*