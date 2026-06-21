# Hugging Face Trending Models Digest 2026-06-21

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-21 03:52 UTC

---

# Hugging Face Trending Models Digest | 2026-06-21

## 1. Today's Highlights

This week's trending models confirm a decisive shift toward **Mixture-of-Experts (MoE) architectures** as the dominant paradigm for open-weight LLMs, with DeepSeek-V4-Pro and GLM-5.2 leading the charge. Google's **Gemma-4 family** is experiencing explosive ecosystem growth, having already spawned specialized GGUF fine-tunes and a diffusion hybrid that together have accrued millions of downloads. The **uncensored fine-merge culture** remains immensely powerful, particularly around the Qwen3.6 backbone, which powers this week's most-downloaded model. Meanwhile, **audio and vision infrastructure** is surging, as streaming ASR, TTS, grounding, and video generation models reach production quality in the open-source domain.

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

**DeepSeek-V4-Pro** ([link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro))
Author: deepseek-ai | Likes: 4,987 | Downloads: 2,797,050
The undisputed champion this week, this flagship MoE conversational model sets the benchmark for open-weight reasoning and performance.

**GLM-5.2** ([link](https://huggingface.co/zai-org/GLM-5.2))
Author: zai-org | Likes: 1,704 | Downloads: 19,683
The latest generation of the GLM MoE series, sparking immediate and massive quantization adoption across the community.

**Rio-3.5-Open-397B** ([link](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B))
Author: prefeitura-rio | Likes: 327 | Downloads: 190,694
A monumental 397B MoE model pushing the frontier of openly available scale for conversational and vision tasks.

**FastContext-1.0-4B-SFT** ([link](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT))
Author: microsoft | Likes: 245 | Downloads: 1,998
Microsoft's long-context specialist optimized for "Explorer SubAgent" capabilities and extended reasoning.

**Nex-N2-Pro** ([link](https://huggingface.co/nex-agi/Nex-N2-Pro))
Author: nex-agi | Likes: 340 | Downloads: 7,724
A strong Qwen3.5-MoE based conversational model gaining steady community traction.

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

**MiniMax-M3** ([link](https://huggingface.co/MiniMaxAI/MiniMax-M3))
Author: MiniMaxAI | Likes: 1,163 | Downloads: 85,771
Leading vision-language model from MiniMax, pushing the boundaries of multimodal interaction.

**diffusiongemma-26B-A4B-it** ([link](https://huggingface.co/google/diffusiongemma-26B-A4B-it))
Author: google | Likes: 1,024 | Downloads: 673,464
An experimental diffusion-LLM hybrid that represents one of the most architecturally novel releases this cycle.

**gemma-4-12B-it** ([link](https://huggingface.co/google/gemma-4-12B-it))
Author: google | Likes: 1,107 | Downloads: 1,696,240
Google's unified any-to-any model bringing strong multimodal reasoning to the rapidly growing Gemma-4 ecosystem.

**LocateAnything-3B** ([link](https://huggingface.co/nvidia/LocateAnything-3B))
Author: nvidia | Likes: 2,217 | Downloads: 235,606
The definitive visual grounding model, essential building block for computer-use agents and visual RAG.

**nemotron-3.5-asr-streaming-0.6b** ([link](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b))
Author: nvidia | Likes: 588 | Downloads: 21,426
High-efficiency streaming ASR enabling low-latency, real-time voice interaction pipelines.

**SCAIL-2** ([link](https://huggingface.co/zai-org/SCAIL-2))
Author: zai-org | Likes: 241 | Downloads: 0
State-of-the-art image-to-video generation for pose-driven character animation via diffusion.

**higgs-audio-v3-tts-4b** ([link](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b))
Author: bosonai | Likes: 499 | Downloads: 72,225
BosonAI's powerful 4B TTS model within the Higgs multimodal family, demonstrating production-ready voice synthesis.

**Inflect-Nano-v1** ([link](https://huggingface.co/owensong/Inflect-Nano-v1))
Author: owensong | Likes: 143 | Downloads: 0
An ultra-small text-to-speech model optimized for edge and mobile deployment.

**ideogram_4_turbotime_lora** ([link](https://huggingface.co/ostris/ideogram_4_turbotime_lora))
Author: ostris | Likes: 83 | Downloads: 1,679
The standout LoRA adapter for accelerating Ideogram 4 image generation workflows.

**lift** ([link](https://huggingface.co/datalab-to/lift))
Author: datalab-to | Likes: 89 | Downloads: 0
A specialized Qwen3.5-based vision-language model optimized for high-precision PDF and document extraction.

---

### 🔧 Specialized Models (code, math, medical, embeddings)

**Kimi-K2.7-Code** ([link](https://huggingface.co/moonshotai/Kimi-K2.7-Code))
Author: moonshotai | Likes: 932 | Downloads: 317,963
A compressed, coding-optimized vision-language model achieving exceptional performance density for coding agents.

**North-Mini-Code-1.0** ([link](https://huggingface.co/CohereLabs/North-Mini-Code-1.0))
Author: CohereLabs | Likes: 468 | Downloads: 18,783
Cohere's conversational MoE coding model, built for agentic code generation and tool use.

**VibeThinker-3B** ([link](https://huggingface.co/WeiboAI/VibeThinker-3B))
Author: WeiboAI | Likes: 515 | Downloads: 16,270
A compact 3B model punching well above its weight in math and reasoning tasks, proving small models still have a vital role.

**LFM2.5-Embedding-350M** ([link](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M))
Author: LiquidAI | Likes: 81 | Downloads: 6,128
Liquid AI's leading embedding model, providing a critical foundation for high-performance RAG infrastructure.

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

**Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))
Author: HauhauCS | Likes: 2,043 | Downloads: 3,812,636
The most downloaded model this entire week—an uncensored vision MoE GGUF pack that captured a massive user base.

**gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF))
Author: yuxinlu1 | Likes: 1,993 | Downloads: 312,332
The definitive GGUF pack for the Gemma-4 Coder, making local code development with Gemma-4 instantly accessible.

**gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF))
Author: yuxinlu1 | Likes: 190 | Downloads: 6,307
An agentic-tuned variant of the Gemma-4 GGUF series, optimized for terminal and tool-use workloads.

**GLM-5.2-GGUF** ([link](https://huggingface.co/unsloth/GLM-5.2-GGUF))
Author: unsloth | Likes: 207 | Downloads: 22,586
Unsloth's rapid GGUF deployment of GLM-5.2, enabling local inference shortly after the base model release.

**GLM-5.2-FP8** ([link](https://huggingface.co/zai-org/GLM-5.2-FP8))
Author: zai-org | Likes: 116 | Downloads: 138,174
The official FP8 quantization of GLM-5.2 for high-efficiency inference deployment.

**Kimi-K2.7-Code-GGUF** ([link](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF))
Author: unsloth | Likes: 147 | Downloads: 37,260
Community GGUF conversion of the highly popular Kimi-K2.7-Code, extending its reach to local users.

**Qwopus3.6-27B-Coder-MTP-GGUF** ([link](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF))
Author: Jackrong | Likes: 269 | Downloads: 168,502
A community merge integrating Multi-Token Prediction into Qwen3.6 27B for enhanced code generation.

**Qwable-3.6-27b** ([link](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b))
Author: Mia-AiLab | Likes: 112 | Downloads: 17,311
Base Qwen3.6 GGUF variant for community experimentation and further fine-tuning.

**Qwen3.6-27B-MTP-pi-tune-GGUF** ([link](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF))
Author: bytkim | Likes: 98 | Downloads: 20,465
Specialized Pi-tune GGUF of Qwen3.6 MTP for targeted instruction following tasks.

**Qwable-v1** ([link](https://huggingface.co/lordx64/Qwable-v1))
Author: lordx64 | Likes: 138 | Downloads: 2,769
A popular community fine-tune of Qwen3.5 MoE optimized for vision-language tasks.

**Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF** ([link](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF))
Author: DavidAU | Likes: 411 | Downloads: 587,521
The definitive community "fine-merge" of the week, combining multiple fine-tune lineages into a dense reasoning and coding powerhouse.

## 3. Ecosystem Signal

The top 30 for June 21 reveals a clear consensus: **Mixture-of-Experts architectures are no longer experimental—they are the mainstream.** From DeepSeek-V4 to GLM-5.2 and the myriad of Qwen3.x MoE variants, the ecosystem has fully adopted parameter-efficient scaling. Meanwhile, **Google's Gemma-4 family is undergoing unprecedented community expansion**, with GGUF fine-tunes generating millions of downloads within days, highlighting the hunger for local, customizable multimodal models. The unrelenting demand for **uncensored and deeply merged fine-tunes** continues, with the Qwen3.6 backbone acting as the primary canvas. Finally, a strong **specialization trend** is emerging: embedding models (LiquidAI), math models (VibeThinker-3B), and streaming audio (NVIDIA, BosonAI) indicate that the community is moving beyond generic chatbots towards building concrete, production-ready agentic pipelines.

## 4. Worth Exploring

**google/diffusiongemma-26B-A4B-it** — The most architecturally daring model in the lineup. This diffusion-LLM hybrid represents a potential paradigm shift in how multimodal generation models reason and create, making it essential for anyone tracking the cutting edge of model design.

**nvidia/LocateAnything-3B** — Validated by over 2,200 community likes, this grounding model is a foundational building block for computer-use agents and visual search systems. It exemplifies how specialized, production-ready tools are dominating their niches.

**deepseek-ai/DeepSeek-V4-Pro** — With nearly 5,000 likes, it has captured the collective imagination of the open-weight community. It serves as the current baseline for MoE performance and should be the first model evaluated for any serious production reasoning pipeline.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*