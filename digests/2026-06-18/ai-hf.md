# Hugging Face 热门模型日报 2026-06-18

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-18 03:37 UTC

---

# Hugging Face 热门模型日报 — 2026-06-18

## 今日速览

1. **DeepSeek V4 Pro** 以 4,926 赞登顶本周热门，社区对顶级开源 MoE LLM 的热情依然高涨。  
2. **阿里 Qwen3.6 视觉语言 MoE 家族**持续爆发：官方版下载超 368 万，HauhauCS、DavidAU 等微调 / 量化版同步入榜，成为多模态领域最活跃生态。  
3. **Google Gemma 4** 正式登场，原生 any‑to‑any 多模态模型（12B、26B）与大量 GGUF 量化版同时走红，反映社区对谷歌新一代架构的认可。  
4. **代码与数学专用模型**保持热度（Kimi‑K2.7‑Code、North‑Mini‑Code、VibeThinker‑3B），**NVIDIA** 在语音识别与视觉定位领域也有重要产出。  
5. 量化活动空前活跃，unsloth 发布多款 GGUF 版模型，极大降低了本地部署门槛。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  作者：deepseek-ai | 👍 4,926 | 📥 2,804,646  
  _DeepSeek 第四代旗舰 MoE LLM，综合能力突出，本周最高赞模型。_

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  作者：zai-org | 👍 1,056 | 📥 666  
  _GLM 系列最新 MoE 架构模型，采用 DSA 设计，专注对话交互。_

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**  
  作者：nex-agi | 👍 317 | 📥 5,579  
  _基于 Qwen3.5‑MoE 的 agent 优化模型，强化推理与工具调用。_

- **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)**  
  作者：nex-agi | 👍 238 | 📥 9,804  
  _Nex‑N2 轻量版，MoE 高能效，适合资源受限场景。_

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**  
  作者：microsoft | 👍 186 | 📥 537  
  _微软发布的长上下文指令微调模型，探索高效长文档处理。_

- **[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)**  
  作者：lordx64 | 👍 104 | 📥 319  
  _社区基于 Qwen3.5‑MoE 微调的对话模型。_

---

### 🎨 多模态与生成（图像、视频、音频、文本到 X）

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**  
  作者：Qwen | 👍 2,157 | 📥 3,683,883  
  _阿里通义千问最新视觉语言 MoE，35B 总参仅激活 3B，社区最热多模态模型。_

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  作者：nvidia | 👍 2,141 | 📥 130,389  
  _NVIDIA 推出的通用视觉定位模型，3B 参数即可实现精准目标检测与分割。_

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  作者：google | 👍 1,072 | 📥 922,952  
  _Google Gemma 4 正式版，原生 any‑to‑any 多模态，指令微调，下载量极高。_

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  作者：MiniMaxAI | 👍 1,066 | 📥 42,198  
  _MiniMax 官方多模态模型，支持图文理解，备受关注。_

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  作者：google | 👍 980 | 📥 460,173  
  _Google 的扩散式多模态 MoE 模型（26B，激活 4B），指令版下载近 50 万。_

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**  
  作者：ideogram-ai | 👍 569 | 📥 15,477  
  _文本到图像模型，FP8 量化，输出高质量图像。_

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  作者：nvidia | 👍 523 | 📥 7,195  
  _流式语音识别模型，0.6B 参数，专为低延迟实时场景优化。_

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
  作者：bosonai | 👍 482 | 📥 40,812  
  _基于 Qwen3 的语音合成模型，4B 参数生成自然语音。_

- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)**  
  作者：prefeitura-rio | 👍 319 | 📥 189,986  
  _397B 超大参数 MoE 多模态模型（基于 Qwen3.5），开源业界最大之一。_

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**  
  作者：zai-org | 👍 223 | 📥 0  
  _图像到视频生成模型，基于 Diffusers，专注角色动画与姿态驱动。_

- **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)**  
  作者：Zyphra | 👍 108 | 📥 629  
  _开源 TTS 模型，语音自然度高，Apache‑2.0 许可。_

---

### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  作者：moonshotai | 👍 849 | 📥 172,727  
  _Moonshot 推出的多模态代码助手，支持图像理解与代码生成，下载量大。_

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**  
  作者：CohereLabs | 👍 422 | 📥 13,449  
  _Cohere 的小型代码生成 MoE 模型，轻量高效，适合快速编码辅助。_

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)**  
  作者：WeiboAI | 👍 317 | 📥 1,950  
  _微博 AI 开源的数学推理模型，3B 参数，专注数学问题求解。_

---

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  作者：HauhauCS | 👍 1,940 | 📥 2,876,624  
  _对 Qwen3.6‑35B 的激进微调 + GGUF，无限制对话风格，下载量惊人，社区热度极高。_

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  作者：yuxinlu1 | 👍 1,501 | 📥 146,784  
  _结合多项技术的 Gemma‑4 代码微调版，GGUF 格式便于本地运行，下载超 14 万。_

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**  
  作者：unsloth | 👍 646 | 📥 579,224  
  _Gemma‑4 指令版的 GGUF 量化版，unsloth 出品，社区最常用量化版本之一。_

- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)**  
  作者：DavidAU | 👍 384 | 📥 427,359  
  _融合多模型风格的 Qwen3.6 混合微调 GGUF，强调思考与无限制，下载 42 万。_

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)**  
  作者：OBLITERATUS | 👍 341 | 📥 78,333  
  _对 Gemma‑4‑12B‑it 的社区微调并封装为 GGUF 格式，下载近 8 万。_

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)**  
  作者：unsloth | 👍 299 | 📥 136,634  
  _DiffusionGemma 指令版的 GGUF 量化，方便多模态本地部署。_

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**  
  作者：Jackrong | 👍 238 | 📥 99,909  
  _Qwen3.6 代码模型的 GGUF 量化版，支持多模态代码任务，下载 10 万。_

- **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)**  
  作者：unsloth | 👍 128 | 📥 23,956  
  _Kimi‑K2.7‑Code 的 GGUF 量化版，便于在 llama.cpp 高效运行。_

- **[unsloth/MiniMax-M3-GGUF](https://huggingface.co/unsloth/MiniMax-M3-GGUF)**  
  作者：unsloth | 👍 98 | 📥 20,504  
  _MiniMax‑M3 的 GGUF 量化版，降低多模态模型使用门槛。_

- **[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)**  
  作者：Mia-AiLab | 👍 80 | 📥 646  
  _Qwable 模型的 GGUF 版，基于 Qwen3.6 社区量化。_

---

## 生态信号

- **模型家族势头**：**Qwen3.6/3.5 系列**是本周最庞大的生态（官方、微调、量化版本不下 8 个），**Gemma 4** 刚发布即被社区快速适配，**DeepSeek V4** 以最高赞巩固旗舰地位，**GLM** 和 **Cohere** 的 MoE 新作也表现强劲。
- **开源权重 vs 闭源**：本周几乎所有模型均开放权重（safetensors / GGUF），开源主导决策。大厂（Google、阿里、NVIDIA、Cohere、DeepSeek）全部拥抱开源，未出现明显闭源迹象。
- **量化与微调活动**：GGUF 格式成为本地部署标准，unsloth 持续输出关键量化版本；社区微调集中于**去审查**（Uncensored）和**代码增强**，同时也出现了融合多模型风格的复杂微调（DavidAU），显示工具链的成熟。

---

## 值得探索

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
   本周人气 No.1，MoE 旗舰，综合性能极强。若想体验当前开源 LLM 的天花板，值得优先尝试。

2. **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**  
   最热门的视觉语言 MoE，35B 参数仅激活 3B，效率与能力兼顾，适合多模态应用与二次开发。

3. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
   轻量通用的视觉定位模型，3B 即可完成任意目标定位与分割，实用性极强，值得研究部署。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*