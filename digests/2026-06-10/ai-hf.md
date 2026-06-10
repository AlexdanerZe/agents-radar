# Hugging Face 热门模型日报 2026-06-10

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-10 03:26 UTC

---

好的，以下是 2026 年 6 月 10 日的 Hugging Face 热门模型日报。

---

# 🤗 Hugging Face 热门模型日报 ｜ 2026-06-10

## 📰 今日速览

本周 Hugging Face 生态迎来大爆发：**DeepSeek-V4-Pro** 以绝对优势登顶，成为社区最受瞩目的语言模型；**Google Gemma-4 系列**形成庞大的矩阵式发布，涵盖官方原版、量化版与社区微调版，实现了从多模态基础到边缘部署的全覆盖；**NVIDIA** 则凭借 LocateAnything、Nemotron-3 Ultra 及 Cosmos3 在视觉定位、超大规模 MoE 与视频生成三条赛道上同步发力。此外，**MoE 架构**已成为绝对主流，本周上榜模型中有超过一半采用稀疏激活结构，标志着大模型效率竞赛进入新阶段。

---

## 🏆 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

1. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** · 点赞: 4,741 · 下载: 4,302,553  
   DeepSeek 最新旗舰语言模型，凭借巨大的性能跃升与强劲的下载热度，本周稳居社区热度榜首。

2. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** · 点赞: 1,596 · 下载: 2,983,909  
   Qwen3.6 的 MoE 去审查版，35B 总参数 (3B 激活)，以激进的对话风格吸引大量社区用户测试。

3. **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** · 点赞: 819 · 下载: 581,354  
   Google 统一多模态 MoE 模型，支持任意输入输出（图像、文本、音频），Gemma-4 系列的指令微调版本。

4. **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** · 点赞: 735 · 下载: 133,351  
   针对人力资源管理场景优化的专用 1B 模型，小巧但精准，吸引企业级关注。

5. **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** · 点赞: 573 · 下载: 137,138  
   Liquid AI 推出的 MoE 模型，8B 总参 (1B 激活)，在效率与性能之间取得出色平衡。

6. **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** · 点赞: 481 · 下载: 122,464  
   Gemma-4 系列的基础版本（非指令微调），适合作为下游微调的骨干模型。

7. **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** · 点赞: 175 · 下载: 56,864  
   NVIDIA 的超大规模 MoE 模型，550B 总参 (55B 激活)，BF16 版本面向高端硬件推理。

8. **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** · 点赞: 154 · 下载: 71,818  
   Nemotron-3 Ultra 的 4-bit 浮点量化版，大幅降低显存需求，加速社区部署。

9. **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** · 点赞: 162 · 下载: 783  
基于 Qwen3.5 MoE 架构的专业版，兼具多模态理解能力，面向高阶 agent 场景。

10. **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)** · 点赞: 113 · 下载: 748  
    Nex-N2 系列的小型化版本，主打轻量级多模态会话。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** · 点赞: 359 · 下载: 46,729  
   Step 系列最新视觉语言模型，支持图像理解与文本生成，推理速度快。

2. **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** · 点赞: 215 · 下载: 36,739  
   NVIDIA Cosmos3 系列的小型版，支持全模态理解与生成，被视为视频生成新标杆。

3. **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** · 点赞: 197 · 下载: 281  
   字节跳动推出的图像到视频渲染模型，能够将静态图转化为连贯视频。

4. **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** · 点赞: 285 · 下载: 16,207  
   基于 Qwen3 架构的 4B 级高质量 TTS 模型，合成语音自然度极高。

5. **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** · 点赞: 281 · 下载: 10,139  
   飞桨新一代视觉语言 OCR 模型，基于 ERNIE4.5 骨干，在文本识别与理解上表现突出。

6. **[Comfy-Org/Ideogram-4](https://huggingface.co/Comfy-Org/Ideogram-4)** · 点赞: 114 · 下载: 0  
   ComfyUI 官方适配的 Ideogram-4 工作流，将顶级文生图能力引入节点式编辑生态。

7. **[jdopensource/JoyAI-Echo](https://huggingface.co/jdopensource/JoyAI-Echo)** · 点赞: 115 · 下载: 4,502  
   京东开源的文本到视频模型，支持音频与视频联合生成，适合短视频等应用。

8. **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** · 点赞: 164 · 下载: 18,216  
   Google 最新实时音频生成模型，适用于交互式音乐与音效创作。

9. **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** · 点赞: 175 · 下载: 0  
   新兴 TTS 模型，关注语音合成中的自然韵律与表现力，发布后收获高赞。

### 🔧 专用模型（代码、ASR、定位、嵌入）

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** · 点赞: 1,733 · 下载: 123,922  
   NVIDIA 发布的通用物体定位与分割模型，3B 参数即可实现高精度视觉定位。

2. **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** · 点赞: 170 · 下载: 1,784  
   Cohere 推出的代码专家模型，轻量级 MoE 架构，专为代码生成与理解优化。

3. **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** · 点赞: 322 · 下载: 4,181  
   NVIDIA 的流式语音识别模型，支持低延迟实时转写，适合在线语音应用。

4. **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** · 点赞: 274 · 下载: 17,571  
   JetBrains 推出的推理增强模型，12B 总参 (2.5B 激活)，专注于深度代码推理与逻辑任务。

### 📦 微调与量化（GGUF、NF4、社区微调）

1. **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** · 点赞: 533 · 下载: 660,140  
   Unsloth 社区为 Gemma-4-12B-it 制作的 GGUF 量化版，下载量极高，推动 gemma 大规模本地部署。

2. **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** · 点赞: 442 · 下载: 5,915  
   Ideogram-4 的 FP8 量化版，在保证质量的前提下显著降低显存占用。

3. **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** · 点赞: 288 · 下载: 5,250  
   Ideogram-4 的 NF4 量化版，专注于极致低比特部署。

4. **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)** · 点赞: 116 · 下载: 63,049  
   Google 官方发布的量化感知训练 (QAT) 版 Gemma-4，提供官方认证的低比特部署方案。

5. **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** · 点赞: 172 · 下载: 127,332  
   Unsloth 基于官方 QAT 检查点转换的 GGUF 量化版，进一步优化生产级推理。

6. **[unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)** · 点赞: 115 · 下载: 96,059  
   Gemma-4 更大规模 26B MoE 版本的量化版，满足高端本地推理需求。

7. **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** · 点赞: 148 · 下载: 8,106  
   社区对 Gemma-4 进行的去审查微调版本，同时也提供 GGUF 格式。

---

## 🔍 生态信号

- **模型家族全面化**：DeepSeek-V4 与 Gemma-4 不再只是单个模型，而是形成了“基础版 + 指令版 + 量化版 + 微调版 + 多模态版”的完整产品矩阵，覆盖从云端到边缘的全场景。NVIDIA 的 Nemotron-3 Ultra 与 Cosmos3 同样呈现“超大 + 高效 + 多模态”的家族化趋势。

- **MoE 成为绝对主流**：本周榜单中超过一半的热门模型采用混合专家架构（MoE），如 DeepSeek-V4、Gemma-4、Nemotron-3 Ultra、Liquid LFM 等。社区共识已从“追求单一大模型”转向“稀疏激活的高效模型”。

- **量化生态高度活跃**：Unsloth 与 Google 官方同时提供 GGUF 量化版，达成“发布即量化”的新常态。尤其是官方直接提供 QAT 版量化模型（如 google/gemma-4-12B-it-qat-q4_0-gguf），进一步拉低了高质量模型的使用门槛。

---

## 💡 值得探索

1. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
   本周唯一的“巨型”热度引擎，性能全面提升，值得立即下载测试其在复杂推理与长文本任务中的表现。

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
   轻量级视觉定位模型的标杆，仅 3B 参数即可完成像素级物体定位，是机器人、自动驾驶等领域的高价值基线。

3. **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)**  
   官方 QAT 量化的多模态 MoE 模型，首次验证了“多模态大模型可高效低比特部署”的可能性，对边缘侧落地极具参考意义。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*