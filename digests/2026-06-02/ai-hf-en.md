# Hugging Face Trending Models Digest 2026-06-02

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-02 03:39 UTC

---

## Hugging Face Trending Models Digest — 2026-06-02

### 1. Today's Highlights

The Hugging Face Hub this week is heavily defined by the release of **DeepSeek-V4**, whose Pro and Flash variants topped the charts as the community benchmarks its frontier reasoning capabilities. Simultaneously, the **Qwen 3.6 family** has generated a massive wave of fine-tuning and quantization activity, with MoE adaptations (35B-A3B), aggressive uncensored variants, and GGUF/FP4 quantizations dominating the download counts. A clear shift toward **extreme efficiency** is visible with models like LiquidAI’s LFM2.5 (1B active parameters) and the experimental ternary bonsai-image model. Finally, the **any-to-any** generative frontier is expanding rapidly, with bytedance-research's Lance and meituan's LongCat-Video-Avatar pushing multimodal generation forward.

---

### 2. Trending Models

#### 🧠 Language Models

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** by deepseek-ai | ❤️ 4,536 | ⬇️ 5,851,826. The flagship open-weight reasoning model this week, trending for its frontier chain-of-thought capability and massive community adoption.
- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** by deepseek-ai | ❤️ 1,342 | ⬇️ 3,511,636. A distilled, faster variant of DeepSeek-V4 optimized for high-throughput reasoning inference.
- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** by openbmb | ❤️ 692 | ⬇️ 45,698. A remarkably capable dense 1B language model pushing the boundaries of on-device text generation.
- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** by LiquidAI | ❤️ 399 | ⬇️ 37,893. An efficiently sparse MoE model delivering strong reasoning while using only ~1B active parameters.

#### 🎨 Multimodal & Generation

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** by Qwen | ❤️ 1,568 | ⬇️ 5,154,729. Alibaba's powerful vision-language foundation model, trending as the base for the week's largest quantization ecosystem.
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** by SulphurAI | ❤️ 1,491 | ⬇️ 1,656,520. A rapidly adopted open text-to-video base model gaining traction for high-quality prompt-based video generation.
- **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** by openbmb | ❤️ 1,088 | ⬇️ 459,188. The latest efficient vision-language model from OpenBMB, balancing strong multimodal ability with a compact size.
- **[bytedance-research/Lance](https://huggingface.co/bytedance-research/Lance)** by bytedance-research | ❤️ 1,002 | ⬇️ 3,041. An ambitious "any-to-any" multimodal model generating and understanding text, images, and video.
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** by nvidia | ❤️ 817 | ⬇️ 35,783. A 3B specialist in open-vocabulary object localization and segmentation from text prompts.
- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** by Supertone | ❤️ 771 | ⬇️ 57,627. A commercial-grade text-to-speech model producing exceptionally expressive and natural synthetic speech.
- **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)** by NemoStation | ❤️ 482 | ⬇️ 17,012. A compact video-text-to-text model bringing video understanding to the sub-3B parameter scale.
- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** by meituan-longcat | ❤️ 469 | ⬇️ 0. Generates talking head avatars from audio and text inputs for virtual content creation.
- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** by stepfun-ai | ❤️ 196 | ⬇️ 9,256. A fast vision-language model optimized for low-latency multimodal interactions.
- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** by nvidia | ❤️ 239 | ⬇️ 577. A diffusion-based super-resolution model for image upscaling and restoration.
- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** by nvidia | ❤️ 78 | ⬇️ 6,261. The entry point to NVIDIA's world model platform for physical AI simulation.
- **[OpenMOSS-Team/MOSS-TTS-v1.5](https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5)** by OpenMOSS-Team | ❤️ 94 | ⬇️ 18,564. A strong open-source Chinese text-to-speech model with natural prosody.

#### 🔧 Specialized Models

- **[pyannote/speaker-diarization-3.1](https://huggingface.co/pyannote/speaker-diarization-3.1)** by pyannote | ❤️ 2,108 | ⬇️ 9,591,005. The industry-standard pipeline for speaker segmentation, widely used for audio transcription preprocessing.
- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** by openai | ❤️ 1,579 | ⬇️ 316,092. A practical token-classification model for detecting and redacting personally identifiable information (PII).
- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** by sapientinc | ❤️ 439 | ⬇️ 149,543. A domain-specific 1B LLM tailored for human resources and people analytics.
- **[tencent/Hy-MT2-30B-A3B](https://huggingface.co/tencent/Hy-MT2-30B-A3B)** by tencent | ❤️ 444 | ⬇️ 4,458. An efficient MoE translation model delivering high-quality multilingual machine translation.
- **[numind/NuExtract3](https://huggingface.co/numind/NuExtract3)** by numind | ❤️ 216 | ⬇️ 59,010. A vision-language model specialized in structured data extraction from documents and images.
- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** by PaddlePaddle | ❤️ 156 | ⬇️ 3,190. An integrated OCR and vision-language model for holistic document layout analysis and text recognition.

#### 📦 Fine-tunes & Quantizations

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** by HauhauCS | ❤️ 1,226 | ⬇️ 2,533,393. A hugely popular uncensored MoE fine-tune of Qwen, trending for creative writing with minimal guardrails.
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** by unsloth | ❤️ 595 | ⬇️ 952,188. The premier optimized GGUF quantization of Qwen3.6, trending as the standard for local inference via llama.cpp.
- **[Jackrong/Qwopus3.6-27B-v2-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)** by Jackrong | ❤️ 184 | ⬇️ 139,952. A community-merged Qwen variant quantized to GGUF, reflecting the vibrant fine-tuning ecosystem.
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** by nvidia | ❤️ 121 | ⬇️ 171,588. NVIDIA's application of FP4 quantization to the Qwen MoE, pushing the boundaries of extreme weight compression.
- **[LiquidAI/LFM2.5-8B-A1B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B-GGUF)** by LiquidAI | ❤️ 146 | ⬇️ 55,212. The official GGUF release of the LFM2.5 MoE, enabling efficient edge deployment via llama.cpp.
- **[stepfun-ai/Step-3.7-Flash-GGUF](https://huggingface.co/stepfun-ai/Step-3.7-Flash-GGUF)** by stepfun-ai | ❤️ 86 | ⬇️ 37,533. The official GGUF variant for the Step Vision-Language model, enabling local multimodal inference.
- **[prism-ml/bonsai-image-ternary-4B-gemlite-2bit](https://huggingface.co/prism-ml/bonsai-image-ternary-4B-gemlite-2bit)** by prism-ml | ❤️ 91 | ⬇️ 0. An experimental 1.58-bit ternary diffusion model exploring the limits of generative model compression.

---

### 3. Ecosystem Signal

The ecosystem is currently defined by a powerful dual trajectory between frontier reasoning capability and extreme operational efficiency. The **DeepSeek-V4** series has unequivocally established itself as the gravity center for open-weight research, with both Pro and Flash variants driving massive adoption as the community integrates frontier reasoning into workflows. Meanwhile, the most vibrant activity is taking place within the **Qwen 3.6 ecosystem**, which is acting as a platform for immense community innovation. The sheer variety of MoE fine-tunes, aggressive uncensored variants, and quantization formats (GGUF, NVFP4) indicates the community has found a highly capable foundation model that can be aggressively shaped for specific deployment needs. This is complemented by a growing appetite for **MoE architectures with low active parameter counts** (e.g., 1–3B active out of 30–35B total), representing a pragmatic scaling philosophy. The generative frontier is also expanding rapidly beyond text-to-image; **any-to-any** models (bytedance Lance), video generation (Sulphur 2), and production-grade TTS (supertonic-3) are mainstreaming on the Hub. The presence of deeply experimental quantization techniques (bonsai ternary) alongside production-ready tooling signals a healthy pipeline from research to practical application.

---

### 4. Worth Exploring

1. **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — This model represents the most practical balance between groundbreaking reasoning quality and deployment cost. It is the mandatory baseline for any team building production reasoning systems this quarter.

2. **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — A critical case study for the future of efficient inference, this MoE directly challenges the necessity of dense scaling. With only 1B active parameters, it offers a compelling metric for “Intelligence per Watt” and is a must-test for high-scale or edge scenarios.

3. **[prism-ml/bonsai-image-ternary-4B-gemlite-2bit](https://huggingface.co/prism-ml/bonsai-image-ternary-4B-gemlite-2bit)** — A deeply experimental entry that hints at a future where generative models run on consumer hardware with minimal memory footprint. It represents the bleeding edge of quantization research and is worth studying for its compression methodology.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*