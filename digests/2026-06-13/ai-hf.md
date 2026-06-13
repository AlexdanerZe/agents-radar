# Hugging Face 热门模型日报 2026-06-13

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-13 03:25 UTC

---

# Hugging Face 热门模型日报 (2026-06-13)

## 今日速览

本周 Hugging Face 焦点被 **DeepSeek-V4-Pro**（4,796 赞）牢牢锁定，下载超过 338 万，成为社区最火爆的纯语言模型。Google **Gemma-4** 系列持续扩大版图，原版 it/base 模型外，unsloth 等团队贡献了大量 GGUF 量化版本，使得多模态能力的本地部署门槛大幅下降。NVIDIA **LocateAnything-3B**（1,927 赞）在目标定位任务上表现突出，吸引大量关注。生成领域，**Ideogram-4** 推出多精度版本，MisoTTS、Higgs Audio 等新语音模型也密集发布，多模态生成赛道热度空前。整体看，**开源权重主导**、**多模态与纯语言并重**、**量化/微调生态爆发**是本周最明显趋势。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 作者: deepseek-ai | 点赞: 4,796 | 下载: 3,384,418  
  💬 DeepSeek 新一代旗舰对话模型，性能超越前代，本周最高赞与最高下载，属于必看模型。

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — 作者: nex-agi | 点赞: 225 | 下载: 2,551  
  💬 基于 Qwen3.5 MoE 的高性能语言模型，Pro 版在推理与对话上表现突出。

- **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)** — 作者: nex-agi | 点赞: 181 | 下载: 2,839  
  💬 同系列轻量版本，保留 MoE 优势，适合资源受限的场景化部署。

- **[XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash)** — 作者: XiaomiMiMo | 点赞: 97 | 下载: 2,607  
  💬 小米推出的 4-bit 量化语言模型，针对 Agent 任务优化，兼顾效率与性能。

---

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 作者: nvidia | 点赞: 1,927 | 下载: 149,206  
  🖼️ NVIDIA 通用目标定位模型，可识别图像中任意物体，在定位任务上领先。

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — 作者: google | 点赞: 970 | 下载: 911,544  
  🧠 Google 原生 any-to-any 多模态模型，支持文本、图像、音频任意组合输入输出，指令微调版本。

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** — 作者: google | 点赞: 526 | 下载: 198,271  
  🧠 Gemma-4 基础版本，多模态能力全面，是社区后续微调与量化的重要基座。

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — 作者: google | 点赞: 625 | 下载: 20,669  
  🖼️ 融合扩散模型与 Gemma 的多模态 MoE 模型，26B 参数仅激活 4B，推理高效。

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — 作者: ideogram-ai | 点赞: 504 | 下载: 4,987  
  🎨 Ideogram 第四代文生图模型，fp8 精度平衡质量与效率，生成效果一流。

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — 作者: ideogram-ai | 点赞: 327 | 下载: 2,910  
  🎨 同系列 4-bit NF4 量化版，显存友好，本地部署首选。

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — 作者: ByteDance | 点赞: 229 | 下载: 373  
  🎬 字节跳动开源的大模型视频生成模型，支持图像/文本输入，配合渲染器产出高质量视频。

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — 作者: zai-org | 点赞: 136 | 下载: 0  
  🎬 基于扩散的角色动画视频生成模型，姿态驱动，刚一发布即获得关注。

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — 作者: MiniMaxAI | 点赞: 276 | 下载: 442  
  🖼️ MiniMax 第三代多模态大模型，支持视觉理解与对话，延续前代高质量。

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — 作者: bosonai | 点赞: 391 | 下载: 29,347  
  🔊 基于 Higgs 多模态框架的 4B TTS 模型，合成语音自然度高，下载快速增长。

- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** — 作者: MisoLabs | 点赞: 195 | 下载: 0  
  🔊 新晋 TTS 模型，采用 PyTorch 实现，旨在提供高质量语音合成，值得关注。

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — 作者: google | 点赞: 185 | 下载: 6,491  
  🎵 Google Magenta 实时音频生成模型第二版，低延迟，适合音乐/音频生成任务。

- **[Comfy-Org/Ideogram-4](https://huggingface.co/Comfy-Org/Ideogram-4)** — 作者: Comfy-Org | 点赞: 142 | 下载: 0  
  🖼️ ComfyUI 集成 Ideogram-4 的节点，方便用户在工作流中直接调用。

- **[RazzzHF/Realism_Engine_Ideogram_4](https://huggingface.co/RazzzHF/Realism_Engine_Ideogram_4)** — 作者: RazzzHF | 点赞: 85 | 下载: 0  
  🖼️ 基于 Ideogram-4 的写实风格微调引擎，进一步提升图像真实感。

---

### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — 作者: moonshotai | 点赞: 358 | 下载: 0  
  📝 月之暗面 Kimi 模型代码专版，专注代码生成与理解，虽未开放下载但关注度很高。

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — 作者: CohereLabs | 点赞: 335 | 下载: 4,054  
  📝 Cohere 推出的代码生成小模型，MoE 架构，适合轻量级代码辅助。

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — 作者: nvidia | 点赞: 394 | 下载: 3,551  
  🎤 NVIDIA 流式语音识别模型，支持低延迟 ASR，专为实时语音交互场景设计。

---

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 作者: HauhauCS | 点赞: 1,727 | 下载: 2,393,894  
  🛠️ 基于 Qwen3.6 MoE 的 uncensored 微调版，GGUF 量化，因“激进风格”和易用性获得大量下载。

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — 作者: unsloth | 点赞: 570 | 下载: 836,531  
  🛠️ unsloth 对 Gemma-4-12B-it 的 GGUF 量化，兼容 llama.cpp，下载量超 83 万。

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** — 作者: unsloth | 点赞: 215 | 下载: 17,666  
  🛠️ DiffusionGemma 26B MoE 的 GGUF 版本，助力多模态模型在 CPU 环境下运行。

- **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** — 作者: unsloth | 点赞: 207 | 下载: 208,889  
  🛠️ 基于量化感知训练的 GGUF 版 Gemma-4-it，精度损失小，下载量超 20 万。

- **[unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)** — 作者: unsloth | 点赞: 148 | 下载: 221,174  
  🛠️ 26B 大版 QAT-GGUF，使大规模 MoE 模型本地部署更可行。

- **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)** — 作者: google | 点赞: 134 | 下载: 175,635  
  🛠️ Google 官方发布的 QAT 4-bit GGUF 量化版本，权威方案，下载量可观。

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** — 作者: OBLITERATUS | 点赞: 256 | 下载: 43,578  
  🛠️ 社区对 Gemma-4-12B 的独特风格微调，偏向 uncensored 文本生成。

- **[huihui-ai/Huihui-gemma-4-12B-it-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-it-abliterated)** — 作者: huihui-ai | 点赞: 148 | 下载: 8,013  
  🛠️ 通过“abliteration”（消除对齐）微调的 Gemma-4-it 版本，用于探索模型边界。

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** — 作者: Jackrong | 点赞: 116 | 下载: 0  
  🛠️ 基于 Qwen3.6 的 27B 代码模型 GGUF 版本，引入 MTP 多阶段提示优化。

---

## 生态信号

- **Gemma-4 系列势能最强**：从官方原版、QAT 量化到 unsloth 的全面 GGUF 覆盖，再到 huihui-ai 与 OBLITERATUS 的深度微调，形成完整的从研究到部署的生态链，Google 的多模态开放策略获得了社区空前响应。
- **DeepSeek-V4-Pro 领跑纯 L**LM：以 4,796 赞、338 万下载的数据证明其影响力，进一步拉平开源与闭源模型的体验差距。社区对高性能、全开源对话模型的需求持续旺盛。
- **量化与微调活动异常活跃**：unsloth 持续扮演量化基础设施角色，多个 GGUF 模型下载量突破十万甚至百万级别；HauhauCS 的 uncensored 版本下载超过 239 万，反映出用户对个性化、少约束模型的强烈偏好。
- **生成模型日趋多元**：Ideogram-4 多精度、Bernini-R 视频生成、MisoTTS 等，都在各自细分场景快速落地，多模态生成正从“能跑”走向“好用”。

## 值得探索

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 本周热度与下载双冠，性能全面跃升，是评估当前开源 LLM 上限的必测模型。

2. **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — 原生 any-to-any 多模态体验，图像、音频、文本混合理解与生成无缝融合，且社区支持丰富，适合作为多模态应用基座。

3. **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — 4-bit NF4 量化版文生图模型，质量损失极小，显存门槛低，是个人创作者高效产出的优选工具。

*以上为 2026-06-13 的热门模型动态。如需进一步分析或深度评测，欢迎持续关注。*

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*