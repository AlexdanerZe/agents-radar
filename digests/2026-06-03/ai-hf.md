# Hugging Face 热门模型日报 2026-06-03

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-03 03:46 UTC

---

好的，以下是基于 2026 年 6 月 3 日 Hugging Face 趋势榜生成的模型日报。

---

# 🤗 Hugging Face 热门模型日报 | 2026-06-03

## 今日速览

本周 Hugging Face 热度由 DeepSeek V4 双核统治—**DeepSeek-V4-Pro** 以 4,577 赞高居榜首，**DeepSeek-V4-Flash** 紧随其后，表明开源语言模型仍是最强流量入口。**Qwen3.6** 系列生态爆发：基础版 **Qwen3.6-27B** 下载超 520 万，社区围绕其推出了量化和 uncensored 版本（HauhauCS、unsloth、Jackrong 等），形成日榜中最大的微调集群。nVIDIA 密集部署多模态阵地，一次性发布 **LocateAnything-3B、PiD、Cosmos3** 家族（Nano、Super、Image2Video 等），覆盖定位、超分、视频生成全链路。视频与音频生成同样火热：**bytedance-research/Lance** 支持任意模态互转、**meituan-longcat** 推出数字人视频生成、**Sulphur-2** 基于 LTX 实现高质量文生视频。工具类模型 **openai/privacy-filter** 快速爬升，反映行业对安全过滤层的刚需。量化与低比特探索持续深化，Ternary 1.58-bit 的 **bonsai** 和 nVIDIA 的 **NVFP4** 代表了两种不同的效率路径。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

1. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
   作者：deepseek-ai | 👍 4,577 | 📥 5,829,042  
   全新第四代 DeepSeek 旗舰对话模型，本日最高赞，延续 MoE 路线，在推理与对话上取得显著突破。

2. **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**  
   作者：deepseek-ai | 👍 1,368 | 📥 3,525,218  
   V4 系列的高效快速变体，采用 MIT 许可，推理速度与生成质量平衡出色，吸引了大量社区试用。

3. **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)**  
   作者：openbmb | 👍 737 | 📥 57,683  
   仅有 1B 参数的最新边缘端语言模型，延续 MiniCPM 家族高效路线，适合移动端和低算力部署。

4. **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)**  
   作者：LiquidAI | 👍 444 | 📥 47,742  
   Liquid 第二代 MoE 模型（8B 总参，1B 激活），专注高效推理，是液态网络架构在文本生成领域的最新实践。

5. **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)**  
   作者：JetBrains | 👍 142 | 📥 799  
   面向深度推理的 MoE 模型，12B 总参仅 2.5B 激活，号称多步推理能力强，是 IDE 厂商入局 LLM 的尝试。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)**  
   作者：Qwen | 👍 1,579 | 📥 5,243,648  
   Qwen3.6 系列原版视觉语言模型，支持图像+文本输入，是同期下载量最高的多模态基础模型。

2. **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)**  
   作者：bytedance-research | 👍 1,013 | 📥 3,192  
   字节跳动发布的全能多模态模型，支持任意模态输入输出（图像、视频、音频、文本），统一框架引人瞩目。

3. **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)**  
   作者：Supertone | 👍 782 | 📥 59,026  
   最新文本语音合成模型，音质自然度高，支持多说话人风格，在语音合成赛道快速升温。

4. **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)**  
   作者：NemoStation | 👍 498 | 📥 17,616  
   专为视频理解设计的 2B MoE 模型（基于 Qwen3.5 架构），擅长视频+文本联合任务，适合视频问答。

5. **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)**  
   作者：meituan-longcat | 👍 493 | 📥 174  
   美团发布的数字人视频生成模型，支持音频/图像/文本驱动，打造虚拟人播报。

6. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
   作者：nvidia | 👍 1,001 | 📥 61,604  
   nVIDIA 推出的细粒度视觉定位模型，可识别并定位图中任意物体，通用性强。

7. **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)**  
   作者：stepfun-ai | 👍 217 | 📥 12,932  
   阶跃星辰的轻量视觉语言模型，主打快速推理，适合端侧视觉应用。

8. **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)**  
   作者：nvidia | 👍 115 | 📥 9,071  
   Cosmos3 系列最小版本，面向全模态理解的轻量模型。

9. **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)**  
   作者：nvidia | 👍 100 | 📥 2,830  
   Cosmos3 系列高性能版本，支撑图像/视频/文本等多种任务，属于系列基石模型。

10. **[nvidia/Cosmos3-Super-Image2Video](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video)**  
    作者：nvidia | 👍 84 | 📥 536  
    Cosmos3 家族中的图生视频专用模块，输入单图即可生成动态视频。

11. **[nvidia/Cosmos3-Super-Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)**  
    作者：nvidia | 👍 80 | 📥 517  
    Cosmos3 家族中的文生图模块，与 Super 系列其他组件配合形成完整多模态管线。

12. **[nvidia/PiD](https://huggingface.co/nvidia/PiD)**  
    作者：nvidia | 👍 268 | 📥 646  
    nVIDIA 最新图像超分辨率扩散模型，恢复高质量细节，适合图像修复与增强。

13. **[Kwai-Keye/Keye-VL-2.0-30B-A3B](https://huggingface.co/Kwai-Keye/Keye-VL-2.0-30B-A3B)**  
    作者：Kwai-Keye | 👍 100 | 📥 964  
    快手开源视觉语言模型，30B 总参、3B 激活的 MoE，特征提取能力强，支持多模态理解。

14. **[OpenMOSS-Team/MOSS-TTS-v1.5](https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5)**  
    作者：OpenMOSS-Team | 👍 123 | 📥 20,615  
    中文 TTS 专用模型，基于 delay 解码架构，发音自然，支持长文本合成。

### 🔧 专用模型（代码、数学、医疗、嵌入、OCR、安全）

1. **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)**  
   作者：openai | 👍 1,595 | 📥 300,247  
   OpenAI 开源的隐私过滤模型，基于 token 分类检测敏感信息，可集成到 pipeline 中，安全方向标杆。

2. **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)**  
   作者：sapientinc | 👍 477 | 📥 153,029  
   专为人力资源管理场景训练的 1B 语言模型，覆盖招聘、入离职等业务流程，垂直领域受关注。

3. **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)**  
   作者：PaddlePaddle | 👍 190 | 📥 4,003  
   百度飞桨最新 OCR 视觉语言模型，融合 ERNIE 4.5 能力，端到端图文识别新高度。

### 📦 微调与量化（社区微调、GGUF、AWQ、NVFP4、Ternary）

1. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
   作者：HauhauCS | 👍 1,287 | 📥 2,573,320  
   基于 Qwen3.6 MoE 的 uncensored 社区微调版（AGG 风格），并以 GGUF 格式发布，MMLU 上表现激进，下载量极高。

2. **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**  
   作者：unsloth | 👍 610 | 📥 982,631  
   Unsloth 出品的 Qwen3.6-27B 量化版（GGUF），支持多令牌预测（MTP），高效推理体验。

3. **[LiquidAI/LFM2.5-8B-A1B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B-GGUF)**  
   作者：LiquidAI | 👍 162 | 📥 70,865  
   官方发布的 LFM2.5 MoE 模型 GGUF 量化版本，针对 llama.cpp 优化，边缘端部署首选。

4. **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)**  
   作者：nvidia | 👍 139 | 📥 313,480  
   nVIDIA 使用 ModelOpt 工具对 Qwen3.6 MoE 进行 NVFP4 量化，4 bit 浮点，下载量已超 31 万。

5. **[Jackrong/Qwopus3.6-27B-v2-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)**  
   作者：Jackrong | 👍 197 | 📥 155,959  
   社区制作的 Qwen3.6-27B 变体 + MTP + GGUF 量化，强调长上下文推理性能。

6. **[stepfun-ai/Step-3.7-Flash-GGUF](https://huggingface.co/stepfun-ai/Step-3.7-Flash-GGUF)**  
   作者：stepfun-ai | 👍 95 | 📥 39,258  
   Step 3.7 Flash 的 GGUF 官方量化版，支持 imatrix 和 MoE 架构，本地运行视觉模型的门槛进一步降低。

7. **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
   作者：SulphurAI | 👍 1,513 | 📥 1,663,826  
   基于 Lightricks/LTX-2.3 微调/量化的文生视频模型，支持 GGUF，以高质量输出斩获超过 166 万下载。

8. **[prism-ml/bonsai-image-ternary-4B-gemlite-2bit](https://huggingface.co/prism-ml/bonsai-image-ternary-4B-gemlite-2bit)**  
   作者：prism-ml | 👍 101 | 📥 41  
   采用 1.58-bit Ternary 极低量化的文生图模型（4B 参数），存储极限压缩，技术尝鲜意义强。

## 生态信号

- **DeepSeek V4 与 Qwen3.6 双王并列**：DeepSeek-V4 系列凭借硬核推理与 MIT 许可成为本周绝对焦点；Qwen3.6 则依靠庞大的社区微调与量化版本来释放长尾需求，二者分别代表了“高质量基础模型”和“开放生态衍生”两种路线。
- **nVIDIA 全线出击**：从视觉定位（LocateAnything）到超分（PiD），再到全模态 Cosmos3 家族，nVIDIA 在 Hugging Face 上形成了最强多模态矩阵，且全部开源权重，明显加速了从研究到落地的步伐。
- **视频/音频生成快速工业化**：Lance（any-to-any）、Sulphur-2、LongCat 等模型覆盖从数字人到通用视频生成，低门槛工具逐渐成熟，同时量化版本（GGUF）使得消费级 GPU 运行视频模型成为可能。
- **量化新范式涌现**：GGUF 仍是社区主流，但 NVFP4（nVIDIA）和 Ternary（bonsai）分别从浮点离群值优化和极低比特切入，预示着下一阶段推理效率的多元竞争。
- **开源安全层稀缺**：OpenAI 的 privacy-filter 高赞说明即使是头部厂商也缺少可部署的过滤模型，该领域仍有较大空间。

## 值得探索

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
   不同于一般视觉语言模型，它专门为“定位”任务优化，可替代传统的目标检测+描述两阶段流程，是视觉 agent 的重要基础组件。

2. **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)**  
   “任意模态到任意模态”的统一框架，目前开源模型中极罕见的设计。如果你想探索下一代多模态基础模型架构，Lance 是最前沿的代表。

3. **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
   基于 LTX-2.3 的高质量文生视频模型，同时提供 GGUF 格式，可在本地显卡上运行。对于想快速体验开授权视频生成的用户来说，当前性价比很高。

4. **[prism-ml/bonsai-image-ternary-4B-gemlite-2bit](https://huggingface.co/prism-ml/bonsai-image-ternary-4B-gemlite-2bit)**  
   1.58-bit 的生成模型是极低比特量化的标杆实验，虽然目前下载量低，但它是未来边缘端生成的重要组成部分，值得技术关注。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*