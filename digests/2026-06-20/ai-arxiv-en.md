# ArXiv AI Research Digest 2026-06-20

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-06-20 03:23 UTC

---

# ArXiv AI Research Digest — 2026-06-18

## Today's Highlights

Today's submissions reveal a powerful convergence on **LLM agent safety and robustness**, with several papers proposing formal verification methods (Solko-Breslin et al.), adversarial stress-testing benchmarks (Lee et al.), and defenses against prompt injection and bias propagation (Soosahabi, Liu). On the architecture side, **agent and serving efficiency** is a core concern, with work on structured state management for policy compliance (Uddin et al.), extreme KV-cache compression (Chakrabarti), and a radical rethinking of serving infrastructure beyond KV caches (Su). Mechanistic interpretability continues to mature, probing latent reasoning in DiffusionGemma (Engels et al.) and analyzing fundamental forgetting mechanisms (Wasilewski et al.). Finally, a strong undercurrent of **diagnosing fundamental limitations** runs through the batch—whether geometric (FP4 training shrinkage, Fisher flatness) or behavioral (what safety-aligned models actually learn from demonstrations).

---

## Key Papers

### 🧠 Large Language Models

**What Do Safety-Aligned LLMs Learn From Mixed Compliance Demonstrations?**
Dai & Patel | http://arxiv.org/abs/2606.20508v1
Reveals dangerous blind spots in alignment by systematically mixing benign and harmful in-context demonstrations, identifying the precise conditions under which jailbreak succeeds.

**Calibration Without Comprehension: Diagnosing the Limits of Fine-Tuning LLMs for Vulnerability Detection in Systems Software**
Zibaeirad & Vieira | http://arxiv.org/abs/2606.20502v1
Introduces CWE-Trace, a rigorous framework of 834 manually curated Linux kernel samples showing that top-performing LLM vulnerability detectors often pattern-match rather than genuinely reason about security.

**Your Mouse and Eyes Secretly Leak Your Preference: LLM Alignment using Implicit Feedback from Users**
Chang et al. | http://arxiv.org/abs/2606.20482v1
Proposes a novel alignment paradigm that mines behavioral signals (mouse movements, gaze patterns) to replace expensive explicit preference ratings, directly tackling the feedback sparsity bottleneck in RLHF.

**Rethinking Shrinkage Bias in LLM FP4 Pretraining: Geometric Origin, Systemic Impact, and UFP4 Recipe**
Zhao et al. | http://arxiv.org/abs/2606.20381v1
Identifies a fundamental geometric origin of shrinkage bias in current FP4 hardware paths and introduces a recipe to mitigate it—directly relevant for next-generation efficient LLM pretraining on Blackwell/Rubin-class systems.

---

### 🤖 Agents & Reasoning

**LedgerAgent: Structured State for Policy-Adherent Tool-Calling Agents**
Uddin et al. | http://arxiv.org/abs/2606.20529v1
Introduces a ledger-based structured state representation that enables tool-calling agents to maintain and enforce complex domain policies across multi-turn interactions.

**Efficient and Sound Probabilistic Verification for AI Agents**
Solko-Breslin et al. | http://arxiv.org/abs/2606.20510v1
Extends formal runtime verification to probabilistic agent policies in Datalog, enabling sound behavioral guarantees for agents operating under uncertainty in complex digital environments.

**Contagion Networks: Evaluator Bias Propagation in Multi-Agent LLM Systems**
Liu | http://arxiv.org/abs/2606.20493v1
Formalizes and empirically demonstrates how evaluation biases (leniency, self-enhancement, uniformity) systematically spread and amplify across interconnected LLM agents—a critical yet understudied vulnerability in LLM-as-a-judge pipelines.

**Marginal Advantage Accumulation for Memory-Driven Agent Self-Evolution**
Yang et al. | http://arxiv.org/abs/2606.20475v1
Solves cross-batch credit assignment in agent self-improvement by accumulating marginal advantages, distinguishing stable effective operations from accidental successes across training batches.

---

### 🔧 Methods & Frameworks

**Optimal Deterministic Multicalibration and Omniprediction**
Noarov & Roth | http://arxiv.org/abs/2606.20557v1
Provides the first optimal deterministic algorithm for multicalibration, a fundamental tool for algorithmic fairness and omniprediction—closing a gap between theory and practical deployment.

**Execution-State Capsules: Graph-Bound Execution-State Checkpoint and Restore for Low-Latency, Small-Batch, On-Device Physical-AI Serving**
Su | http://arxiv.org/abs/2606.20537v1
Proposes a radical shift from KV-cache-based LLM serving to full execution-state management, enabling low-latency physical AI applications (robotics, autonomous systems) by checkpointing the entire computation graph.

**On the Redundancy of Timestep Embeddings in Diffusion Models**
Chávez | http://arxiv.org/abs/2606.20416v1
Challenges a core design assumption by showing that explicit timestep embeddings in diffusion models are largely redundant and can be learned implicitly through analysis of U-Net and DiT architectures.

**Fisher-Geometric Sharpness and the Implicit Bias of SGD toward Flat Minima**
Ahmed et al. | http://arxiv.org/abs/2606.20469v1
Provides a rigorously reparametrization-invariant geometric measure of flatness using the Fisher information metric, offering a principled explanation for SGD's generalization advantage.

---

### 📊 Applications & Safety

**LLM Agent Safety, Multi-Turn Red-Teaming, Jailbreak Benchmarks, Adversarial Robustness, Safety-Critical Systems**
Lee et al. | http://arxiv.org/abs/2606.20408v1
Presents NRT-Bench, a dedicated multi-turn adversarial benchmark for evaluating LLM agents acting as supervisory components in safety-critical systems—a timely resource as agents move into high-stakes deployments.

**Multi-LCB: Extending LiveCodeBench to Multiple Programming Languages**
Ivanova et al. | http://arxiv.org/abs/2606.20517v1
Extends the widely-adopted LiveCodeBench to multiple programming languages, enabling contamination-aware, robust evaluation of code LLMs beyond Python.

**Scalable Training of Spatially Grounded 2D Vision-Language Models for Radiology**
Salcan et al. | http://arxiv.org/abs/2606.20477v1
Demonstrates scalable training of spatially-aware clinical VLMs using 1.2M bilingual CT/MR pairs without manual bounding box annotations, with strong localization performance.

---

## Research Trend Signal

Today's submissions point to a significant **maturation of agent infrastructure**, where security and reliability are increasingly tackled with formal methods (probabilistic Datalog verification, certificate-bound authority). A notable emerging risk signal is the formalization of **bias propagation in multi-agent systems** (Liu), challenging the unguarded use of LLMs as evaluators in autonomous loops. On the methods front, there is a strong push toward **implicit learning and inference efficiency**, from mining user behavioral signals for alignment (Chang et al.) to stripping redundant architectural components (Chávez) and rethinking serving paradigms beyond KV caches (Su). Most encouragingly, the community is increasingly focused on **diagnosing fundamental limitations** rather than applying ad-hoc fixes—whether geometric (FP4 shrinkage bias, Fisher flatness) or mechanistic (what safety alignment actually learns, how forgetting occurs). These trends signal a shift from building models that work *on average* to systems designed for provable guarantees in interactive, safety-critical environments.

---

## Worth Deep Reading

**1. *Contagion Networks: Evaluator Bias Propagation in Multi-Agent LLM Systems* (Liu)**
This paper touches a nerve for anyone deploying multi-agent LLM systems. The insight that evaluation biases don't average out across agents but systematically propagate, amplify, and corrupt downstream decisions is a critical alarm bell for the widely adopted LLM-as-a-judge paradigm. It formalizes an underappreciated failure mode with clear empirical evidence.

**2. *Execution-State Capsules: Graph-Bound Execution-State Checkpoint and Restore...* (Su)**
A genuinely thought-provoking architectural proposal. The entire LLM serving ecosystem centers on KV-cache management. This paper argues that the latency demands of Physical AI (robotics, real-time control) require checkpointing the *entire* execution graph, proposing a fundamental rethinking of how we serve models in edge and real-time scenarios.

**3. *What Do Safety-Aligned LLMs Learn From Mixed Compliance Demonstrations?* (Dai & Patel)**
While many papers demonstrate jailbreaks, this one systematically identifies *why* they work at a mechanistic level. By carefully controlling the mix of benign and harmful demonstrations, it reveals the precise decision boundaries learned by safety alignment. Understanding this mechanism is essential for moving beyond brittle adversarial patching toward genuinely robust alignment strategies.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*