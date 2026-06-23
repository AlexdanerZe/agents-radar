# Hugging Face Trending Models Digest 2026-06-23

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-23 02:54 UTC

---

# Hugging Face Trending Models Digest | June 23, 2026

---

## 1. Today's Highlights

This week marks a decisive shift towards MoE architectures and unified multimodal models. DeepSeek-V4-Pro dominates the likes chart with unprecedented community engagement, while the Google Gemma 4 ecosystem undergoes massive adoption through widespread GGUF quantization for coding and agentic tasks. The Qwen3.x family remains the most active playground for community experimentation, with uncensored MoE merges and vision-coder hybrids surpassing millions of raw downloads. Meanwhile, infrastructure models like Nvidia's LocateAnything-3B and Microsoft's FastContext highlight a growing preference for efficient, specialized foundation models over generalist behemoths.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs)

**[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — Author: deepseek-ai | 5,013 likes | 2.4M downloads — The reigning heavyweight conversational model setting the open-weight performance baseline this week with massive community traction.

**[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — Author: zai-org | 2,044 likes | 33k downloads — Zhipu AI's latest MoE-DSA architecture rapidly became a headline release, quickly spawning an entire quantization ecosystem.

**[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — Author: microsoft | 289 likes | 3.5k downloads — A compact 4B model optimized for fast context retrieval and agentic sub-tasks, representing the industry push for smaller, deployable language backends.

---

### 🎨 Multimodal & Generation

**[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — Author: nvidia | 2,294 likes | 247k downloads — A powerful zero-shot object localization and grounding model trending for its remarkable accuracy in a lightweight 3B footprint.

**[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — Author: MiniMaxAI | 1,209 likes | 119k downloads — A comprehensive multimodal vision-language model strengthening MiniMax's position in the open-source MLLM space.

**[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — Author: google | 1,050 likes | 874k downloads — An innovative MoE diffusion transformer that bridges LLMs and generative image creation, making it the most architecturally experimental model this week.

**[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — Author: google | 1,139 likes | 1.9M downloads — Google's unified "any-to-any" model handling text, images, and speech in a single architecture, signaling the mature shift to native multimodal base models.

**[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — Author: nvidia | 631 likes | 34k downloads — A tiny 0.6B streaming ASR model with cache-aware architecture, trending for state-of-the-art real-time speech recognition on edge hardware.

**[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — Author: baidu | 192 likes | 47 downloads — A high-difficulty OCR solution leveraging visual LLMs for robust document parsing and text extraction.

**[ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora)** — Author: ostris | 102 likes | 3.2k downloads — A community LoRA fine-tune for Ideogram 4 optimizing inference speed while retaining output quality.

**[Boogu/Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)** — Author: Boogu | 101 likes | 473 downloads — A new entrant in the diffusion-based image editing space leveraging Diffusers for targeted modifications.

**[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** — Author: owensong | 167 likes | 0 downloads — An ultra-small TTS model designed for edge deployment, generating significant discussion in speech synthesis circles.

---

### 🔧 Specialized Models (Code, Math, Embeddings)

**[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — Author: WeiboAI | 615 likes | 32k downloads — A compact Qwen2-based model punching far above its weight in mathematical reasoning, trending for exceptional efficiency.

**[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — Author: moonshotai | 964 likes | 412k downloads — Kimi's advanced vision-capable code generation model with compressed tensors, gaining momentum for efficient multi-modal software development.

**[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — Author: CohereLabs | 481 likes | 21k downloads — Cohere's competitive MoE code model optimized for agentic coding workflows and efficient inference.

**[poolside/Laguna-M.1](https://huggingface.co/poolside/Laguna-M.1)** — Author: poolside | 91 likes | 2.7k downloads — A specialized software engineering model optimized for vLLM and SGLang, targeting the full development lifecycle.

**[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — Author: empero-ai | 131 likes | 842 downloads — A Qwen3.5-based reasoning fine-tune blending Claude-style outputs with open-weight flexibility.

**[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)** & **[LiquidAI/LFM2.5-ColBERT-350M](https://huggingface.co/LiquidAI/LFM2.5-ColBERT-350M)** — Authors: LiquidAI | 101 / 79 likes | 8.8k / 2.2k downloads — Liquid AI's latest embedding models offering efficient dense and ColBERT-based retrieval for RAG pipelines.

---

### 📦 Fine-tunes & Quantizations

**[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — Author: yuxinlu1 | 2,175 likes | 414k downloads — The definitive community GGUF of Gemma 4 for coding that has dominated local LLM quantizations this week.

**[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — Author: yuxinlu1 | 388 likes | 50k downloads — Agentic variant of the Gemma 4 GGUF specifically tuned for terminal and tool-use tasks.

**[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — Author: HauhauCS | 2,118 likes | 4M downloads — The most downloaded model on the entire list, this aggressive uncensored vision MoE GGUF satisfies massive demand for unconstrained generation.

**[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — Author: unsloth | 257 likes | 41k downloads — Unsloth's signature optimized GGUF release bringing the cutting-edge GLM-5.2 MoE model to consumer hardware.

**[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** — Author: zai-org | 133 likes | 334k downloads — The official FP8 quantization from Zhipu AI directly enabling high-efficiency production deployment of their flagship model.

**[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** — Author: Jackrong | 282 likes | 214k downloads — A highly popular vision-coder fusion of Qwen3.6 quantized with Multi-Token Prediction support for enhanced local reasoning.

**[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — Author: empero-ai | 140 likes | 6.6k downloads — The llama.cpp quantized companion to the widely-discussed Qwythos reasoning model.

**[bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)** — Author: bytkim | 107 likes | 52k downloads — A pi-tuned GGUF of Qwen3.6 27B bringing optimized MTP performance to local inference.

**[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)** — Author: Mia-AiLab | 125 likes | 23k downloads — A community GGUF merge of the Qwen3.6 family offering a balanced general-purpose option for local deployment.

**[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)** — Author: lordx64 | 162 likes | 3.7k downloads — A community fine-tune of Qwen3.5 MoE architecture blending vision and language capabilities.

**[datalab-to/lift](https://huggingface.co/datalab-to/lift)** — Author: datalab-to | 125 likes | 1.8k downloads — A Qwen3.5-based vision model specialized for PDF and document understanding.

---

## 3. Ecosystem Signal

The ecosystem has fully entered the "Era of MoE and Multimodal." Almost every flagship release this week (DeepSeek V4, GLM-5.2, DiffusionGemma, Gemma 4, Qwen3.6, North-Mini) leverages Mixture-of-Experts architecture, recognizing it as the definitive path to maximize performance without proportionally scaling compute. Equally significant is the shift from text-only to *native* multimodal base models: Google's "any-to-any" Gemma 4 and Nvidia's LocateAnything signal that future state-of-the-art will be designed from the ground up for multi-modality. On the community side, "uncensored" and "aggressive" tuned variants (led by HauhauCS Qwen merges) continue driving the highest raw download counts, indicating a large user segment prioritizing unrestrained generation. Quantization—specifically GGUF via llama.cpp—has evolved from a convenience layer into the primary distribution vector for local inference, democratizing access to massive MoE models like DeepSeek V4 and GLM-5.2 for users with limited hardware. The sheer breadth of activity around the Qwen3.x ecosystem suggests it has become the new "Llama" of the open-weight community for experimentation and fine-tuning.

---

## 4. Worth Exploring

**[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — This model perfectly embodies the current trend toward small, capable, and specialized. It solves a concrete pain point (visual grounding/localization) with remarkable accuracy in a tiny 3B footprint. Immediate utility for any engineers building multimodal pipelines, visual RAG systems, or robotics workflows.

**[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — A fascinating architectural innovation merging LLM and diffusion paradigms. Given its massive download count and unique "MoE diffusion transformer" design, it is highly recommended for researchers and engineers wanting to explore the next generation of generative models where language understanding and image creation converge.

**[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — Unavoidable given its overwhelming community engagement and benchmark performance. Anyone evaluating the cutting edge of open-weight conversational AI should start here to understand the new performance baseline set by the community's top-voted model this week.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*