# ArXiv AI 研究日报 2026-06-03

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-03 03:46 UTC

---

# ArXiv AI 研究日报 (2026-06-03)

## 今日速览

今日 arXiv 投稿集中聚焦 LLM 安全与可靠性：多项工作提出攻击与防御新范式，包括全面的黑盒对抗攻击框架（[1]）以及针对模型合并供应链漏洞的首次系统性攻击（[39]）。生成可靠性方面，幻觉拒绝采样（[3]）有效抑制长文本中的幻觉雪崩；测试时强化学习（[6]）可在无标注条件下提升推理 Pass@k。效率优化上，方差归一化的 KV 缓存量化（[25]）显著减少长推理误差累积，而多源校准数据混合（[44]）对高稀疏剪枝至关重要。架构分析层面，Transformer 多流超连接中的流塌缩被深入诊断（[22]），模型合并与 MoE 路由的兼容性问题首次被揭示（[30]）。此外，视觉学习中的低频捷径（[21]）和图基础模型（[47]）等方向也有重要进展。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. Black-box, Adaptive, Efficient, Transferable, Harmful, Applicable... Attacks Are All You Need to Break LLMs** (http://arxiv.org/abs/2606.03647v1)  
作者: V. Limbach et al.  
一句话说明: 提出一个系统化、标准化的黑盒对抗攻击框架，覆盖多种攻击场景，旨在为 LLM 鲁棒性评估提供可靠基准，推动防御研究的一致性与可比性。

**2. Building Reliable Long-Form Generation via Hallucination Rejection Sampling** (http://arxiv.org/abs/2606.03628v1)  
作者: L. Li et al.  
一句话说明: 针对长文本生成中的幻觉雪崩现象，提出幻觉拒绝采样（HRS），通过迭代选择可靠序列片段，显著提升长文本输出的事实正确性。

**3. When Model Merging Breaks Routing: Training-Free Calibration for MoE** (http://arxiv.org/abs/2606.03391v1)  
作者: C. Huang et al.  
一句话说明: 发现现有模型合并技术会严重破坏 MoE 架构的路由机制，提出无需训练的路由校准方法，是首个深入分析合并与 MoE 兼容性的工作。

**4. RogueMerge: Robust and Unified Attacks against LLM Model Merging** (http://arxiv.org/abs/2606.03344v1)  
作者: J. Zhang et al.  
一句话说明: 揭示模型合并中第三方任务向量可嵌入恶意行为，提出统一的供应链攻击方法，凸显当前合并流程的严重安全风险。

**5. Calibration Data Trade-offs Across Capability Dimensions: Why Multi-Source Mixing Matters for High-Sparsity LLM Pruning** (http://arxiv.org/abs/2606.03328v1)  
作者: H. Xu et al.  
一句话说明: 指出校准数据来源对高稀疏剪枝后的多维能力有显著影响，多源混合校准优于单一来源，挑战了“校准源影响有限”的已有结论。

### 🤖 智能体与推理（推理、工具使用、多智能体、思维链）

**6. Exploiting Verification-Generation Gap: Test-Time Reinforcement Learning with Confidence-Conditioned Verification** (http://arxiv.org/abs/2606.03608v1)  
作者: J. Li et al.  
一句话说明: 提出置信度条件验证的测试时强化学习方法，无需外部标签即可优化 LLM 推理的 Pass@k，探索验证与生成之间的差距，为无监督推理增强提供新范式。

**7. CauTion: Knowing When to Trust LLMs for Ensemble Causal Discovery** (http://arxiv.org/abs/2606.03602v1)  
作者: B. Peng et al.  
一句话说明: 将 LLM 的领域知识与统计因果方法结合，设计信任评估机制以决定何时采纳 LLM 输出，增强了因果发现的可解释性和鲁棒性。

**8. PerchRL: Vision-Based Agile Perching on Inclined Platforms under Rapid and Irregular Motion** (http://arxiv.org/abs/2606.03441v1)  
作者: Z. Lu et al.  
一句话说明: 利用强化学习实现四旋翼在倾斜、移动平台上的视觉灵巧降落，克服视场限制与快速不规则运动，展示了 RL 在具身飞行控制中的前沿应用。

### 🔧 方法与框架（新技术、基准测试、效率优化）

**9. Demystifying Pipeline Parallelism: First Theory for PipeDream** (http://arxiv.org/abs/2606.03498v1)  
作者: I. Ilin et al.  
一句话说明: 为 PipeDream 流水线并行训练建立首个严格理论分析，揭示其收敛特性与调度策略的影响，填补分布式训练理论的重要空白。

**10. Low-Frequency Shortcuts in Texture-Driven Visual Learning** (http://arxiv.org/abs/2606.03493v1)  
作者: U. Şirin et al.  
一句话说明: 发现神经网络在纹理驱动的视觉任务（如医学图像）中依赖低频捷径，揭示了对形状之外偏置的忽视，对 OOD 泛化与可解释性提出重要警示。

**11. Analyzing Stream Collapse in Hyper-Connections: From Diagnosis to Mitigation** (http://arxiv.org/abs/2606.03483v1)  
作者: E. Alimaskina et al.  
一句话说明: 对 Transformer 多流超连接结构中的流塌缩（dominant-stream usage）进行系统诊断，分析其发生机制并提出有效的缓解策略。

**12. KVarN: Variance-Normalized KV-Cache Quantization Mitigates Error Accumulation in Reasoning Tasks** (http://arxiv.org/abs/2606.03458v1)  
作者: L. K. Muller et al.  
一句话说明: 提出方差归一化的 KV 缓存量化方法，在长序列推理中有效抑制量化误差累积，兼顾效率与准确率，对部署大模型推理极有实用价值。

### 📊 应用（垂直领域、多模态、代码生成）

**13. P²-DPO: Grounding Hallucination in Perceptual Processing via Calibration Direct Preference Optimization** (http://arxiv.org/abs/2606.03376v1)  
作者: R. Zhang et al.  
一句话说明: 针对视觉语言模型的幻觉问题，将 DPO 与感知校准结合，使偏好学习对齐到感知处理阶段，显著减少多模态生成中的幻觉内容。

**14. Multi-Modal Graph Neural Network with Transformer-Guided Adaptive Diffusion for Preclinical Alzheimer Classification** (http://arxiv.org/abs/2606.03322v1)  
作者: J. Sim et al.  
一句话说明: 融合多模态脑影像与 Transformer 引导的自适应扩散图神经网络，实现临床前阿尔茨海默症的高精度分类，为早期诊断提供新方法。

---

## 研究趋势信号

从今日投稿可观察到以下新兴方向：**模型合并的安全风险与兼容性**成为焦点（RogueMerge、MoE 校准），社区需警惕第三方组件带来的供应链隐患。**长序列推理中的误差累积**问题得到系统关注（幻觉雪崩、KV 量化误差、流塌缩），推动架构与工程协同创新。**测试时计算扩展**正从监督范式走向无标签强化学习（测试时 RL），降低推理增强的成本。**视觉学习中的非形状捷径**（低频、纹理）被揭示，提醒解释性与泛化研究需超越形状偏置。此外，**图基础模型**的跨图泛化尝试（谱解析+原型传播）和图神经网络可解释性（层次语义解释器）表明结构学习正迈向通用化与透明化。

---

## 值得精读

1. **Black-box, Adaptive, Efficient, Transferable, Harmful, Applicable... Attacks Are All You Need to Break LLMs** — 该文试图统一 LLM 对抗攻击的评测标准，类似 AutoAttack 在图像领域的地位，对鲁棒性研究的方法论有深远影响。

2. **RogueMerge: Robust and Unified Attacks against LLM Model Merging** — 模型合并正在快速普及，本文首次系统性展示其供应链安全漏洞，攻击路径清晰、实验全面，对开源社区和工业部署具有重要警示。

3. **KVarN: Variance-Normalized KV-Cache Quantization Mitigates Error Accumulation in Reasoning Tasks** — 长链推理对 KV 缓存精度极为敏感，文章提出的方差归一化方法简单且效果好，理论与实践结合紧密，是落地推理加速的实用方案。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*