# Hugging Face 热门模型日报 2026-06-22

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-22 03:54 UTC

---

# Hugging Face 热门模型日报 - 2026-06-22

## 📰 今日速览

- **DeepSeek-V4‑Pro** 以 4,999 周点赞登顶，成为本周最重磅的基础模型发布，彰显开源大模型持续进化。
- **多模态浪潮加速**：Qwen3.6‑35B‑A3B 下载量突破 500 万，Gemma‑4、MiniMax‑M3 等多模态模型占据榜单近半。
- **代码与 Agent 专用化**：Kimi‑K2.7‑Code、Cohere North‑Mini‑Code、Poolside Laguna‑M.1 等密集发布，模型正向垂直任务深度渗透。
- **社区量化如火如荼**：GGUF 量化版本超过 10 款，HauhauCS 的 Qwen3.6 解禁版下载逼近 400 万，“开箱即用”成为刚需。
- **小而专趋势**：VibeThinker‑3B（数学）、LocateAnything‑3B（视觉定位）等小参数专用模型上榜，端侧 AI 潜力初显。

---

## 🧠 语言模型（LLM、对话模型、指令微调）

#### [DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) - deepseek-ai
点赞：4,999 | 下载：2,611,991  
DeepSeek 最新旗舰语言模型，凭借强悍性能本周收获近 5,000 点赞，社区关注度极高。

#### [zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) - zai-org
点赞：1,848 | 下载：27,413  
智谱 GLM 系列最新 MoE 模型，引入 DSA 稀疏注意力机制，中文社区反响热烈。

#### [nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro) - nex-agi
点赞：343 | 下载：7,872  
基于 Qwen3.5-MoE 微调的语言模型，专为推理与文本生成场景优化。

#### [lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1) - lordx64
点赞：145 | 下载：3,351  
社区微调的 Qwen3.5-MoE 变体，融合多模态理解能力，兼顾图文任务。

---

## 🎨 多模态与生成（图像、视频、音频、文本到X）

#### [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) - nvidia
点赞：2,248 | 下载：241,845  
NVIDIA 推出的 3B 视觉定位模型，可精准定位图中任意物体，落地潜力突出。

#### [Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B) - Qwen
点赞：2,198 | 下载：5,148,673  
Qwen 最新 MoE 多模态模型，一周下载超 500 万，社区部署最广泛的多模态模型之一。

#### [MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3) - MiniMaxAI
点赞：1,177 | 下载：104,076  
MiniMax 最新图文多模态模型，支持图像文本交互，位居多模态热门榜前列。

#### [google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it) - google
点赞：1,129 | 下载：1,815,370  
Google Gemma-4 统一 any-to-any 模型，能处理文本、图像、音频任意组合，下载超 180 万。

#### [google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it) - google
点赞：1,037 | 下载：762,861  
Google 扩散语言模型指令版（26B-A4B），擅长文生图任务，周点赞破千。

#### [moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code) - moonshotai
点赞：946 | 下载：363,308  
Kimi 最新多模态代码模型，同时擅长代码生成与图文理解，下载超 36 万。

#### [owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1) - owensong
点赞：155 | 下载：0（新发布）  
超小型文本转语音模型，适合边缘与移动端部署，轻量级 TTS 新选择。

#### [datalab-to/lift](https://huggingface.co/datalab-to/lift) - datalab-to
点赞：110 | 下载：516  
面向 PDF 文档理解的图像到文本模型，基于 Qwen3.5 架构，专注知识文档场景。

#### [ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora) - ostris
点赞：91 | 下载：2,452  
Ideogram 4 的 LoRA 快速微调版，用于风格化图像生成。

#### [Boogu/Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit) - Boogu
点赞：84 | 下载：374  
中文友好的图像编辑扩散模型，支持区域修改与重绘。

---

## 🔧 专用模型（代码、数学、医疗、嵌入、语音等）

#### [nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b) - nvidia
点赞：613 | 下载：27,275  
英伟达流式语音识别模型，支持低延迟缓存感知 ASR，适合实时转写。

#### [WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B) - WeiboAI
点赞：565 | 下载：20,277  
3B 参数数学推理专用模型，专注提升数学问题解答准确率。

#### [CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0) - CohereLabs
点赞：475 | 下载：19,551  
Cohere 全新 North 系列轻量代码模型，面向代码补全与生成。

#### [microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT) - microsoft
点赞：267 | 下载：2,593  
微软推出的快速上下文推理模型（4B），适合长文档 Agent 与检索增强应用。

#### [LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M) - LiquidAI
点赞：93 | 下载：7,726  
高性能语义嵌入模型（350M），LFM2.5 系列，适用于检索与相似度任务。

#### [poolside/Laguna-M.1](https://huggingface.co/poolside/Laguna-M.1) - poolside
点赞：84 | 下载：2,580  
poolside 出品的代码生成模型，专注于软件工程领域，基于 vLLM 部署。

---

## 📦 微调与量化（社区微调、GGUF、AWQ 等）

#### [yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF) - yuxinlu1
点赞：2,094 | 下载：358,677  
Gemma-4-12B 代码增强版 GGUF 量化，社区下载超 35 万，代码量化热门选择。

#### [HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) - HauhauCS
点赞：2,082 | 下载：3,966,691  
Qwen3.6 多模态解禁量化版，Aggressive 训练，下载逼近 400 万，社区热度极高。

#### [yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF) - yuxinlu1
点赞：289 | 下载：21,730  
Gemma-4 Agent 增强版量化（3.5x），针对终端代理场景优化。

#### [Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF) - Jackrong
点赞：276 | 下载：190,993  
Qwen3.6 27B 代码多模态模型 GGUF 版，支持 MTP 多 token 预测。

#### [unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF) - unsloth
点赞：229 | 下载：32,260  
unsloth 提供的 GLM-5.2 GGUF 量化，便于 llama.cpp 等框架本地推理。

#### [unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF) - unsloth
点赞：151 | 下载：42,837  
Kimi-K2.7-Code 的 GGUF 量化版，低资源设备也可运行多模态代码模型。

#### [zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8) - zai-org
点赞：123 | 下载：217,361  
GLM-5.2 官方 FP8 量化，显存友好，适合大规模部署。

#### [Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b) - Mia-AiLab
点赞：121 | 下载：22,879  
Qwable 3.6-27B 的社区 GGUF 量化，拓展 Qwable 系列可及性。

#### [bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF) - bytkim
点赞：102 | 下载：36,421  
Qwen3.6 27B 带 MTP 与 pi-tune 优化的 GGUF 格式，适合高级用户调优。

#### [empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF) - empero-ai
点赞：77 | 下载：688  
基于 Qwen3.5 的 Claude 风格 GGUF 量化，轻量角色扮演模型。

---

## 📈 生态信号

本周榜单呈现三大信号：**模型家族化竞争加剧**——Qwen 3.5/3.6 系列衍生出至少 6 款微调/量化版本，已是社区最重要基座之一；Gemma-4 从官方多模态到社区代码/Agent 变体，生态快速成型。**多模态成为标配**，榜单超半数模型具备图文处理能力，并向 any-to-any 演进（如 Gemma-4-it）。**开源权重 + 社区量化**成为主流发布模式：DeepSeek-V4-Pro、Qwen3.6 等旗舰开源，而 GGUF 量化模型超过 10 款，FP8 新格式同步落地，用户对“开箱即用”的强烈需求推动模型消费化。同时，代码、数学、ASR、嵌入等专用模型加速涌现，大模型正从通用走向深度垂直。

---

## 🔭 值得探索

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 本周最热门的基础模型，性能强大，适合作为基座进行微调与系统研究，值得第一时间评测。
- **[Nvidia LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 以 3B 参数实现精准视觉定位，创新性强，在机器人、自动驾驶等领域应用前景广阔，值得动手试玩。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 社区微调量化的现象级作品，近 400 万下载量，反映用户对高效、低门槛部署的渴求，适合快速体验多模态对话。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*