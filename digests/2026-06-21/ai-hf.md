# Hugging Face 热门模型日报 2026-06-21

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-21 03:52 UTC

---

好的，以下是根据您提供的 2026年6月21日 Hugging Face 榜单数据生成的热门模型日报。

---

# Hugging Face 热门模型日报 | 2026-06-21

## 今日速览

本周 Hugging Face 生态呈现几大亮点：DeepSeek-V4-Pro 以近 5k 点赞强势登顶，印证了国产开源大模型的领先地位；多模态模型迎来爆发式增长，Google 的 DiffusionGemma 和 Any-to-Any 架构 Gemma-4 引领潮流；MoE 架构成为绝对主流，GLM-5、Qwen3.6 系列及其衍生版占据榜单半壁江山；社区量化与微调活动异常活跃，GGUF 格式模型占到总量约三分之一，大幅降低了部署门槛。此外，代码与数学垂直领域的专用小模型持续获得开发者青睐。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  **作者**：zai-org | **点赞**：1,704 | **下载**：19,683  
  智谱开源的最新 MoE 语言模型，凭借出色的中英文对话能力迅速成为社区焦点。

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**  
  **作者**：microsoft | **点赞**：245 | **下载**：1,998  
  微软为长上下文推理优化的指令微调模型，在 Explorer SubAgent 等场景表现优异。

- **[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)**  
  **作者**：lordx64 | **点赞**：138 | **下载**：2,769  
  基于 Qwen3.5-MoE 的社区微调对话模型，兼顾效率与质量，适合轻量部署。

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  **作者**：deepseek-ai | **点赞**：4,987 | **下载**：2,797,050  
  本周热度冠军，DeepSeek 第四代旗舰语言模型，综合能力跻身第一梯队，开源权重引发巨大关注。

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**  
  **作者**：nex-agi | **点赞**：340 | **下载**：7,724  
  基于 Qwen3.5-MoE 的对话模型，在推理与 MoE 效率之间取得平衡，受到开发者测试。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  **作者**：MiniMaxAI | **点赞**：1,163 | **下载**：85,771  
  MiniMax 最新多模态模型，统一图像与文本处理，社区试用热情高涨。

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  **作者**：moonshotai | **点赞**：932 | **下载**：317,963  
  月之暗面推出的代码多模态模型，支持图文混合编程，填补了视觉编程空白。

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  **作者**：google | **点赞**：1,024 | **下载**：673,464  
  Google 创新的扩散语言模型，结合扩散生成与 Gemma 系列，开辟图像对话与生成新路径。

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  **作者**：nvidia | **点赞**：2,217 | **下载**：235,606  
  NVIDIA 的交互式目标定位模型，自然语言即可在图像中任意定位，人机交互体验极佳。

- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)**  
  **作者**：prefeitura-rio | **点赞**：327 | **下载**：190,694  
  基于 Qwen3.5-MoE 的超大规模开源多模态模型，397B 参数展示了“更大即更强”的路线。

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)**  
  **作者**：owensong | **点赞**：143 | **下载**：0  
  极小参数量的语音合成模型，专为端侧与边缘设备设计，零下载暗示刚刚发布但期待值高。

- **[datalab-to/lift](https://huggingface.co/datalab-to/lift)**  
  **作者**：datalab-to | **点赞**：89 | **下载**：0  
  专注 PDF 文档理解的多模态模型，填补文档级别 AI 分析的空白。

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  **作者**：google | **点赞**：1,107 | **下载**：1,696,240  
  Google 的 Any-to-Any 统一多模态模型，可接受并生成文本/图像等任意格式，概念引领行业。

- **[ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora)**  
  **作者**：ostris | **点赞**：83 | **下载**：1,679  
  基于 Ideogram 4 的文生图 LoRA，加速推理并支持风格微调，为创意工作者提供便利。

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**  
  **作者**：zai-org | **点赞**：241 | **下载**：0  
  智谱开源的角色驱动视频生成模型，实现了可控且连贯的角色动画生成。

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
  **作者**：bosonai | **点赞**：499 | **下载**：72,225  
  基于 Qwen3 架构的 4B 参数 TTS 模型，在语音自然度与表现力上达到新高度。

### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)**  
  **作者**：WeiboAI | **点赞**：515 | **下载**：16,270  
  专注数学推理的 3B 小模型，以极低参数量实现了令人印象深刻的数学能力，小而精的范例。

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  **作者**：nvidia | **点赞**：588 | **下载**：21,426  
  NVIDIA 推出的流式语音识别模型，0.6B 参数实现低延迟 ASR，适合实时交互场景。

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**  
  **作者**：CohereLabs | **点赞**：468 | **下载**：18,783  
  Cohere 专攻代码生成的 MoE 小型模型，在代码任务上表现出色，丰富了企业级代码模型生态。

- **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)**  
  **作者**：LiquidAI | **点赞**：81 | **下载**：6,128  
  Liquid AI 的新一代嵌入式模型，在句子相似度等语义任务上表现领先，巩固了其嵌入模型系列。

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  **作者**：yuxinlu1 | **点赞**：1,993 | **下载**：312,332  
  面向编程的 Gemma-4 量化版，结合 Composer 技术大幅提升代码生成效率。

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**  
  **作者**：yuxinlu1 | **点赞**：190 | **下载**：6,307  
  同一作者的 Agent 强化版量化模型，专为终端与代理工具调用场景优化。

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)**  
  **作者**：unsloth | **点赞**：207 | **下载**：22,586  
  unsloth 为 GLM-5.2 优化的 GGUF 版本，极大降低了该模型的部署与推理门槛。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  **作者**：HauhauCS | **点赞**：2,043 | **下载**：3,812,636  
  无审查版 Qwen3.6-MoE 的量化版，以极夸张的名称和超高下载量（380 万）成为社区现象级微调。

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)**  
  **作者**：zai-org | **点赞**：116 | **下载**：138,174  
  GLM-5.2 的 FP8 量化版本，在保持模型质量的同时实现更高推理效率。

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**  
  **作者**：Jackrong | **点赞**：269 | **下载**：168,502  
  基于 Qwen3.6 的代码多模态模型量化版，支持视觉与编程混合任务，MTP 技术提高效率。

- **[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)**  
  **作者**：Mia-AiLab | **点赞**：112 | **下载**：17,311  
  轻量化的 Qwen3.6 对话模型 GGUF 版，方便快速部署与测试。

- **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)**  
  **作者**：unsloth | **点赞**：147 | **下载**：37,260  
  unsloth 优化的 Kimi 代码模型量化版，为 Kimi 的代码多模态能力提供本地化方案。

- **[bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)**  
  **作者**：bytkim | **点赞**：98 | **下载**：20,465  
  强调多 token 预测（MTP）的 Qwen3.6 精细量化版，展示了社区在量化调优上的深入尝试。

- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)**  
  **作者**：DavidAU | **点赞**：411 | **下载**：587,521  
  功能集大成的无审查量化模型，融合多种风格与优化，凭借极长命名与高下载量成为话题之作。

## 生态信号

本周 Hugging Face 生态呈现三大趋势：**经典家族强势扩展**，Qwen3.6 系列衍生出近 10 个变体，GLM-5.2 与 Gemma-4 也成为社区微调基础；**开源权重全面领先**，前十名中多数为首发开源模型（DeepSeek-V4-Pro、GLM-5.2 等），证明开放策略仍是获得社区关注的核心手段；**量化与追求极致化**，GGUF 模型占到榜单约 30%，大量社区用户通过量化在消费级硬件上运行 30B+ 模型，同时“无审查”“激进微调”等非主流版本也积累了极高下载量，反映出用户对个性化与实用性的强烈需求。

## 值得探索

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – 本周最热且性能霸榜的语言模型，是探究当前开源 LLM 能力上限的必试之选。
2. **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** – 开创性的扩散语言模型架构，适合想要研究下一代多模态生成范式的开发者。
3. **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** – 小体量但数学能力亮眼，是研究专用小模型推理能力与知识压缩的极佳样本。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*