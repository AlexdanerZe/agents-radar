# Hugging Face Trending Models Digest 2026-05-29

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-29 02:54 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-05-29

## 1. Today's Highlights

The Hugging Face ecosystem is electrified by the simultaneous dominance of **DeepSeek V4** (Pro and Flash) and the rapidly expanding **Qwen 3.6** model family, which together command millions of downloads and hundreds of derivative fine-tunes. ByteDance's surprise release of **Lance**, a cutting-edge any-to-any multimodal model, signals a decisive industry shift toward unified generative architectures. Meanwhile, the community is heavily focused on quantizing and "uncensoring" the latest Mixture-of-Experts (MoE) releases, and production-grade audio and video pipelines from Stability AI, Supertone, and Pyannote demonstrate that the platform has matured well beyond pure language modeling into a comprehensive open-weight AI ecosystem.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** | Author: deepseek-ai | Likes: 4,407 | Downloads: 5,281,601  
  The new flagship foundation model, trending for its fusion of deep chain-of-thought reasoning and conversational fluency, dominating community benchmarks.

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** | Author: deepseek-ai | Likes: 1,279 | Downloads: 3,327,898  
  The highly optimized, distilled variant of DeepSeek V4 enabling high-throughput production inference with minimal quality trade-off.

- **[tencent/Hy-MT2-30B-A3B](https://huggingface.co/tencent/Hy-MT2-30B-A3B)** | Author: tencent | Likes: 417 | Downloads: 2,894  
  Tencent's advanced MoE translation model, gaining attention for strong multilingual performance with only 3B active parameters.

- **[tencent/Hy-MT2-1.8B](https://huggingface.co/tencent/Hy-MT2-1.8B)** | Author: tencent | Likes: 1,079 | Downloads: 14,600  
  A dense, compact translation model ideally suited for high-speed on-device multilingual inference.

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** | Author: LiquidAI | Likes: 119 | Downloads: 0  
  An architectural standout activating only 1B out of 8B parameters, representing a significant leap in cost-efficient language modeling.

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** | Author: sapientinc | Likes: 400 | Downloads: 121,862  
  A compact text generation model trending for its reliable performance in enterprise-specific language workflows.

- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** | Author: openbmb | Likes: 500 | Downloads: 15,629  
  The latest in the acclaimed MiniCPM series, offering state-of-the-art performance-per-parameter at the 1B scale.

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)** | Author: bytedance-research | Likes: 956 | Downloads: 2,506  
  ByteDance's landmark any-to-any model unifying text, image, video, and audio generation in a single framework—the most architecturally ambitious release this week.

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** | Author: Qwen | Likes: 1,510 | Downloads: 4,790,806  
  Alibaba's latest vision-language powerhouse, setting a new open-weight standard for multimodal reasoning with high-resolution understanding.

- **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** | Author: openbmb | Likes: 1,047 | Downloads: 388,525  
  A standout "open textbook" VLM delivering surprisingly strong vision-language performance in a highly accessible, efficient package.

- **[circlestone-labs/Anima](https://huggingface.co/circlestone-labs/Anima)** | Author: circlestone-labs | Likes: 1,580 | Downloads: 704,160  
  A massively popular community diffusion model for ComfyUI, trending as a strong open alternative for high-quality image generation.

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** | Author: SulphurAI | Likes: 1,424 | Downloads: 1,472,982  
  A leading open-source text-to-video base model driving the current surge of interest in AI video creation.

- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** | Author: Supertone | Likes: 728 | Downloads: 52,022  
  A top-tier text-to-speech model celebrated for its natural expressiveness and emotional range in voice synthesis.

- **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)** | Author: NemoStation | Likes: 430 | Downloads: 13,855  
  A dedicated video-text model optimized for dense video captioning, filling a crucial niche in multimodal understanding.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** | Author: nvidia | Likes: 208 | Downloads: 1,755  
  NVIDIA's visual grounding specialist enabling precise object localization and segmentation from natural language prompts.

- **[microsoft/Lens](https://huggingface.co/microsoft/Lens)** | Author: microsoft | Likes: 138 | Downloads: 1,061  
  A new text-to-image diffusion model from Microsoft pushing the boundaries of visual composition and fidelity.

- **[microsoft/Lens-Turbo](https://huggingface.co/microsoft/Lens-Turbo)** | Author: microsoft | Likes: 125 | Downloads: 1,478  
  The fast distilled variant of Lens, optimized for rapid text-to-image inference in creative pipelines.

- **[stabilityai/stable-audio-3-medium](https://huggingface.co/stabilityai/stable-audio-3-medium)** | Author: stabilityai | Likes: 132 | Downloads: 0  
  Stability AI's latest music and sound effects generation model, representing continued maturity in open audio synthesis.

- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** | Author: nvidia | Likes: 163 | Downloads: 335  
  NVIDIA's pixel-based diffusion model specializing in high-quality super-resolution and image restoration.

- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** | Author: meituan-longcat | Likes: 368 | Downloads: 0  
  A specialized model for generating realistic talking head avatars synchronized to audio and image inputs.

- **[numind/NuExtract3](https://huggingface.co/numind/NuExtract3)** | Author: numind | Likes: 186 | Downloads: 44,827  
  A fine-tuned vision-language model designed for efficient structured data extraction from images and documents.

---

### 🔧 Specialized Models (code, math, medical, embeddings, etc.)

- **[pyannote/speaker-diarization-3.1](https://huggingface.co/pyannote/speaker-diarization-3.1)** | Author: pyannote | Likes: 2,044 | Downloads: 9,845,884  
  The undisputed industry standard for voice segmentation and speaker identification, critical for transcription and meeting intelligence pipelines.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** | Author: froggeric | Likes: 446 | Downloads: 0  
  A vital community utility providing corrected chat templates for the Qwen family, solving a widespread integration issue.

- **[zhen-nan/L2P](https://huggingface.co/zhen-nan/L2P)** | Author: zhen-nan | Likes: 78 | Downloads: 0  
  A novel research model exploring advanced representation learning techniques, accompanied by a recent arxiv paper.

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | Author: HauhauCS | Likes: 1,005 | Downloads: 1,956,558  
  The most viral community fine-tune of the Qwen 3.6 MoE, trending for its unrestricted creative writing and role-playing capabilities.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** | Author: unsloth | Likes: 533 | Downloads: 806,874  
  Unsloth's meticulously optimized GGUF quant of the dense Qwen 3.6 27B, enabling broad local deployment of a top vision-language model.

- **[unsloth/Qwen3.6-35B-A3B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-MTP-GGUF)** | Author: unsloth | Likes: 404 | Downloads: 686,839  
  The GGUF quantized MoE variant of Qwen 3.6, trending for balancing flagship performance with accessible local hardware requirements.

- **[Jackrong/Qwopus3.6-27B-v2-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-GGUF)** | Author: Jackrong | Likes: 174 | Downloads: 24,336  
  A high-quality community GGUF conversion of the Qwen 3.6 architecture, a favorite among local inference practitioners.

- **[Jackrong/Qwopus3.6-27B-v2-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)** | Author: Jackrong | Likes: 151 | Downloads: 65,968  
  The multi-token prediction (MTP) variant GGUF conversion, gaining traction for its speculative decoding compatibility.

- **[OBLITERATUS/Qwen3.6-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.6-27B-OBLITERATED)** | Author: OBLITERATUS | Likes: 112 | Downloads: 13,911  
  A popular "abliterated" Qwen 3.6 fine-tune, part of the broader community trend toward reduced model restrictions.

---

## 3. Ecosystem Signal

The current trending page reveals an ecosystem in rapid transition. **MoE is no longer experimental—it is the standard architecture for new flagship models.** Every major family represented (DeepSeek V4, Qwen 3.6, Tencent Hy-MT2, Liquid LFM2.5) deploys sparse activation, driving an unprecedented wave of GGUF quantizations from community providers like Unsloth to make these models viable on consumer hardware. The "uncensored" fine-tuning movement has reached a fever pitch around the Qwen 3.6 families, reflecting strong user demand for unconstrained creative and narrative generation. 

Furthermore, the platform is experiencing a **convergence of modalities**. ByteDance's Lance pushes for unified any-to-any generation, while specialized vision, video, and audio models demonstrate that the ecosystem is simultaneously deepening individual sense-making capabilities. Audio generation has hit a new maturity milestone with production-grade pipelines from Stability AI, Supertone, and Pyannote. **Open-weight models have decisively won** on Hugging Face; no proprietary-locked model makes the top 30, underscoring the platform's role as the global epicenter of open AI development and distribution.

---

## 4. Worth Exploring

1. **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)**  
   Beyond its immediate utility, Lance is a case study in architectural unification. Researchers and builders should explore how ByteDance mixes modalities natively (rather than stitching separate models together)—this provides critical insight into the next generation of generative AI platforms.

2. **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)**  
   With only 1 billion active parameters out of 8 billion total, this model represents a fascinating engineering trade-off. It is highly worth studying for deployment scenarios where latency and cost are at an extreme premium, without entirely sacrificing model capacity.

3. **[pyannote/speaker-diarization-3.1](https://huggingface.co/pyannote/speaker-diarization-3.1)**  
   With nearly 10 million downloads and over 2,000 likes, this is a quiet titan of the ecosystem. For anyone building voice agents, transcription services, or audio processing pipelines, this model remains the gold standard for the critical—and often overlooked—task of speaker segmentation.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*