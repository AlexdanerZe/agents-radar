# Hugging Face Trending Models Digest 2026-06-06

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-06 02:50 UTC

---

# Hugging Face Trending Models Digest

## 1. Today's Highlights

This week’s trending leaderboard signals a clear inflection point for the open-weight ecosystem. DeepSeek-V4-Pro and DeepSeek-V4-Flash have cemented their dominance, accumulating millions of downloads and defining the trajectory of large-scale MoE language modeling. Simultaneously, the generative AI frontier is shifting decisively toward video, with models like **Sulphur-2-base** and Nvidia's comprehensive **Cosmos3** suite generating explosive community interest. Nvidia continues its aggressive vertical integration, releasing everything from a tiny 3B localization model to a 550B enterprise MoE beast, while community quantizers like Unsloth and fine-tuners like HauhauCS ensure the top architectures are accessible to everyone.

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** by deepseek-ai (4,658 likes, 5.5M downloads): The undisputed top-tier open-weight MoE LLM of the month, setting the benchmark for performance and community adoption.
- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** by deepseek-ai (1,413 likes, 3.4M downloads): The accelerated, high-throughput sibling of V4 Pro, optimized for speed without sacrificing quality.
- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** by LiquidAI (526 likes, 82k downloads): A highly efficient 8B MoE model offering a compelling performance-to-compute ratio.
- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** by openbmb (771 likes, 91k downloads): A remarkably capable 1B parameter model proving small-scale LLMs still pack a punch.
- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** by JetBrains (225 likes, 14k downloads): A reasoning-oriented MoE model designed for deep integration with coding workflows.
- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** by google (339 likes, 53k downloads): The strong base foundation model powering the Gemma 4 ecosystem of fine-tunes.
- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** by sapientinc (702 likes, 159k downloads): A rapidly adopted specialized 1B text-generation model for enterprise or domain-specific applications.
- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** by nvidia (118 likes, 9k downloads): Nvidia's flagship enterprise MoE LLM, demonstrating extreme scale at 550B total parameters.
- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** by nvidia (109 likes, 7k downloads): The hardware-optimized NVFP4 quantized variant of the Nemotron 3 Ultra.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** by nvidia (1,379 likes, 101k downloads): A highly specialized 3B model for object localization and feature extraction that is punching far above its weight.
- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** by google (553 likes, 142k downloads): Google's instruction-tuned any-to-any multimodal flagship, pushing open-model capabilities.
- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** by stepfun-ai (332 likes, 27k downloads): A strong vision-language MoE model representing the vanguard of efficient VLMs.
- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** by ideogram-ai (270 likes, 1k downloads): Ideogram's latest generation text-to-image model in an efficient FP8 format.
- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** by ideogram-ai (192 likes, 1k downloads): The ultra-compressed NF4 variant of Ideogram 4 for memory-constrained inference.
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** by SulphurAI (1,566 likes, 1.6M downloads): The breakout open-weight text-to-video diffusion model of the week, marking video gen as the new frontier.
- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** by nvidia (176 likes, 21k downloads): The entry-level model in Nvidia's sophisticated Cosmos3 world model ecosystem.
- **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)** by nvidia (142 likes, 19k downloads): The premium, high-fidelity variant of Nvidia's Cosmos3 world model.
- **[nvidia/Cosmos3-Super-Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)** by nvidia (116 likes, 1k downloads): The text-to-image specialization branch of the Cosmos3 Super model.
- **[nvidia/Cosmos3-Super-Image2Video](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video)** by nvidia (106 likes, 1k downloads): The image-to-video specialization branch of the Cosmos3 Super model.
- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** by ByteDance (142 likes, 175 downloads): A novel 3D-aware image-to-video renderer exploring new frontiers in video generation.
- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** by meituan-longcat (519 likes, 1k downloads): A specialized audio+text-to-video model for generating realistic talking avatars.
- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** by bosonai (120 likes, 408 downloads): A large-scale 4B parameter text-to-speech model targeting high-fidelity audio generation.
- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** by MisoLabs (111 likes, 0 downloads): A fresh entrant into the competitive TTS landscape.
- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** by nvidia (310 likes, 901 downloads): A diffusion-based super-resolution model showcasing Nvidia's depth in image restoration.
- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** by PaddlePaddle (245 likes, 6k downloads): An advanced Vision-Language OCR model for robust document understanding.

### 🔧 Specialized Models

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** by nvidia (197 likes, 597 downloads): A highly optimized streaming ASR model designed for real-time, low-latency speech recognition.

### 📦 Fine-tunes & Quantizations

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** by HauhauCS (1,452 likes, 2.6M downloads): A massively popular uncensored fine-tune of Qwen 3.6 MoE, representing the frontier of community alignment experimentation.
- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** by unsloth (379 likes, 296k downloads): The standard GGUF quantization of Google's Gemma 4, the primary gateway for local inference.
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** by unsloth (666 likes, 1M downloads): A highly efficient GGUF quantization of a Qwen 3.6 MoE model with Multi-Token Prediction.
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** by nvidia (191 likes, 822k downloads): Nvidia's first-party optimized NVFP4 variant of Qwen 3.6 MoE, combining quantization with hardware-level optimization.

## 3. Ecosystem Signal

The defining architectural trend of this ecosystem snapshot is the complete dominance of Mixture-of-Experts (MoE). From DeepSeek-V4 to Qwen3.6, Nemotron-3, LFM2.5, and Mellum2, every frontier model relies on sparse activation—signal that the industry has decisively pivoted from dense transformers for large-scale models. Nvidia has transformed into the most vertically integrated publisher on the Hub, releasing a full stack ranging from a 550B MoE LLM to specialized vision, video, and audio models, while using its proprietary NVFP4 quantization to lock the stack into its hardware ecosystem. Open-weight releases, led by DeepSeek's V4 family, continue to dominate over closed models in community traction.

Quantization is the unsung hero of real-world adoption: GGUF variants by Unsloth and NVFP4 variants by Nvidia consistently achieve downloads an order of magnitude higher than their original weight counterparts, proving that accessibility drives usage more than absolute precision. Finally, the explosion of new video generation models—Sulphur-2, Cosmos3, Bernini-R, LongCat—makes this the most dynamic sector of the month. The race for the best open-weight video model is the defining competitive narrative of mid-2026.

## 4. Worth Exploring

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** (deepseek-ai)
An essential baseline for the entire open-weight LLM ecosystem. Its staggering community adoption makes it the single most important model for understanding the current state-of-the-art in MoE language modeling.

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** (nvidia)
A standout for its elegant specialization. In a field crowded with general-purpose models, this compact 3B model solves a specific problem—object localization—and solves it extremely well. It provides a powerful case study in the growing demand for task-specific vision models.

3. **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** (SulphurAI)
The model that best captures the "Gen-Video" inflection point. Its explosive growth in downloads and likes solidifies text-to-video as the next great frontier, and studying its architecture and community reception is critical for anyone tracking where open generative AI is heading.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*