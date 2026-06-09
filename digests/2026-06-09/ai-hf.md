# Hugging Face 热门模型日报 2026-06-09

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-09 02:49 UTC

---

好的，以下是针对 2026-06-09 Hugging Face Hub 热门模型生成的专业日报。

---

## **Hugging Face 热门模型日报 | 2026-06-09**

### **今日速览**

本周 Hugging Face 生态被 **DeepSeek V4 系列**与 **Google Gemma 4 系列**双主线主导，两者在开源多模态与 MoE 架构上的竞争进入白热化。视频生成赛道迎来爆发式增长，NVIDIA Cosmos3、字节跳动 Bernini-R 与社区版 Sulphur-2 密集涌现。同时，**模型量化生态空前繁荣**，Unsloth 贡献了多条 Gemma 4 与 Qwen 3.6 的 GGUF 模型，NVFP4 与 QAT 等新型量化技术正在加速落地，全民本地部署顶级模型的时代已来临。

---

### **热门模型**

#### 🧠 **语言模型（LLM / MoE）**

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  作者: deepseek-ai | 点赞: 4,723 | 下载: 5.4M  
  一句话：本周绝对霸主，推理与编码能力封顶的下一代开源 MoE 旗舰。

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**  
  作者: deepseek-ai | 点赞: 1,449 | 下载: 3.3M  
  一句话：V4 的高效蒸馏版，兼顾顶尖性能与极速推理，下载量爆款。

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)**  
  作者: nvidia | 点赞: 167 | 下载: 55k  
  一句话：英伟达开源的超大规模 MoE（55B 激活），探索 Scaling Law 前沿。

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)**  
  作者: LiquidAI | 点赞: 551 | 下载: 135k  
  一句话：极致高效的稀疏 MoE（1B 激活），性价比远超同等规模密集模型。

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)**  
  作者: JetBrains | 点赞: 260 | 下载: 17k  
  一句话：代码大厂出品，专注推理与代码生成的 MoE 模型。

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**  
  作者: nex-agi | 点赞: 125 | 下载: 716  
  一句话：基于 Qwen 3.5 架构优化的 MoE 对话模型。

#### 🎨 **多模态与生成（图像/视频/音频）**

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  作者: nvidia | 点赞: 1,628 | 下载: 121k  
  一句话：通用视觉定位新范式，可根据语言指令框选或分割任意物体。

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  作者: google | 点赞: 754 | 下载: 554k  
  一句话：Google 旗舰多模态指令模型，原生支持图文输入输出。

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
  作者: SulphurAI | 点赞: 1,601 | 下载: 1.7M  
  一句话：社区最热文生视频模型，基于 LTX-2.3 的量化优化版。

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**  
  作者: ideogram-ai | 点赞: 394 | 下载: 5k  
  一句话：顶级文生图模型的 FP8 高效推理版，质量与速度绝佳平衡。

- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)**  
  作者: stepfun-ai | 点赞: 352 | 下载: 45k  
  一句话：阶跃星辰强视觉语言模型，快思考架构。

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)**  
  作者: ByteDance | 点赞: 186 | 下载: 278  
  一句话：字节跳动开源图像转视频模型，视频生成赛道新玩家。

- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)**  
  作者: nvidia | 点赞: 206 | 下载: 34k  
  一句话：世界模型 Cosmos 3 的小型版，主打视频理解与物理模拟。

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
  作者: bosonai | 点赞: 251 | 下载: 15k  
  一句话：多模态大模型驱动的自然 TTS，语音合成效果显著提升。

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)**  
  作者: google | 点赞: 152 | 下载: 17k  
  一句话：谷歌实时音乐生成模型，音乐 AI 迈入交互时代。

- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)**  
  作者: PaddlePaddle | 点赞: 277 | 下载: 9k  
  一句话：OCR 与视觉文档理解的集大成者。

#### 🔧 **专用模型（ASR / 奖励 / TTS）**

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)**  
  作者: sapientinc | 点赞: 728 | 下载: 163k  
  一句话：针对 LLM 对齐优化（Reward Model）的 1B 级专用模型。

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  作者: nvidia | 点赞: 293 | 下载: 3k  
  一句话：低延迟流式实时语音识别模型。

#### 📦 **量化与微调**

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  作者: HauhauCS | 点赞: 1,555 | 下载: 3.0M  
  一句话：Qwen 3.6 社区极致微调版，去审查并强化 Agent 能力。

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**  
  作者: unsloth | 点赞: 504 | 下载: 645k  
  一句话：Gemma 4 指令版最热门的 GGUF 量化版，本地部署神器。

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**  
  作者: unsloth | 点赞: 696 | 下载: 1.2M  
  一句话：Qwen 3.6 多模态模型的 GGUF 版，低资源运行首选。

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)**  
  作者: nvidia | 点赞: 145 | 下载: 66k  
  一句话：NVFP4 超低精度量化的旗舰 MoE，超大模型推理新路径。

- **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)**  
  作者: google | 点赞: 101 | 下载: 52k  
  一句话：Google 官方 QAT 量化版，官方与社区技术的首次结合。

---

### **生态信号**

**模型家族势头正旺：** DeepSeek V4 系列以巨大优势领跑，展现了当前开源 LLM 的天花板。Google Gemma 4 系列则展现出极强的“生态磁吸效应”，带动了大量量化（Unsloth、QAT）和二次微调活动。NVIDIA 通过 **Nemotron**（语言）、**Cosmos**（世界模型）、**LocateAnything**（视觉）三线布局，正成为开源生态最全面的玩家。MoE 架构已完全普及，上榜大模型几乎均为混合专家设计。

**开源 vs 闭源：** 本周榜单几乎是开源权重的天下。头部厂商（DeepSeek、Google、NVIDIA、阶跃星辰）持续开源各自的旗舰模型，闭源模型的“护城河”正被快速侵蚀。

**量化与微调：** 量化技术已进入多元繁荣期。GGUF 与 NVFP4 并行发展，**量化感知训练**成为本周最大技术信号——模型从训练阶段就开始为最终低精度部署做准备。社区微调方面，“去审查”（Uncensored）与 Agent 行为对齐是社区核心需求，Qwen 3.6 社区的活跃度即是明证。

---

### **值得探索**

1.  **deepseek-ai/DeepSeek-V4-Pro**  
    **理由：** 若想了解当前开源大模型的性能上限，或需要私有化部署强推理/编程模型，这是绝对标杆。

2.  **nvidia/LocateAnything-3B**  
    **理由：** 超越了 SAM 的纯分割逻辑，根据指令精准定位物体并分割。对于 RPA、自动驾驶等场景，极大降低了目标检测的应用门槛。

3.  **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4**  
    **理由：** 不仅是 550B 的超大规模参数，其搭载的 **NVFP4** 新型量化格式代表了超大模型在 H100 等硬件上的极致推理未来，值得所有部署工程师关注。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*