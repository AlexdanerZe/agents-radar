# Hugging Face Trending Models Digest 2026-06-01

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-01 03:42 UTC

---

Here is the structured Hugging Face Trending Models Digest for the week of June 1, 2026.

---

### 1. Today's Highlights

The Hugging Face Hub this week is overwhelmingly defined by the release of **DeepSeek-V4-Pro** and **DeepSeek-V4-Flash**, which collectively amassed over 9 million downloads and nearly 6,000 likes, cementing DeepSeek’s leadership in the open-weight frontier model race. **Qwen3.6-27B** continues its remarkable run as the most versatile and popular vision-language foundation model, spawning a massive ecosystem of community fine-tunes (including the uncensored “HauhauCS” variant with 2.4M downloads) and extensive quantization efforts by Unsloth and NVIDIA. In the generative media space, **SulphurAI’s Sulphur-2-base** and **ByteDance’s Lance** are signaling a major platform shift towards robust text-to-video and any-to-any generation, while **circlestone-labs/Anima** demonstrates the enduring power of the open-source diffusion community with massive ComfyUI adoption. Alongside these heavyweights, **LiquidAI’s LFM2.5-8B-A1B** has emerged as a dark horse, captivating the edge deployment community with its radically efficient 1B active-parameter MoE architecture.

---

### 2. Trending Models

#### 🧠 Language Models
- **deepseek-ai/DeepSeek-V4-Pro** ([link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro), 4,503 likes, 5.8M downloads): The flagship open-weight reasoning model; trending due to its unmatched performance against proprietary systems and the AI community’s excitement over its architecture and training methodology.
- **deepseek-ai/DeepSeek-V4-Flash** ([link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash), 1,323 likes, 3.4M downloads): The distilled, efficient counterpart to V4-Pro; trending for bringing frontier-level intelligence to a dramatically lower compute footprint, ideal for production serving.
- **LiquidAI/LFM2.5-8B-A1B** ([link](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B), 323 likes, 27k downloads): Liquid AI’s new MoE model series; trending as a breakthrough in extremely sparse activation (1B active / 8B total), redefining the efficiency frontier for edge language models.
- **openbmb/MiniCPM5-1B** ([link](https://huggingface.co/openbmb/MiniCPM5-1B), 661 likes, 36k downloads): A highly compact text-generation model; trending for its surprising capability density, challenging much larger models in language understanding and generation tasks on mobile hardware.

#### 🎨 Multimodal & Generation
- **circlestone-labs/Anima** ([link](https://huggingface.co/circlestone-labs/Anima), 1,610 likes, 756k downloads): A massive community success for a single-file diffusion model; trending due to its seamless ComfyUI integration, stellar image quality, and active community around styles.
- **Qwen/Qwen3.6-27B** ([link](https://huggingface.co/Qwen/Qwen3.6-27B), 1,553 likes, 5M downloads): The foundational vision-language MoE model; trending for its exceptional reasoning, instruction following, and multimodal capabilities, making it the default base for the current fine-tuning wave.
- **SulphurAI/Sulphur-2-base** ([link](https://huggingface.co/SulphurAI/Sulphur-2-base), 1,473 likes, 1.5M downloads): A highly popular open-source text-to-video model; trending for its dramatic quality improvements over previous versions, significantly closing the gap with closed-source video generation leaders.
- **openbmb/MiniCPM-V-4.6** ([link](https://huggingface.co/openbmb/MiniCPM-V-4.6), 1,084 likes, 444k downloads): The latest iteration of the efficient MiniCPM-V series; trending for delivering desktop-class multimodal intelligence on mobile devices.
- **bytedance-research/Lance** ([link](https://huggingface.co/bytedance-research/Lance), 993 likes, 2.9k downloads): ByteDance’s ambitious “any-to-any” generation model; trending for its ability to flexibly process and generate across text, image, and video, pushing the boundary of unified generative models.
- **Supertone/supertonic-3** ([link](https://huggingface.co/Supertone/supertonic-3), 754 likes, 56k downloads): A state-of-the-art text-to-speech model; trending for its exceptional naturalness, expressiveness, and emotional control in speech synthesis.
- **nvidia/LocateAnything-3B** ([link](https://huggingface.co/nvidia/LocateAnything-3B), 620 likes, 24k downloads): NVIDIA’s powerful grounding and object localization model; trending for its zero-shot segmentation capabilities and integration into complex multimodal agent workflows.
- **NemoStation/Marlin-2B** ([link](https://huggingface.co/NemoStation/Marlin-2B), 472 likes, 16k downloads): A small yet powerful video understanding model; trending for its ability to reason over long video contexts, making video understanding accessible on consumer hardware.
- **meituan-longcat/LongCat-Video-Avatar-1.5** ([link](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5), 441 likes, 0 downloads): An innovative avatar generation model; trending for its combined audio+text-to-video avatar pipeline, enabling realistic digital human creation.
- **nvidia/PiD** ([link](https://huggingface.co/nvidia/PiD), 220 likes, 498 downloads): NVIDIA’s super-resolution diffusion model; trending for its practical image enhancement capabilities and efficient architecture for upscaling.
- **stepfun-ai/Step-3.7-Flash** ([link](https://huggingface.co/stepfun-ai/Step-3.7-Flash), 162 likes, 7.6k downloads): StepFun’s latest efficient VLM; trending as a strong competitor in the high-performance vision-language arena, highlighting the rapid evolution of Chinese AI labs.
- **microsoft/Lens** ([link](https://huggingface.co/microsoft/Lens), 149 likes, 1.9k downloads): Microsoft’s diffusion-based text-to-image model; trending for its novel architectural approach detailed in the accompanying arXiv paper and strong aesthetic generation.
- **OpenMOSS-Team/MOSS-TTS-v1.5** ([link](https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5), 83 likes, 14k downloads): A specialized TTS model from the MOSS team; trending for its strong performance in Chinese speech generation with low latency.

#### 🔧 Specialized Models & Tooling
- **openai/privacy-filter** ([link](https://huggingface.co/openai/privacy-filter), 1,573 likes, 306k downloads): OpenAI’s first major open-model release for safety; trending due to the critical need for privacy tooling, its Transformer.js compatibility, and the weight of the OpenAI brand in the open model space.
- **tencent/Hy-MT2-1.8B** ([link](https://huggingface.co/tencent/Hy-MT2-1.8B), 1,094 likes, 17k downloads): Tencent’s efficient dense translation model; trending for its breakthrough in machine translation quality and domain adaptation in a compact package.
- **tencent/Hy-MT2-30B-A3B** ([link](https://huggingface.co/tencent/Hy-MT2-30B-A3B), 440 likes, 4.2k downloads): Tencent’s MoE translation model; trending for setting a new state-of-the-art in production translation systems with superior efficiency.
- **froggeric/Qwen-Fixed-Chat-Templates** ([link](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates), 469 likes, 0 downloads): A meticulously curated repository of corrected Jinja chat templates; trending because correct chat templates are a silent but critical bottleneck for inference quality with the Qwen3.x ecosystem.
- **sapientinc/HRM-Text-1B** ([link](https://huggingface.co/sapientinc/HRM-Text-1B), 429 likes, 143k downloads): A specialized 1B parameter model for text generation; trending for its surprising effectiveness in targeted enterprise applications running at the edge.
- **numind/NuExtract3** ([link](https://huggingface.co/numind/NuExtract3), 208 likes, 57k downloads): A specialized extraction model built on Qwen3.5; trending for its exceptional accuracy in structured data extraction from documents and images.
- **PaddlePaddle/PaddleOCR-VL-1.6** ([link](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6), 118 likes, 2.7k downloads): The latest version of the popular PaddleOCR; trending for its unified vision-language OCR architecture (ERNIE 4.5 based), setting new standards for document understanding.

#### 📦 Fine-tunes & Quantizations
- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive), 1,164 likes, 2.4M downloads): The most popular fine-tune of Qwen3.6 this period; trending for removing alignment restrictions and pairing the base model with aggressive reasoning prompt styling.
- **unsloth/Qwen3.6-27B-MTP-GGUF** ([link](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF), 578 likes, 926k downloads): The definitive GGUF quantization of Qwen3.6 from Unsloth; trending for its flawless Multi-Token Prediction (MTP) implementation, enabling efficient inference on local hardware.
- **Jackrong/Qwopus3.6-27B-v2-GGUF** and **-MTP-GGUF** ([link](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-GGUF), 190 likes / [link](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF), 178 likes): Alternative community GGUF quantizations; trending for offering specific optimizations that resonate strongly with the local inference and fine-tuning community.
- **LiquidAI/LFM2.5-8B-A1B-GGUF** ([link](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B-GGUF), 133 likes, 41k downloads): Official GGUF quantizations of Liquid AI’s LFM2.5; trending as the go-to choice for deploying extremely efficient MoE models on laptops and edge devices.
- **nvidia/Qwen3.6-35B-A3B-NVFP4** ([link](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4), 94 likes, 105k downloads): NVIDIA’s highly optimized NVFP4 quantization; trending for its cutting-edge memory savings and throughput speeds achieved using the NVIDIA Model Optimizer.

---

### 3. Ecosystem Signal

The Hugging Face ecosystem is undergoing a profound structural shift. **Mixture-of-Experts (MoE)** has moved from an experimental architecture to the consensus standard for frontier models, as demonstrated by DeepSeek V4, Qwen3.6, Liquid LFM2.5, and Tencent Hy-MT2, with the community now fixating on *active* parameter counts as the new metric for capability-per-compute. **Quantization is no longer an afterthought** but a simultaneous, first-class release, with NVIDIA deploying NVFP4 optimizations and Unsloth widely distributing GGUF quantizations, directly enabling the massive download figures seen by Qwen3.6 variants. **Liquid AI’s LFM2.5** stands out as a critical non-Transformer signal, challenging the Qwen/DeepSeek duopoly in the efficiency niche. Simultaneously, **video generation** (Sulphur-2, Lance) is empirically crossing the chasm into utility, while a powerful cultural tension plays out between unrestricted community fine-tuning and the release of specialized safety tooling like OpenAI’s privacy-filter. The result is a maturing ecosystem where choice, efficiency, and safety are being aggressively optimized side-by-side.

---

### 4. Worth Exploring

1. **DeepSeek-V4-Flash** ([link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)): While V4-Pro gets the headlines, V4-Flash represents the true workhorse for most practitioners. It delivers a staggering proportion of the Pro’s reasoning capability at a fraction of the cost, making it essential for anyone evaluating production-ready open-weight LLMs.

2. **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)): This model is a critical case study in the “uncensored” ecosystem. Its massive 2.4M downloads in a single period reveal an overwhelming user demand for minimal restrictions, providing researchers valuable data on latent model capabilities and the practical dynamics of safety guardrails.

3. **LiquidAI/LFM2.5-8B-A1B** ([link](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)): The 1B active parameter MoE model is quietly reshaping the edge computing landscape. Practitioners evaluating next-generation architectures for mobile, IoT, or cost-sensitive inference should treat this model as a mandatory study in how far efficiency can be pushed without sacrificing reasoning quality.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*