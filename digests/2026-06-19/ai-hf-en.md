# Hugging Face Trending Models Digest 2026-06-19

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-19 03:59 UTC

---

**Hugging Face Trending Models Digest (June 19, 2026)**

---

### 1. Today's Highlights

DeepSeek-V4-Pro is the undisputed leader by likes this week, signaling a continued strong appetite for the most advanced open-weight reasoning models. Google's DiffusionGemma 26B and Gemma 4 12B both secure top spots, representing a major push towards unified any-to-any models and cementing the Gemma family as a cornerstone of the open ecosystem. NVIDIA's LocateAnything-3B demonstrates the rapidly rising demand for small, highly specialized vision models optimized for visual grounding and agentic workflows. Quantization activity around the new wave of base models (GLM-5.2, MiniMax-M3, DiffusionGemma, Kimi K2.7) is massive, with Unsloth and community contributors rapidly publishing GGUF variants to meet local inference demand. Finally, the prevalence of uncensored and experimental "composer" merges highlights a persistent community trend of aggressively fine-tuning models to push their behavioral and performance boundaries.

---

### 2. Trending Models

#### 🧠 Language Models

* **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — Author: deepseek-ai | Likes: 4,957 | Downloads: 2,948,726 — *The most-liked model of the week, DeepSeek's latest reasoning LLM proves its dominance in the open-weight frontier with massive community engagement.*
* **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — Author: zai-org | Likes: 1,361 | Downloads: 4,307 — *Zhipu AI's new MoE language model generates strong interest for its advanced DSA architecture, challenging established Western models in multilingual benchmarks.*
* **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — Author: nex-agi | Likes: 329 | Downloads: 6,640 — *An agent-centric model built on Qwen 3.5 MoE, signaling the growing demand for LLMs optimized for autonomous task execution.*
* **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — Author: microsoft | Likes: 207 | Downloads: 957 — *Microsoft's efficient long-context specialist, fine-tuned from Qwen3 to push the boundaries of retrieval and reasoning over extended documents.*
* **[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)** — Author: lordx64 | Likes: 120 | Downloads: 836 — *A community-tuned variant of the Qwen 3.5 MoE, highlighting the vibrant fine-tuning ecosystem around the Qwen architecture.*

#### 🎨 Multimodal & Generation

* **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — Author: nvidia | Likes: 2,166 | Downloads: 183,093 — *NVIDIA's compact visual grounding model is a standout this week for its incredible zero-shot localization utility in vision agents.*
* **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — Author: MiniMaxAI | Likes: 1,102 | Downloads: 56,162 — *MiniMax's flagship multimodal MoE, directly competing with proprietary VLMs like GPT-4o, is a key model to watch in the open-source vision space.*
* **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — Author: google | Likes: 1,085 | Downloads: 1,309,625 — *Google's unified any-to-any model generates massive downloads, setting a new standard for native multimodal processing in the open community.*
* **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — Author: google | Likes: 1,005 | Downloads: 527,080 — *A novel diffusion-based language model from Google, challenging the autoregressive paradigm and generating huge excitement for its architectural innovation.*
* **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — Author: bosonai | Likes: 489 | Downloads: 57,380 — *A leading open-source TTS model based on Qwen3 audio, recognized for exceptional naturalness and voice quality.*
* **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — Author: nvidia | Likes: 544 | Downloads: 13,033 — *NVIDIA's efficient streaming ASR model, optimized for cache-aware low-latency speech recognition, showcasing niche specialization.*
* **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)** — Author: prefeitura-rio | Likes: 324 | Downloads: 190,501 — *A massive open-weight VL MoE, this model attracts attention for scaling multimodal reasoning in a fully open format.*
* **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — Author: zai-org | Likes: 228 | Downloads: 0 — *Zhipu's image-to-video diffusion character animation model, unique in the top 30, it trends for its specialist video generation capabilities.*
* **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)** — Author: Zyphra | Likes: 115 | Downloads: 669 — *A high-quality text-to-speech model released under Apache 2.0, contributing to the renaissance of open TTS.*
* **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** — Author: owensong | Likes: 93 | Downloads: 0 — *An ultra-small TTS model, targeting edge deployment and demonstrating the breadth of the audio generation ecosystem.*

#### 🔧 Specialized Models

* **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — Author: yuxinlu1 | Likes: 1,719 | Downloads: 211,424 — *A highly popular community-crafted coding fine-tune merge of Gemma-4, proving the community's strong appetite for specialized code reasoning quantizations.*
* **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — Author: moonshotai | Likes: 889 | Downloads: 229,156 — *Moonshot AI's vision-code model blends visual understanding with code generation, trending for its unique dual-domain specialization.*
* **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — Author: WeiboAI | Likes: 410 | Downloads: 6,589 — *A compact 3B model excelling at mathematical reasoning, demonstrating that domain-specific small models can still generate significant community interest.*
* **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — Author: CohereLabs | Likes: 450 | Downloads: 15,285 — *Cohere's entry into the open code model space, utilizing an efficient MoE architecture and marking a major expansion of its model ecosystem.*
* **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** — Author: Jackrong | Likes: 251 | Downloads: 122,175 — *A quantized vision-coder fine-tune from the Qwen 3.6 family, representing the convergence of multimodal and coding inference for local use.*

#### 📦 Fine-tunes & Quantizations

* **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — Author: HauhauCS | Likes: 1,971 | Downloads: 3,420,052 — *The top fine-tuned model by downloads, this aggressively uncensored and quantized Qwen 3.6 MoE variant captures immense attention through unfiltered performance.*
* **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)** — Author: DavidAU | Likes: 395 | Downloads: 529,069 — *An extraordinarily complex "composer" fine-tune merge, the ultimate example of the community's trend of pushing models towards maximal capabilities in a single file.*
* **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** — Author: OBLITERATUS | Likes: 351 | Downloads: 96,805 — *The "abliterated" version of Gemma-4-12B continues the strong tradition of alignment removal from major new base models.*
* **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — Author: unsloth | Likes: 653 | Downloads: 918,431 — *Unsloth's timely and highly optimized GGUF quantization is the premier gateway for the community to run Google's flagship unified model locally.*
* **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** — Author: unsloth | Likes: 307 | Downloads: 164,209 — *Bringing Google's novel diffusion LLM to consumer hardware via efficient quantization, driving significant experimentation.*
* **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)** — Author: unsloth | Likes: 135 | Downloads: 29,287 — *The GGUF quant of Moonshot's vision-coder, making it accessible to a wider audience of local inference developers.*
* **[unsloth/MiniMax-M3-GGUF](https://huggingface.co/unsloth/MiniMax-M3-GGUF)** — Author: unsloth | Likes: 103 | Downloads: 22,659 — *Unsloth's efficient quantization of the MiniMax M3 multimodal MoE, enabling broad community access.*
* **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — Author: unsloth | Likes: 126 | Downloads: 305 — *The community gateway to running Zhipu's GLM-5.2 on consumer hardware via Unsloth's optimized recipes.*
* **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** — Author: zai-org | Likes: 91 | Downloads: 24,967 — *The official FP8 quantization of GLM-5.2, providing an expert-crafted efficient variant for higher-end local deployment.*
* **[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)** — Author: Mia-AiLab | Likes: 95 | Downloads: 2,496 — *A community GGUF quantization of the Qwen 3.6 family, adding another option to the rich ecosystem of Qwen-derived local models.*

---

### 3. Ecosystem Signal

The ecosystem is heavily coalescing around a powerful set of base architectures: DeepSeek V4, the Qwen 3.x/3.6 MoE family, Google's Gemma 4, Zhipu's GLM-5, and MiniMax M3 define the current frontier. The open-weight ecosystem is incredibly vibrant, with DeepSeek and Google pushing state-of-the-art standards openly while companies like Cohere and Moonshot AI actively enter the space. Quantization remains the primary driver of raw engagement; Unsloth expertly quantizes every major release within hours, driving massive download volumes. The prevalence of GGUF and FP8 formats highlights the community's overwhelming preference for local inference. Fine-tuning trends persist, with "uncensoring" and "abliteration" applied ritually to every major new base model. Additionally, aggressive "composer" merges (such as DavidAU's) blend multiple objectives into single files, representing a new peak of community experimentation. Crucially, multimodality is now the default expectation—top LLMs like Gemma 4, Qwen 3.6, and Kimi K2.7 are native vision-text models, indicating the community expects integrated vision capabilities out-of-the-box.

---

### 4. Worth Exploring

1.  **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — As the absolute leader in likes this week, it represents the current pinnacle of open-weight reasoning. Evaluating it provides a clear, definitive benchmark for the state of the entire frontier model landscape and is essential for anyone tracking LLM capabilities.

2.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — This model perfectly exemplifies the "small, specific, and powerful" trend that is reshaping deployment strategies. Its extraordinary utility for developers building visual agentic systems and its minimal footprint make it one of the most practically applicable models on the list.

3.  **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — Architecturally unique in the top 30, this diffusion-based language model challenges the autoregressive status quo. Studying it offers critical insight into the future of non-autoregressive generation and represents a potential paradigm shift in how generative AI is approached.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*