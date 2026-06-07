# Hugging Face Trending Models Digest 2026-06-07

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-07 03:35 UTC

---

Here is your structured Hugging Face Trending Models Digest based on the data provided.

---

## Hugging Face Trending Models Digest | 2026-06-07

### 1. Today's Highlights

DeepSeek **V4 Pro** and **V4 Flash** dominate the language model charts this week, signaling a clear new frontier for open-weight reasoning and solidifying Mixture-of-Experts as the definitive scaling strategy. NVIDIA executes a comprehensive platform play, releasing an entire ecosystem of models (Cosmos3 world models, LocateAnything, Nemotron-3 Ultra) alongside highly optimized NVFP4 quantizations, marking a shift from GPU vendor to full-stack AI middleware provider. Video generation continues to explode into the mainstream with the community-driven **Sulphur-2** and new entries from ByteDance and NVIDIA, while the massive adoption of domain-specific models like **HRM-Text** and quantized runtimes (GGUF, NVFP4, NF4) underscores the market's relentless demand for efficient, deployable intelligence.

### 2. Trending Models

#### 🧠 Language Models

- **deepseek-ai/DeepSeek-V4-Pro** (Link: https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)
  Author: deepseek-ai | Likes: 4,681 | Downloads: 5,510,611
  DeepSeek's flagship open-weight reasoning MoE, leading the ecosystem this week as the definitive frontier LLM release.

- **deepseek-ai/DeepSeek-V4-Flash** (Link: https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)
  Author: deepseek-ai | Likes: 1,421 | Downloads: 3,436,213
  The distilled, high-throughput companion to V4-Pro, dominating alongside its sibling for scalable, cost-efficient inference.

- **LiquidAI/LFM2.5-8B-A1B** (Link: https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)
  Author: LiquidAI | Likes: 534 | Downloads: 95,440
  An efficient 8B MoE model highly sought after for its impressive performance-to-parameter ratio in the competitive small LLM space.

- **JetBrains/Mellum2-12B-A2.5B-Thinking** (Link: https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)
  Author: JetBrains | Likes: 240 | Downloads: 16,395
  JetBrains' specialized reasoning model for code generation, reflecting the wider industry trend towards domain-specific thinking LLMs.

- **openbmb/MiniCPM5-1B** (Link: https://huggingface.co/openbmb/MiniCPM5-1B)
  Author: openbmb | Likes: 775 | Downloads: 100,575
  A remarkably capable 1B parameter model driving strong interest in ultra-efficient, on-device language deployment.

- **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16** (Link: https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)
  Author: nvidia | Likes: 145 | Downloads: 47,285
  NVIDIA's massive enterprise-grade MoE LLM, representing the high end of the open-weight frontier for large-scale text generation.

#### 🎨 Multimodal & Generation

- **google/gemma-4-12B-it** (Link: https://huggingface.co/google/gemma-4-12B-it)
  Author: google | Likes: 622 | Downloads: 315,131
  Google's breakthrough "any-to-any" small model, trending as the most versatile multimodal entry in the sub-15B category.

- **nvidia/LocateAnything-3B** (Link: https://huggingface.co/nvidia/LocateAnything-3B)
  Author: nvidia | Likes: 1,460 | Downloads: 111,078
  A groundbreaking zero-shot visual grounding model that decouples localization from recognition, highly popular for its flexibility and accuracy.

- **stepfun-ai/Step-3.7-Flash** (Link: https://huggingface.co/stepfun-ai/Step-3.7-Flash)
  Author: stepfun-ai | Likes: 343 | Downloads: 38,716
  A competitive vision-language model from Stepfun, gaining traction as a strong open-weight alternative in the mid-size VL space.

- **SulphurAI/Sulphur-2-base** (Link: https://huggingface.co/SulphurAI/Sulphur-2-base)
  Author: SulphurAI | Likes: 1,581 | Downloads: 1,704,964
  A celebrated community fine-tune of LTX-2.3 for text-to-video generation, skyrocketing in popularity and downloads this week.

- **ByteDance/Bernini-R** (Link: https://huggingface.co/ByteDance/Bernini-R)
  Author: ByteDance | Likes: 151 | Downloads: 223
  ByteDance's new image-to-video renderer, contributing to the explosive growth of open-source video generation models.

- **nvidia/Cosmos3-Nano** (Link: https://huggingface.co/nvidia/Cosmos3-Nano)
  Author: nvidia | Likes: 183 | Downloads: 24,820
  NVIDIA's entry-level world model for video understanding, building the foundation for its ambitious Cosmos3 ecosystem.

- **nvidia/Cosmos3-Super** (Link: https://huggingface.co/nvidia/Cosmos3-Super)
  Author: nvidia | Likes: 149 | Downloads: 20,403
  The higher-tier Cosmos3 model for advanced video generation and world simulation.

- **nvidia/Cosmos3-Super-Text2Image** (Link: https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)
  Author: nvidia | Likes: 120 | Downloads: 1,634
  Text-to-image variant of the Cosmos3 Super world model, extending its multimodal capabilities.

- **nvidia/Cosmos3-Super-Image2Video** (Link: https://huggingface.co/nvidia/Cosmos3-Super-Image2Video)
  Author: nvidia | Likes: 111 | Downloads: 1,295
  NVIDIA's image-to-video generation model, completing the Cosmos3 suite for dynamic world creation.

- **ideogram-ai/ideogram-4-fp8** (Link: https://huggingface.co/ideogram-ai/ideogram-4-fp8)
  Author: ideogram-ai | Likes: 311 | Downloads: 2,818
  The highly anticipated FP8 quantization of Ideogram-4, making state-of-the-art text-to-image generation more accessible.

- **nvidia/PiD** (Link: https://huggingface.co/nvidia/PiD)
  Author: nvidia | Likes: 312 | Downloads: 972
  A practical diffusion model for image super-resolution and restoration, carving a strong niche in the image enhancement domain.

- **bosonai/higgs-audio-v3-tts-4b** (Link: https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)
  Author: bosonai | Likes: 156 | Downloads: 2,184
  A high-quality 4B parameter TTS model built on a multimodal Qwen3 base, representing the convergence of language and speech synthesis.

- **meituan-longcat/LongCat-Video-Avatar-1.5** (Link: https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)
  Author: meituan-longcat | Likes: 526 | Downloads: 1,806
  Meituan's talking head avatar model, demonstrating strong demand for controllable audio-to-video generation pipelines.

- **google/magenta-realtime-2** (Link: https://huggingface.co/google/magenta-realtime-2)
  Author: google | Likes: 111 | Downloads: 9,394
  Google's real-time text-to-audio generation model, re-establishing the Magenta project's presence in the generative audio landscape.

- **MisoLabs/MisoTTS** (Link: https://huggingface.co/MisoLabs/MisoTTS)
  Author: MisoLabs | Likes: 131 | Downloads: 0
  A fresh, promising TTS model entering the scene, sparking significant community interest despite being freshly released.

#### 🔧 Specialized Models

- **sapientinc/HRM-Text-1B** (Link: https://huggingface.co/sapientinc/HRM-Text-1B)
  Author: sapientinc | Likes: 712 | Downloads: 161,627
  A finely tuned 1B language model for Human Resources management workflows, showcasing the growing appetite for domain-specific small models.

- **PaddlePaddle/PaddleOCR-VL-1.6** (Link: https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)
  Author: PaddlePaddle | Likes: 258 | Downloads: 8,365
  The latest vision-language update to PaddleOCR, integrating VL capabilities for robust document AI and text recognition.

- **nvidia/nemotron-3.5-asr-streaming-0.6b** (Link: https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)
  Author: nvidia | Likes: 221 | Downloads: 1,380
  A low-latency, streaming automatic speech recognition model from NVIDIA, optimized explicitly for real-time voice interfaces.

#### 📦 Fine-tunes & Quantizations

- **unsloth/gemma-4-12b-it-GGUF** (Link: https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)
  Author: unsloth | Likes: 423 | Downloads: 458,174
  The essential GGUF quantization for Gemma-4-12B, making Google's latest multimodal model locally runnable for the vast majority of the community.

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** (Link: https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)
  Author: HauhauCS | Likes: 1,491 | Downloads: 2,771,843
  A highly popular uncensored fine-tune of the Qwen3.6 MoE, demonstrating massive community demand for unconstrained, creative text generation.

- **nvidia/Qwen3.6-35B-A3B-NVFP4** (Link: https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)
  Author: nvidia | Likes: 198 | Downloads: 1,015,381
  NVIDIA's official NVFP4 quantization of Qwen3.6, heavily downloaded and proving the power of infrastructure-level model optimization for MoEs.

- **ideogram-ai/ideogram-4-nf4** (Link: https://huggingface.co/ideogram-ai/ideogram-4-nf4)
  Author: ideogram-ai | Likes: 214 | Downloads: 2,671
  The NF4 quantized variant of Ideogram-4, lowering the hardware barrier for high-quality image generation.

- **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4** (Link: https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)
  Author: nvidia | Likes: 119 | Downloads: 17,225
  The NVFP4 packed version of the Nemotron-3 Ultra, enabling efficient deployment of a massive 550B enterprise MoE.

- **google/gemma-4-12B** (Link: https://huggingface.co/google/gemma-4-12B)
  Author: google | Likes: 380 | Downloads: 84,549
  The original base model for the Gemma-4 family, serving as the foundation for the week's extensive fine-tuning and adaptation activity.

### 3. Ecosystem Signal

The ecosystem this week is overwhelmingly shaped by **DeepSeek V4's dominance** and **NVIDIA's platform strategy**. DeepSeek V4 Pro and Flash set the standard for open-weight reasoning, while the entire community rallies around the Mixture-of-Experts architecture—present in nearly every major release from Qwen3.6 and Nemotron to Liquid LFM and Mellum. NVIDIA is executing a masterful platform shift, publishing a complete stack of foundation models (Cosmos3, Nemotron, LocateAnything) alongside proprietary optimizations (NVFP4). The massive download figures for quantized formats (GGUF, NVFP4, NF4) confirm that inference efficiency is the single largest bottleneck the community is actively solving. Meanwhile, open-source video generation has fully matured, with models like Sulphur-2 and Bernini-R achieving mainstream traction. The open-weight paradigm clearly dominates the trending list; proprietary model releases remain secondary to the thriving ecosystem of open foundation models, quantizations, and domain-specific fine-tunes.

### 4. Worth Exploring

1.  **nvidia/LocateAnything-3B** (Link: https://huggingface.co/nvidia/LocateAnything-3B): A fundamental breakthrough in vision-language AI. By decoupling object localization from recognition, it becomes an indispensable building block for virtually any visual pipeline, from retrieval and segmentation to robotics and document AI.

2.  **deepseek-ai/DeepSeek-V4-Pro** (Link: https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro): The definitive model release of the week. Studying its architecture, reasoning traces, and MoE routing provides a complete blueprint for the current frontier of open-weight LLMs.

3.  **SulphurAI/Sulphur-2-base** (Link: https://huggingface.co/SulphurAI/Sulphur-2-base): An exemplary case study in community-driven video model success. Its massive adoption and foundation on LTX-2.3 make it the most accessible and thoroughly tested entry point into open-source video generation today.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*