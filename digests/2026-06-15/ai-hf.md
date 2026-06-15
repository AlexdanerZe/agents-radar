# Hugging Face 热门模型日报 2026-06-15

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-15 03:56 UTC

---

# Hugging Face 热门模型日报 — 2026-06-15

## 今日速览

- **DeepSeek-V4-Pro** 以 4.8k 周点赞断崖式领先，成为本周最受关注的开源对话模型，下载量突破 300 万，标志着开源 LLM 的能力再次拉高天花板。
- **Google Gemma-4 系列**生态全面爆发：官方 any-to-any 模型（12B）下载超百万，同时 Unsloth 等社区发布的 GGUF 量化版本以及 OBLITERATUS、yuxinlu1 等魔改微调大量上榜，显示出围绕 Gemma 的二次开发非常活跃。
- **多模态占据绝对主流**：前 30 中超过 2/3 涉及图像、视频、音频处理或跨模态理解；Nvidia 贡献的 **LocateAnything-3B**（2k 赞）成为视觉定位领域的黑马，**Ideogram-4** 系列（fp8/nf4）则推动开源图像生成质量的提升。
- **社区审查对抗加剧**：以 HauhauCS 和 DavidAU 为代表的 “Uncensored” 系列（基于 Qwen3.6）下载量合计近 300 万，表明用户对模型控制权和定制化的强烈需求。
- **量化与压缩工具化**：Unsloth 几乎成为 GGUF 量化的事实标准，DiffusionGemma、Gemma-4、Kimi-K2.7 等模型的 GGUF 版本均快速上线，大幅降低了消费级硬件的部署门槛。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**DeepSeek-V4-Pro**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) | deepseek-ai | 4,836 | 3,075,369 | 本周最大热点，DeepSeek 最新一代对话模型，性能与开放性引发社区轰动。 |
| [**Nex-N2-Pro**](https://huggingface.co/nex-agi/Nex-N2-Pro) | nex-agi | 261 | 3,396 | 基于 Qwen3.5-MoE 的高效文本生成模型，专注推理加速。 |
| [**Nex-N2-mini**](https://huggingface.co/nex-agi/Nex-N2-mini) | nex-agi | 211 | 7,010 | N2 系列轻量版，适合资源受限的本地部署场景。 |
| [**MiMo-V2.5-Pro-FP4-DFlash**](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash) | XiaomiMiMo | 115 | 4,108 | 小米推出的 Agent 模型，采用 FP4 量化与 DFlash 技术优化推理效率。 |
| [**Quasar-Preview**](https://huggingface.co/silx-ai/Quasar-Preview) | silx-ai | 74 | 307 | 新秀模型 Quasar 的预览版，主打超长上下文支持。 |

### 🎨 多模态与生成（图像、视频、音频、文本到 X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**Gemma-4-12B-it**](https://huggingface.co/google/gemma-4-12B-it) | google | 1,010 | 1,084,405 | Google 最新旗舰多模态模型，支持 any-to-any 输入输出，指令版下载量极高。 |
| [**DiffusionGemma-26B-A4B-it**](https://huggingface.co/google/diffusiongemma-26B-A4B-it) | google | 802 | 198,912 | 融合扩散与语言架构的 26B 多模态模型，在图文理解与生成上展现新范式。 |
| [**Gemma-4-12B**](https://huggingface.co/google/gemma-4-12B) | google | 545 | 213,502 | Gemma-4 基座版本，未指令微调，适合研究者进一步微调。 |
| [**Ideogram-4-fp8**](https://huggingface.co/ideogram-ai/ideogram-4-fp8) | ideogram-ai | 535 | 8,263 | Ideogram 最新图像生成模型，FP8 量化版，画质与速度兼顾。 |
| [**MiniMax-M3**](https://huggingface.co/MiniMaxAI/MiniMax-M3) | MiniMaxAI | 508 | 6,643 | MiniMax 第三代多模态模型，图文理解能力强，支持对话。 |
| [**Higgs-Audio-v3-TTS-4B**](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b) | bosonai | 428 | 35,122 | 基于 Higgs 多模态框架的 4B 参数 TTS 模型，语音合成自然度高。 |
| [**Ideogram-4-nf4**](https://huggingface.co/ideogram-ai/ideogram-4-nf4) | ideogram-ai | 337 | 3,763 | Ideogram-4 的 NF4 4-bit 量化版，进一步降低显存占用。 |
| [**Rio-3.5-Open-397B**](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B) | prefeitura-rio | 278 | 112,371 | 里约项目开源的 397B MoE 多模态模型，参数规模惊人。 |
| [**SCAIL-2**](https://huggingface.co/zai-org/SCAIL-2) | zai-org | 176 | 0 | 人体姿态驱动的角色动画视频生成模型，专注图像到视频。 |
| [**Comfy-Org/Ideogram-4**](https://huggingface.co/Comfy-Org/Ideogram-4) | Comfy-Org | 150 | 0 | Ideogram-4 的 ComfyUI 官方节点，方便工作流集成。 |
| [**Realism_Engine_Ideogram_4**](https://huggingface.co/RazzzHF/Realism_Engine_Ideogram_4) | RazzzHF | 95 | 0 | 社区为 Ideogram-4 打造的写实风格增强模型（LoRA 或微调）。 |

### 🔧 专用模型（代码、定位、语音识别、嵌入等）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**LocateAnything-3B**](https://huggingface.co/nvidia/LocateAnything-3B) | nvidia | 2,007 | 75,201 | Nvidia 推出的通用视觉定位模型，支持指代理解与分割，成为工具类黑马。 |
| [**Kimi-K2.7-Code**](https://huggingface.co/moonshotai/Kimi-K2.7-Code) | moonshotai | 645 | 15,145 | Kimi 最新代码多模态模型，采用压缩张量技术，代码理解能力突出。 |
| [**Nemotron-3.5-ASR-Streaming-0.6B**](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b) | nvidia | 412 | 4,505 | 支持缓存感知的流式 ASR 模型，0.6B 参数低延迟语音识别。 |
| [**North-Mini-Code-1.0**](https://huggingface.co/CohereLabs/North-Mini-Code-1.0) | CohereLabs | 370 | 9,932 | Cohere 轻量代码 MoE 模型，针对编程任务优化。 |

### 📦 微调与量化（社区微调、GGUF、AWQ 等）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 1,809 | 2,516,709 | 基于 Qwen3.6 的无审查激进微调版，下载量惊人，引发安全讨论。 |
| [**Gemma-4-12b-it-GGUF**](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF) | unsloth | 599 | 926,372 | Gemma-4-12B-it 的 GGUF 量化版，最便捷的本地部署入口之一。 |
| [**Qwen3.6-40B-Claude-4.6-Opus-...-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF) | DavidAU | 339 | 375,966 | 命名极长的 Qwen3.6-40B 魔改量化合集，融合多种风格，社区话题性强。 |
| [**Gemma-4-12B-OBLITERATED**](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED) | OBLITERATUS | 305 | 60,949 | 社区对 Gemma-4-12B 的“消融”微调版，意图去除限制。 |
| [**Qwopus3.6-27B-v2-MTP-GGUF**](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF) | Jackrong | 304 | 175,472 | Qwen3.6 改进版多模态量化模型，v2 完善图文能力。 |
| [**DiffusionGemma-26B-A4B-it-GGUF**](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF) | unsloth | 262 | 80,118 | DiffusionGemma 的 GGUF 版，将扩散+语言模型带入消费级硬件。 |
| [**Gemma-4-12B-it-qat-GGUF**](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF) | unsloth | 234 | 255,424 | 采用量化感知训练（QAT）的 Gemma-4 GGUF，质量更高。 |
| [**Gemma-4-12B-coder-fable5-composer2.5-v1-GGUF**](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF) | yuxinlu1 | 192 | 6,219 | 针对代码任务微调并量化的 Gemma-4 模型，集成多种编程能力。 |
| [**Qwopus3.6-27B-Coder-MTP-GGUF**](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF) | Jackrong | 185 | 33,720 | 面向代码生成的多模态量化模型（MTP），支持图文编程。 |
| [**Kimi-K2.7-Code-GGUF**](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF) | unsloth | 73 | 25 | 最新发布的 Kimi 代码模型量化版，目前下载量尚在初期。 |

---

## 生态信号

- **Gemma-4 与 Qwen3.6 两大阵营胶着**：Google Gemma-4 系列带来真正的 any-to-any 能力，官方模型与大量社区衍生版本形成丰富生态；Qwen3.6 则成为微调爱好者的首选基座，Uncensored 变体下载量甚至超越原版，反映出用户对模型定制与内容控制的强烈两极需求。
- **开源权重持续领先，但量化成为必选项**：本周几乎全部高赞模型都提供了开放权重，闭源模型（如 Ideogram-4 仍有 API）仅在图像生成领域保有少量阵地。然而，超过 1/3 的热门项是 GGUF 量化版，说明在实际应用侧，本地部署与效率优化已成为用户优先考虑的基础设施。
- **微调活动高度活跃**：社区不仅通过 Unsloth 快速跟进模型量化，还涌现出大量融合多个模型风格的“混搭”微调（如 DavidAU），以及针对特定任务（代码、写实风格）的精调，表明大模型正从通用走向个性化。

---

## 值得探索

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 通用视觉定位模型，无需微调即可完成指代理解和分割，对于机器人和图像编辑场景极具研究价值，且点赞/下载比极高，质量受到社区认可。  
2. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 周下载量超 250 万的现象级微调模型，值得深入分析其“无审查”训练策略、数据构造方式以及对安全对齐的影响，是研究模型定制化与治理的绝佳样本。  
3. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 本周最高赞模型，代表开源 LLM 的最新水平，与其前代相比在推理和多语言上的提升值得 Benchmark 复现，也是对比闭源模型实力的一面镜子。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*