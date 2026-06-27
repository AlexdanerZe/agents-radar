# Hugging Face 热门模型日报 2026-06-27

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-27 02:49 UTC

---

# Hugging Face 热门模型日报（2026-06-27）

## 今日速览

本周 Hugging Face 热门榜由 **GLM-5.2** 与 **Gemma-4-12B** 微调家族领跑，二者衍生出大量 GGUF 量化版本并占据榜单近半；阿里 **Qwen** 推出 AgentWorld 系列拓展智能体应用，**MiniMax-M3** 和 **Krea-2** 多模态模型双双上榜，表明文本生成之外的方向持续升温；NVIDIA 发力量化基础设施，**NVFP4** 技术助力大型 MoE（如 Qwen3.6-35B）部署至单卡；专用模型方面，百度 **Unlimited-OCR** 与 NVIDIA **LocateAnything-3B** 分别引领 OCR 与目标定位赛道。

## 热门模型

### 🧠 语言模型

- **zai-org/GLM-5.2**（[链接](https://huggingface.co/zai-org/GLM-5.2)）| 作者：zai-org | 点赞：2,603 | 下载：83,589  
  > 基于 MoE 的先进对话模型，推理能力强，本周点赞最高，社区热度遥遥领先。

- **WeiboAI/VibeThinker-3B**（[链接](https://huggingface.co/WeiboAI/VibeThinker-3B)）| 作者：WeiboAI | 点赞：734 | 下载：54,638  
  > 轻量数学推理模型，3B 参数实现优异数学性能，吸引学术与教育场景关注。

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M**（[链接](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)）| 作者：empero-ai | 点赞：452 | 下载：20,346  
  > 基于 Qwen3.5 的微调对话模型，擅长复杂推理，原始版本关注度高。

- **microsoft/FastContext-1.0-4B-SFT**（[链接](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)）| 作者：microsoft | 点赞：355 | 下载：5,735  
  > 微软基于 Qwen3 微调的长上下文模型，针对 Agent 场景优化，支持高效推理。

- **Qwen/Qwen-AgentWorld-35B-A3B**（[链接](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)）| 作者：Qwen | 点赞：323 | 下载：13,186  
  > 阿里 Qwen 发布的智能体专用 MoE 模型，总参 35B 仅激活 3B，兼顾性能与效率。

- **deepreinforce-ai/Ornith-1.0-35B**（[链接](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)）| 作者：deepreinforce-ai | 点赞：124 | 下载：1,005  
  > Ornith 系列 35B 成员，基于 Qwen3.5-MoE 的通用语言模型，覆盖多种生成任务。

- **deepreinforce-ai/Ornith-1.0-9B**（[链接](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)）| 作者：deepreinforce-ai | 点赞：115 | 下载：218  
  > Ornith 系列 9B 版本，平衡计算开销与生成能力，适合轻量部署。

- **LiquidAI/LFM2.5-230M**（[链接](https://huggingface.co/LiquidAI/LFM2.5-230M)）| 作者：LiquidAI | 点赞：114 | 下载：8,286  
  > 仅 230M 参数的语言模型，极致轻量，适用于移动端或嵌入式场景。

- **Chunjiang-Intelligence/DeepSeek-v4-Fable**（[链接](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)）| 作者：Chunjiang-Intelligence | 点赞：108 | 下载：1,103  
  > 基于 DeepSeek v4 的领域微调模型，专注网络安全分析，体现开源模型垂直化趋势。

- **deepreinforce-ai/Ornith-1.0-397B**（[链接](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)）| 作者：deepreinforce-ai | 点赞：107 | 下载：126  
  > Ornith 系列最大版本，397B 参数，面向大规模推理与高端硬件部署。

### 🎨 多模态与生成

- **MiniMaxAI/MiniMax-M3**（[链接](https://huggingface.co/MiniMaxAI/MiniMax-M3)）| 作者：MiniMaxAI | 点赞：1,247 | 下载：169,951  
  > 全新开源多模态大模型，支持图文联合理解与生成，凭借强大性能迅速走红。

- **krea/Krea-2-Turbo**（[链接](https://huggingface.co/krea/Krea-2-Turbo)）| 作者：krea | 点赞：285 | 下载：8,721  
  > 第二代图像生成模型 Turbo 版，在速度与画质间取得平衡，吸引创作者关注。

- **krea/Krea-2-Raw**（[链接](https://huggingface.co/krea/Krea-2-Raw)）| 作者：krea | 点赞：204 | 下载：10,408  
  > Krea-2 的基础权重，开放给社区进行微调与风格定制。

- **datalab-to/lift**（[链接](https://huggingface.co/datalab-to/lift)）| 作者：datalab-to | 点赞：159 | 下载：6,054  
  > 基于 Qwen3.5 的图像理解模型，专为 PDF 文档信息提取设计，效率突出。

- **Comfy-Org/Krea-2**（[链接](https://huggingface.co/Comfy-Org/Krea-2)）| 作者：Comfy-Org | 点赞：137 | 下载：10  
  > Krea-2 的 ComfyUI 工作流节点，方便用户通过节点化界面进行推理与组合。

### 🔧 专用模型

- **nvidia/LocateAnything-3B**（[链接](https://huggingface.co/nvidia/LocateAnything-3B)）| 作者：nvidia | 点赞：2,385 | 下载：494,756  
  > NVIDIA 推出的通用目标定位模型，3B 参数，可从图像中识别并定位任意物体。

- **baidu/Unlimited-OCR**（[链接](https://huggingface.co/baidu/Unlimited-OCR)）| 作者：baidu | 点赞：1,046 | 下载：134,146  
  > 百度开源高精度 OCR 模型，支持多场景文字识别，文档/票据等场景应用广泛。

- **nvidia/nemotron-3.5-asr-streaming-0.6b**（[链接](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)）| 作者：nvidia | 点赞：709 | 下载：56,434  
  > 流式语音识别模型，0.6B 参数基于 NeMo 框架，适合实时语音转文字。

### 📦 微调与量化

- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF**（[链接](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)）| 作者：yuxinlu1 | 点赞：2,402 | 下载：516,333  
  > Gemma-4-12B 代码版微调并 GGUF 量化，社区代码任务首选，周赞与下载双高。

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**（[链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)）| 作者：HauhauCS | 点赞：2,265 | 下载：3,453,492  
  > Qwen3.6-35B MoE 的无审查微调+GGUF 量化版，以极高自由度吸引大量用户。

- **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF**（[链接](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)）| 作者：yuxinlu1 | 点赞：690 | 下载：186,663  
  > Gemma-4-12B 智能体微调量化版，优化终端与工具使用场景。

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF**（[链接](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)）| 作者：empero-ai | 点赞：596 | 下载：486,810  
  > Qwythos 对话模型的 GGUF 量化版，借助 llama.cpp 实现本地高效运行。

- **unsloth/GLM-5.2-GGUF**（[链接](https://huggingface.co/unsloth/GLM-5.2-GGUF)）| 作者：unsloth | 点赞：411 | 下载：107,553  
  > 利用 Unsloth 工具对 GLM-5.2 进行 GGUF 量化，提供开箱即用的轻量版本。

- **nvidia/Qwen3.6-35B-A3B-NVFP4**（[链接](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)）| 作者：nvidia | 点赞：361 | 下载：4,812,629  
  > NVIDIA 采用 NVFP4 量化压缩 Qwen3.6-35B MoE，单卡可部署，下载量全榜第一。

- **deepreinforce-ai/Ornith-1.0-35B-GGUF**（[链接](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)）| 作者：deepreinforce-ai | 点赞：241 | 下载：3,002  
  > Ornith 35B 的 GGUF 版本，方便社区在本地运行该 MoE 模型。

- **deepreinforce-ai/Ornith-1.0-9B-GGUF**（[链接](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)）| 作者：deepreinforce-ai | 点赞：165 | 下载：1,779  
  > Ornith 9B 的 GGUF 量化版本，兼顾便携性与性能。

- **huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated**（[链接](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)）| 作者：huihui-ai | 点赞：136 | 下载：5,445  
  > Gemma-4-12B 代码版的去审查（abliterated）微调，移除安全限制以提供无约束生成。

- **Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF**（[链接](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)）| 作者：Jackrong | 点赞：95 | 下载：35,027  
  > Qwopus 多模态编码模型的 GGUF 版，适用于视觉编程与理解任务。

- **HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced**（[链接](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)）| 作者：HauhauCS | 点赞：93 | 下载：23,772  
  > Gemma4-12B 多模态的无审查 QAT 量化版，在安全与能力之间取得平衡。

- **nvidia/GLM-5.2-NVFP4**（[链接](https://huggingface.co/nvidia/GLM-5.2-NVFP4)）| 作者：nvidia | 点赞：88 | 下载：441  
  > NVIDIA 针对 GLM-5.2 的 NVFP4 量化部署方案，精度损失极小，代表前沿量化方向。

## 生态信号

- **主流家族**：**GLM-5.2**、**Gemma-4-12B** 与 **Qwen3.x-MoE** 三大家族衍生变体最多，**Ornith** 系列以 9B/35B/397B 全尺寸覆盖也颇具规模。  
- **开放趋势**：所有上榜模型均公开权重，社区通过微调与量化快速迭代，闭源 API 模型未见入榜。  
- **量化与微调**：GGUF 版本占据 10+ 席，已成为社区部署标准；NVIDIA 的 **NVFP4** 开始嵌入主流模型。**Uncensored** 与 **Abliterated** 模型需求旺盛，反映用户对更高自由度的追求。  
- **多模态升温**：图像理解/生成与 ASR 均有代表性模型上榜，多模态不再只是语言能力的附属。

## 值得探索

1. **nvidia/Qwen3.6-35B-A3B-NVFP4** → 首个大规模应用 NVFP4 量化的 MoE 模型，下载量 480 万居首，验证了极低比特量化在大型模型上的可行性，值得所有关注高效部署的开发者尝试。  
2. **MiniMaxAI/MiniMax-M3** → 多模态新星，周点赞 1,247，图文理解生成能力出色，是探索下一代交互界面的理想起点。  
3. **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** → 以 2,402 周赞成为最热代码模型之一，GGUF 量化后仍保持强大编码能力，适合开发者日常辅助。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*