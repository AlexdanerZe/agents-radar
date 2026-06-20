# Hugging Face 热门模型日报 2026-06-20

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-20 03:23 UTC

---

# Hugging Face 热门模型日报（2026-06-20）

## 今日速览

本周 Hugging Face 热度依然由多模态和量化微调主导：**DeepSeek-V4-Pro** 以近 5,000 点赞再证开源 LLM 的统治力，**Nvidia LocateAnything-3B** 与 **Google diffusiongemma** 则在视觉‑语言领域掀起新一轮关注。社区量化活动达到高峰，30 个热门模型中近一半为 GGUF 格式，尤其围绕 **Gemma‑4** 和 **Qwen3.6** 两大系列展开大量微调与 “uncensored” 衍生。与此同时，语音合成（ZONOS2、higgs‑audio）和代码专用模型（Kimi‑K2.7‑Code、North‑Mini‑Code）也展现出强劲的垂直势头。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | 点赞 4,969 | 下载 3,015,772  
   DeepSeek 第四代 Pro 版文本生成模型，以本周最高点赞数登顶，印证开源大模型在通用对话领域的持续领先。

2. **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 点赞 1,546 | 下载 11,871  
   智谱 GLM 系列最新 MoE 对话模型，延续高关注度，成为国产开源 LLM 的代表作之一。

3. **[Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — nex-agi | 点赞 336 | 下载 7,507  
   基于 Qwen3.5‑MoE 的文本生成模型，同时具备图像理解标签，周点赞三百余，社区定制版本活跃。

4. **[FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — microsoft | 点赞 232 | 下载 1,437  
   微软基于 Qwen3 的 SFT 微调模型，专注高效长上下文处理，为 LLM 应用场景提供轻量选择。

5. **[Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)** — lordx64 | 点赞 130 | 下载 1,865  
   基于 Qwen3.5‑MoE 的社区文本生成模型，吸引特定用户群，体现了 Qwen 系列的可塑生态。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **[LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 点赞 2,195 | 下载 228,669  
   NVIDIA 推出的视觉定位模型，可接受图像与文本描述指定目标位置，发布首周即成为多模态明星。

2. **[MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — MiniMaxAI | 点赞 1,135 | 下载 67,836  
   MiniMax 新一代多模态模型，支持图像‑文本交互，在图文理解任务上表现突出。

3. **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — google | 点赞 1,096 | 下载 1,590,882  
   Google Gemma‑4 指令版，统一 any‑to‑any 多模态，下载量超过 150 万，成为社区基准模型。

4. **[diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — google | 点赞 1,011 | 下载 601,208  
   Google 融合扩散过程的 Gemma 变体，26B 激活仅 4B，在多模态对话生成中引发大量讨论。

5. **[Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | 点赞 910 | 下载 274,865  
   月之暗面发布的代码导向多模态模型，结合图像特征提取与压缩技术，下载量高居前列。

6. **[Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)** — prefeitura-rio | 点赞 325 | 下载 190,639  
   基于 Qwen3.5‑MoE 的 397B 超大 MoE 多模态模型，全权重开源，成为大参数开放模型的亮点。

7. **[higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — bosonai | 点赞 493 | 下载 69,143  
   bosonai 的 4B 参数语音合成模型，采用 Higgs 多模态架构，周点赞近 500，TTS 领域热度最高。

8. **[SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — zai-org | 点赞 235 | 下载 0  
   基于扩散模型的图像到视频生成模型，专注于角色动画与姿态驱动，刚发布便吸引专业目光。

9. **[Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** — owensong | 点赞 124 | 下载 0  
   超小型 TTS 模型（ultra‑small），面向边缘端语音合成，尚未有下载，潜力值得跟踪。

10. **[ZONOS2](https://huggingface.co/Zyphra/ZONOS2)** — Zyphra | 点赞 116 | 下载 719  
    Zyphra 的第二代 TTS 模型，Apache‑2.0 许可，为轻量语音合成提供高质量开源选项。

### 🔧 专用模型（代码、数学、医疗、嵌入）

1. **[nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | 点赞 564 | 下载 18,809  
   NVIDIA 的流式语音识别模型，0.6B 超轻量，支持缓存感知 ASR，适合实时语音场景。

2. **[VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — WeiboAI | 点赞 463 | 下载 12,148  
   基于 Qwen2 微调的数学推理专用模型，聚焦数学问题求解，反映出专用小模型的市场需求。

3. **[North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — CohereLabs | 点赞 459 | 下载 17,693  
   Cohere 推出的轻量代码模型，基于 Cohere2 MoE 架构，专为代码生成与补全场景优化。

### 📦 微调与量化（社区微调、GGUF、AWQ）

1. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 点赞 2,010 | 下载 3,730,978  
   Qwen3.6 MoE 视觉模型的无审查版 GGUF，凭借超大下载量成为本周社区微调焦点。

2. **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | 点赞 1,856 | 下载 268,102  
   Gemma‑4‑12B 的代码特化 GGUF 版，兼顾量化与代码推理能力，深受开发者喜爱。

3. **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)** — DavidAU | 点赞 406 | 下载 588,753  
   名字极长的 Qwen3.6 融合微调版 GGUF，主打无审查、代码与思考增强，下载量高达 58 万。

4. **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** — OBLITERATUS | 点赞 355 | 下载 106,885  
   社区移除安全限制的 Gemma‑4‑12B 微调版（uncensored），为内容生成提供更高自由度。

5. **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** — unsloth | 点赞 318 | 下载 202,867  
   Google diffusiongemma 的 unsloth GGUF 量化版，推动多模态模型在 llama.cpp 上高效运行。

6. **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** — Jackrong | 点赞 261 | 下载 148,525  
   Qwen3.6 代码模型的 GGUF 版，支持多任务处理（MTP），量化后仍保持高下载量。

7. **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — unsloth | 点赞 184 | 下载 8,392  
   Unsloth 对 GLM‑5.2 的 GGUF 量化，降低国产 MoE 模型的本地部署门槛。

8. **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)** — unsloth | 点赞 141 | 下载 33,667  
   Kimi‑K2.7‑Code 的 GGUF 量化版，让代码多模态模型更容易在消费级硬件上运行。

9. **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 点赞 107 | 下载 0  
   同作者推出的 Gemma‑4 Agentic 版 GGUF，强化终端代理能力，刚发布暂无下载，值得跟踪。

10. **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** — zai-org | 点赞 105 | 下载 93,927  
    GLM‑5.2 的官方 FP8 量化版本，进一步压缩模型体积，适合高吞吐推理。

11. **[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)** — Mia-AiLab | 点赞 104 | 下载 16,105  
    Qwen3.6‑27B 的 GGUF 社区量化版，体现 Qwen3.6 系列丰富的量化生态。

12. **[bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)** — bytkim | 点赞 86 | 下载 8,138  
    Qwen3.6 的 MTP pi‑tune 量化版，针对多任务处理优化，吸引进阶用户尝试。

## 生态信号

本周生态呈现三大信号：**Gemma‑4** 与 **Qwen3.6** 两大系列衍生最多，从量化（GGUF）到无审查微调几乎占据热门半壁；**DeepSeek‑V4‑Pro**、**MiniMax‑M3**、**Rio‑3.5‑Open** 等大厂开放权重模型继续拉高用户期待，闭源模型在榜单上不显著。量化工具（如 Unsloth）使 GGUF 格式触手可及，推动模型在消费级 GPU 上快速部署。值得注意的还有 **语音合成（TTS/ASR）** 与 **视觉定位（LocateAnything）** 等垂直模型进入热门，表明多模态与专用小模型正成为下一波增长点。

## 值得探索

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 开创了“视觉定位”这一交互范式，用户只需自然语言即可在图像中标记任意目标，是研究与构建多模态 agent 的理想基座。

2. **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — 微软在长上下文高效处理上的最新尝试，4B 参数即可应对长文档任务，适合研究与部署资源敏感的场景。

3. **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)** — 轻量级 Apache‑2.0 TTS 模型，仅需少量资源即可生成高质量语音，是语音合成研究或嵌入式集成的优秀起点。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*