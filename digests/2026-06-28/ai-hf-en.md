# Hugging Face Trending Models Digest 2026-06-28

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-28 03:30 UTC

---

Here is your structured Hugging Face Trending Models Digest for June 2026.

---

## 1. Today’s Highlights

The Hugging Face ecosystem this week has rallied around a handful of powerful architectural backbones—**Qwen 3.5/3.6**, **Gemma‑4**, and **GLM‑5.2**—which collectively underpin the vast majority of viral community releases. Quantization and fine‑tuning are the dominant distribution vectors: **HauhauCS**, **yuxinlu1**, and **empero‑ai** have driven multi‑million downloads with uncensored, coding, and creative‑reasoning variants. On the frontier, **DeepSeek** dropped the **V4‑Pro‑DSpark** model while **NVIDIA** delivered a trio of impactful specialized releases spanning object localization, streaming ASR, and efficient FP4 quantization. The **Krea‑2** family also marks a significant leap forward for open‑source text‑to‑image generation.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction‑tuned)

**zai‑org/GLM‑5.2** ([Link](https://huggingface.co/zai-org/GLM-5.2))  
Author: zai‑org | 2,690 likes | 98,994 downloads  
The flagship open‑weight MoE language model from Zhipu AI, building the largest community infrastructure of quants and fine‑tunes this cycle.

**deepseek‑ai/DeepSeek‑V4‑Pro‑DSpark** ([Link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark))  
Author: deepseek‑ai | 132 likes | 0 downloads  
DeepSeek’s frontier reasoning model, representing a major step forward in open‑weight LLM research and competition.

**Qwen/Qwen‑AgentWorld‑35B‑A3B** ([Link](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B))  
Author: Qwen | 362 likes | 18,872 downloads  
An efficient 35B‑A3B MoE model from Qwen specifically designed for complex agentic and tool‑use workflows.

**LiquidAI/LFM2.5‑230M** ([Link](https://huggingface.co/LiquidAI/LFM2.5-230M))  
Author: LiquidAI | 130 likes | 9,791 downloads  
A small yet capable 230M‑parameter model exploring non‑transformer architectures for efficient edge deployment.

---

### 🎨 Multimodal & Generation (image, video, audio, text‑to‑X)

**baidu/Unlimited‑OCR** ([Link](https://huggingface.co/baidu/Unlimited-OCR))  
Author: baidu | 1,143 likes | 212,760 downloads  
A comprehensive scene‑text recognition and extraction model that sets a new high bar for open‑source OCR.

**empero‑ai/Qwythos‑9B‑Claude‑Mythos‑5‑1M** ([Link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M))  
Author: empero‑ai | 491 likes | 30,298 downloads  
A creative community multimodal merge blending Qwen 3.5 with the structured reasoning traces of Mythos 5.

**krea/Krea‑2‑Raw** ([Link](https://huggingface.co/krea/Krea-2-Raw)) & **krea/Krea‑2‑Turbo** ([Link](https://huggingface.co/krea/Krea-2-Turbo))  
Author: krea | ~500 total likes | ~35k total downloads  
A new state‑of‑the‑art open‑source text‑to‑image family, quickly becoming the community standard for high‑quality generative art.

**nvidia/LocateAnything‑3B** ([Link](https://huggingface.co/nvidia/LocateAnything-3B))  
Author: nvidia | 2,409 likes | 570,466 downloads  
A transformative zero‑shot object localization model that finds any promptable object in an image without task‑specific training.

**nvidia/nemotron‑3.5‑asr‑streaming‑0.6b** ([Link](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b))  
Author: nvidia | 719 likes | 61,857 downloads  
A low‑latency streaming speech recognition model optimized for real‑time interactive applications.

**MiniMaxAI/MiniMax‑M3** ([Link](https://huggingface.co/MiniMaxAI/MiniMax-M3))  
Author: MiniMaxAI | 1,253 likes | 182,714 downloads  
An exceptionally capable and permissively licensed multimodal foundation model, often overlooked among larger ecosystems.

**deepreinforce‑ai/Ornith‑1.0‑9B / 35B / 397B** ([Link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B))  
Author: deepreinforce‑ai | ~460 total likes | ~9k total downloads  
A complete open family of MoE multimodal models scaling from 9B to 397B parameters.

---

### 🔧 Specialized Models (code, math, medical, embeddings, long‑context)

**WeiboAI/VibeThinker‑3B** ([Link](https://huggingface.co/WeiboAI/VibeThinker-3B))  
Author: WeiboAI | 742 likes | 57,521 downloads  
A masterclass in targeted efficient scaling: a compact 3B math‑reasoning model that rivals much larger generalists on mathematical benchmarks.

**microsoft/FastContext‑1.0‑4B‑SFT** ([Link](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT))  
Author: microsoft | 366 likes | 6,447 downloads  
A purpose‑built 4B model pushing the frontier of extreme long‑context reasoning, ideal for RAG and document extraction pipelines.

**Chunjiang‑Intelligence/DeepSeek‑v4‑Fable** ([Link](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable))  
Author: Chunjiang‑Intelligence | 113 likes | 1,328 downloads  
A specialized DeepSeek‑v4 fine‑tune tailored for cybersecurity and threat analysis use‑cases.

---

### 📦 Fine‑tunes & Quantizations (community fine‑tunes, GGUF, AWQ, NVFP4)

**HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive** ([Link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))  
Author: HauhauCS | 2,279 likes | 3,331,475 downloads  
The viral sensation of the week: an uncensored, aggressive‑persona GGUF of Qwen 3.6 MoE, dominating local inference charts.

**yuxinlu1/gemma‑4‑12B‑coder‑fable5‑composer2.5‑v1‑GGUF** ([Link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF))  
Author: yuxinlu1 | 2,428 likes | 536,130 downloads  
The most popular Gemma‑4 coding quant, enabling powerful agentic code generation on consumer hardware.

**unsloth/GLM‑5.2‑GGUF** ([Link](https://huggingface.co/unsloth/GLM-5.2-GGUF))  
Author: unsloth | 426 likes | 125,230 downloads  
Unsloth’s highly optimized GGUF quants, the primary gateway for local GLM‑5.2 usage.

**nvidia/Qwen3.6‑35B‑A3B‑NVFP4** ([Link](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4))  
Author: nvidia | 367 likes | 5,022,254 downloads  
The highest‑download single file this cycle—NVIDIA’s enterprise‑grade FP4 quantization for Qwen 3.6 MoE.

**empero‑ai/Qwythos‑9B‑Claude‑Mythos‑5‑1M‑GGUF** ([Link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF))  
Author: empero‑ai | 680 likes | 712,627 downloads  
The GGUF entry point for the popular Qwythos multimodal fine‑tune, making it widely accessible.

**huihui‑ai/Huihui‑gemma‑4‑12B‑coder‑fable5‑composer2.5‑v1‑abliterated** ([Link](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated))  
Author: huihui‑ai | 137 likes | 6,250 downloads  
The abliterated (safety‑removed) version of the popular Gemma‑4 coder fine‑tune.

**HauhauCS/Gemma4‑12B‑QAT‑Uncensored‑HauhauCS‑Balanced** ([Link](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced))  
Author: HauhauCS | 97 likes | 32,222 downloads  
An uncensored Gemma‑4 quant optimized via Quantization‑Aware Training for a balance of performance and safety removal.

**deepreinforce‑ai/Ornith‑1.0‑35B‑GGUF** ([Link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)) & **Ornith‑1.0‑9B‑GGUF** ([Link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF))  
Author: deepreinforce‑ai | ~550 total likes | ~31k total downloads  
Bringing the powerful Ornith MoE multimodal family to local CPU/GPU inference via standard GGUF formats.

**Jackrong/Qwopus3.6‑27B‑Coder‑Compat‑MTP‑GGUF** ([Link](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF))  
Author: Jackrong | 97 likes | 49,935 downloads  
A code‑focused quant of a Qwen 3.6 multimodal variant with MTP compatibility.

**nvidia/GLM‑5.2‑NVFP4** ([Link](https://huggingface.co/nvidia/GLM-5.2-NVFP4))  
Author: nvidia | 132 likes | 6,464 downloads  
Official NVIDIA FP4 quantization for GLM‑5.2, enabling high‑throughput enterprise deployment.

**Note:** *Comfy‑Org/Krea‑2* ([Link](https://huggingface.co/Comfy-Org/Krea-2)) is not a model itself but a ComfyUI integration pack for the Krea‑2 family, further underscoring the rapid adoption of the model in production workflows.

---

## 3. Ecosystem Signal

The dense concentration of fine‑tunes and quants around **Qwen 3.6**, **Gemma‑4**, and **GLM‑5.2** signals a strong consolidation of community engineering efforts around three vital architectures. Quantization has bifurcated into two clear streams: **hobbyist/local** (GGUF, driven by unsloth and independent creators like yuxinlu1/HauhauCS) and **enterprise** (NVFP4, driven by NVIDIA ModelOpt). The demand for **uncensored and abliterated** variants remains a powerful viral undercurrent, with the HauhauCS Qwen3.6 GGUF achieving a staggering 3.3M downloads—far exceeding its base model. This highlights that the “distribution layer” of community fine‑tuned quants is now the primary interface for most users. Concurrently, specialized tools addressing concrete business needs—**OCR, object localization, streaming ASR, long‑context, and cybersecurity**—are earning strong, specific traction, proving the ecosystem is maturing beyond generic chatbots into a structured marketplace of vertical AI assets.

---

## 4. Worth Exploring

- **nvidia/LocateAnything‑3B** ([Link](https://huggingface.co/nvidia/LocateAnything-3B)) — This model redefines standard computer vision workflows by enabling zero‑shot object localization via any prompt. Its clean interface, high accuracy, and massive download count make it an essential building block for visual agents and robotics, well worth a deep study.

- **microsoft/FastContext‑1.0‑4B‑SFT** ([Link](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)) — Highly recommended for anyone building long‑document RAG or extraction pipelines. A compact 4B model that pushes the frontier of context windows, it is remarkably easy to serve while competing with much larger instruction models on long‑form understanding.

- **MiniMaxAI/MiniMax‑M3** ([Link](https://huggingface.co/MiniMaxAI/MiniMax-M3)) — Often overshadowed by the Qwen ecosystem, this is an exceptionally strong and permissively licensed multimodal foundation model. It deserves a close look as a baseline for vision‑language benchmarks and as a high‑quality candidate for downstream multimodal fine‑tuning.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*