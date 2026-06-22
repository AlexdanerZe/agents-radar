# Hugging Face Trending Models Digest 2026-06-22

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-22 03:54 UTC

---

## 1. Today's Highlights

This week marks a decisive victory for Mixture-of-Experts architectures, with nearly every frontier release—DeepSeek-V4 Pro, Qwen3.6-35B, GLM-5.2, and Gemma-4—relying on sparse activation to push the compute-performance frontier. Multimodality has become the new baseline: Google's novel DiffusionGenma and "any-to-any" Gemma-4 signal that text-only models are rapidly becoming legacy. The local inference war is also escalating sharply, with advanced GGUF quantizations introducing Multi-Token Prediction and specialized pruning (MTP, pi-tune) to wring maximum speed from consumer hardware. Finally, the insatiable demand for uncensored and roleplay-tuned models persists, with the HauhauCS Qwen3.6 fine-tune attracting nearly 4 million downloads in a single week.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

**[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**
Author: deepseek-ai | Likes: 4,999 | Downloads: 2,611,991
The undisputed frontier leader this week, this MoE flagship pushes open-weight reasoning and coding benchmarks to new heights, setting the standard the rest of the ecosystem must chase.

**[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
Author: zai-org | Likes: 1,848 | Downloads: 27,413
Zhipu AI's latest MoE entry featuring the novel DSA architecture, gaining rapid traction as a premier bilingual (CN/EN) conversational model.

**[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**
Author: CohereLabs | Likes: 475 | Downloads: 19,551
A compact MoE code generation model from Cohere, carving out a niche as an efficient, domain-specific alternative for developer workflows.

**[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**
Author: microsoft | Likes: 267 | Downloads: 2,593
Microsoft's explicit foray into long-context agentic exploration ("Explorer SubAgent"), signaling deep institutional investment in models that combine extended reasoning trajectories with tool use.

**[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**
Author: nex-agi | Likes: 343 | Downloads: 7,872
A polished community fine-tune of Qwen3.5 MoE optimized for advanced agentic instructions, illustrating the growing premium market for refined inference-tier model releases.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

**[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**
Author: Qwen | Likes: 2,198 | Downloads: 5,148,673
The **most downloaded model** across the entire Hub this week, setting the community standard for open-weight VLMs by combining 35B total parameters with only 3B active for remarkable efficiency.

**[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**
Author: google | Likes: 1,129 | Downloads: 1,815,370
Google's unified "any-to-any" reasoning model for the Gemma family, trending for its seamless processing of text and images within a single MoE framework.

**[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**
Author: MiniMaxAI | Likes: 1,177 | Downloads: 104,076
A flagship VLM from MiniMax with deep image understanding integrated into conversational generation, solidifying the company's position in the top tier of multimodal open releases.

**[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
Author: HauhauCS | Likes: 2,082 | Downloads: 3,966,691
A radically fine-tuned, uncensored variant of Qwen3.6-35B that has become a viral phenomenon for creative writing and roleplay, proving massive demand for minimal refusal behavior in a high-efficiency MoE package.

**[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**
Author: moonshotai | Likes: 946 | Downloads: 363,308
A multimodal coding pioneer utilizing compressed tensors for efficient image-to-code generation, uniquely positioned for UI-to-code and visual programming tasks.

**[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
Author: nvidia | Likes: 2,248 | Downloads: 241,845
NVIDIA's hyper-specialized visual grounding model for precise object localization, attracting massive traction in robotics and computer vision for its targeted efficiency.

**[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**
Author: google | Likes: 1,037 | Downloads: 762,861
A groundbreaking diffusion-native language model that generates and understands images directly within the generative process, signaling a potential paradigm shift beyond next-token prediction.

**[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**
Author: nvidia | Likes: 613 | Downloads: 27,275
A small, cache-aware streaming ASR model optimized for real-time speech recognition on edge devices and low-latency voice pipelines.

**[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)**
Author: owensong | Likes: 155 | Downloads: 0
An ultra-compact TTS model pushing the boundaries of on-device speech synthesis for wearables and IoT, highlighting the drive toward tiny, specialized assistants.

**[datalab-to/lift](https://huggingface.co/datalab-to/lift)**
Author: datalab-to | Likes: 110 | Downloads: 516
A fine-tuned VLM on the Qwen3.5 base specifically designed for PDF and document understanding, riding the wave of enterprise demand for reliable structured data extraction.

**[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)**
Author: lordx64 | Likes: 145 | Downloads: 3,351
A community-driven VLM adaptation of the Qwen3.5 MoE, demonstrating the thriving ecosystem of modality-specific fine-tuning around strong base architectures.

**[ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora)**
Author: ostris | Likes: 91 | Downloads: 2,452
A community LoRA adapter accelerating Ideogram 4 inference, reflecting the prolific fine-tuning culture within the text-to-image generation community.

**[Boogu/Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)**
Author: Boogu | Likes: 84 | Downloads: 374
An open-source diffusion model for instruction-based image editing, generating early excitement for its potential to democratize precise image manipulation.

### 🔧 Specialized Models (code, math, medical, embeddings)

**[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)**
Author: WeiboAI | Likes: 565 | Downloads: 20,277
A compact reasoning and math LLM punching far above its weight class, attracting strong interest for chain-of-thought problem-solving in a small footprint.

**[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)**
Author: LiquidAI | Likes: 93 | Downloads: 7,726
Liquid AI's latest embedding model optimized for RAG and semantic search, delivering high retriever precision in a remarkably efficient 350M-parameter package.

**[poolside/Laguna-M.1](https://huggingface.co/poolside/Laguna-M.1)**
Author: poolside | Likes: 84 | Downloads: 2,580
Poolside's dedicated LLM for agentic software engineering, optimized for vLLM/SGLang, and representing the sharp end of specialization in developer tooling infrastructure.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

**[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**
Author: yuxinlu1 | Likes: 2,094 | Downloads: 358,677
The premier GGUF quantization of a fine-tuned Gemma-4 coder, exploding in popularity for enabling state-of-the-art local code generation on consumer GPUs.

**[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**
Author: yuxinlu1 | Likes: 289 | Downloads: 21,730
An agentic-optimized companion to the coder variant, tailored for terminal and autonomous task execution, epitomizing the "agent in a box" GGUF trend.

**[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)**
Author: unsloth | Likes: 229 | Downloads: 32,260
Unsloth's highly efficient GGUF conversion of GLM-5.2, making Zhipu's MoE accessible to the local inference ecosystem with drastically reduced memory requirements.

**[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)**
Author: zai-org | Likes: 123 | Downloads: 217,361
The official FP8 quantized variant of GLM-5.2, offering an optimized balance between deployment efficiency and high-fidelity performance for production environments.

**[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**
Author: Jackrong | Likes: 276 | Downloads: 190,993
A GGUF quantization of a Qwen3.6 coding MoE incorporating Multi-Token Prediction, driving significant downloads as users prioritize inference speed for coding workflows.

**[bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)**
Author: bytkim | Likes: 102 | Downloads: 36,421
An innovative GGUF quant combining MTP with "pi-tune" optimizations, reflecting the community's relentless pursuit of improving inference throughput on MoE models.

**[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)**
Author: Mia-AiLab | Likes: 121 | Downloads: 22,879
A community fine-tune targeting specific roleplay and generation traits on the Qwen3.6 base, demonstrating the deep local customization culture.

**[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)**
Author: unsloth | Likes: 151 | Downloads: 42,837
Unsloth's efficient GGUF quantization of the Kimi-K2.7-Code multimodal model, extending the reach of visual code generation to local inference environments.

**[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**
Author: empero-ai | Likes: 77 | Downloads: 688
A niche "persona merge" GGUF blending Claude's stylistic output with a Qwen3.5 base, representing the flourishing subculture of stylistic merges and alignment relaxation.

---

## 3. Ecosystem Signal

This week’s rankings confirm several structural shifts. **MoE is the consensus standard**: every major foundation release (DeepSeek-V4 Pro, Qwen3.6, GLM-5.2, Gemma-4) relies on sparse activation, cementing the architecture as the default path to maximizing capability per compute unit. **Multimodality is now the baseline expectation**: the success of Qwen3.6-35B, DiffusionGenma, and Gemma-4 shows users demand native vision and language understanding; text-only releases are rapidly becoming a niche.

The **local inference optimization race** is intensifying sharply. Beyond standard GGUF, advanced techniques like Multi-Token Prediction (MTP) and specialized pruning ("pi-tune") are the differentiating features driving downloads, with Unsloth acting as critical infrastructure. Finally, the persistent volume of the "uncensored" Qwen3.6 fine-tune (nearly 4M downloads) proves that demand for minimally-aligned models for creative writing and roleplay remains a massive, non-negotiable force shaping the community's download priorities.

---

## 4. Worth Exploring

**1. [google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it) — Most architecturally innovative release**
This is not just another VLM; it is a native diffusion language model. Instead of generating text autoregressively, it iteratively denoises entire sequences. For researchers and engineers tracking the future beyond next-token prediction, DiffusionGenma combined with MoE is a must-study artifact representing a genuine paradigm shift in how language generation is modeled.

**2. [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) — Best example of hyper-specialization**
While massive VLMs dominate chat, this 3B model perfectly executes a single, hard task: precise spatial grounding. It represents the growing trend of "small, focused, and excellent" models that integrate seamlessly into robotics, visual search, and pipeline architectures. Studying it offers direct insights into designing minimal viable architectures for specific real-world tasks.

**3. [yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF) — Template for high-quality local coding**
This model is a perfect case study in the modern local inference stack: a top-tier base model (Gemma-4), a refined community fine-tune (fable5/composer), and expert GGUF quantization. Understanding why this specific chain of optimizations produces such a high-quality local experience provides a template for deploying any future state-of-the-art coder on consumer hardware.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*