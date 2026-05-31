# Hugging Face 热门模型日报 2026-05-31

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-31 03:31 UTC

---

# Hugging Face 热门模型日报 (2026‑05‑31)

## 今日速览

DeepSeek‑V4 Pro 与 Flash 双版本霸榜，周点赞合计超 5 700，下载量突破 930 万，成为本周期最大赢家。多模态与生成模型占据榜单过半席位，阿里 Qwen3.6‑27B、面壁 MiniCPM‑V‑4.6 等视觉语言模型热度持续，字节跳动 Lance 与美团 LongCat‑Video‑Avatar 则展现了任意模态与数字人领域的最新突破。社区微调与量化活动围绕 Qwen3.6 系列集中爆发，Uncensored 版和多个 GGUF 版本频频上榜。此外，pyannote 说话人分离、OpenAI 隐私过滤器等高实用性专用模型下载量居高不下，折射出模型落地需求的强劲增长。

---

## 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

- **[deepseek-ai/DeepSeek‑V4‑Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  deepseek‑ai | 点赞 4 466 | 下载 5 918 111  
  DeepSeek V4 旗舰版本，综合文本生成与对话能力顶尖，周点赞与下载量双双登顶。

- **[deepseek-ai/DeepSeek‑V4‑Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**  
  deepseek‑ai | 点赞 1 306 | 下载 3 427 926  
  V4 的高效蒸馏版，在保持较强性能的同时显著提升推理速度，紧随 Pro 之后。

- **[openbmb/MiniCPM5‑1B](https://huggingface.co/openbmb/MiniCPM5-1B)**  
  openbmb | 点赞 610 | 下载 28 793  
  面壁智能推出的 1B 端侧语言模型，轻量设计与高质量生成使其成为小参数模型的代表。

- **[LiquidAI/LFM2.5‑8B‑A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)**  
  LiquidAI | 点赞 283 | 下载 17 084  
  稀疏 MoE 架构，总参 8B 仅激活 1B，能以极低算力实现高效文本生成。

---

### 🎨 多模态与生成（图像、视频、音频、文本到 X）

- **[circlestone‑labs/Anima](https://huggingface.co/circlestone-labs/Anima)**  
  circlestone‑labs | 点赞 1 602 | 下载 736 443  
  扩散单文件模型，适配 ComfyUI，支持高质量图像/动画生成，社区反响热烈。

- **[Qwen/Qwen3.6‑27B](https://huggingface.co/Qwen/Qwen3.6-27B)**  
  Qwen | 点赞 1 539 | 下载 4 971 730  
  阿里最新视觉语言模型，27B 参数在图文理解与对话上表现突出，官方版本备受关注。

- **[SulphurAI/Sulphur‑2‑base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
  SulphurAI | 点赞 1 456 | 下载 1 557 858  
  开源文生视频基础模型，基于扩散架构，引领视频生成领域的新浪潮。

- **[openbmb/MiniCPM‑V‑4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)**  
  openbmb | 点赞 1 074 | 下载 433 156  
  面壁多模态模型系列最新，延续小参数量强性能路线，视觉与语言融合出色。

- **[bytedance‑research/Lance](https://huggingface.co/bytedance-research/Lance)**  
  bytedance‑research | 点赞 981 | 下载 2 856  
  任意模态（any‑to‑any）生成模型，统一处理文本、图像、视频，技术极具前瞻性。

- **[Supertone/supertonic‑3](https://huggingface.co/Supertone/supertonic-3)**  
  Supertone | 点赞 746 | 下载 55 382  
  第三代文本转语音模型，自然度和表现力达到新高度。

- **[nvidia/LocateAnything‑3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  nvidia | 点赞 506 | 下载 18 327  
  通用目标定位与分割模型，结合图像与文本输入，精准识别语义目标。

- **[NemoStation/Marlin‑2B](https://huggingface.co/NemoStation/Marlin-2B)**  
  NemoStation | 点赞 457 | 下载 15 780  
  基于 Qwen3.5 的视频理解轻量模型，2B 参数实现视频到文本的高效处理。

- **[meituan‑longcat/LongCat‑Video‑Avatar‑1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)**  
  meituan‑longcat | 点赞 411 | 下载 0  
  音频/图像驱动的数字人生成模型，刚发布即引关注，下载量即将爆发。

- **[numind/NuExtract3](https://huggingface.co/numind/NuExtract3)**  
  numind | 点赞 205 | 下载 53 338  
  基于 Qwen3.5 的文档结构提取模型，可从图像中准确抽取表格、字段等结构化信息。

- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)**  
  nvidia | 点赞 194 | 下载 437  
  像素扩散超分辨率模型，在图像细节恢复上表现优异。

- **[microsoft/Lens](https://huggingface.co/microsoft/Lens)**  
  microsoft | 点赞 145 | 下载 1 517  
  微软推出的文本到图像扩散生成模型，为创意场景提供高质量图像。

- **[stepfun‑ai/Step‑3.7‑Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)**  
  stepfun‑ai | 点赞 139 | 下载 3 400  
  阶跃星辰的轻量视觉语言模型，兼顾图文理解与快速推理。

- **[OpenMOSS‑Team/MOSS‑TTS‑v1.5](https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5)**  
  OpenMOSS‑Team | 点赞 74 | 下载 11 254  
  复旦开源的中文 TTS 模型，支持自然流畅的语音合成。

---

### 🔧 专用模型（代码、数学、医疗、翻译、识别、过滤等）

- **[pyannote/speaker‑diarization‑3.1](https://huggingface.co/pyannote/speaker-diarization-3.1)**  
  pyannote | 点赞 2 073 | 下载 9 771 170  
  说话人分离流水线最新版，下载量近千万，是音频会议分析的首选工具。

- **[openai/privacy‑filter](https://huggingface.co/openai/privacy-filter)**  
  openai | 点赞 1 570 | 下载 304 691  
  隐私信息识别模型，支持 Transformers.js，可在浏览器侧部署，实用性强。

- **[tencent/Hy‑MT2‑1.8B](https://huggingface.co/tencent/Hy-MT2-1.8B)**  
  tencent | 点赞 1 092 | 下载 16 805  
  腾讯混元翻译的密集版本，1.8B 参数即达到高质量多语种翻译。

- **[tencent/Hy‑MT2‑30B‑A3B](https://huggingface.co/tencent/Hy-MT2-30B-A3B)**  
  tencent | 点赞 434 | 下载 3 833  
  混元翻译的 MoE 版本，总量 30B、激活仅 3B，兼顾效果与效率。

- **[sapientinc/HRM‑Text‑1B](https://huggingface.co/sapientinc/HRM-Text-1B)**  
  sapientinc | 点赞 421 | 下载 138 118  
  专为人力资源管理场景训练的文本模型，在 HR 文档处理与对话中表现突出。

- **[PaddlePaddle/PaddleOCR‑VL‑1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)**  
  PaddlePaddle | 点赞 108 | 下载 2 294  
  百度视觉语言 OCR 模型，融合 ERNIE 4.5，实现识别与语义理解一体化。

---

### 📦 微调与量化（社区微调、GGUF、AWQ 等）

- **[HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  HauhauCS | 点赞 1 112 | 下载 2 227 885  
  社区对 Qwen3.6 进行无审查微调并打包为 GGUF，下载量超 220 万，成为榜单黑马。

- **[unsloth/Qwen3.6‑27B‑MTP‑GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**  
  unsloth | 点赞 567 | 下载 877 938  
  Unsloth 优化并量化的 Qwen3.6 多令牌预测版，兼顾本地部署性能与新训练特性。

- **[froggeric/Qwen‑Fixed‑Chat‑Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**  
  froggeric | 点赞 460 | 下载 0  
  修复 Qwen 系列模型聊天模板的配置文件，解决微调与推理中的兼容性问题，开发者必备。

- **[Jackrong/Qwopus3.6‑27B‑v2‑GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-GGUF)**  
  Jackrong | 点赞 186 | 下载 33 167  
  社区微调并量化的 Qwen3.6 视觉语言模型 GGUF 版，v2 版本进一步优化。

- **[Jackrong/Qwopus3.6‑27B‑v2‑MTP‑GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)**  
  Jackrong | 点赞 172 | 下载 105 264  
  上述模型的 MTP 变体，利用多令牌预测技术提升生成质量。

- **[LiquidAI/LFM2.5‑8B‑A1B‑GGUF](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B-GGUF)**  
  LiquidAI | 点赞 124 | 下载 23 685  
  Liquid 语言模型的 GGUF 量化版，适合在 CPU 或边缘设备上高效运行。

---

## 生态信号

**Qwen3.6 生态一骑绝尘。** 从官方旗舰到社区无审查微调，再到 Unsloth、Jackrong 等多家团体推出的 GGUF 版本，Qwen3.6 已形成覆盖视觉、语言、量化、微调的完整生态，成为当前社区最活跃的模型家族。  
**DeepSeek‑V4 开辟旗舰新标杆。** 虽然暂未出现大规模社区微调（因发布不久），但 Pro 与 Flash 双版本以绝对点赞和下载量表明，开放重量级权重的路线仍是主流。  
**开源权重主导，闭源仅零星出现。** 榜单几乎全部为可下载权重的开放模型，OpenAI 的隐私过滤器为例外但亦提供 ONNX 部署。  
**GGUF 量化成为社区“标配”。** 几乎所有热门模型都伴随量化版出现，且社区更偏好“无审查”微调，反映了用户对自定义行为和本地化部署的强烈需求。

---

## 值得探索

1. **[deepseek-ai/DeepSeek‑V4‑Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
   当前公开可用的最强语言模型之一，适合进行综合能力评测、指令微调研究以及生产环境部署，是了解 2026 年 LLM 天花板的理想起点。

2. **[bytedance‑research/Lance](https://huggingface.co/bytedance-research/Lance)**  
   真正意义上的 any‑to‑any 多模态模型，统一视听图文生成，代表了多模态融合的前沿方向，适合关注下一代基础架构的研究者深入挖掘。

3. **[pyannote/speaker‑diarization‑3.1](https://huggingface.co/pyannote/speaker-diarization-3.1)**  
   下载量近千万的成熟音频管线，可直接集成于会议转录、语音分析等应用。对于追求落地效果的团队是最实用的选择之一。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*