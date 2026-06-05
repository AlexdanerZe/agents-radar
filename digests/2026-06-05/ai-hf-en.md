# Hugging Face Trending Models Digest 2026-06-05

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-05 03:29 UTC

---

# Hugging Face Trending Models Digest — June 5, 2026

## 1. Today's Highlights

This week is defined by the explosive crossover of **DeepSeek V4**, whose Pro and Flash variants dominate the top of the chart with a combined 6,000+ weekly likes and over 9 million downloads, signaling an outright paradigm shift in the open-weight LLM hierarchy. **Mixture-of-Experts (MoE)** has solidified as the dominant architecture across the board, with Qwen 3.6, Liquid's LFM2.5, Step-3.7, and DeepSeek V4 Flash all leveraging MoE, while an accompanying quantization arms race (NVFP4, imatrix GGUF) showcases the community's relentless drive toward local deployment. In the generative arena, **Sulphur-2** (1.6M downloads) marks a "Linux moment" for open-source text-to-video, while Nvidia makes a massive coordinated push with its Cosmos3 omni-generation family and the breakthrough visual grounding model **LocateAnything-3B**. Meanwhile, the extreme popularity of the **MiniCPM5-1B** and the **HRM-Text-1B** domain model underscores that the market for small, efficient, and specialized language models is decisively maturing alongside the frontier giants.

---

## 2. Trending Models

### 🧠 Language Models

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** (deepseek-ai, 4,632 likes, 5.7M downloads) – The undisputed heavyweight of the week; a frontier-class text-generation model reshaping the competitive landscape for open-weight LLMs.
- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** (deepseek-ai, 1,402 likes, 3.5M downloads) – The efficient, high-throughput sibling of V4-Pro, heavily downloaded for cost-sensitive and scalable inference.
- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** (LiquidAI, 513 likes, 72k downloads) – A breakthrough MoE model delivering frontier capability with only 1B active parameters, defining state-of-the-art in efficient generative AI.
- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** (openbmb, 768 likes, 79k downloads) – A remarkably capable 1B model proving that ultra-efficient, on-device LLMs are a primary demand vector in the community.

### 🎨 Multimodal & Generation

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** (nvidia, 1,295 likes, 91k downloads) – A breakthrough vision-language model for point-level object localization, signaling a shift toward dedicated, high-utility spatial AI.
- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** (google, 430 likes, 14k downloads) – Google's first unified "any-to-any" open model natively processing text, images, and audio, cementing the multimodal convergence trend.
- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** (stepfun-ai, 252 likes, 22k downloads) – An efficient vision-language MoE flash model highly competitive for real-time image understanding.
- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8) & [nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** (ideogram-ai, ~200 likes, ~350 downloads) – The official FP8 and NF4 quantized versions of Ideogram 4, lowering the barrier for state-of-the-art text-to-image generation.
- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** (PaddlePaddle, 233 likes, 5.9k downloads) – An advanced vision-language OCR model extending the PaddleOCR ecosystem into holistic document understanding.
- **[nvidia/Cosmos3 Super](https://huggingface.co/nvidia/Cosmos3-Super) & Variants** (nvidia, ~100–166 likes, ~900–17k downloads) – A comprehensive omni-generation family covering text-to-image, image-to-video, and more, emphasizing physics-aware visual generation.
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** (SulphurAI, 1,550 likes, 1.6M downloads) – The defining open video generation model of the week; built on LTX-Video and absorbing massive community adoption.
- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** (meituan, 516 likes, 381 downloads) – An audio-to-video avatar generation model pushing the boundaries of expressive, language-aware digital humans.
- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** (ByteDance, 123 likes, 129 downloads) – An experimental image-text-to-video renderer from ByteDance, hinting at the next wave of generative storytelling tools.
- **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)** (NemoStation, 518 likes, 19k downloads) – A video-text-to-text model enabling direct language understanding of videos, a crucial step for multimodal comprehension.

### 🔧 Specialized Models

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** (JetBrains, 204 likes, 12k downloads) – JetBrains' new thinking-oriented MoE model, a strong signal for deeply integrated AI reasoning in developer tooling.
- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** (nvidia, 303 likes, 852 downloads) – A photorealistic image super-resolution diffusion model pushing the envelope in image restoration.
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** (nvidia, 119 likes, 225 downloads) – A tiny cache-aware streaming ASR model optimized for real-time edge speech transcription.
- **[OpenMOSS-Team/MOSS-TTS-v1.5](https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5)** (OpenMOSS-Team, 145 likes, 28k downloads) – A high-fidelity Chinese TTS model with advanced delay-based speech synthesis.
- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** (sapientinc, 620 likes, 157k downloads) – A domain-specific 1B language model for human resource management, validating strong demand for specialized enterprise SLMs.

### 📦 Fine-tunes & Quantizations

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (HauhauCS, 1,409 likes, 2.6M downloads) – The most downloaded model on the entire list; an aggressive uncensored fine-tune of Qwen 3.6 MoE, illustrating massive demand for unconstrained frontier VLMs.
- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** (unsloth, 299 likes, 62k downloads) – Unsloth's highly optimized GGUF quantization of Gemma 4, making Google's latest multimodal model portable.
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** (unsloth, 649 likes, 1.0M downloads) – A massive community hit, this GGUF quant unlocks the powerful Qwen 3.6 MoE vision model for consumer GPUs.
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** (nvidia, 178 likes, 629k downloads) – Nvidia's own extreme 4-bit NVFP4 quantization of Qwen 3.6, showcasing the industry push for ultra-compact MoE deployment.
- **[LiquidAI/LFM2.5-8B-A1B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B-GGUF)** (LiquidAI, 182 likes, 102k downloads) – Official GGUF quantization of Liquid's efficient MoE architecture for seamless local inference.
- **[stepfun-ai/Step-3.7-Flash-GGUF](https://huggingface.co/stepfun-ai/Step-3.7-Flash-GGUF)** (stepfun-ai, 107 likes, 44k downloads) – The official GGUF packaging of the Step-3.7 vision flash model, leveraging imatrix quantization for MoE efficiency.

---

## 3. Ecosystem Signal

The current market is defined by the **competitive dynamics of MoE architectures** and the rapid commoditization of frontier models. The **DeepSeek V4 family** (Pro & Flash) has emerged as the clear gravitational center, challenging the de facto supremacy of previous leaders through raw performance and massive community traction. Simultaneously, the **"Any-to-Any" paradigm** is solidifying; Google's Gemma 4 and Nvidia's Cosmos3 are openly competing to become the developer's choice for unified multimodal processing.

The community is overwhelmingly focused on **compression and accessibility**. The instant proliferation of quantizations (GGUF, NVFP4) for the largest MoE models (Qwen 3.6, Step-3.7) and the explosive demand for niche fine-tunes (the uncensored Qwen 3.6 pipeline) illustrate an ecosystem moving aggressively toward self-hostable, frontier-class AI at reduced cost. The simultaneous rise of ultra-efficient small models (MiniCPM5-1B, LFM2.5) alongside specialized domain models (HRM-Text) signals a **polarization of the market**: users either demand absolute top-tier general intelligence (DeepSeek V4) or incredibly efficient, task-specific solutions. **Open-weight** releases from former proprietary heavyweights (DeepSeek, ByteDance, Google, Nvidia) are accelerating this trend, applying immense pressure to the closed-source model ecosystem.

---

## 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – Represents a clean break from general-purpose VLMs toward a laser-focused, high-utility spatial grounding model. It is the archetype of a successful "AI agent component" and should be closely studied by anyone building robotic, retrieval, or visual reasoning systems.

2. **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** – JetBrains entering the frontier thinking-model space is a massive vote of confidence for open-weight reasoning models. This model is poised to define the future of AI-assisted coding and professional IDEs, making it a critical model to evaluate for tooling ecosystems.

3. **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** – The intense popularity of this tiny model is a powerful market signal that the edge AI and on-device LLM market has fully matured. It serves as a fascinating case study in capability-per-parameter optimization, essential for any engineer focused on mobile, browser, or resource-constrained deployments.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*