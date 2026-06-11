# ArXiv AI 研究日报 2026-06-11

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-11 03:38 UTC

---

好的，这是基于2026年6月11日 ArXiv 论文生成的 AI 研究日报。

---

# ArXiv AI 研究日报 | 2026-06-11

## 今日速览

今日投稿呈现两大焦点：**机器人学习与具身智能**涌现大量高质量工作，涵盖力传感、次优数据模仿学习及多机器人协作，推动基础模型向物理世界落地。同时，**大模型的安全性与理论基础**仍是核心议题，一篇理论论文论证了“完全获取AI潜在知识的不可能性”，引发对齐研究反思。此外，模型**推理效率与架构创新**持续活跃，包括视觉令牌路由、投机解码验证及混合专家路由改进。

---

## 重点论文

### 🧠 大语言模型与多模态基础模型

1.  **[Reroute, Don't Remove: Recoverable Visual Token Routing for Vision-Language Models](http://arxiv.org/abs/2606.12412v1)**
    *Cheng-Yu Yang et al.*
    提出视觉令牌的“重路由”而非“移除”策略，在保持关键信息的同时大幅减少VLM的推理开销，是提升大模型效率的优雅方案。

2.  **[Redesign Mixture-of-Experts Routers with Manifold Power Iteration](http://arxiv.org/abs/2606.12397v1)**
    *Songhao Wu et al.*
    从流形学习视角重新设计MoE路由器，通过幂迭代方法优化专家选择，有潜力提升大规模稀疏模型的下游性能。

3.  **[ALIGNBEAM: Inference-Time Alignment Transfer via Cross-Vocabulary Logit Mixing](http://arxiv.org/abs/2606.12342v1)**
    *Chirag Chawla et al.*
    解决领域微调后模型安全对齐退化的问题，通过跨词汇表的对数混合实现推理时对齐转移，在专有模型的部署中颇具价值。

4.  **[Unstable Features, Reproducible Subspaces: Understanding Seed Dependence in Sparse Autoencoders](http://arxiv.org/abs/2606.12138v1)**
    *Gleb Gerasimov et al.*
    系统研究稀疏自编码器（SAE）的可重复性问题，结论虽指出特征不完全稳定，但子空间具有可重复性，为可解释性研究提供了关键信心和指导。

### 🤖 智能体、推理与机器人

5.  **[FACTR 2: Learning External Force Sensing for Commodity Robot Arms Improves Policy Learning](http://arxiv.org/abs/2606.12406v1)**
    *Steven Oh et al.*
    提出NEXT方法，仅通过数据驱动学习估计机器人外部关节扭矩，无需力传感器。这大幅降低了触觉感知的硬件门槛，对精细操作任务意义重大。

6.  **[DIRECT: When and Where Should You Allocate Test-Time Compute in Embodied Planners?](http://arxiv.org/aa/2606.12402v1)**
    *Jadelynn Dao et al.*
    深入分析VLM作为具身规划器时，缩放测试时计算带来的收益递减问题，为智能体的高效资源配置提供了经验指导。

7.  **[APPO: Agentic Procedural Policy Optimization](http://arxiv.org/abs/2606.12384v1)**
    *Xucong Wang et al.*
    针对智能体强化学习中粗粒度信用分配问题，提出基于程序化过程的策略优化，精细化管理大语言模型智能体的工具使用行为。

8.  **[Ambient Diffusion Policy: Imitation Learning from Suboptimal Data in Robotics](http://arxiv.org/abs/2606.12365v1)**
    *Adam Wei et al.*
    提出扩散策略的变体，专注于从非最优、低质量数据中进行模仿学习，旨在解决机器人高质量演示数据稀缺的实际瓶颈。

9.  **[CHORUS: Decentralized Multi-Embodiment Collaboration with One VLA Policy](http://arxiv.org/abs/2606.12352v1)**
    *Ria Doshi et al.*
    实现一个统一的VLA策略控制不同形态的机器人（如无人机、机械臂）进行去中心化协作，是多智能体泛化的重要一步。

### 🔧 方法论与理论框架

10. **[Natural-Language Temporal Grounding in Hour-Long Videos is a Search Problem](http://arxiv.org/abs/2606.12300v1)**
    *Sukmin Seo et al.*
    将小时级视频的时序定位重新定义为搜索问题，并建立了基准。其分解式的分析为处理长视频提供了新视角。

11. **[The Standard Interpretable Model](http://arxiv.org/abs/2606.12289v1)**
    *Pietro Barbiero et al.*
    借鉴拉格朗日力学，提出可解释性的通用理论，试图演绎性地设计可解释方法，为可解释性和概念学习提供了统一的理论基础。

12. **[The Impossibility of Eliciting Latent Knowledge](http://arxiv.org/abs/2606.12268v1)**
    *Korbinian Friedl et al.*
    引发关注的理论论文：论证了在不依赖特定假设下，完全并可靠地从AI系统中提取其潜在知识在数学上是不可能的，对AI对齐评估提出了根本性挑战。

13. **[VIA-SD: Verification via Intra-Model Routing for Speculative Decoding](http://arxiv.org/abs/2606.12243v1)**
    *Yuchen Xian et al.*
    改进投机解码的验证策略，提出拒绝令牌可被部分验证而非全部重算，在保证质量的条件下进一步提升了LLM推理速度。

### 📊 垂直领域与应用

14. **[Atlas H&E-TME: Scalable AI-Based Tissue Profiling at Expert Pathologist-Level Accuracy](http://arxiv.org/abs/2606.12346v1)**
    *Kai Standvoss et al.*
    发布基于基础模型的病理学系统，在大规模H&E染色全切片图像上实现了专家级别的组织微环境分析，代表了AI医疗落地的前沿进展。

15. **[OpenMedReason: Scientific Reasoning Supervision for Medical Vision-Language Models](http://arxiv.org/abs/2606.12169v1)**
    *Negin Baghbanzadeh et al.*
    构建大规模多模态医学推理语料库，用于监督医学VLM的结合视觉证据和临床知识的科学推理，而非仅追求答案正确性。

16. **[MSUE: Multi-Modal Soccer Understanding Expert](http://arxiv.org/abs/2606.12106v1)**
    *Litao Li et al.*
    针对SoccerNet VQA挑战赛的解决方案，通过VLM驱动的数据合成流水线实现高效的体育视频理解，展示了数据增强在垂直领域的应用潜力。

---

## 研究趋势信号

- **具身智能与基础模型的深度融合**：机器人领域不再局限于控制，而是深度融入VLA、扩散策略和数据驱动感知。特别是“廉价传感”（如无传感器力估计）和“次优数据利用”的兴起，标志着社区正寻求降低机器人学的人工和硬件成本，推动规模化发展。
- **安全对齐的“不可能三角”与工程妥协**：一方面理论工作揭示了完全对齐的极限（如潜在知识不可提取），另一方面工程论文（如跨词汇表对齐）在实践层面积极寻找妥协方案。这种理论与工程的对立与交织，预示着安全研究将进入更求实的阶段。
- **可解释性从实证走向理论**：多篇论文（如标准可解释模型、SAE稳定性分析）不再满足于事后解释，而是尝试建立可解释系统的设计理论或探索现有方法的哲学边界，显示出该领域的成熟度在提升。

---

## 值得精读

- **[FACTR 2: Learning External Force Sensing for Commodity Robot Arms Improves Policy Learning](http://arxiv.org/abs/2606.12406v1)**
    *推荐理由*：解决了机器人操作中的一个核心瓶颈——力感知的硬件成本。NEXT方法的思路清晰，实用性强，有望成为后续机器人触觉研究的基础框架。

- **[The Standard Interpretable Model](http://arxiv.org/abs/2606.12289v1)**
    *推荐理由*：尝试建立可解释AI的“牛顿力学”。无论你是否同意其具体框架，这种从理论物理中寻找灵感的做法、以及对可解释性进行公理化定义的雄心，都使其成为一篇值得深入研读的思想性论文。

- **[The Impossibility of Eliciting Latent Knowledge](http://arxiv.org/abs/2606.12268v1)**
    *推荐理由*：一篇将在时间检验下可能极其重要的论文。它直指当前AI对齐和评估范式的根本性漏洞（无法完全提权知识）。理解这里的“不可能”对于设计和约束更强大的AI系统至关重要。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*