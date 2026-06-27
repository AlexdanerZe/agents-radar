# Hugging Face Trending Models Digest 2026-06-27

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-27 02:49 UTC

---

Here is your structured Hugging Face Trending Models Digest for **June 27, 2026**.

---

## 1. Today's Highlights

This week’s leaderboard represents a decisive inflection point for the open-source AI ecosystem. **Mixture-of-Experts (MoE)** architectures have gone from cutting-edge to completely dominant, with GLM‑5.2, the Ornith family, and Qwen’s AgentWorld sweeping the charts. Simultaneously, the quantization war is reaching fever pitch: NVIDIA’s **NVFP4** format scored a blockbuster week (over 4.8M downloads for a single variant), directly challenging the GGUF/llama.cpp ecosystem led by Unsloth. The massive community success of **agentic** models (FastContext, Qwen-AgentWorld, terminal-tuned Gemma‑4) confirms that autonomous tool-use is no longer a lab curiosity, while “uncensored” and “abliterated” fine-tunes continue to generate millions of downloads, proving that a large segment of users prioritizes creative flexibility over safety alignment.

## 2. Trending Models

### 🧠 Language Models

* **GLM-5.2** ([Link](https://huggingface.co/zai-org/GLM-5.2)) by zai-org — 2,603 Likes | 83,589 Downloads  
  Zhipu AI’s latest MoE conversational model featuring Dynamic Sparse Attention, trending heavily as the community benchmarks its novel architecture.

* **Ornith-1.0 Series** (397B, 35B, 9B) ([Link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)) by deepreinforce‑ai — 107–241 Likes | 126–3,002 Downloads  
  A family of Qwen‑3.5 MoE models spanning 9B to 397B total parameters, offering a unified architecture for scaling reasoning across compute budgets.

* **Qwythos-9B-Claude-Mythos-5-1M** ([Link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)) by empero‑ai — 452 Likes | 20,346 Downloads  
  A creative fine-tune blending Qwen‑3.5 with synthetic Claude reasoning traces, gaining traction for its unique holistic output style.

* **LiquidAI LFM2.5-230M** ([Link](https://huggingface.co/LiquidAI/LFM2.5-230M)) by LiquidAI — 114 Likes | 8,286 Downloads  
  A highly compact 230M parameter model that challenges the assumption that scale alone drives performance.

* **DeepSeek-v4-Fable** ([Link](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)) by Chunjiang‑Intelligence — 108 Likes | 1,103 Downloads  
  A specialized cybersecurity LLM based on DeepSeek v4, highlighting the trend of vertical fine-tuning on top of strong base models.

---

### 🎨 Multimodal & Generation

* **MiniMax-M3** ([Link](https://huggingface.co/MiniMaxAI/MiniMax-M3)) by MiniMaxAI — 1,247 Likes | 169,951 Downloads  
  A leading open multimodal MoE model excelling at image and video comprehension, setting a new benchmark for open‑weight vision-language AI.

* **baidu/Unlimited-OCR** ([Link](https://huggingface.co/baidu/Unlimited-OCR)) by baidu — 1,046 Likes | 134,146 Downloads  
  A robust OCR model for complex document text extraction, catching fire in the enterprise document AI community.

* **krea/Krea-2-Turbo** ([Link](https://huggingface.co/krea/Krea-2-Turbo)) by krea — 285 Likes | 8,721 Downloads  
  krea’s latest text-to-image model, offering significantly faster inference than its predecessor while maintaining high generation quality.

* **nvidia/LocateAnything-3B** ([Link](https://huggingface.co/nvidia/LocateAnything-3B)) by nvidia — 2,385 Likes | 494,756 Downloads  
  A lightweight, highly specialized model for precise object localization and visual grounding, demonstrating strong demand for fine-grained vision tools.

* **datalab-to/lift** ([Link](https://huggingface.co/datalab-to/lift)) by datalab‑to — 159 Likes | 6,054 Downloads  
  A specialized suite for PDF and document understanding, riding the wave of enterprise interest in automated data extraction.

* **nvidia/nemotron-3.5-asr-streaming-0.6b** ([Link](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)) by nvidia — 709 Likes | 56,434 Downloads  
  A low-latency streaming speech-to-text (ASR) model, reflecting the growing importance of real-time voice interfaces.

* **Comfy-Org/Krea-2** ([Link](https://huggingface.co/Comfy-Org/Krea-2)) by Comfy‑Org — 137 Likes | 10 Downloads  
  The official ComfyUI workflow for Krea-2, making the popular image generation pipeline easily reproducible.

---

### 🔧 Specialized Models

* **microsoft/FastContext-1.0-4B-SFT** ([Link](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)) by microsoft — 355 Likes | 5,735 Downloads  
  A compact 4B model fine-tuned for long-context reasoning and sub‑agent orchestration, marking a key milestone in accessible agentic AI.

* **Qwen-AgentWorld-35B-A3B** ([Link](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)) by Qwen — 323 Likes | 13,186 Downloads  
  Qwen’s dedicated agent model routing a 35B total parameter count through an extremely efficient 3B active MoE for complex tool-use and simulation.

* **WeiboAI/VibeThinker-3B** ([Link](https://huggingface.co/WeiboAI/VibeThinker-3B)) by WeiboAI — 734 Likes | 54,638 Downloads  
  An exceptionally strong 3B model for mathematical reasoning, proving that specialized fine-tuning can create state-of-the-art performance at tiny scales.

---

### 📦 Fine-tunes & Quantizations

* **nvidia/Qwen3.6-35B-A3B-NVFP4** ([Link](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)) by nvidia — 361 Likes | **4,812,629 Downloads**  
  The week’s most downloaded model by a wide margin, using NVIDIA’s novel NVFP4 format to make the powerful Qwen MoE extremely efficient on recent GPUs.

* **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** ([Link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)) by yuxinlu1 — 2,402 Likes | 516,333 Downloads  
  The premier coding fine-tune of Google’s Gemma‑4, perfectly optimized for local usage and dominating the community coding quantization space.

* **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([Link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)) by HauhauCS — 2,265 Likes | 3,453,492 Downloads  
  A massively popular uncensored Qwen MoE fine-tune, demonstrating the enormous and sustained demand for unrestrained creative model outputs.

* **unsloth/GLM-5.2-GGUF** ([Link](https://huggingface.co/unsloth/GLM-5.2-GGUF)) by unsloth — 411 Likes | 107,553 Downloads  
  Unsloth’s highly optimized GGUF quantization tree for the GLM‑5.2, providing comprehensive bitrate options for the llama.cpp ecosystem.

* **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** ([Link](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)) by yuxinlu1 — 690 Likes | 186,663 Downloads  
  A companion agentic fine-tune of Gemma‑4, optimized for terminal use and autonomous task execution.

* **huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated** ([Link](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)) by huihui‑ai — 136 Likes | 5,445 Downloads  
  An “abliterated” safety-removed version of the Gemma‑4 coder, enabling maximum creative flexibility for advanced local users.

* **HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced** ([Link](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)) by HauhauCS — 93 Likes | 23,772 Downloads  
  A “balanced” uncensored variant of Gemma‑4, broadening the accessible fine-tune options for Google’s latest dense model.

* **Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF** ([Link](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)) by Jackrong — 95 Likes | 35,027 Downloads  
  A GGUF quantization of a powerful vision-coder MoE model, catering to the growing niche of multimodal coding assistants.

---

## 3. Ecosystem Signal

The current trending landscape signals a **decisive shift toward Mixture-of-Experts (MoE)** as the dominant architecture for high-performance open-weight models. GLM‑5.2, the entire Ornith line, Qwen’s AgentWorld, and MiniMax‑M3 all leverage sparse MoE routing to pack immense capability into efficient parameter budgets. This architectural choice creates a massive downstream tension: the **compression of these sparse models** is the central opportunity of the moment. **NVFP4** and **GGUF** are locked in a format war, with NVIDIA scoring a massive adoption coup via the Qwen3.6‑NVFP4 release.

Beyond architecture, the **“Agentic Turn”** is no longer hypothetical. Microsoft’s FastContext, Qwen’s AgentWorld, and yuxinlu1’s terminal-tuned Gemma‑4 quantizations demonstrate that the community is voting heavily for models that orchestrate tools and perform autonomous tasks. The persistent power of the **“Uncensored” ecosystem** cannot be overstated: HauhauCS and huihui‑ai have cornered a massive market that prioritizes unrestricted outputs over safety alignment, often generating millions of downloads per release. Finally, **Google’s Gemma‑4** proves that well-trained dense models still command fierce loyalty—its strong coding performance made it the foundation for some of the week’s most liked fine-tunes, holding its own in an otherwise MoE-dominated landscape.

## 4. Worth Exploring

* **nvidia/Qwen3.6-35B-A3B-NVFP4** ([Link](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4))  
  Explosive download counts (4.8M) make this a **must-study artifact**. It perfectly demonstrates the market’s massive appetite for efficiently packed MoE power and represents the first serious challenger to GGUF in the high-performance quantization space.

* **MiniMax-M3** ([Link](https://huggingface.co/MiniMaxAI/MiniMax-M3))  
  The clearest signal yet that **open-source multimodal MoE is maturing rapidly**. As a viable competitor to proprietary vision-language models, its architecture and performance set a new benchmark that researchers and builders should closely examine.

* **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** ([Link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF))  
  The ultimate template for a **breakthrough community fine-tune**. By pairing Google’s excellent Gemma‑4 base with a highly targeted coding dataset and perfect GGUF packaging, this model became a local-dev essential (2.4k likes, 516k downloads) and a blueprint for ecosystem success.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*