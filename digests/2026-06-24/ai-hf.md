# Hugging Face 热门模型日报 2026-06-24

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-24 02:54 UTC

---

# Hugging Face 热门模型日报 | 2026-06-24

## 今日速览

本周 Hugging Face 社区的热度高度集中在多模态 MoE 大模型上。DeepSeek-V4-Pro 以 5,031 赞强势登顶，证明顶尖开源 MoE 模型的强大号召力。NVIDIA 发布的 LocateAnything-3B 开创了通用语言指令定位的新范式，紧随其后。Google 的 Gemma‑4 系列（包括 any‑to‑any 的 it 版本和扩散融合的 DiffusionGemma）推动多模态走向统一。量化与微调生态持续活跃，围绕 GLM‑5.2 与 Gemma‑4 涌现大量 GGUF 及社区微调版本，大幅降低部署门槛。同时，端侧小模型（TTS、流式 ASR、数学推理）也开始获得关注。

## 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** - 作者: deepseek-ai | 点赞: 5,031 | 下载: 2,245,489  
  *深度求索最新 MoE 模型，综合性能超越前代，开源社区热情最高。*

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** - 作者: zai-org | 点赞: 2,203 | 下载: 40,127  
  *智谱 GLM 系列最新 MoE 对话模型，采用混合注意力机制，本周热度第二。*

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** - 作者: microsoft | 点赞: 323 | 下载: 4,391  
  *微软出品的小参数长上下文模型，通过 SFT 优化记忆与推理速度，适合资源受限场景。*

- **[poolside/Laguna-M.1](https://huggingface.co/poolside/Laguna-M.1)** - 作者: poolside | 点赞: 93 | 下载: 2,787  
  *专注于软件工程领域的基础模型，为代码生成与理解提供新选择。*

### 🎨 多模态与生成（图像、视频、音频、文本到 X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** - 作者: nvidia | 点赞: 2,319 | 下载: 274,025  
  *NVIDIA 推出的通用物体定位与分割模型，只需文本或图像提示即可定位任意目标，极具创新性。*

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** - 作者: HauhauCS | 点赞: 2,161 | 下载: 3,955,016  
  *社区基于 Qwen3.6 MoE 的“解除审查”多模态版本，下载量近 400 万，反映宽松内容控制的市场需求。*

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** - 作者: MiniMaxAI | 点赞: 1,221 | 下载: 131,057  
  *MiniMax 最新多模态 MoE 模型，支持图文联合理解，兼顾性能与效率。*

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** - 作者: google | 点赞: 1,156 | 下载: 1,991,703  
  *Google 发布的统一多模态模型（any‑to‑any），能处理文本、图像、音频混合输入，代表未来趋势。*

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** - 作者: google | 点赞: 1,056 | 下载: 948,996  
  *融合扩散模型与 LLM 的多模态模型，参数量 26B 但仅激活 4B（MoE），生成质量高且高效。*

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** - 作者: moonshotai | 点赞: 976 | 下载: 447,920  
  *月之暗面 Kimi 新版本，专注于代码的 MoE 多模态模型，支持图像与代码混合推理。*

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** - 作者: nvidia | 点赞: 658 | 下载: 41,050  
  *NVIDIA 的超低延迟流式语音识别模型，适合实时语音交互与端侧部署。*

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** - 作者: baidu | 点赞: 494 | 下载: 8,396  
  *百度开源的通用 OCR 模型，能处理复杂文档与自然场景文字识别。*

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** - 作者: empero-ai | 点赞: 222 | 下载: 1,856  
  *基于 Qwen3.5 融合 Claude 风格数据的多模态模型，提供差异化的对话体验。*

- **[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)** - 作者: lordx64 | 点赞: 173 | 下载: 4,547  
  *基于 Qwen3.5 MoE 的社区视觉语言微调版本，兼顾性能与定制性。*

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** - 作者: owensong | 点赞: 179 | 下载: 0  
  *超小型 TTS 模型，适合移动端离线语音合成，具有端侧部署潜力。*

- **[datalab-to/lift](https://huggingface.co/datalab-to/lift)** - 作者: datalab-to | 点赞: 136 | 下载: 3,216  
  *针对 PDF 文档理解的多模态模型，基于 Qwen3.5，专注文档智能。*

- **[Boogu/Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)** - 作者: Boogu | 点赞: 113 | 下载: 592  
  *图像编辑模型，基于扩散架构实现局部修改与重构。*

- **[ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora)** - 作者: ostris | 点赞: 111 | 下载: 3,672  
  *对 ideogram 4 模型进行 LoRA 加速的版本，提升生成速度。*

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** - 作者: krea | 点赞: 90 | 下载: 84  
  *Krea 第二代图像生成模型的 Turbo 加速版。*

- **[Comfy-Org/Boogu-Image](https://huggingface.co/Comfy-Org/Boogu-Image)** - 作者: Comfy-Org | 点赞: 85 | 下载: 0  
  *Boogu 图像模型在 ComfyUI 的工作流集成，方便可视化搭建。*

### 🔧 专用模型（代码、数学、嵌入等）

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** - 作者: WeiboAI | 点赞: 667 | 下载: 41,170  
  *微博 AI 推出的 3B 参数数学推理模型，在数学问题上表现突出，小参数高精度。*

- **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)** - 作者: LiquidAI | 点赞: 115 | 下载: 10,117  
  *LiquidAI 的新一代文本嵌入模型，用于语义表示与检索，效率优秀。*

- **[LiquidAI/LFM2.5-ColBERT-350M](https://huggingface.co/LiquidAI/LFM2.5-ColBERT-350M)** - 作者: LiquidAI | 点赞: 87 | 下载: 2,534  
  *同系列的 ColBERT 版本，采用迟交互机制优化检索准确性。*

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** - 作者: yuxinlu1 | 点赞: 2,245 | 下载: 456,117  
  *基于 Gemma-4-12B 的代码量化版，强烈反映开发者对编码模型本地部署的迫切需求。*

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** - 作者: yuxinlu1 | 点赞: 454 | 下载: 96,459  
  *面向 Agent 场景微调并量化的 Gemma-4 版本，适合终端自主代理。*

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** - 作者: unsloth | 点赞: 306 | 下载: 55,820  
  *Unsloth 提供的 GLM-5.2 量化版，本地部署首选，下载量高。*

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** - 作者: empero-ai | 点赞: 193 | 下载: 27,218  
  *Qwythos 模型的 GGUF 量化版，方便低资源运行。*

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** - 作者: zai-org | 点赞: 149 | 下载: 395,290  
  *GLM-5.2 官方 FP8 量化版，在精度与效率之间取得良好平衡。*

- **[huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)** - 作者: huihui-ai | 点赞: 114 | 下载: 3,320  
  *社区对 Gemma-4 编码模型进行的“去审查”(abliterated)微调，移除安全对齐限制。*

- **[bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)** - 作者: bytkim | 点赞: 112 | 下载: 65,765  
  *针对 Qwen3.6 的多预测微调量化版，优化多轮生成效率。*

## 生态信号

本轮热门模型呈现几个鲜明趋势：**MoE 架构已全面成为主流**——DeepSeek‑V4、GLM‑5.2、Qwen3.6、Gemma‑4、DiffusionGemma、MiniMax‑M3、Kimi‑K2.7 等核心模型均采用混合专家设计，用更少的激活参数实现更大容量。**多模态走向统一**，Google 的 any‑to‑any 模式与 DiffusionGemma 将生成和理解整合到单一框架，有望引领下一阶段。**量化与社区微调生态极度活跃**，几乎每一款热门模型都迅速得到 GGUF 或 FP8 版本，并催生针对编码、Agent、去审查等垂直用途的衍生版，反映出本地化和定制化需求的强劲。值得注意的还有 **国产模型的群体性崛起**（智谱、深度求索、月之暗面、MiniMax、百度、微博），在开放权重领域形成强力矩阵。另一方面，闭源模型并未出现在榜上，说明当前社区注意力仍在开源权重一侧。

## 值得探索

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
   *理由：将自然语言或视觉提示转化为任意目标的定位分割，为机器人、图像编辑、交互式应用打开全新可能，且模型轻量。*

2. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
   *理由：本周最高赞模型，代表目前开源 MoE 的天花板，适合研究前沿能力与对比实验。*

3. **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)**  
   *理由：占地极小（Nano）的 TTS 模型，适合端侧离线语音生成，探索边缘设备的生成式 AI 应用值得关注。*

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*