# Hugging Face 热门模型日报 2026-06-06

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-06 02:50 UTC

---

# Hugging Face 热门模型日报 | 2026-06-06

## 今日速览

本周 Hugging Face 最耀眼的明星莫过于 **DeepSeek-V4-Pro/Flash**，以绝对优势占据点赞与下载榜首，标志着国产开源大模型实现又一次跨越。**Google Gemma-4** 系列首次亮相，凭借 “any-to-any” 统一多模态能力迅速登榜。社区微调与量化生态持续火爆，**HauhauCS** 的 Qwen3.6 非审查版下载量突破 268 万。NVIDIA 则在多模态生成（Cosmos3）与超大 MoE（Nemotron-3 Ultra）上全面发力，视频生成和数字人赛道同样迎来多款热门模型。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — LiquidAI 高效稀疏 MoE 语言模型，以 1B 激活参数实现 8B 总参性能，适合资源受限部署。 | 点赞: 526 | 下载: 82,709
- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — JetBrains 推出的思考链语言模型，强调推理能力，总参 12B（激活 2.5B）。 | 点赞: 225 | 下载: 14,709
- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** — 面壁智能轻量级语言模型，仅 1B 参数适合端侧部署，社区热度高。 | 点赞: 771 | 下载: 91,235
- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — 面向特定垂直领域（推测为人力资源）的文本生成模型。 | 点赞: 702 | 下载: 159,014
- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 深度求索最新旗舰语言模型，本周以最高点赞（4,658）和下载（556 万）强势霸榜。 | 点赞: 4,658 | 下载: 5,562,821
- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — DeepSeek-V4 的轻量快速版，兼顾推理速度与质量，广受开发者欢迎。 | 点赞: 1,413 | 下载: 3,473,265
- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** — NVIDIA 超大 MoE 语言模型，总参 550B 激活 55B，BF16 精度，旗舰级性能。 | 点赞: 118 | 下载: 9,125

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — Google Gemma-4 指令微调版，支持 any-to-any（图文混合输入输出），多模态能力亮眼。 | 点赞: 553 | 下载: 142,851
- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** — Gemma-4 基座模型，统一多模态架构，社区积极下载。 | 点赞: 339 | 下载: 53,525
- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — 阶跃星辰视觉语言模型快速版，擅长图像理解与对话。 | 点赞: 332 | 下载: 27,948
- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** — NVIDIA Cosmos3 系列轻量版多模态模型，兼顾生成速度与质量。 | 点赞: 176 | 下载: 21,625
- **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)** — Cosmos3 高性能版本，支持多种多模态生成任务。 | 点赞: 142 | 下载: 19,227
- **[nvidia/Cosmos3-Super-Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)** — Cosmos3 系列专用文生图模型，输出高质量图像。 | 点赞: 116 | 下载: 1,194
- **[nvidia/Cosmos3-Super-Image2Video](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video)** — Cosmos3 系列图生视频模型，扩展动态内容生成。 | 点赞: 106 | 下载: 1,076
- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — 字节跳动提出的图像/文本到视频生成模型，采用渲染器架构。 | 点赞: 142 | 下载: 175
- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** — 美团数字人生成模型，从音频+文本生成逼真视频，关注度高。 | 点赞: 519 | 下载: 1,675
- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — Boson AI 高保真语音合成模型，4B 参数，自然度出色。 | 点赞: 120 | 下载: 408
- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** — 新晋 TTS 模型，虽刚上线下载为零，但迅速获得关注。 | 点赞: 111 | 下载: 0

### 🔧 专用模型（代码、数学、医疗、嵌入等）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — NVIDIA 通用目标定位与特征抽取模型，可用于细粒度图像理解。 | 点赞: 1,379 | 下载: 101,823
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — NVIDIA 流式语音识别模型，0.6B 参数，支持低延迟 ASR。 | 点赞: 197 | 下载: 597
- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** — 百度飞桨 OCR 视觉语言模型，结合 ERNIE4.5 大模型，文字识别与理解一体化。 | 点赞: 245 | 下载: 6,881
- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** — NVIDIA 基于扩散模型的图像超分辨率模型，实现高质量放大。 | 点赞: 310 | 下载: 901

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — unsloth 提供的 Gemma-4 指令版 GGUF 量化，方便个人本地运行。 | 点赞: 379 | 下载: 296,410
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 社区对 Qwen3.6-MoE 的激进微调，去除安全审查，下载量突破 268 万。 | 点赞: 1,452 | 下载: 2,687,304
- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — Ideogram 最新文生图模型的 FP8 量化版本，降低显存需求。 | 点赞: 270 | 下载: 1,246
- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — Ideogram 4 的 NF4 量化版，进一步压缩模型尺寸。 | 点赞: 192 | 下载: 1,594
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — NVIDIA 使用 ModelOpt 对 Qwen3.6-MoE 进行 NVFP4 量化，推理效率更高。 | 点赞: 191 | 下载: 822,125
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — 基于 Lightricks LTX-2.3 优化的文本生视频模型，量化加速，下载超 169 万。 | 点赞: 1,566 | 下载: 1,691,633
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth 对 Qwen3.6-27B 多任务模型（MTP）的 GGUF 量化，适配广泛设备。 | 点赞: 666 | 下载: 1,092,323
- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** — NVIDIA 550B 超级 MoE 模型的 NVFP4 量化版，使超大模型部署更加可行。 | 点赞: 109 | 下载: 7,419

## 生态信号

本周模型生态呈现几个鲜明趋势：**DeepSeek-V4 系列** 与 **Google Gemma-4** 分别代表了开源大模型向极致规模与统一多模态演进；**NVIDIA Nemotron-3 Ultra** 再次确认 MoE 在超大规模上的主导地位。社区侧，**Qwen3.6** 的微调与量化异常活跃（HauhauCS、unsloth、NVIDIA 多个版），表明国内开源模型生态成熟。量化技术（GGUF、NVFP4）广泛覆盖从 1B 到 550B 的模型，加速大模型平民化。同时，**视频生成**与 **数字人** 领域迎来多个突破（Sulphur-2、Bernini-R、LongCat），多模态生成热度持续攀升。

## 值得探索

1. **DeepSeek-V4-Flash** — 在旗舰性能与轻量化间取得优秀平衡，适合商用部署和二次开发，是当前最成熟的国产开源选择之一。
2. **google/gemma-4-12B-it** — “any-to-any” 统一多模态模型，可同时处理文本、图像等，为多模态 Agent 开发提供了统一基础。
3. **SulphurAI/Sulphur-2-base** — 基于开源视频生成模型优化的量化版本，一键生成视频，社区反响极大，是体验 AI 视频生成的绝佳入口。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*