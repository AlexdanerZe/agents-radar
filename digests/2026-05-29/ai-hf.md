# Hugging Face 热门模型日报 2026-05-29

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-29 02:54 UTC

---

# Hugging Face 热门模型日报（2026-05-29）

## 📰 今日速览

DeepSeek V4 系列（Pro & Flash）以极高点赞和下载量强势领跑，树立开源对话模型新标杆。多模态生成全面爆发：字节跳动 [Lance](https://huggingface.co/bytedance-research/Lance) 实现任意模态互转，[Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B) 成为视觉语言生态中心，[Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base) 与 [stable-audio-3-medium](https://huggingface.co/stabilityai/stable-audio-3-medium) 分别主攻视频和音频生成。社区围绕 Qwen3.6 的微调与量化活动异常活跃（无审查版、GGUF、甚至 chat‑template 修复均获高赞），反映出用户对可控性和部署便利性的迫切需求。与此同时，腾讯 [Hy-MT2](https://huggingface.co/tencent/Hy-MT2-1.8B) 翻译系列与 [pyannote/speaker-diarization-3.1](https://huggingface.co/pyannote/speaker-diarization-3.1) 等专用工具下载量惊人，垂直场景的实用价值持续凸显。

---

## 🔥 热门模型

### 🧠 语言模型（LLM / 对话 / 指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai · 点赞 4,407 · 下载 5,281,601  
  新一代开源对话模型，周点赞与下载双冠，代表当前开源 LLM 的顶尖能力。

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — deepseek-ai · 点赞 1,279 · 下载 3,327,898  
  V4 的轻量高效版，保持强大对话性能的同时推理更敏捷，热度持续走高。

- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** — openbmb · 点赞 500 · 下载 15,629  
  仅 1B 参数的高效语言模型，在极小尺寸下实现扎实的文本生成，瞄准端侧部署。

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — sapientinc · 点赞 400 · 下载 121,862  
  专注人力资源管理场景的 1B 文本生成模型，为企业级垂直应用提供开源基础。

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — LiquidAI · 点赞 119 · 下载 0  
  采用 MoE 架构（8B 参数，激活 1B）的语言模型，在效率与性能间寻求新平衡，刚发布即受关注。

### 🎨 多模态与生成（图像 / 视频 / 音频 / 文本到 X）

- **[circlestone-labs/Anima](https://huggingface.co/circlestone-labs/Anima)** — circlestone-labs · 点赞 1,580 · 下载 704,160  
  单文件格式的图像生成模型（兼容 ComfyUI），社区驱动的高质量文生图工具，热度攀升。

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — Qwen · 点赞 1,510 · 下载 4,790,806  
  Qwen 团队最新视觉语言模型，支持图文理解与对话，生态核心，衍生大量社区版本。

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — SulphurAI · 点赞 1,424 · 下载 1,472,982  
  高性能文本到视频生成模型，扩散架构配合 GGUF 量化，在视频生成赛道迅速走红。

- **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** — openbmb · 点赞 1,047 · 下载 388,525  
  轻量级视觉语言模型，移动端级别参数实现出色的图像理解与对话能力。

- **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)** — bytedance-research · 点赞 956 · 下载 2,506  
  字节跳动 any-to-any 全能生成模型（图像/视频/音频等），多模态大一统方向的前沿探索。

- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** — Supertone · 点赞 728 · 下载 52,022  
  超真实感文本到语音合成模型，语音质量突出，适用于内容创作与虚拟角色。

- **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)** — NemoStation · 点赞 430 · 下载 13,855  
  视频到文本模型，擅长视频字幕与理解任务，为视频内容分析提供轻量方案。

- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** — meituan-longcat · 点赞 368 · 下载 0  
  美团出品的长视频数字人生成模型，支持音频/图像/文本联合驱动，发布即受关注。

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia · 点赞 208 · 下载 1,755  
  NVIDIA 视觉定位模型，可根据文本指令精准定位图像中任意目标，3B 参数兼具性能与效率。

- **[numind/NuExtract3](https://huggingface.co/numind/NuExtract3)** — numind · 点赞 186 · 下载 44,827  
  面向文档/图像的提取模型，支持从图片中结构化抽取信息，实用性强，下载活跃。

- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** — nvidia · 点赞 163 · 下载 335  
  基于扩散模型的图像超分辨率方案，在画质增强方向提供新思路。

- **[microsoft/Lens](https://huggingface.co/microsoft/Lens)** — microsoft · 点赞 138 · 下载 1,061  
  微软推出的文本到图像生成模型，强调可控性和高质量，同步发布论文（arXiv:2605.21573）。

- **[stabilityai/stable-audio-3-medium](https://huggingface.co/stabilityai/stable-audio-3-medium)** — stabilityai · 点赞 132 · 下载 0  
  Stability AI 最新文本到音频生成模型，支持音乐与音效，刚发布即登上趋势榜。

- **[microsoft/Lens-Turbo](https://huggingface.co/microsoft/Lens-Turbo)** — microsoft · 点赞 125 · 下载 1,478  
  Lens 的快速推理版，在更少步数内生成同等质量图像，满足效率敏感场景。

### 🔧 专用模型（代码 / 数学 / 医疗 / 嵌入）

- **[pyannote/speaker-diarization-3.1](https://huggingface.co/pyannote/speaker-diarization-3.1)** — pyannote · 点赞 2,044 · 下载 9,845,884  
  说话人分离与语音识别 pipeline，下载量近千万，语音处理领域的标杆开源工具。

- **[tencent/Hy-MT2-1.8B](https://huggingface.co/tencent/Hy-MT2-1.8B)** — tencent · 点赞 1,079 · 下载 14,600  
  腾讯混元系列高效翻译模型，1.8B 参数在翻译质量与推理速度间取得优秀平衡。

- **[tencent/Hy-MT2-30B-A3B](https://huggingface.co/tencent/Hy-MT2-30B-A3B)** — tencent · 点赞 417 · 下载 2,894  
  腾讯 MoE 翻译大模型（30B 参数，激活 3B），面向高精度翻译场景，扩展性强。

- **[zhen-nan/L2P](https://huggingface.co/zhen-nan/L2P)** — zhen-nan · 点赞 78 · 下载 0  
  来自学术论文（arXiv:2605.12013）的研究模型，可能涉及预训练或提示学习，值得研究者关注。

### 📦 微调与量化（社区微调 / GGUF / AWQ）

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS · 点赞 1,005 · 下载 1,956,558  
  基于 Qwen3.6-35B-MoE 的“无审查”微调版，下载量极大，反映社区对宽松限制模型的需求。

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth · 点赞 533 · 下载 806,874  
  unsloth 对 Qwen3.6-27B 的多令牌预测（MTP）量化版，成为主流本地部署选择。

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric · 点赞 446 · 下载 0  
  非权重资源，而是为 Qwen 修复聊天模板，因兼容性问题普遍而获得高赞，体现社区对“开箱即用”的重视。

- **[unsloth/Qwen3.6-35B-A3B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-MTP-GGUF)** — unsloth · 点赞 404 · 下载 686,839  
  unsloth 对 MoE 版 Qwen3.6-35B 的量化版，降低在有限硬件上运行 MoE 模型的门槛。

- **[Jackrong/Qwopus3.6-27B-v2-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-GGUF)** — Jackrong · 点赞 174 · 下载 24,336  
  社区提供的 Qwen3.6-27B 非官方 GGUF 版本，可配合 llama.cpp 高效运行。

- **[Jackrong/Qwopus3.6-27B-v2-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)** — Jackrong · 点赞 151 · 下载 65,968  
  类似上条，额外包含多令牌预测支持，进一步优化生成效率。

- **[OBLITERATUS/Qwen3.6-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.6-27B-OBLITERATED)** — OBLITERATUS · 点赞 112 · 下载 13,911  
  基于 Qwen3.6-27B 的极端风格微调（“obliterated”），探索模型行为边界，吸引研究与猎奇用户。

---

## 📊 生态信号

**模型家族态势：** DeepSeek V4 系列以完全开源（MIT）姿态雄踞 LLM 榜首，显示高质量开源对话模型的需求依然旺盛。Qwen 3.6 家族则通过“官方基座 + 社区微调/量化”模式形成最活跃生态，覆盖从多模态到纯文本、从完整权重到 GGUF 的全链条。字节、腾讯、美团、微软等企业也在多模态生成与翻译领域密集开源，进一步丰富生态版图。

**开源 vs 闭源趋势：** 本周上榜模型几乎全部开源权重，且越来越多的企业将核心模型（如 Lance、Hy-MT2、Lens）以 permissive 协议释放，推动社区信任与二次开发。

**量化与微调活动：** 围绕 Qwen3.6 的 GGUF 量化版本多达 5 个，无审查、极端风格等微调版本表明用户对模型控制权与个性化有强烈诉求。甚至非权重资源（chat‑template 修复）也迎来高赞，暗示部署工具链的完善同样关键。专业化量化工具（如 unsloth）正在成为生态基础设施。

---

## 🔭 值得探索

1. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 当前最强开源对话模型之一，适合评测最新 LLM 能力或作为应用基座。
2. **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — 官方视觉语言核心模型，生态中心，后续社区版本多基于此，值得深入研究与二次开发。
3. **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)** — 代表 any-to-any 多模态生成的前沿方向，同一模型处理图像/视频/音频，极具实验价值。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*