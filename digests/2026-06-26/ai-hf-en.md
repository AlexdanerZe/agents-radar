# Hugging Face Trending Models Digest 2026-06-26

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-26 03:23 UTC

---

Here is the structured **Hugging Face Trending Models Digest** for the week of **June 26, 2026**.

---

## 🗞️ Today's Highlights

The open-weight ecosystem is experiencing a tectonic shift this week, anchored by **DeepSeek-V4-Pro** (5,063 likes), which has become the undeniable center of gravity for conversational MoE models and looks to be defining a new generation of benchmarks. Simultaneously, the **Gemma 4** family has formed an entire sub-ecosystem within the Hub: the official “any-to-any” release by Google is generating a wave of specialized community fine-tunes and quantizations, most notably **yuxinlu1’s coder variant** and **huihui-ai’s abliterated** version, signaling an explosion of localized, unrestricted model usage. The **Qwen 3.5/3.6 lineage** continues to fuel massive download figures through uncensored variants (HauhauCS) and enterprise-grade quantizations (NVIDIA NVFP4). Finally, smaller specialized models like **NVIDIA’s LocateAnything-3B** and **MiniMax-M3** highlight a rapidly maturing market for precise, task-specific vision and reasoning rather than brute-force scaling.

---

## 📈 Trending Models

### 🧠 Language Models

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai, 5,063 likes, 1.8M downloads. The week’s flagship MoE conversational model, representing a significant generational leap in the DeepSeek lineage.
- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org, 2,488 likes, 67k downloads. Zhipu AI’s massive new MoE—trending for its strong multilingual dialogue capabilities and unique DSA architecture.
- **[Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — Qwen, 249 likes, 3k downloads. A purpose-built MoE for agentic and tool-use workflows, blending vision and structured reasoning.
- **[FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — microsoft, 345 likes, 5k downloads. Microsoft’s compact 4B parameter model, optimized for long-context retrieval and agentic sub-tasks.
- **[DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** — Chunjiang-Intelligence, 94 likes, 646 downloads. A specialized DeepSeek-V4 fine-tune targeting cybersecurity analysis and defensive reasoning.
- **[LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** — LiquidAI, 76 likes, 7k downloads. Liquid AI’s ultra-small 230M parameter foundation model, proving that strong performance can fit in a very small footprint.

### 🎨 Multimodal & Generation

- **[Gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — google, 1,179 likes, 2.1M downloads. Google’s groundbreaking “any-to-any” unified model that serves as the backbone for the entire thriving Gemma 4 community ecosystem.
- **[LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia, 2,365 likes, 407k downloads. NVIDIA’s high-precision visual grounding model, a massive hit for open-set object detection and image feature extraction.
- **[MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — MiniMaxAI, 1,241 likes, 154k downloads. MiniMax’s latest multimodal vision-language model, widely adopted for its strong generalist image understanding.
- **[Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu, 900 likes, 70k downloads. Baidu’s best-in-class optical character recognition model, setting a new standard for document digitization workflows.
- **[Nemotron-3.5-ASR-Streaming-0.6B](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia, 695 likes, 50k downloads. A lightweight streaming ASR model optimized for real-time voice interfaces and cache-aware inference.
- **[Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea, 245 likes, 2k downloads. The accelerated text-to-image generation model from Krea, offering fast iteration on high-quality outputs.
- **[Krea-2-Raw](https://huggingface.co/krea/Krea-2-Raw)** — krea, 185 likes, 5k downloads. The base raw weights for the Krea-2 ecosystem, giving advanced users fine-grained control over generation.
- **[Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** — owensong, 201 likes, 0 downloads. An ultra-small text-to-speech model pushing efficient on-device voice synthesis.
- **[Lift](https://huggingface.co/datalab-to/lift)** — datalab-to, 152 likes, 5k downloads. A Qwen3.5-based document visual understanding model built for complex PDF and form extraction.
- **[Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)** — Boogu, 124 likes, 824 downloads. A Diffusers-native model specialized in instruction-based image editing.
- **[Comfy-Org/Krea-2](https://huggingface.co/Comfy-Org/Krea-2)** — Comfy-Org, 121 likes, 10 downloads. The official ComfyUI integration node connecting the Krea-2 model family to a visual workflow interface.

### 🔧 Specialized Models

- **[gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1, 2,367 likes, 495k downloads. The definitive open-weight code generation fine-tune for the Gemma 4 family, dominating local coding deployments.
- **[gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1, 622 likes, 165k downloads. A specialized GGUF variant focused on terminal-based agentic coding and tool-calling workflows.
- **[Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai, 992 likes, 502k downloads. Moonshot AI’s compressed vision-code model, quietly revolutionizing how coding assistants understand visual context.
- **[VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — WeiboAI, 716 likes, 51k downloads. A compact 3B reasoning model that punches far above its weight class, specifically tuned for mathematical problem-solving.

### 📦 Fine-tunes & Quantizations

- **[Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS, 2,239 likes, 3.5M downloads. The most downloaded uncensored Qwen 3.6 MoE this week, driving a huge wave of local, unrestricted deployment.
- **[Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — nvidia, 343 likes, 4.6M downloads. NVIDIA’s official NVFP4 quantization, offering top-tier performance-per-bit on Hopper GPUs and dominating the high-efficiency quantization charts.
- **[GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — unsloth, 387 likes, 88k downloads. Unsloth’s expertly optimized GGUF conversion of the massive GLM-5.2, democratizing its use on consumer hardware.
- **[Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai, 495 likes, 134k downloads. A highly stylized “mythos” reasoning fine-tune of Qwen3.5, widely adopted for creative writing and narrative roleplay.
- **[Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — empero-ai, 394 likes, 10k downloads. The full-precision transformers version of the popular Qwythos creative reasoning fine-tune chain.
- **[Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)** — HauhauCS, 83 likes, 15k downloads. An innovative QAT-trained GGUF of an uncensored Gemma 4, pushing accuracy retention in quantized formats.
- **[Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai, 100 likes, 0 downloads. A brand new 35B base model launched directly into the GGUF ecosystem, bypassing full-precision release entirely.
- **[Huihui-gemma-4-12B-coder-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)** — huihui-ai, 127 likes, 4k downloads. The abliterated variant of the popular Gemma 4 coder, removing safety alignment for unrestricted code generation.
- **[Qwopus3.6-27B-Coder-Compat-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)** — Jackrong, 89 likes, 19k downloads. A MTP-compatible Qwen 3.6 vision model quantized for local coder environments.

---

## 📊 Ecosystem Signal

The ecosystem is undergoing a definitive architectural pivot towards **Mixture-of-Experts** (MoE) models. DeepSeek-V4-Pro, the Qwen 3.6 MoE family, and GLM-5.2 all leverage this design, and the community has responded overwhelmingly with quantized GGUF and NVFP4 variants to make them consumable. Open-weight models, especially from the **Qwen** and **Gemma** families, are fueling a virtuous cycle of fine-tuning and uncensored “abliteration.” The **uncensored model movement** has become a massive stable sub-trend rather than a niche, driven largely by HauhauCS and huihui-ai’s relentless output. Quantization formats are diversifying: **GGUF** is the universal standard for local POC use, while **NVIDIA’s NVFP4** is emerging as the format of choice for production Hopper clusters. A significant trend is the **proliferation of small, task-specific models** (VibeThinker-3B, FastContext-4B, LocateAnything-3B, Nemotron-ASR-0.6B). The community is maturing beyond brute-force scaling and actively seeking optimized, efficient weights for retrieval, coding, vision, and speech tasks.

---

## 💡 Worth Exploring

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — This model is a must-try for any computer vision pipeline. Its massive popularity (2,365 likes) and low latency make it the best open-weight solution for granular visual grounding, filling a critical “Swiss Army knife” role for object localization.
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — A fascinating study in efficient model design. The combination of compressed tensors, vision input, and strong coding performance represents the cutting edge of multi-modal code agents without requiring a massive parameter count.
- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — A sleeper hit for RAG and agentic system builders. Its 4B size combined with optimized SFT for extremely long contexts makes it an ideal and cost-effective backbone for retrieval-augmented inference and tool-calling loops.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*