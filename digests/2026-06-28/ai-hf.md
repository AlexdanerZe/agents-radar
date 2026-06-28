# Hugging Face 热门模型日报 2026-06-28

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-28 03:30 UTC

---

## Hugging Face 热门模型日报 — 2026‑06‑28

### 今日速览
本周 Hugging Face 榜单呈现几个鲜明特征：**GLM‑5.2** 家族（原版 + GGUF + NVFP4）持续霸榜，MoE 架构备受青睐；**NVIDIA** 凭通用定位模型 LocateAnything‑3B 和 NVFP4 量化技术双线出击；多模态模型全面爆发，**MiniMax‑M3**、**Qwen‑AgentWorld**、**Ornith** 系列等均收获大量关注；社区微调异常活跃，基于 **Qwen3.6** 和 **Gemma‑4** 的 uncensored / abliterated 版本下载量达数百万；同时 **DeepSeek‑V4** 新变体 DSpark 首次亮相，生态竞争进一步升温。

---

### 热门模型

#### 🧠 语言模型（LLM、对话、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — 作者：zai-org | 点赞：2,690 | 下载：98,994  
  智谱 AI 最新 MoE 大语言模型，采用 DSA 架构，本周点赞榜首，社区讨论热烈。

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — 作者：deepseek-ai | 点赞：132 | 下载：0  
  DeepSeek V4 专业版，引入 DSpark 推理加速，刚发布便上榜，新版本风向标。

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** — 作者：LiquidAI | 点赞：130 | 下载：9,791  
  仅 230M 参数的高效语言模型，面向边缘部署与低延时场景。

- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** — 作者：Chunjiang-Intelligence | 点赞：113 | 下载：1,328  
  基于 DeepSeek‑v4 的网络安全领域微调版，体现垂直定制趋势。

#### 🎨 多模态与生成（图像、视频、音频、文本到 X）

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — 作者：MiniMaxAI | 点赞：1,253 | 下载：182,714  
  MiniMax 第三代多模态大模型，支持图文联合理解，国产多模态新标杆。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — 作者：empero-ai | 点赞：491 | 下载：30,298  
  基于 Qwen3.5 的多模态模型，使用 Claude 合成数据进行对齐，视觉语言能力突出。

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — 作者：Qwen | 点赞：362 | 下载：18,872  
  Qwen 系列面向具身智能体的世界模型，MoE 稀疏架构支持多模态输入。

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — 作者：krea | 点赞：311 | 下载：17,445  
  Krea 最新文生图 Turbo 版本，在速度与画质上进一步优化。

- **[krea/Krea-2-Raw](https://huggingface.co/krea/Krea-2-Raw)** — 作者：krea | 点赞：215 | 下载：17,748  
  Krea‑2 基础版本，提供高质量文本条件图像生成。

- **[deepreinforce-ai/Ornith-1.0-9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)** — 作者：deepreinforce-ai | 点赞：170 | 下载：1,501  
  Ornith 系列多模态模型入门款，基于 Qwen3.5，兼顾图像理解与语言生成。

- **[deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)** — 作者：deepreinforce-ai | 点赞：165 | 下载：7,571  
  Ornith 中型版本，35B 参数平衡性能与资源消耗。

- **[Comfy-Org/Krea-2](https://huggingface.co/Comfy-Org/Krea-2)** — 作者：Comfy-Org | 点赞：159 | 下载：10  
  ComfyUI 对 Krea‑2 的集成节点，方便工作流调用。

- **[deepreinforce-ai/Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)** — 作者：deepreinforce-ai | 点赞：125 | 下载：463  
  Ornith 系列超大 MoE 变体，397B 参数稀疏激活，多模态能力最强。

#### 🔧 专用模型（代码、数学、OCR、ASR、定位等）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 作者：nvidia | 点赞：2,409 | 下载：570,466  
  NVIDIA 通用物体定位模型，支持自然语言指令下的开放词汇目标检测。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — 作者：baidu | 点赞：1,143 | 下载：212,760  
  百度推出的通用 OCR 模型，覆盖多场景文字识别，实用性强。

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — 作者：WeiboAI | 点赞：742 | 下载：57,521  
  专注数学推理的 3B 模型，基于 Qwen2 架构，在推理榜单表现亮眼。

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — 作者：nvidia | 点赞：719 | 下载：61,857  
  英伟达流式语音识别模型，支持低延迟实时 ASR，适合对话系统。

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — 作者：microsoft | 点赞：366 | 下载：6,447  
  微软长上下文推理模型，经过 SFT 优化，在超长序列任务中有显著加速。

#### 📦 微调与量化（社区微调、GGUF、NVFP4、QAT 等）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — 作者：yuxinlu1 | 点赞：2,428 | 下载：536,130  
  基于 Gemma‑4 的代码微调版 GGUF 量化，兼顾编码能力与本地部署。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 作者：HauhauCS | 点赞：2,279 | 下载：3,331,475  
  Qwen3.6 的 uncensored 去限制版本，GGUF 格式，社区下载量极高。

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — 作者：yuxinlu1 | 点赞：736 | 下载：206,828  
  Gemma‑4 Agentic 版本，针对智能体任务进行微调并量化。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — 作者：empero-ai | 点赞：680 | 下载：712,627  
  热门多模态模型 Qwythos 的 GGUF 量化版，适合 CPU/边缘设备。

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — 作者：unsloth | 点赞：426 | 下载：125,230  
  使用 Unsloth 工具量化的 GLM‑5.2 GGUF 版，加速本地推理。

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — 作者：nvidia | 点赞：367 | 下载：5,022,254  
  英伟达 NVFP4 4 位浮点量化版 Qwen3.6，下载量突破 500 万，存储效率极佳。

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — 作者：deepreinforce-ai | 点赞：332 | 下载：20,266  
  Ornith 35B 的 GGUF 量化版本，降低显存需求。

- **[deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)** — 作者：deepreinforce-ai | 点赞：223 | 下载：11,034  
  Ornith 9B 的 GGUF 版，轻量级多模态方案。

- **[huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)** — 作者：huihui-ai | 点赞：137 | 下载：6,250  
  Gemma‑4 代码版的 abliterated 微调，移除内容限制，社区常见玩法。

- **[nvidia/GLM-5.2-NVFP4](https://huggingface.co/nvidia/GLM-5.2-NVFP4)** — 作者：nvidia | 点赞：132 | 下载：6,464  
  GLM‑5.2 的 NVFP4 量化版本，探索 FP4 精度在实际任务中的表现。

- **[Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)** — 作者：Jackrong | 点赞：97 | 下载：49,935  
  基于 Qwen3.6 的代码多模态版本，GGUF 格式，含 MTP 优化。

- **[HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)** — 作者：HauhauCS | 点赞：97 | 下载：32,222  
  Gemma‑4 的 QAT 量化 uncensored 版，在平衡性上做了特别调整。

---

### 生态信号

- **家族效应凸显**：Qwen 3.5/3.6 围绕的衍生模型数量最多（Ornith、Qwythos、AgentWorld、HauhauCS 等），GLM‑5.2 与 Gemma‑4 也形成庞大的微调与量化矩阵。
- **多模态成为标配**：榜单中超过一半模型支持图像输入，“纯文本”模型越来越少，视觉语言模型正成为主流。
- **开源权重持续扩大，量化成关键入口**：DeepSeek‑V4、MiniMax‑M3 等新模型均开源权重；同时 GGUF 仍是本地部署首选，NVIDIA 的 NVFP4 新量化格式开始获得关注，下载量惊人（Qwen3.6‑NVFP4 超 500 万）。
- **社区微调方向**：“uncensored”与“abliterated”版本流行，反映用户对审查机制的回调需求；代码与 Agent 微调也是两大热点。

---

### 值得探索

1. **nvidia/LocateAnything‑3B** — 通用开放词汇目标定位任务的新范式，无需微调即可理解自然语言指令，值得研究其视觉‑语言对齐方法。
2. **MiniMax‑M3** — 国产多模态大模型的代表，架构融合密度与 MoE，在多模态榜单上表现优异，可作为研究前沿多模态系统的基线。
3. **HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑Aggressive** — 社区微调的极致案例，展示如何通过数据筛选与量化快速获得高下载量，适合观察安全对齐与能力之间的实际博弈。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*