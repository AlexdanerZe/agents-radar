# Hugging Face 热门模型日报 2026-06-07

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-07 03:35 UTC

---

# 《Hugging Face 热门模型日报》（2026-06-07）

**今日速览**  
本周 Hugging Face 榜单迎来多点爆发：**DeepSeek-V4-Pro** 以 4,681 赞断层领先，展示社区对最新开源大模型的强烈追捧；**NVIDIA** 密集发布定位（LocateAnything-3B）、世界模型（Cosmos3 系列）和超大 MoE（Nemotron-3）的完整矩阵；**Google Gemma-4** 系列首次搭载“any-to-any”多模态能力，成为视觉‑语言‑文本全能基线；社区微调与量化热度不减，**HauhauCS** 的 Qwen3.6 Uncensored GGUF 下载近 280 万，**unsloth** 和 **NVIDIA ModelOpt** 同步为 Gemma-4、Nemotron-3 提供高效量化格式；视频生成赛道再添 **Sulphur-2-base** 和 **LongCat 数字人**等强力选手。超大 MoE、多模态统一、量化部署成为本周三大关键词。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — 作者: LiquidAI | ❤️ 534 | ⬇️ 95,440 — 高度稀疏 MoE 语言模型，仅激活 1B 参数达到密集 8B 性能，推理效率极高
- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — 作者: JetBrains | ❤️ 240 | ⬇️ 16,395 — 集成思考链的 MoE 对话模型，强化推理与编码能力
- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 作者: deepseek-ai | ❤️ 4,681 | ⬇️ 5,510,611 — V4 旗舰版，性能比肩顶级闭源模型，是社区目前最受关注的开源 LLM
- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** — 作者: openbmb | ❤️ 775 | ⬇️ 100,575 — 仅 1B 参数的小模型，在端侧设备上展现强劲文本生成能力
- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** — 作者: nvidia | ❤️ 145 | ⬇️ 47,285 — 550B 总参/55B 激活的超大 MoE，当前社区可获取的最大开放模型之一
- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — 作者: deepseek-ai | ❤️ 1,421 | ⬇️ 3,436,213 — V4 高效版，推理速度更快，适合大规模部署

### 🎨 多模态与生成（图像、视频、音频、文本到 X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 作者: nvidia | ❤️ 1,460 | ⬇️ 111,078 — 通用视觉定位模型，根据文字指令在图像中精确圈出目标，填补开放词表定位空白
- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — 作者: google | ❤️ 622 | ⬇️ 315,131 — 首个“any-to-any”多模态模型，可同时理解和生成文本、图像等
- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** — 作者: google | ❤️ 380 | ⬇️ 84,549 — Gemma-4 基础版，为多模态理解与生成提供强大基座
- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — 作者: ideogram-ai | ❤️ 311 | ⬇️ 2,818 — 第四代图像生成模型 FP8 精度版，画质与推理效率均衡
- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — 作者: ideogram-ai | ❤️ 214 | ⬇️ 2,671 — 4-bit NF4 量化版，进一步降低显存占用
- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — 作者: stepfun-ai | ❤️ 343 | ⬇️ 38,716 — 阶跃星辰的多模态模型 Flash 版，快速支持图文理解任务
- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** — 作者: nvidia | ❤️ 183 | ⬇️ 24,820 — Cosmos3 世界模型系列的小型版，适用于场景理解与生成
- **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)** — 作者: nvidia | ❤️ 149 | ⬇️ 20,403 — 世界模型 Super 版，建模与生成能力更强
- **[nvidia/Cosmos3-Super-Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)** — 作者: nvidia | ❤️ 120 | ⬇️ 1,634 — 基于世界模型的文本到图像生成，一致性与细节优秀
- **[nvidia/Cosmos3-Super-Image2Video](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video)** — 作者: nvidia | ❤️ 111 | ⬇️ 1,295 — 图生视频模型，将静态图转化为连贯视频
- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** — 作者: nvidia | ❤️ 312 | ⬇️ 972 — 扩散模型超分辨率模型，常用于图像修复与放大
- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — 作者: ByteDance | ❤️ 151 | ⬇️ 223 — 图像+文本到视频渲染模型，可将描述转化为动态视频
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — 作者: SulphurAI | ❤️ 1,581 | ⬇️ 1,704,964 — 基于 LTX-2.3 的文本到视频模型，高赞高下载，视频生成新星
- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** — 作者: meituan-longcat | ❤️ 526 | ⬇️ 1,806 — 音频/文本驱动的数字人生成模型，支持表情与动作同步
- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — 作者: google | ❤️ 111 | ⬇️ 9,394 — 实时音乐生成模型，支持交互式创作与低延迟伴奏

### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — 作者: sapientinc | ❤️ 712 | ⬇️ 161,627 — 人力资源管理场景专用文本生成模型，1B 轻量高效
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — 作者: nvidia | ❤️ 221 | ⬇️ 1,380 — 流式语音识别模型，0.6B 超低延迟，即输即转写
- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — 作者: bosonai | ❤️ 156 | ⬇️ 2,184 — 基于 Qwen3 的文本到语音模型，4B 参数，自然度高
- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** — 作者: PaddlePaddle | ❤️ 258 | ⬇️ 8,365 — 视觉语言 OCR 模型，检测与识别一体，实用性强
- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** — 作者: MisoLabs | ❤️ 131 | ⬇️ 0 — 新开源 TTS 模型，专注语音合成，模型文件尚未开放但已获关注

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — 作者: unsloth | ❤️ 423 | ⬇️ 458,174 — 为 Gemma-4-12B-it 提供的 GGUF 量化版，大幅降低推理门槛
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 作者: HauhauCS | ❤️ 1,491 | ⬇️ 2,771,843 — 社区微调的无审查版 Qwen3.6 MoE（带视觉），GGUF 量化后爆红
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — 作者: nvidia | ❤️ 198 | ⬇️ 1,015,381 — NVIDIA ModelOpt 混合精度量化 Qwen3.6 MoE，质量损失小，显存占用低
- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** — 作者: nvidia | ❤️ 119 | ⬇️ 17,225 — 550B 超大 MoE 的 NVFP4 量化版，使超大模型部署更可行

---

## 生态信号

本周榜单突出几大信号：**DeepSeek-V4** 系列稳居人气巅峰，证明开源前沿大模型仍是社区最大流量保证；**NVIDIA** 以 LocateAnything、Cosmos3 和 Nemotron-3 形成多模态与超大规模矩阵，全面布局；社区微调需求强劲（Qwen3.6 Uncensored 近 300 万下载），量化工具（GGUF、NVFP4）紧跟新模型发布，用户部署成本持续下降；**视频生成模型**（Sulphur-2、LongCat）开始成为每周榜单常客。整体来看，“多模态 + MoE + 量化”已成为当前模型生态的核心增长点。

---

## 值得探索

1. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 本周最强大语言模型，几乎无可争议，适合作为通用基座深入测试。
2. **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — 视频生成新星，社区赞数 1,581，演示效果惊艳，是探索文本到视频的极佳入口。
3. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 开放式定位模型，结合视觉与语言指令，应用前景广阔（自动驾驶、机器人等），值得提前上手。

让这些模型成为你本周研究的起点！

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*