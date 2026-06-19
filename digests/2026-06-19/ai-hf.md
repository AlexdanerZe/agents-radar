# Hugging Face 热门模型日报 2026-06-19

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-19 03:59 UTC

---

# Hugging Face 热门模型日报 · 2026-06-19

## 🔍 今日速览
本周 Hugging Face 生态呈现三大热点：**DeepSeek V4 Pro** 以近 5 千周点赞登顶，成为社区最瞩目的开源旗舰；**Google Gemma 4 系列**（diffusiongemma、gemma-4-12B-it）多模态与统一架构模型全面开花，下载量均超百万；**量化与微调活动**极为活跃，Unsloth 批量产出 GGUF 版本，社区微调（Uncensored 风格、代码增强）模型下载量惊人，反映出开发者对高效部署和个性化需求的强烈关注。此外，NVIDIA 的通用定位模型 *LocateAnything‑3B* 也获得极高互动，模型细分赛道持续丰富。

---

## 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — 作者: zai-org | 点赞: 1,361 | 下载: 4,307  
  智谱最新 MoE 对话模型，兼具性能与效率，首次登榜即受关注。

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — 作者: microsoft | 点赞: 207 | 下载: 957  
  面向 Agent 长上下文任务的小型模型，基于 Qwen3 轻量微调。

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 作者: deepseek-ai | 点赞: 4,957 | 下载: 2,948,726  
  本周最热模型，第四代 MoE 旗舰，综合性能领先，完全开源。

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — 作者: nex-agi | 点赞: 329 | 下载: 6,640  
  基于 Qwen3.5 MoE 优化的 32B 级模型，平衡速度与生成质量。

- **[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)** — 作者: lordx64 | 点赞: 120 | 下载: 836  
  社区打造的 Qwen3.5 MoE 微调实验，探索轻量对话模型边界。

---

## 🎨 多模态与生成（图像、视频、音频、文本到 X）

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — 作者: MiniMaxAI | 点赞: 1,102 | 下载: 56,162  
  MiniMax 新一代多模态大模型，图文理解与对话能力突出。

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — 作者: moonshotai | 点赞: 889 | 下载: 229,156  
  Kimi 2.7 的代码分支，融合视觉与代码理解，专为编程场景设计。

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — 作者: google | 点赞: 1,005 | 下载: 527,080  
  Google 开源的多模态 Diffusion Gemma，稀疏激活（26B 总量，4B 激活）实现高效对话。

- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)** — 作者: prefeitura-rio | 点赞: 324 | 下载: 190,501  
  基于 Qwen3.5 的超大规模开放 MoE 多模态模型，参数达 397B。

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 作者: nvidia | 点赞: 2,166 | 下载: 183,093  
  NVIDIA 通用视觉定位模型，3B 参数即可完成任意目标的文字描述定位。

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — 作者: nvidia | 点赞: 544 | 下载: 13,033  
  超轻量流式语音识别模型，适合实时 ASR 场景。

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — 作者: google | 点赞: 1,085 | 下载: 1,309,625  
  Gemma 4 统一多模态指令模型，支持文本、图像、视频等任意输入。

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — 作者: bosonai | 点赞: 489 | 下载: 57,380  
  4B 参数的高质量文本转语音模型，语音自然流畅。

- **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)** — 作者: Zyphra | 点赞: 115 | 下载: 669  
  Apache‑2.0 许可的开源语音合成模型，适合语音交互研究。

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — 作者: zai-org | 点赞: 228 | 下载: 0  
  图像到视频的角色动画模型，基于扩散模型，支持姿态控制，创新性强。

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** — 作者: owensong | 点赞: 93 | 下载: 0  
  超微型 TTS 模型，面向嵌入式与边缘设备，参数极少仍能合成语音。

---

## 🔧 专用模型（代码、数学、医疗、嵌入）

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — 作者: WeiboAI | 点赞: 410 | 下载: 6,589  
  专攻数学推理的 3B 小模型，轻量级逻辑能力出色。

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — 作者: CohereLabs | 点赞: 450 | 下载: 15,285  
  Cohere 开源迷你代码模型，擅长代码补全与解释，响应极快。

---

## 📦 微调与量化（社区微调、GGUF、AWQ）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — 作者: yuxinlu1 | 点赞: 1,719 | 下载: 211,424  
  基于 Gemma-4-12B 的代码微调，融合多套高质量数据，GGUF 格式便于本地部署。

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** — 作者: Jackrong | 点赞: 251 | 下载: 122,175  
  Qwopus 3.6 的代码多模态微调版，支持多轮预测（MTP），量化后依然高效。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 作者: HauhauCS | 点赞: 1,971 | 下载: 3,420,052  
  Qwen3.6 MoE 的激进无审查微调，下载量超 340 万，社区反响极强。

- **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)** — 作者: unsloth | 点赞: 135 | 下载: 29,287  
  Kimi K2.7‑Code 的 GGUF 转化版，降低模型使用门槛。

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — 作者: unsloth | 点赞: 126 | 下载: 305  
  GLM-5.2 的 GGUF 量化版本。

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** — 作者: unsloth | 点赞: 307 | 下载: 164,209  
  diffusiongemma‑26B‑A4B‑it 的 GGUF 版，让多模态模型更易部署。

- **[unsloth/MiniMax-M3-GGUF](https://huggingface.co/unsloth/MiniMax-M3-GGUF)** — 作者: unsloth | 点赞: 103 | 下载: 22,659  
  MiniMax‑M3 多模态模型的 GGUF 量化版，适配 llama.cpp。

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — 作者: unsloth | 点赞: 653 | 下载: 918,431  
  Gemma‑4‑12B‑it 的 GGUF 版，下载量极高，社区认可度突出。

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** — 作者: zai-org | 点赞: 91 | 下载: 24,967  
  GLM-5.2 的 FP8 量化版，权衡精度与推理效率。

- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)** — 作者: DavidAU | 点赞: 395 | 下载: 529,069  
  多模型融合的激进无审查微调，侧重代码与思维链，命名极具辨识度。

- **[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)** — 作者: Mia-AiLab | 点赞: 95 | 下载: 2,496  
  Qwable 3.6 的社区 GGUF 量化版。

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** — 作者: OBLITERATUS | 点赞: 351 | 下载: 96,805  
  Gemma‑4‑12B 的极端风格微调，含 GGUF 及原始权重，社区热度高。

---

## 🌐 生态信号

- **模型家族势头**：**DeepSeek‑V4、Qwen3.6、Gemma‑4** 成为本周三大核心基座，围绕它们产生了大量量化与微调版本。MoE 架构（DeepSeek‑V4、GLM‑5.2、Qwen3.6）已占据主导地位。  
- **开源权重 vs 闭源**：本周热度榜全部来自开源模型，说明社区依然高度拥抱开放权重；权重 + 量化版齐发，使得个人开发者也能运行前沿模型。  
- **量化活动**：**Unsloth** 几乎同步为每款热门模型推出 GGUF，下载量巨大，表明现场部署需求旺盛；社区微调则呈现 **Uncensored / 风格化** 趋势（如 HauhauCS、DavidAU），反映了部分用户对突破内容限制的强烈偏好。  
- **垂直专用**：代码（*Kimi‑K2.7‑Code、North‑Mini‑Code*）、数学（*VibeThinker‑3B*）、语音（*nemotron、Higgs、ZONOS2*）等细分模型持续涌现，多模态与专业能力并存。

---

## 🧪 值得探索

1. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 当前开源 LLM 的巅峰代表，MoE 设计使其在多项基准上媲美闭源模型，值得深入评测与二次开发。  
2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 全新的通用视觉定位范式，3B 参数即可实现开放世界定位，交互式应用潜力极大，值得研究部署与二次训练。  
3. **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — Google 统一多模态基础模型，支持任意输入模态，为多任务学习与 zero‑shot 迁移提供了新基线，研究与工程均值得跟进。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*