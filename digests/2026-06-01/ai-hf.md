# Hugging Face 热门模型日报 2026-06-01

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-01 03:42 UTC

---

# Hugging Face 热门模型日报（2026-06-01）

## 📌 今日速览
- **DeepSeek V4 双星登顶**：DeepSeek-V4-Pro 以 4503 赞拿下总量第一，Flash 版也收获 1323 赞，开源 LLM 持续领跑。
- **阿里 Qwen3.6 视觉语言模型生态爆发**：Qwen3.6-27B 官方模型获 1553 赞，社区围绕它孵化了 uncensored、GGUF、NVFP4 等大量衍生版本，形成最活跃的生态。
- **OpenAI 意外开源 `privacy-filter`**：该模型（1573 赞）专注于隐私信息识别与过滤，是企业级安全刚需，成为本周最大黑马。
- **视频与图像生成持续高热**：Anima（1610 赞）和 Sulphur-2-base（1473 赞）分别代表文生图与文生视频两类应用，多模态创作模型用户热情不减。
- **小模型与 MoE 趋势强劲**：MiniCPM5-1B、LFM2.5-8B-A1B、tencent Hy-MT2-1.8B 等高效模型获得大量点赞，兼顾性能与部署成本。

## 🧠 语言模型（LLM、对话、翻译）
- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**（deepseek-ai | 👍4,503 | 📥5,886,599）— 本周最热门模型，DeepSeek 第四代旗舰，能力与开源权重并重，覆盖对话与生成。
- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**（deepseek-ai | 👍1,323 | 📥3,483,641）— V4 轻量版本，推理速度更快，适合生产环境部署。
- **[tencent/Hy-MT2-1.8B](https://huggingface.co/tencent/Hy-MT2-1.8B)**（tencent | 👍1,094 | 📥17,471）— 腾讯高效翻译模型，1.8B 参数平衡速度与质量，获得高赞。
- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)**（openbmb | 👍661 | 📥36,730）— OpenBMB 轻量级 1B 语言模型，适合端侧部署。
- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)**（LiquidAI | 👍323 | 📥27,677）— 高效 MoE 模型，8B 参数仅激活 1B，边缘计算新秀。
- **[tencent/Hy-MT2-30B-A3B](https://huggingface.co/tencent/Hy-MT2-30B-A3B)**（tencent | 👍440 | 📥4,226）— 腾讯 MoE 翻译模型，30B 参数激活 3B，专攻高精度翻译。
- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)**（sapientinc | 👍429 | 📥143,904）— 面向人力资源管理场景的专用文本生成模型，企业 AI 需求体现。

## 🎨 多模态与生成（图像、视频、音频、文本到 X）
- **[circlestone-labs/Anima](https://huggingface.co/circlestone-labs/Anima)**（circlestone-labs | 👍1,610 | 📥756,861）— 文生图扩散模型，在 ComfyUI 社区极受欢迎。
- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)**（Qwen | 👍1,553 | 📥5,064,096）— 阿里最新视觉语言模型，综合能力强大，VLM 领域标杆。
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**（SulphurAI | 👍1,473 | 📥1,590,236）— 文生视频基础模型，下载量超 150 万，视频生成赛道主力。
- **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)**（openbmb | 👍1,084 | 📥444,679）— MiniCPM 多模态最新版，性能跃升，吸引大量开发者。
- **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)**（bytedance-research | 👍993 | 📥2,948）— 字节跳动 Any-to-Any 全模态模型，同时支持图像、视频、音频生成。
- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)**（Supertone | 👍754 | 📥56,472）— 高音质 TTS 模型，语音合成质量领先，受创作者青睐。
- **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)**（NemoStation | 👍472 | 📥16,277）— 基于 Qwen3.5 的视频理解模型，支持视频输入问答。
- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)**（meituan-longcat | 👍441 | 📥0）— 美团数字人视频生成模型，支持音频/文本驱动，新发布即受关注。
- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)**（stepfun-ai | 👍162 | 📥7,638）— StepFun 推出的快速 VLM，兼顾性能与推理速度。
- **[microsoft/Lens](https://huggingface.co/microsoft/Lens)**（microsoft | 👍149 | 📥1,959）— 微软文生图扩散模型，科研社区持续关注。
- **[OpenMOSS-Team/MOSS-TTS-v1.5](https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5)**（OpenMOSS-Team | 👍83 | 📥14,272）— MOSS 团队中文 TTS，开源语音合成新选择。

## 🔧 专用模型（OCR、安全、特征提取、工具）
- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)**（openai | 👍1,573 | 📥306,344）— OpenAI 开源的隐私信息过滤模型（token 分类），填补 AI 安全工具空白。
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**（nvidia | 👍620 | 📥24,586）— Nvidia 零样本跨模态特征定位模型，适用开放目标检测与分割。
- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**（froggeric | 👍469 | 📥0）— 修复 Qwen 系列聊天模板的社区工具，解决兼容性问题，被广泛引用。
- **[numind/NuExtract3](https://huggingface.co/numind/NuExtract3)**（numind | 👍208 | 📥57,248）— 基于视觉语言模型的文档信息提取工具，专精结构化数据抽取。
- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)**（nvidia | 👍220 | 📥498）— Nvidia 扩散超分辨率模型，研究社区认可度高。
- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)**（PaddlePaddle | 👍118 | 📥2,731）— PaddleOCR 多模态视觉语言模型 v1.6，OCR 与文档理解专用。

## 📦 微调与量化（社区优化、GGUF、NVFP4）
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**（HauhauCS | 👍1,164 | 📥2,439,402）— Qwen3.6 MoE 的去审查 + 激进风格微调版，下载量巨大，反映定制化需求。
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**（unsloth | 👍578 | 📥926,440）— Unsloth 优化的多令牌预测 GGUF 量化版，近乎百万下载。
- **[Jackrong/Qwopus3.6-27B-v2-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-GGUF)**（Jackrong | 👍190 | 📥37,241）— Qwen3.6 的社区 GGUF 版本，适配 llama.cpp 本地推理。
- **[Jackrong/Qwopus3.6-27B-v2-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)**（Jackrong | 👍178 | 📥124,807）— 加入 MTP 优化的 GGUF 版，兼顾性能与容量。
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)**（nvidia | 👍94 | 📥105,608）— 基于 Nvidia ModelOpt 的 4-bit NVFP4 量化版，显著降低显存占用。
- **[LiquidAI/LFM2.5-8B-A1B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B-GGUF)**（LiquidAI | 👍133 | 📥41,828）— LFM2.5 的 GGUF 量化版，推动 MoE 模型本地部署。

## 🌐 生态信号
1. **模型家族势头**：DeepSeek V4、Qwen3.6、tencent Hy-MT2、MiniCPM 四个系列成为本周最活跃的模型家族，覆盖从语言、翻译到视觉语言的全场景。其中 Qwen3.6 社区衍生版超过 5 个，生态丰富度最高。  
2. **开源权重继续主导**：虽然业界存在闭源压力，但本周 Top30 中绝大多数模型（包括 DeepSeek、Qwen、MiniCPM，甚至 OpenAI）均提供了可用权重，强调可复现性与社区共建。  
3. **量化与微调活动白热化**：几乎所有热门基础模型（Qwen3.6、LFM2.5）都同步有 GGUF 或 NVFP4 量化版，且 uncensored 等风格微调下载量极高，显示出社区对模型定制化与本地高效推理的强烈需求。  
4. **MoE + 小模型成为效率标配**：LFM2.5-8B-A1B、Hy-MT2-30B-A3B、Qwen3.6-35B-A3B 等 MoE 模型在保持能力的同时大幅降低计算成本，是边缘部署与实时应用的首选方向。

## 🔍 值得探索
1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 本周最强开源 LLM，在多种基准上表现突出，适合作为通用对话与推理的基座模型，也是评估其他模型的起点。  
2. **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — 当前最值得尝试的开源视觉语言模型，支持图文理解与生成，覆盖自动驾驶、文档分析等场景，且社区对其量化版本支持极好。  
3. **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** — OpenAI 罕见开源的安全类模型，专注于隐私实体识别，对于构建合规 AI 应用具有示范意义，值得研究其架构与微调方法。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*