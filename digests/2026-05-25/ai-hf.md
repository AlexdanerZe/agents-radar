# Hugging Face 热门模型日报 2026-05-25

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-25 09:58 UTC

---

# Hugging Face 热门模型日报（2026-05-25）

## 📌 今日速览

- **DeepSeek‑V4‑Pro** 以破纪录的 4,244 周点赞和 480 万下载量领跑全榜，成为新一代通用大模型的标杆，社区关注度极高。  
- **Qwen 3.6** 多模态生态全面爆发：官方版 **Qwen3.6‑27B** 下载超 440 万，社区同步释出十余种量化与微调变体（Unsloth、Jackrong、HauhauCS 等），展现了极强的生态活力。  
- **视频生成赛道升温**：Sulphur‑2‑base 下载量突破 135 万，Anima（图像生成单文件）获得 1,534 赞，字节跳动 Lance（任意‑to‑任意多模态）也首次亮相，生成式 AI 正向可控、高保真方向快速发展。  
- **腾讯集中发布翻译模型**：Hy‑MT2 系列（1.8B / 7B / 30B‑A3B）三款同时上架，构建全尺寸机器翻译方案。  
- **TTS 领域迎来新玩家**：Supertonic‑3 与 Dramabox 双双上榜，语音合成与语音克隆功能的实用化趋势明显。  

---

## 🧠 语言模型（LLM、对话、指令微调）

- **[DeepSeek‑V4‑Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** · deepseek‑ai · 点赞 4,244 · 下载 4,820,866  
  全新一代超大规模语言模型，在推理、对话等任务上全面超越前代，以压倒性热度登顶趋势榜。

- **[Hy‑MT2‑1.8B](https://huggingface.co/tencent/Hy-MT2-1.8B)** · tencent · 点赞 694 · 下载 5,552  
  腾讯基于 Hunyuan 架构的轻量翻译模型，吞吐高、易部署，适用于资源受限的翻译场景。

- **[Hy‑MT2‑30B‑A3B](https://huggingface.co/tencent/Hy-MT2-30B-A3B)** · tencent · 点赞 318 · 下载 1,494  
  腾讯大参数 MoE 翻译模型，30B 总参数、3B 激活，兼顾翻译质量与推理效率。

- **[Hy‑MT2‑7B](https://huggingface.co/tencent/Hy-MT2-7B)** · tencent · 点赞 152 · 下载 3,060  
  腾讯 Hy‑MT2 系列的中等尺寸版本，在评测中平衡了 BLEU 值与计算成本。

- **[HRM‑Text‑1B](https://huggingface.co/sapientinc/HRM-Text-1B)** · sapientinc · 点赞 274 · 下载 90,026  
  专注于人力资源领域的文本生成模型，下载量接近 10 万，反映企业级轻量模型的旺盛需求。

---

## 🎨 多模态与生成（图像、视频、音频、文本 → X）

- **[bytedance‑research/Lance](https://huggingface.co/bytedance-research/Lance)** · bytedance‑research · 点赞 779 · 下载 1,679  
  字节跳动推出的“任意‑to‑任意”多模态生成模型，支持图像/视频/音频/文本之间的自由转换。

- **[Marlin‑2B](https://huggingface.co/NemoStation/Marlin-2B)** · NemoStation · 点赞 320 · 下载 7,291  
  2B 参数视频‑文本模型，从视频和文本输入生成文本描述，适合视频理解与搜索。

- **[supertonic‑3](https://huggingface.co/Supertone/supertonic-**3) · Supertone · 点赞 652 · 下载 45,800  
  高拟真度文本转语音模型，支持多风格语音合成，下载量增长迅速。

- **[Sulphur‑2‑base](https://huggingface.co/SulphurAI/Sulphur-**2-base) · SulphurAI · 点赞 1,333 · 下载 1,354,786  
  开源文本到视频扩散基础模型，下载量超 135 万，社区普遍认为其生成质量接近商用水平。

- **[MiniCPM‑V‑4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6) · openbmb · 点赞 929 · 下载 285,414**  
  面壁智能最新多模态模型，以极小参数实现强大视觉语言能力，适合端侧部署。

- **[LongCat‑Video‑Avatar‑1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5) · meituan‑longcat · 点赞 167 · 下载 0**  
  美团开源的虚拟人视频生成模型，利用音频/图像/文本联合生成说话头像，功能极具创意。

- **[Anima](https://huggingface.co/circlestone-labs/Anima) · circlestone‑labs · 点赞 1,534 · 下载 651,655**  
  社区图像生成模型，ComfyUI 单文件支持，下载量超过 65 万，深受 AI 画师喜爱。

- **[command‑a‑plus‑05‑2026‑bf16](https://huggingface.co/CohereLabs/command-a-plus-05-2026-bf16) · CohereLabs · 点赞 113 · 下载 12,824**  
  Cohere 最新多模态大模型（图像+文本），bf16 权重开放，可以与 GPT‑4V 对标。

- **[SANA‑WM_bidirectional](https://huggingface.co/Efficient-Large-Model/SANA-WM_bidirectional) · Efficient‑Large‑Model · 点赞 100 · 下载 0**  
  支持双向图像‑视频生成的模型，可控制相机运动轨迹，论文后已开源。

- **[Dramabox](https://huggingface.co/ResembleAI/Dramabox) · ResembleAI · 点赞 248 · 下载 1,498**  
  具备语音克隆能力的 TTS 模型，适用于角色对话与有声书制作。

- **[Qwen3.6‑27B](https://huggingface.co/Qwen/Qwen3.6-27B) · Qwen · 点赞 1,433 · 下载 4,423,521**  
  Qwen 官方下一代视觉语言模型，多模态能力大幅增强，下载量超过 440 万，社区反响强烈。

- **[stable‑audio‑3‑medium](https://huggingface.co/stabilityai/stable-audio-3-medium) · stabilityai · 点赞 86 · 下载 0**  
  Stability AI 的最新音频生成模型，面向音乐与音效生成，虽刚发布但已引起关注。

- **[Lens‑Turbo](https://huggingface.co/microsoft/Lens-Turbo) · microsoft · 点赞 78 · 下载 695**  
  微软提出的加速文本‑图像生成模型，配合论文量化部署，有望降低扩散模型推理成本。

---

## 🔧 专用模型（代码、数学、医疗、嵌入）

- **[NuExtract3](https://huggingface.co/numind/NuExtract3) · numind · 点赞 113 · 下载 17,501**  
  基于视觉语言模型的结构化数据提取工具，可从文档图像中精准抽取字段，效率优于传统 OCR 管线。

- **[Nemotron‑Labs‑Diffusion‑14B](https://huggingface.co/nvidia/Nemotron-Labs-Diffusion-14B) · nvidia · 点赞 93 · 下载 5,195**  
  NVIDIA 的实验性模型，将扩散结构用于文本生成与特征提取，为扩散模型开辟新用途。

---

## 📦 微调与量化（社区微调、GGUF、AWQ）

- **[Qwen3.6‑27B‑MTP‑GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF) · unsloth · 点赞 463 · 下载 695,277**  
  Unsloth 为 Qwen3.6 官方版提供的 GGUF 量化，显著降低多模态模型本地运行门槛。

- **[command‑a‑plus‑05‑2026‑w4a4](https://huggingface.co/CohereLabs/command-a-plus-05-2026-w4a4) · CohereLabs · 点赞 193 · 下载 7,449**  
  官方推出的 4 位权重量化版 command‑a‑plus，模型体积缩小近 75%，部署更友好。

- **[Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) · HauhauCS · 点赞 809 · 下载 1,392,596**  
  社区无审查微调的 Qwen3.6 MoE 量化版，下载超百万，反映对宽松对话模型的强烈需求。

- **[Qwen3.6‑35B‑A3B‑MTP‑GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-MTP-GGUF) · unsloth · 点赞 360 · 下载 578,580**  
  Unsloth 针对 Qwen3.6 MoE 架构的量化，兼顾模型容量与推理速度。

- **[Qwen‑Fixed‑Chat‑Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) · froggeric · 点赞 398 · 下载 0**  
  修复 Qwen 系列聊天模板配置的工具，受到开发者关注（无下载但高赞），表明优质工具同样能引爆社区。

- **[Qwopus3.6‑27B‑v2‑GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-GGUF) · Jackrong · 点赞 121 · 下载 12,677**  
  Jackrong 量化的 Qwen3.6 衍生版 v2，在本地部署和推理上做了针对性优化。

- **[Qwopus3.5‑9B‑Coder‑GGUF](https://huggingface.co/Jackrong/Qwopus3.5-9B-Coder-GGUF) · Jackrong · 点赞 183 · 下载 42,644**  
  专注于代码生成的 Qwen 量化模型，下载超过 4 万，满足开发者本地代码辅助需求。

- **[Qwopus3.5‑9B‑Coder‑MTP‑GGUF](https://huggingface.co/Jackrong/Qwopus3.5-9B-Coder-MTP-GGUF) · Jackrong · 点赞 91 · 下载 37,628**  
  代码模型的 MTP（Multi‑Token Prediction）分支，推理速度进一步优化。

- **[Qwopus3.6‑27B‑v2‑MTP‑GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF) · Jackrong · 点赞 84 · 下载 23,762**  
  Jackrong 推出的 Qwen3.6 v2 MTP 量化版，性能稳定，下载量持续增长。

- **[Qwen3.6‑27B‑OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.6-27B-OBLITERATED) · OBLITERATUS · 点赞 82 · 下载 7,701**  
  社区移除了视觉部分的 Qwen3.6 纯文本无限制版，引起部分用户的探索兴趣。

---

## 🌱 生态信号

**家族势力**：Qwen 3.6 系列无疑是本周最活跃的生态引擎，官方版与十余款社区量化/微调版本同时霸榜，涵盖从 9B 到 35B、从纯文本到多模态、从通用到 Coder 的多种变体。DeepSeek‑V4‑Pro 以绝对优势成为新晋“顶流”。腾讯 Hy‑MT2 密集发布表明大厂正在布局全尺寸翻译模型。Cohere command‑a‑plus 的加入使多模态开放模型阵营更加壮大。

**开源 vs 闭源**：榜单上除少数企业模型外，几乎所有模型都直接提供了安全张量（safetensors）或 GGUF 权重，社区主导的开放模型生态依然强势。即便如 Cohere 等商业公司，也选择完全开放权重（包括量化版），这反映出开源开放已成为行业共识，以吸引部署和二次开发。

**量化与微调活动**：Unsloth 和 Jackrong 围绕 Qwen 3.6 进行了大量量化工作，带动了数十万至百万级别下载。尤其是“无审查”版本（HauhauCS、OBLITERATUS）下载量极高，说明部分用户对内容限制非常敏感。此外，froggeric 的工具型模型（修复聊天模板）虽无下载量却获近 400 赞，提示社区开发者对实用配套工具的需求不可忽视。

---

## 🧪 值得探索

- **[DeepSeek‑V4‑Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 周点赞与月下载均为全场最高，是当前最具潜力的大语言模型，值得全面评测与部署测试。  
- **[Sulphur‑2‑base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — 开源文本到视频模型的里程碑之作，下载量已破百万，建议关注其生成质量与可控性边界。  
- **[Qwen3.6‑27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — 阿里 Qwen 系列最新视觉语言基座，性能大幅跃升，且社区已经积累大量量化与适配方案，入手门槛极低，可作为多模态应用的起点。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*