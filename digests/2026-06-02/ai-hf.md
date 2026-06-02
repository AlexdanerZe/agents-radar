# Hugging Face 热门模型日报 2026-06-02

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-02 03:39 UTC

---

# Hugging Face 热门模型日报 (2026-06-02)

## 今日速览
- **DeepSeek V4 Pro 和 Flash 登顶本周热度**，前者以 4,536 赞成为最高点赞模型，后者下载量破 351 万，V4 系列在开源 LLM 中持续领跑。
- **Qwen 3.6 多模态生态全面开花**：官方 27B 模型下载超 515 万，社区涌现基于该架构的 uncensored 微调、NVFP4 量化、GGUF 衍生版，形成多层生态。
- **视频与多模态生成爆发**：SulphurAI 文生视频模型下载 165 万，美团虚拟人生成器、NVIDIA Cosmos3‑Nano 等新作获高关注，表明应用正加速落地。
- **专用模型刚需凸显**：pyannote 说话人分离持续霸榜（下载 959 万），OpenAI 隐私过滤器上线即获 1,579 赞，任务专精模型需求强劲。

---

## 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

- **[deepseek‑ai/DeepSeek‑V4‑Pro](https://huggingface.co/deepseek‑ai/DeepSeek‑V4‑Pro)** — deepseek‑ai | 点赞 4,536 | 下载 5,851,826  
  DeepSeek 第四代旗舰，综合性能对标闭源巨头，MIT 许可使其成为社区首选对话模型。

- **[deepseek‑ai/DeepSeek‑V4‑Flash](https://huggingface.co/deepseek‑ai/DeepSeek‑V4‑Flash)** — deepseek‑ai | 点赞 1,342 | 下载 3,511,636  
  V4 轻量高效版，兼顾速度与能力，适配低延迟场景，与 Pro 形成完整产品矩阵。

- **[openbmb/MiniCPM5‑1B](https://huggingface.co/openbmb/MiniCPM5‑1B)** — openbmb | 点赞 692 | 下载 45,698  
  仅 1B 参数的新一代 MiniCPM，专注纯文本生成，目标为移动端和边缘设备。

- **[sapientinc/HRM‑Text‑1B](https://huggingface.co/sapientinc/HRM‑Text‑1B)** — sapientinc | 点赞 439 | 下载 149,543  
  专为人力资源场景定制的 1B 对话模型，体现垂直领域 LLM 的实用化趋势。

- **[LiquidAI/LFM2.5‑8B‑A1B](https://huggingface.co/LiquidAI/LFM2.5‑8B‑A1B)** — LiquidAI | 点赞 399 | 下载 37,893  
  MoE 架构高效模型，8B 总参仅激活 1B，专注边缘推理，Liquid AI 出品。

---

### 🎨 多模态与生成（图像、视频、音频、文本到 X）

- **[Qwen/Qwen3.6‑27B](https://huggingface.co/Qwen/Qwen3.6‑27B)** — Qwen | 点赞 1,568 | 下载 5,154,729  
  Qwen3.6 多模态官方主力，27B 参数，兼具理解与生成，开源社区生态基座。

- **[SulphurAI/Sulphur‑2‑base](https://huggingface.co/SulphurAI/Sulphur‑2‑base)** — SulphurAI | 点赞 1,491 | 下载 1,656,520  
  高质量开源文生视频模型，基于 Diffusers 架构，下载量飙升，视频生成赛道新星。

- **[openbmb/MiniCPM‑V‑4.6](https://huggingface.co/openbmb/MiniCPM‑V‑4.6)** — openbmb | 点赞 1,088 | 下载 459,188  
  小参数多模态模型，延续 MiniCPM 高效路线，在端侧即可运行图像‑文本任务。

- **[bytedance‑research/Lance](https://huggingface.co/bytedance‑research/Lance)** — bytedance‑research | 点赞 1,002 | 下载 3,041  
  字节跳动 Any‑to‑Any 统一多模态生成，同时处理图像、视频、音频、文本，创新架构。

- **[nvidia/LocateAnything‑3B](https://huggingface.co/nvidia/LocateAnything‑3B)** — nvidia | 点赞 817 | 下载 35,783  
  NVIDIA 视觉定位与生成模型，3B 参数，可定位图像中任意物体并融合文本生成。

- **[Supertone/supertonic‑3](https://huggingface.co/Supertone/supertonic‑3)** — Supertone | 点赞 771 | 下载 57,627  
  高表现力 TTS 模型，声学质量突出，支持多种风格，ONNX 推理高效。

- **[NemoStation/Marlin‑2B](https://huggingface.co/NemoStation/Marlin‑2B)** — NemoStation | 点赞 482 | 下载 17,012  
  视频理解轻量模型，基于 Qwen3.5 架构，2B 参数实现视频‑文本任务。

- **[meituan‑longcat/LongCat‑Video‑Avatar‑1.5](https://huggingface.co/meituan‑longcat/LongCat‑Video‑Avatar‑1.5)** — meituan‑longcat | 点赞 469 | 下载 0  
  美团虚拟人生成模型，支持音频或图像驱动视频生成，应用导向强。

- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** — nvidia | 点赞 239 | 下载 577  
  NVIDIA 扩散超分辨率模型，专注图像到图像提升，图像恢复场景。

- **[numind/NuExtract3](https://huggingface.co/numind/NuExtract3)** — numind | 点赞 216 | 下载 59,010  
  基于 Qwen3.5 的图像信息提取模型，可结构化输出，实用工具型。

- **[stepfun‑ai/Step‑3.7‑Flash](https://huggingface.co/stepfun‑ai/Step‑3.7‑Flash)** — stepfun‑ai | 点赞 196 | 下载 9,256  
  阶跃星辰多模态语言模型，强调推理速度，视觉语言能力接近闭源。

- **[OpenMOSS‑Team/MOSS‑TTS‑v1.5](https://huggingface.co/OpenMOSS‑Team/MOSS‑TTS‑v1.5)** — OpenMOSS‑Team | 点赞 94 | 下载 18,564  
  复旦开源 TTS 系列新版，中文发音自然，社区自部署首选。

- **[Kwai‑Keye/Keye‑VL‑2.0‑30B‑A3B](https://huggingface.co/Kwai‑Keye/Keye‑VL‑2.0‑30B‑A3B)** — Kwai‑Keye | 点赞 89 | 下载 784  
  快手多模态 MoE 模型，30B 总参仅激活 3B，高效视觉语言理解。

- **[nvidia/Cosmos3‑Nano](https://huggingface.co/nvidia/Cosmos3‑Nano)** — nvidia | 点赞 78 | 下载 6,261  
  NVIDIA Cosmos3 全模态生成轻量版，覆盖文本、图像、视频，多合一。

---

### 🔧 专用模型（代码、数学、医疗、嵌入及其他专用）

- **[pyannote/speaker‑diarization‑3.1](https://huggingface.co/pyannote/speaker‑diarization‑3.1)** — pyannote | 点赞 2,108 | 下载 9,591,005  
  说话人分离黄金标杆，会议与语音分析刚需，下载量逼近千万。

- **[openai/privacy‑filter](https://huggingface.co/openai/privacy‑filter)** — openai | 点赞 1,579 | 下载 316,092  
  OpenAI 官方隐私过滤模型，基于 token 分类，保护敏感信息，企业关注度极高。

- **[tencent/Hy‑MT2‑30B‑A3B](https://huggingface.co/tencent/Hy‑MT2‑30B‑A3B)** — tencent | 点赞 444 | 下载 4,458  
  腾讯多模态翻译 MoE 模型，30B 总参（3B 激活），在翻译任务上表现突出。

- **[PaddlePaddle/PaddleOCR‑VL‑1.6](https://huggingface.co/PaddlePaddle/PaddleOCR‑VL‑1.6)** — PaddlePaddle | 点赞 156 | 下载 3,190  
  百度光学字符识别视觉语言融合版，兼顾 OCR 与通用 VL 理解，硬核实用。

---

### 📦 微调与量化（社区微调、GGUF、AWQ 及其他压缩）

- **[HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive](https://huggingface.co/HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive)** — HauhauCS | 点赞 1,226 | 下载 2,533,393  
  基于 Qwen3.6 MoE 的社区 uncensored 版本，同时提供 GGUF，下载量惊人，满足特定开箱需求。

- **[unsloth/Qwen3.6‑27B‑MTP‑GGUF](https://huggingface.co/unsloth/Qwen3.6‑27B‑MTP‑GGUF)** — unsloth | 点赞 595 | 下载 952,188  
  UnsLoth 优化的 Qwen3.6 GGUF 量化，引入 MTP 加速，极大降低大模型推理门槛。

- **[Jackrong/Qwopus3.6‑27B‑v2‑MTP‑GGUF](https://huggingface.co/Jackrong/Qwopus3.6‑27B‑v2‑MTP‑GGUF)** — Jackrong | 点赞 184 | 下载 139,952  
  社区 Qwen3.6 GGUF 量化另一衍生版，进一步丰富部署选择。

- **[LiquidAI/LFM2.5‑8B‑A1B‑GGUF](https://huggingface.co/LiquidAI/LFM2.5‑8B‑A1B‑GGUF)** — LiquidAI | 点赞 146 | 下载 55,212  
  官方发布的 LFM2.5 GGUF 量化版，使 MoE 模型在消费级硬件上流畅运行。

- **[nvidia/Qwen3.6‑35B‑A3B‑NVFP4](https://huggingface.co/nvidia/Qwen3.6‑35B‑A3B‑NVFP4)** — nvidia | 点赞 121 | 下载 171,588  
  NVIDIA 使用 Model Optimizer 完成的 4‑bit 浮点量化，企业级加速下载量高。

- **[prism‑ml/bonsai‑image‑ternary‑4B‑gemlite‑2bit](https://huggingface.co/prism‑ml/bonsai‑image‑ternary‑4B‑gemlite‑2bit)** — prism‑ml | 点赞 91 | 下载 0  
  1.58‑bit 三元量化文生图模型，前沿压缩研究，探索极低比特生成。

- **[stepfun‑ai/Step‑3.7‑Flash‑GGUF](https://huggingface.co/stepfun‑ai/Step‑3.7‑Flash‑GGUF)** — stepfun‑ai | 点赞 86 | 下载 37,533  
  Step‑3.7‑Flash 的官方 GGUF 量化版，带 imatrix，社区推理利器。

---

## 生态信号

**模型家族势头**：DeepSeek V4 系列（Pro + Flash）以压倒性的点赞和下载量稳坐开源 LLM 头把交椅；Qwen 3.6 则成为多模态领域最活跃的基座，围绕它的微调和量化版本已形成“生态雨林”。**MoE 全面普及**：榜单中超半数模型采用混合专家架构（LFM、Qwen3.6 MoE、Step Flash、Keye‑VL、Hy‑MT2、Cosmos3 等），稀疏激活成为兼顾性能与效率的主流选择。**开源权重持续领先**：30 个热门模型全部开源权重，未见纯闭源 API 类产品入榜，开源社区仍为创新主阵地。**量化活动密集**：GGUF 仍是个人部署标准，NVFP4 代表企业级量化方向，三元量化（1.58‑bit）开始进入图像生成领域，压缩技术正在从 LLM 向多模态扩散。

---

## 值得探索

1. **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — 速度与能力的最佳平衡，特别适合需要低延迟的聊天和推理场景，同时又保持较高的模型质量。

2. **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — 开源文生视频的最新标杆，可直接在 Diffusers 中运行，适合研究视频生成或构建自定义应用。

3. **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — 多模态时代的通用入口，27B 参数既能做图像理解又能做文本生成，社区扩展丰富（GGUF、微调、量化），值得优先上手体验。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*