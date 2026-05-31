# Hugging Face Trending Models Digest 2026-05-31

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-31 03:31 UTC

---

# Hugging Face Trending Models Digest (2026-05-31)

## 1. Today's Highlights

This week's Hugging Face trending board is defined by the explosive ecosystem around **DeepSeek V4** and **Qwen 3.6**. DeepSeek-V4-Pro leads in overall likes, marking a major open-weight LLM milestone, while Qwen3.6-27B anchors a sprawling ecosystem of multimodal fine-tunes, MoE variants, and immediate GGUF quantizations. Video generation is undeniably the hottest modality, headlined by ByteDance's paradigm-shifting any-to-any model *Lance* and the remarkably popular *Sulphur-2-base*. Specialized models are also breaking out: OpenAI entered the safety tooling space, NVIDIA released a top-tier grounding model, and the audio sector is seeing a renaissance driven by pyannote 3.1 and Supertone 3. The ecosystem is rapidly standardizing around open-weight MoE architectures and immediate local deployment.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

1. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | Likes: 4,466 | Downloads: 5.9M
   The flagship open-weight MoE LLM of the month, setting new benchmarks in reasoning and conversational ability across the community.

2. **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — deepseek-ai | Likes: 1,306 | Downloads: 3.4M
   A distilled, higher-throughput variant of V4 Pro optimized for production inference without sacrificing core quality.

3. **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** — openbmb | Likes: 610 | Downloads: 28.8k
   A surprisingly capable 1B parameter LLM pushing the boundaries of what is achievable on edge and mobile devices.

4. **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — LiquidAI | Likes: 283 | Downloads: 17.1k
   Liquid's latest MoE model (8B total, 1B active), showcasing continued investment in dynamic, inference-efficient architectures.

5. **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — sapientinc | Likes: 421 | Downloads: 138k
   A specialized small model fine-tuned for HRM and enterprise text processing tasks, proving demand for vertical-specific LLMs.

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

1. **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — Qwen | Likes: 1,539 | Downloads: 4.9M
   The 27B anchor VLM of the Qwen3.6 family, driving a massive ecosystem of community fine-tunes, quantizations, and tool integrations.

2. **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)** — bytedance-research | Likes: 981 | Downloads: 2.8k
   ByteDance's ambitious "any-to-any" model unifying image generation, video generation, and understanding under a single transformer.

3. **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — SulphurAI | Likes: 1,456 | Downloads: 1.5M
   A high-quality text-to-video base model that has gained massive community traction for its output quality and ComfyUI compatibility.

4. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | Likes: 506 | Downloads: 18.3k
   NVIDIA's dedicated grounding and feature extraction model for precise object localization and visual RAG pipelines.

5. **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** — openbmb | Likes: 1,074 | Downloads: 433k
   The latest iteration of the strong edge VLM family, providing impressive vision-language performance in a compact package.

6. **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)** — NemoStation | Likes: 457 | Downloads: 15.8k
   A video-text-to-text model optimized for understanding and processing video content, ideal for captioning and QA.

7. **[circlestone-labs/Anima](https://huggingface.co/circlestone-labs/Anima)** — circlestone-labs | Likes: 1,602 | Downloads: 736k
   A widely adopted diffusion single-file model for image generation, deeply integrated into the ComfyUI ecosystem.

8. **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** — meituan-longcat | Likes: 411 | Downloads: 0
   A video avatar model that generates talking head videos from audio, text, and image inputs, pushing avatar quality forward.

9. **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — stepfun-ai | Likes: 139 | Downloads: 3.4k
   Stepfun's flash-grade VLM, optimized for faster inference while maintaining strong multimodal reasoning.

10. **[microsoft/Lens](https://huggingface.co/microsoft/Lens)** — microsoft | Likes: 145 | Downloads: 1.5k
    A new text-to-image diffusion model from Microsoft, backed by a recent arXiv publication (2605.21573).

11. **[numind/NuExtract3](https://huggingface.co/numind/NuExtract3)** — numind | Likes: 205 | Downloads: 53.3k
    A vision-language model specializing in document and image data extraction for structured outputs.

12. **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** — PaddlePaddle | Likes: 108 | Downloads: 2.2k
    PaddlePaddle's latest unified OCR and vision-language model for high-accuracy text recognition in images.

---

### 🔧 Specialized Models (safety, translation, audio, OCR, super-resolution)

1. **[pyannote/speaker-diarization-3.1](https://huggingface.co/pyannote/speaker-diarization-3.1)** — pyannote | Likes: 2,073 | Downloads: 9.7M
   The definitive open-source speaker diarization pipeline, widely used for meeting analysis and transcription.

2. **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** — openai | Likes: 1,570 | Downloads: 304k
   OpenAI's new token-classification model for detecting and filtering PII, signaling a big push into open safety tooling.

3. **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** — Supertone | Likes: 746 | Downloads: 55k
   A state-of-the-art text-to-speech model achieving high naturalness, gathering significant traction for voice applications.

4. **[tencent/Hy-MT2-30B-A3B](https://huggingface.co/tencent/Hy-MT2-30B-A3B)** — tencent | Likes: 434 | Downloads: 3.8k
   Tencent's massive MoE translation model (30B total, 3B active) optimized for enterprise-grade multilingual translation.

5. **[tencent/Hy-MT2-1.8B](https://huggingface.co/tencent/Hy-MT2-1.8B)** — tencent | Likes: 1,092 | Downloads: 16.8k
   The highly efficient, smaller sibling of the Hy-MT2 translation series, balancing quality and speed for production workloads.

6. **[OpenMOSS-Team/MOSS-TTS-v1.5](https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5)** — OpenMOSS-Team | Likes: 74 | Downloads: 11.2k
   A custom-code TTS model optimized for Chinese language generation, expanding the open-source TTS landscape.

7. **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** — nvidia | Likes: 194 | Downloads: 437
   NVIDIA's diffusion-based super-resolution model for enhancing low-resolution images with high fidelity.

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

1. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | Likes: 1,112 | Downloads: 2.2M
   A widely downloaded uncensored fine-tune of the Qwen3.6 MoE VLM, reflecting strong community demand for unfiltered variants.

2. **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth | Likes: 567 | Downloads: 877k
   The go-to GGUF MTP quantization for Qwen3.6-27B, essential for running this popular VLM locally with high performance.

3. **[LiquidAI/LFM2.5-8B-A1B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B-GGUF)** — LiquidAI | Likes: 124 | Downloads: 23.6k
   Official GGUF weights for Liquid's latest MoE model, enabling direct edge deployment from the model creator.

4. **[Jackrong/Qwopus3.6-27B-v2-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)** — Jackrong | Likes: 172 | Downloads: 105k
   An optimized MTP GGUF quantization of the Qwen3.6 series pushing the frontier of inference speed for quantized VLMs.

5. **[Jackrong/Qwopus3.6-27B-v2-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-GGUF)** — Jackrong | Likes: 186 | Downloads: 33k
   A companion standard GGUF quantization of the Qwopus 27B VLM, offering a speed-versus-capability trade-off.

6. **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | Likes: 460 | Downloads: 0
   A high-impact utility providing corrected Jinja chat templates for Qwen models, essential for smooth local framework integration.

---

## 3. Ecosystem Signal

The model ecosystem is coalescing around a small number of dominant families. **DeepSeek V4** and **Qwen 3.6** serve as the primary foundation models, with community efforts almost immediately focused on quantization and uncensored fine-tuning. Open-weight releases from NVIDIA, Microsoft, and Tencent reinforce the norm that frontier research is increasingly shared openly, even as OpenAI enters specific safety tooling for the first time. A key signal is the sheer velocity of the **GGUF ecosystem**—top Qwen quantizations have millions of combined downloads, proving that local inference is no longer an afterthought but a primary deployment target. Meanwhile, the **audio and generation sector** (TTS, diarization, text-to-video) is experiencing a clear renaissance, with Supertone and pyannote providing production-ready open tools that challenge proprietary equivalents. The market is moving swiftly toward specialized, efficient, and locally deployable models.

---

## 4. Worth Exploring

**1. [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
   Rather than relying on massive general-purpose VLMs for every task, NVIDIA released a dedicated 3B model focused exclusively on spatial grounding and feature extraction. For anyone building visual RAG, agentic workflows, or precise object localization systems, this offers a dramatically better cost/performance ratio than prompt-engineering a 70B+ VLM. Its rapid rise (506 likes) signals strong industrial demand for disentangled, specialized vision models.

**2. [bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)**
   The "any-to-any" modeling paradigm is one of the most ambitious architectural bets in the current landscape. ByteDance's Lance aims to unify generation and understanding across text, image, video, and audio into a single transformer—a direct challenge to the fragmented pipelines of most current systems. If it succeeds, it could define the next generation of multimodal AI. This is the model to study for anyone interested in the future of foundation model architectures.

**3. [Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)**
   Text-to-Speech is notoriously difficult to democratize, yet Supertone has achieved remarkable community traction (746 likes, 55k downloads) with a high-quality model. The engagement strongly suggests a leap in naturalness and controllability that rivals proprietary APIs. It is an excellent candidate for developers looking to build fully open-source, high-quality voice applications without compromising on output quality.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*