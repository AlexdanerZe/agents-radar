# Hugging Face 热门模型日报 2026-06-08

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-08 03:40 UTC

---

# Hugging Face 热门模型日报 — 2026‑06‑08

## 今日速览

本周热榜被 **DeepSeek V4** 系列霸屏——Pro 版以 4,700 赞高居榜首，高效版 Flash 也获超 1,400 赞，持续领跑开源 LLM 竞赛。多模态与生成方向百花齐放：NVIDIA 推出 **LocateAnything‑3B** 定位模型与 **Cosmos3** 世界模型全家族，**Sulphur‑2** 文生视频模型跃升第二，**Ideogram‑4** 带来 FP8/NF4 量化精度版，Google **Gemma‑4** 多模态及 **Magenta‑2** 实时音频生成同样受瞩目。社区量化与微调极其活跃：Unsloth 为 Gemma‑4 和 Qwen3.6 提供 GGUF，**HauhauCS** 的 Qwen3.6 去审查版近 300 万下载；垂直领域模型 **HRM‑Text‑1B**、NVIDIA 流式 ASR 及 **PaddleOCR‑VL 1.6** 亦入榜，生态日趋多元。

---

## 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

1. **[DeepSeek‑V4‑Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
   作者: deepseek‑ai | 点赞: 4,700 | 下载: 5,515,325  
   说明: DeepSeek 新一代旗舰对话模型，推理与生成能力达到前沿水平，周赞绝对领先。

2. **[DeepSeek‑V4‑Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**  
   作者: deepseek‑ai | 点赞: 1,435 | 下载: 3,347,429  
   说明: V4 的高效蒸馏版本，速度更快、资源更省，与 Pro 版形成完整生态。

3. **[MiniCPM5‑1B](https://huggingface.co/openbmb/MiniCPM5-1B)**  
   作者: openbmb | 点赞: 779 | 下载: 114,329  
   说明: OpenBMB 推出的小参数语言模型（约 1B），在边缘设备上即可运行，推理高效。

4. **[LFM2.5‑8B‑A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)**  
   作者: LiquidAI | 点赞: 541 | 下载: 118,326  
   说明: Liquid AI 第二代 MoE 模型，8B 参数仅激活 1B，兼顾质量与能效。

5. **[JetBrains/Mellum2‑12B‑A2.5B‑Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)**  
   作者: JetBrains | 点赞: 252 | 下载: 16,924  
   说明: 12B 总参/2.5B 激活的 MoE 模型，强化思维链能力，对代码与逻辑推理友好。

6. **[NVIDIA‑Nemotron‑3‑Ultra‑550B‑A55B‑BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)**  
   作者: nvidia | 点赞: 157 | 下载: 49,784  
   说明: NVIDIA 超大 MoE 语言模型，550B 参数 / 55B 激活，面向企业级文本生成场景。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

7. **[Sulphur‑2‑base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
   作者: SulphurAI | 点赞: 1,587 | 下载: 1,715,710  
   说明: 基于 LTX‑2.3 的文生视频模型，生成质量出色，本周下载量超 170 万。

8. **[nvidia/LocateAnything‑3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
   作者: nvidia | 点赞: 1,534 | 下载: 115,556  
   说明: 多模态通用定位模型，可根据文本或图像在任意图片中定位目标，功能极具创新性。

9. **[google/gemma‑4‑12B‑it](https://huggingface.co/google/gemma-4-12B-it)**  
   作者: google | 点赞: 696 | 下载: 434,969  
   说明: Gemma‑4 多模态系列的指令微调版，支持任意模态输入输出，交互灵活。

10. **[google/gemma‑4‑12B](https://huggingface.co/google/gemma-4-12B)**  
    作者: google | 点赞: 415 | 下载: 99,655  
    说明: Gemma‑4 多模态基座模型，提供强大的多模态表示能力。

11. **[ideogram‑4‑fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**  
    作者: ideogram‑ai | 点赞: 355 | 下载: 4,377  
    说明: Ideogram 第四代图像生成模型，FP8 量化版，在保持质量同时减小体积。

12. **[Step‑3.7‑Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)**  
    作者: stepfun‑ai | 点赞: 349 | 下载: 43,196  
    说明: 轻量级视觉语言模型，擅长图像理解与多模态对话，适合快速推理。

13. **[ideogram‑4‑nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)**  
    作者: ideogram‑ai | 点赞: 238 | 下载: 3,844  
    说明: Ideogram‑4 的 NF4 4‑bit 量化版，进一步压缩模型，利于本地部署。

14. **[Cosmos3‑Nano](https://huggingface.co/nvidia/Cosmos3-Nano)**  
    作者: nvidia | 点赞: 197 | 下载: 29,697  
    说明: NVIDIA 世界模型系列的最轻量版本，聚焦高效视觉生成与理解。

15. **[higgs‑audio‑v3‑tts‑4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
    作者: bosonai | 点赞: 198 | 下载: 7,557  
    说明: 基于 Qwen3 多模态架构的高质量 TTS 模型，语音自然。

16. **[Bernini‑R](https://huggingface.co/ByteDance/Bernini-R)**  
    作者: ByteDance | 点赞: 169 | 下载: 246  
    说明: 字节跳动提出的图像到视频生成模型，采用贝叶斯渲染技术（arXiv:2605.22344）。

17. **[Cosmos3‑Super](https://huggingface.co/nvidia/Cosmos3-Super)**  
    作者: nvidia | 点赞: 153 | 下载: 24,002  
    说明: Cosmos3 世界模型的中型版，在质量与速度之间取得平衡。

18. **[MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)**  
    作者: MisoLabs | 点赞: 144 | 下载: 0  
    说明: 全新发布的 TTS 模型，虽然尚无可下载量但获社区快速收藏，期待成品。

19. **[google/magenta‑realtime‑2](https://huggingface.co/google/magenta-realtime-2)**  
    作者: google | 点赞: 133 | 下载: 13,338  
    说明: Magenta 第二代实时音频生成模型，支持音乐与音频的交互式创作。

20. **[Cosmos3‑Super‑Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)**  
    作者: nvidia | 点赞: 124 | 下载: 5,075  
    说明: Cosmos3 Super 的文本到图像分支，利用世界模型知识生成图像。

21. **[Cosmos3‑Super‑Image2Video](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video)**  
    作者: nvidia | 点赞: 115 | 下载: 4,515  
    说明: Cosmos3 Super 的图像到视频分支，实现静态图到动态视频的转换。

### 🔧 专用模型（代码、数学、医疗、嵌入、OCR、ASR 等）

22. **[HRM‑Text‑1B](https://huggingface.co/sapientinc/HRM-Text-1B)**  
    作者: sapientinc | 点赞: 719 | 下载: 162,822  
    说明: 专注人力资源管理领域的文本生成模型，垂直场景友好，领跑行业模型榜。

23. **[PaddleOCR‑VL‑1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)**  
    作者: PaddlePaddle | 点赞: 269 | 下载: 9,084  
    说明: PaddleOCR 推出的视觉语言模型，强项是文字识别与语义理解（OCR 1.6）。

24. **[nemotron‑3.5‑asr‑streaming‑0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
    作者: nvidia | 点赞: 262 | 下载: 3,439  
    说明: 低延迟流式语音识别模型，0.6B 参数，适合实时 ASR 部署。

### 📦 微调与量化（社区微调、GGUF、NVFP4）

25. **[Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
    作者: HauhauCS | 点赞: 1,522 | 下载: 2,923,564  
    说明: 社区基于 Qwen3.6 微调的“去审查”版本，GGUF 量化 + 激进风格，近 300 万下载。

26. **[unsloth/Qwen3.6‑27B‑MTP‑GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**  
    作者: unsloth | 点赞: 687 | 下载: 1,150,295  
    说明: Qwen3.6 多模态版的 GGUF 量化，极大降低本地部署显存，下载超百万。

27. **[unsloth/gemma‑4‑12b‑it‑GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**  
    作者: unsloth | 点赞: 458 | 下载: 568,158  
    说明: Google Gemma‑4 指令版的 GGUF 量化，使多模态模型更易在消费级硬件上运行。

28. **[nvidia/Qwen3.6‑35B‑A3B‑NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)**  
    作者: nvidia | 点赞: 201 | 下载: 1,185,362  
    说明: NVIDIA 用 NVFP4 技术对 Qwen3.6 MoE 模型进行量化，高压缩高下载。

29. **[NVIDIA‑Nemotron‑3‑Ultra‑550B‑A55B‑NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)**  
    作者: nvidia | 点赞: 133 | 下载: 39,864  
    说明: Nemotron‑3 Ultra 超大模型的 NVFP4 量化版，为企业部署提供高效方案。

30. **[unsloth/gemma‑4‑12B‑it‑qat‑GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)**  
    作者: unsloth | 点赞: 123 | 下载: 85,842  
    说明: 基于量化感知训练（QAT）进一步优化的 Gemma‑4 GGUF 版，质量更优。

---

## 生态信号

**模型家族势头**：DeepSeek V4 称霸纯语言赛道；NVIDIA 在多模态与生成领域密集落子（LocateAnything、Cosmos3、Qwen3.6 NVFP4）；Google Gemma‑4 多模态系列快速起量；Unsloth 则作为“量化基础设施”将热门模型几乎同步带入 GGUF 生态。

**开源权重趋势**：DeepSeek V4、Gemma‑4、Cosmos3 等均开放完整权重，推动开源模型能力向闭源看齐；社区微调与量化版本层出不穷，用户可选择从原版到高度个性化的分支。

**量化与微调活跃度**：GGUF 和 NVFP4 是本周主要量化格式，Unsloth 与 NVIDIA 分别主导第三方与官方量化；“去审查”等个性化微调需求显著，HauhauCS 版 Qwen3.6 成为社区焦点；世界模型（Cosmos3、Sulphur‑2）等生成类模型也开始出现量化版本，显示部署效率诉求正从 LLM 扩散至多模态领域。

---

## 值得探索

1. **[nvidia/LocateAnything‑3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
   理由：开创性的“任意定位”能力，将多模态理解与空间定位结合，应用场景覆盖图像编辑、视觉问答、机器人等，值得深入研究。

2. **[Sulphur‑2‑base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
   理由：文本到视频生成的最新热门模型，基于 LTX‑2.3 优化，社区反馈积极，是探索视频生成技术路线的重要参考。

3. **[unsloth/Qwen3.6‑27B‑MTP‑GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**  
   理由：Qwen3.6 多模态+GGUF 的组合，既保留视觉语言能力又大幅降低硬件需求，适合在本地快速搭建实验环境或进行二次开发。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*