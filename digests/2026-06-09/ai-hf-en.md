# Hugging Face Trending Models Digest 2026-06-09

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-09 02:49 UTC

---

# Hugging Face Trending Models Digest | 2026-06-09

---

## 1. Today's Highlights

The Hugging Face ecosystem is electrified this week by the explosive debut of **deepseek-ai/DeepSeek-V4-Pro**, which swept the board with the highest weekly likes, and the broad, ecosystem-defining wave of **Google's Gemma 4** family spanning base models, instruction-tuned variants, and multiple quantization formats. Mixture-of-Experts (MoE) has solidified its position as the dominant architecture for scaling, appearing across nearly every major frontier release from DeepSeek, NVIDIA, Google, and Liquid AI. NVIDIA continues to execute a formidable full-stack strategy with top entries in visual grounding, speech, text generation, and world models, while the community's "uncensored" fine-tuning subculture demonstrates tremendous download volume. Simultaneously, the text-to-video space is heating up dramatically, driven by a record-breaking community fine-tune of LTX-2.3.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** & **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** | *deepseek-ai* | 4,723 + 1,449 likes | 5.4M + 3.3M downloads
  The undisputed heavy-lifters of the week, defining frontier-level open-weight text generation with strong reasoning and flexible inference options.
- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** | *LiquidAI* | 551 likes | 135k downloads
  Liquid AI's latest MoE foundation model pushing the efficiency frontier; what an 8B active model can achieve in complex reasoning continues to impress.
- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** & **[NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** | *nvidia* | 167 + 145 likes | 56k + 66k downloads
  NVIDIA's colossal 550B MoE model available in high-precision BF16 and extremely efficient NVFP4, showcasing the frontier of open-weight scale.
- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** | *sapientinc* | 728 likes | 164k downloads
  A highly specialized 1B model for enterprise HR applications, proving the massive traction available for focused, purpose-built small language models.
- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** | *JetBrains* | 260 likes | 17k downloads
  JetBrains' strategic entry into thinking models—a 12B MoE conversational model designed for structured reasoning.
- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** | *nex-agi* | 125 likes | 716 downloads
  A Qwen 3.5 MoE fine-tune purpose-built for autonomous agentic workflows and tool orchestration.

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** | *nvidia* | 1,628 likes | 122k downloads
  The top trending multimodal model—a remarkably capable 3B visual grounding model for precise object localization and segmentation.
- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** & **[gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** | *google* | 754 + 452 likes | 554k + 117k downloads
  Google's flagship any-to-any multimodal models anchoring the week's most active ecosystem with strong performance across text, image, and video.
- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** | *stepfun-ai* | 352 likes | 45k downloads
  A high-speed Vision-Language model optimized for rapid inference without compromising complex visual reasoning.
- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** & **[ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** | *ideogram-ai* | 394 + 262 likes | 5.5k + 5k downloads
  Ideogram's latest diffusion model delivers state-of-the-art prompt adherence via FP8, with an NF4 variant enabling extreme memory compression.
- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** | *bosonai* | 251 likes | 15k downloads
  A highly expressive 4B text-to-speech system built on Qwen3, pushing the quality boundary of open-source neural voice synthesis.
- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** | *MisoLabs* | 156 likes | 0 downloads
  A fresh TTS entry experiencing a surge of community anticipation, ranking highly on likes immediately upon release.
- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** | *google* | 152 likes | 17k downloads
  Google's breakthrough real-time text-to-music model, well-supported by strong research with citations to recent arxiv papers.
- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** | *ByteDance* | 186 likes | 278 downloads
  ByteDance's competitive new image-text-to-video diffusion model pushing open-weight video generation forward.
- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** & **[Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)** | *nvidia* | 206 + 158 likes | 34k + 27k downloads
  NVIDIA's world model series, bridging multimodal generation with physics-aware simulation for next-generation embodied AI.
- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** | *PaddlePaddle* | 277 likes | 10k downloads
  The latest visual-language model for OCR and document understanding, leveraging the ERNIE 4.5 architecture.
- **[jdopensource/JoyAI-Echo](https://huggingface.co/jdopensource/JoyAI-Echo)** | *jdopensource* | 103 likes | 4k downloads
  JD.com's unified text-to-video and audio generation model, streamlining multimodal short-form content production.

---

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** | *nvidia* | 293 likes | 3.9k downloads
  A dedicated cache-aware streaming ASR model designed for real-time, high-accuracy, low-latency speech transcription.

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** | *unsloth* | 504 likes | 645k downloads
  The definitive GGUF quantization of Gemma 4-12B-IT, serving as the primary vehicle for democratizing local inference.
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | *HauhauCS* | 1,555 likes | 3M downloads
  A blockbuster download count for an uncensored MoE vision-language fine-tune of Qwen 3.6, demonstrating massive demand for unconstrained models.
- **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** & **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)** | *unsloth / google* | 147 + 101 likes | 121k + 52k downloads
  Quantization-Aware Training GGUF quants of Gemma 4 marking a maturation of the deployment pipeline—significantly better quality at extreme compression ratios.
- **[unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)** | *unsloth* | 104 likes | 87k downloads
  The QAT GGUF of the larger 26B MoE variant, bringing flagship any-to-any performance to local hardware.
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** | *SulphurAI* | 1,601 likes | 1.7M downloads
  A community-defining text-to-video fine-tune of Lightricks/LTX-2.3, massively outperforming the base model and proving the power of community-driven iterative improvement.
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** | *unsloth* | 696 likes | 1.1M downloads
  Unsloth's high-quality GGUF quantization of the MoE Qwen3.6 27B, a staple for accessible local vision-language inference.

---

## 3. Ecosystem Signal

The model ecosystem this week is shaped by a structural convergence on Mixture-of-Experts (MoE) as the architecture of choice for scaling—DeepSeek V4, Nemotron-3 Ultra, Gemma 4 26B, Qwen 3.6, and LiquidAI LFM 2.5 all deploy MoE at varying ratios, suggesting the community has decisively adopted it as the default frontier blueprint.

A critical operational trend is the standardization of the quantization pipeline. Unsloth has consolidated its role as the essential middleware between base model releases and broadly usable GGUF packages. The prominent use of Quantization-Aware Training (QAT) in the Gemma 4 ecosystem—adopted directly by Google—signals a future where quantization is not an afterthought but a first-class design constraint baked into training.

Open-weight momentum remains robust with no gated models on this list, though the "uncensored" fine-tuning subculture (exemplified by the 3M downloads of HauhauCS's Qwen 3.6 variant) underscores that the community's appetite for unconstrained models is a major market force. The emerging "any-to-any" paradigm—led by Gemma 4's unified architecture and NVIDIA's Cosmos3 world models—is beginning to blur the traditional boundaries between LLMs, VLMs, TTS, and video diffusion, pointing toward a future of truly omni-modal foundation models.

---

## 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — This compact 3B model perfectly exemplifies the trend of small, highly capable specialized models. It solves the practical problem of visual grounding with exceptional accuracy while being deployable on edge devices. A must-try for any computer vision pipeline requiring flexible object localization.

2. **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — With 1.7 million downloads in its first week, this community fine-tune of Lightricks/LTX-2.3 is a masterclass in the power of open-source iteration. It redefines what is possible in text-to-video generation and is the single model to study for understanding community-driven model improvement.

3. **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — Somewhat hidden despite 152 likes, this real-time text-to-music model is a fascinating scientific release backed by strong research papers. It deserves far more attention from the audio and creative AI community for its novel architecture and potential to democratize music generation.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*