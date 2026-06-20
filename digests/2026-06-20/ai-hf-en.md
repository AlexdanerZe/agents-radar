# Hugging Face Trending Models Digest 2026-06-20

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-20 03:23 UTC

---

# Hugging Face Trending Models Digest | June 20, 2026

## 1. Today's Highlights

The Hugging Face ecosystem is dominated this week by the explosive release of **DeepSeek-V4-Pro**, which secured the highest weekly like count (4,969) and is setting new expectations for open-weight reasoning and conversational AI. Meanwhile, Google's **Gemma 4** family has achieved critical mass, with the official `gemma-4-12B-it` and `diffusiongemma-26B-A4B-it` driving over 1.5M and 600K downloads respectively, while the community rushes to create specialized fine-tunes and quantizations. The **Qwen 3.6 MoE** ecosystem continues to define the fine-tuning landscape, led by an uncensored variant that amassed a staggering 3.7 million downloads—the highest of any model this week. In the specialized arena, **nvidia/LocateAnything-3B** is redefining vision-based localization, and **bosonai/higgs-audio-v3-tts-4b** signals that open-weight text-to-speech has finally reached production quality. Quantization infrastructure—led by **Unsloth**—has become a major vector for model adoption, with official GGUF releases for GLM-5.2, Kimi-K2.7-Code, and diffusiongemma.

---

## 2. Trending Models

### 🧠 Language Models

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  deepseek-ai | Likes: 4,969 | Downloads: 3,015,772  
  A flagship open-weight LLM setting new benchmarks for reasoning, conversational coherence, and long-context performance.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  zai-org | Likes: 1,546 | Downloads: 11,871  
  An advanced MoE architecture with Dynamic Sparse Attention, offering a competitive alternative to traditional dense LLMs for long-context generation.

---

### 🎨 Multimodal & Generation

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  nvidia | Likes: 2,195 | Downloads: 228,669  
  The highest-liked multimodal model this week, enabling zero-shot object localization and visual grounding in images.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  google | Likes: 1,096 | Downloads: 1,590,882  
  Google's unified any-to-any model natively processing text, image, and audio inputs, redefining small-scale multimodal capability.

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  google | Likes: 1,011 | Downloads: 601,208  
  A hybrid diffusion-and-language model bringing high-quality text-guided image generation into the LLM workflow.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  MiniMaxAI | Likes: 1,135 | Downloads: 67,836  
  A robust vision-language model pushing open-weight performance in image-text-to-text tasks.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  moonshotai | Likes: 910 | Downloads: 274,865  
  A vision-coder hybrid capable of reading diagrams, UI screenshots, and code simultaneously.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
  bosonai | Likes: 493 | Downloads: 69,143  
  A state-of-the-art open TTS model built on Qwen3, marking a quality inflection point for open-weight voice synthesis.

- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)**  
  prefeitura-rio | Likes: 325 | Downloads: 190,639  
  An enormous open MoE vision-language model that democratizes access to massive-scale multimodal understanding.

- **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)**  
  Zyphra | Likes: 116 | Downloads: 719  
  A high-fidelity Apache-2.0 TTS model carving a niche against proprietary offerings.

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**  
  zai-org | Likes: 235 | Downloads: 0  
  A pose-driven image-to-video diffusion model for controllable character animation.

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**  
  nex-agi | Likes: 336 | Downloads: 7,507  
  A Qwen3.5 MoE-based multimodal model balancing text generation and vision understanding.

- **[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)**  
  lordx64 | Likes: 130 | Downloads: 1,865  
  A fine-tuned Qwen3.5 MoE variant adapted for vision-language inference.

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)**  
  owensong | Likes: 124 | Downloads: 0  
  An ultra-small TTS model built for on-device speech synthesis.

---

### 🔧 Specialized Models

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  yuxinlu1 | Likes: 1,856 | Downloads: 268,102  
  The top specialized coding model this week, combining Gemma 4's base with a refined composer dataset for state-of-the-art local code generation.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  nvidia | Likes: 564 | Downloads: 18,809  
  A cache-aware streaming ASR model designed for real-time speech recognition on edge hardware.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**  
  CohereLabs | Likes: 459 | Downloads: 17,693  
  Cohere's MoE-powered compact code model delivering efficient, high-quality code generation.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)**  
  WeiboAI | Likes: 463 | Downloads: 12,148  
  A 3B math reasoning model that punches well above its weight class for constrained environments.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**  
  microsoft | Likes: 232 | Downloads: 1,437  
  Microsoft's exploration into efficient long-context attention mechanisms, optimized for massive sequence processing.

---

### 📦 Fine-tunes & Quantizations

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  HauhauCS | Likes: 2,010 | Downloads: 3,730,978  
  The most downloaded model of the week, an aggressive uncensored MoE fine-tune pushing creative and expressive freedom.

- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)**  
  DavidAU | Likes: 406 | Downloads: 588,753  
  An extreme community merge combining multiple high-performance model trajectories into a single uncensored thinking GGUF.

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)**  
  OBLITERATUS | Likes: 355 | Downloads: 106,885  
  The flagship "abliterated" Gemma 4 variant, removing alignment constraints for unrestricted creative use.

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)**  
  unsloth | Likes: 318 | Downloads: 202,867  
  Unsloth's official GGUF of Google's diffusion gemma, making high-quality generative vision accessible on consumer hardware.

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**  
  Jackrong | Likes: 261 | Downloads: 148,525  
  A specialized coding quantization of Qwen3.6 with Multi-Token Prediction support for faster inference.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**  
  yuxinlu1 | Likes: 107 | Downloads: 0  
  A forward-looking GGUF fine-tune explicitly optimized for tool-use and agentic coding workflows.

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)**  
  unsloth | Likes: 184 | Downloads: 8,392  
  The official Unsloth GGUF conversion of GLM-5.2, democratizing access to this complex MoE architecture.

- **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)**  
  unsloth | Likes: 141 | Downloads: 33,667  
  The GGUF pathway for Moonshot's vision-coder, enabling local multimodal code review.

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)**  
  zai-org | Likes: 105 | Downloads: 93,927  
  The official FP8 quantized variant of GLM-5.2 for high-throughput, low-latency inference.

- **[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)**  
  Mia-AiLab | Likes: 104 | Downloads: 16,105  
  A community GGUF conversion of the Qwen 3.6 architecture for accessible local inference.

- **[bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)**  
  bytkim | Likes: 86 | Downloads: 8,138  
  A tuned GGUF variant of Qwen 3.6 focusing on positional interpolation and Multi-Token Prediction.

---

## 3. Ecosystem Signal

This week's chart reveals a definitive shift toward **MoE saturation, open-weight dominance, and a thriving "uncensored" economy**. Qwen 3.6 MoE, GLM-5.2, and Cohere North Mini illustrate the industry's complete embrace of sparse activation for better efficiency. Google's **Gemma 4** strategy—releasing a strong base model and letting the community fine-tune it—is paying dividends, generating an entire ecosystem of coders, agents, and abliterated variants. The **uncensored modding movement** is the single largest download driver this week (HauhauCS, DavidAU, OBLITERATUS), indicating a massive user base prioritizing creative freedom over guardrails. **Unsloth** has cemented itself as the canonical quantization provider for major releases, effectively serving as the adoption bridge between raw model weights and local deployment. Finally, **open-weight audio generation** is crossing the quality chasm: models like Higgs Audio v3 and Nemotron ASR prove that fully open speech pipelines can now compete directly with proprietary walled gardens.

---

## 4. Worth Exploring

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – The highest-liked multimodal model this week for good reason. Its ability to perform open-vocabulary object localization without task-specific fine-tuning makes it a foundational utility for any AI vision pipeline.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** – Represents the gold standard of the current "specialized coder" trend. Combining Gemma 4's premier base architecture with a refined coding dataset and efficient GGUF quantization delivers the best local coding assistant experience this week.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** – Open-weight TTS has historically struggled with naturalness. This model marks a clear inflection point where an open-source TTS model rivals commercial offerings in quality, making it a must-study for voice interface developers.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*