# ArXiv AI 研究日报 2026-06-10

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-10 03:26 UTC

---

# ArXiv AI 研究日报 (2026-06-10)

## 今日速览

今日投稿聚焦推理模型的安全性与记忆退化难题：多项研究揭示思维链微调会无意中破坏长程召回与对齐行为，促使社区重新审视推理能力与可信度的平衡。智能体领域涌现多种测试时干预和评估框架，包括在线提示学习、行为预测引导及多场景基准，推动智能体从静态评估走向动态适应。生成模型方面，流匹配与扩散模型的强化学习对齐（Flow‑DPPO、奖励反向传播）持续升温，而多模态学习迎来理论统一的“相图”，为模态对齐策略提供系统指导。此外，高质量专业基准（幻觉检测、控制干预意识、肺癌耐药预测）进一步细化评估维度。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

- **A Unifying Lens on Supervised Fine-Tuning Through Target Distribution Design**  
  [http://arxiv.org/abs/2606.11189v1](http://arxiv.org/abs/2606.11189v1)  
  Tong Xie et al.  
  → 将 SFT 理解为目标分布设计问题，指出 one‑hot 拟合可能次优，为微调策略提供理论统一视角。

- **Attention Amnesia in Hybrid LLMs: When CoT Fine-Tuning Breaks Long-Range Recall, and How to Fix It**  
  [http://arxiv.org/abs/2606.11052v1](http://arxiv.org/abs/2606.11052v1)  
  Xinyu Zhou et al.  
  → 发现 CoT 微调系统性地损害混合线性‑注意力模型的长程检索能力，并提出缓解方案，对推理模型设计有重要警示。

- **Does Reasoning Preserve Alignment? On the Trustworthiness of Large Reasoning Models**  
  [http://arxiv.org/abs/2606.11046v1](http://arxiv.org/abs/2606.11046v1)  
  Prajakta Kini et al.  
  → 系统考察指令微调模型转化为推理模型后，原有对齐行为（如安全拒绝）是否保持，答案值得警惕。

- **AuRA: Internalizing Audio Understanding into LLMs as LoRA**  
  [http://arxiv.org/abs/2606.11033v1](http://arxiv.org/abs/2606.11033v1)  
  Bo Cheng et al.  
  → 通过轻量 LoRA 将音频理解直接内化到 LLM 中，无需级联 ASR 或桥接模块，向原生语音‑语言模型迈进。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

- **EEVEE: Towards Test-time Prompt Learning in the Real World for Self-Improving Agents**  
  [http://arxiv.org/abs/2606.11182v1](http://arxiv.org/abs/2606.11182v1)  
  Weixian Xu et al.  
  → 首个多数据集测试时提示学习框架，使 LLM 智能体在异构任务流中自我改进，实用性强。

- **Predicting Future Behaviors in Reasoning Models Enables Better Steering**  
  [http://arxiv.org/abs/2606.11172v1](http://arxiv.org/abs/2606.11172v1)  
  Evgenii Kortukov et al.  
  → 提出预测推理模型即将产生的行为，利用内部特征实现更精准的测试时引导，避免质量下降。

- **TRACE: A Unified Rollout Budget Allocation Framework for Efficient Agentic Reinforcement Learning**  
  [http://arxiv.org/abs/2606.11119v1](http://arxiv.org/abs/2606.11119v1)  
  Heming Zou et al.  
  → 针对 RLVR 中因奖励对比不足导致的 rollout 浪费，提出统一预算分配框架，显著提升训练效率。

- **T1-Bench: Benchmarking Multi-Scenario Agents in Real-World Domains**  
  [http://arxiv.org/abs/2606.11070v1](http://arxiv.org/abs/2606.11070v1)  
  Genta Indra Winata et al.  
  → 覆盖金融、医疗等多个真实领域的智能体评估基准，任务复杂度高，填补现行基准的维度缺失。

---

### 🔧 方法与框架（新技术、基准测试、效率优化）

- **When to Align, When to Predict: A Phase Diagram for Multimodal Learning**  
  [http://arxiv.org/abs/2606.11190v1](http://arxiv.org/abs/2606.11190v1)  
  Ilay Kamai et al.  
  → 构建跨模态对齐与跨模态预测的“相图”，明确各自成功的条件与失败模式，是多模态学习的理论里程碑。

- **Itô maps for any-step SDEs**  
  [http://arxiv.org/abs/2606.11156v1](http://arxiv.org/abs/2606.11156v1)  
  Zhengkai Pan et al.  
  → 将确定性流映射推广到随机动力学，提出 Itô 图实现任意步 SDE 的精炼蒸馏，为扩散模型加速提供新范式。

- **Flow-DPPO: Divergence Proximal Policy Optimization for Flow Matching Models**  
  [http://arxiv.org/abs/2606.11025v1](http://arxiv.org/abs/2606.11025v1)  
  Bowen Ping et al.  
  → 将在线 RL 引入流匹配生成模型，基于散度约束的 PPO 改进实现图像/视频的高效对齐。

- **Exploring the Design Space of Reward Backpropagation for Flow Matching**  
  [http://arxiv.org/abs/2606.11075v1](http://arxiv.org/abs/2606.11075v1)  
  Ruoyu Wang et al.  
  → 系统分析直接奖励反向传播在流匹配中的梯度失效问题，提出多种缓解策略，极具工程参考价值。

---

### 📊 应用（垂直领域、多模态、代码生成）

- **OncoTraj: a public benchmark for longitudinal resistance prediction in EGFR-mutant non-small-cell lung cancer on osimertinib**  
  [http://arxiv.org/abs/2606.11144v1](http://arxiv.org/abs/2606.11144v1)  
  Abhijoy Sarkar et al.  
  → 首个公开的肺癌纵向耐药预测基准，填补了精准医疗中可重复评估的空白，对临床决策建模意义重大。

- **DMT: Demographic Conditioning, Morphology-Enhanced Transformer for Cuffless Blood Pressure Estimation from PPG Signals**  
  [http://arxiv.org/abs/2606.11125v1](http://arxiv.org/abs/2606.11125v1)  
  Yidan Shen et al.  
  → 融合人口统计信息与形态增强 Transformer，显著提升无袖带血压估计的精度与公平性。

- **Flexible Kernels for Protein Property Prediction**  
  [http://arxiv.org/abs/2606.11057v1](http://arxiv.org/abs/2606.11057v1)  
  Martin Jankowiak et al.  
  → 引入基于进化替换矩阵的灵活序列核，在稀疏实验数据下有效预测蛋白质热稳定性与结合亲和力。

---

## 研究趋势信号

今日投稿最突出的信号是 **“推理能力的代价”** ：Attention Amnesia 与 Alignment Preservation 两篇工作直接挑战当前通过 CoT 或强化学习提升推理的默认做法，引发对推理模型内部稳定性的关注。同时，**测试时干预工具链快速成熟**——从行为预测到预算分配再到提示学习，目标均是使智能体在不重新训练的前提下持续适应。此外，**流匹配/扩散模型的强化学习对齐**正在成为生成式 AI 的核心课题，多篇论文从不同角度（DPPO、奖励反向传播）探索稳定对齐路径。最后，**专业评估基准走向精细化**（幻觉、办公效率、控制干预意识），反映出社区对衡量真实世界能力的更高要求。

---

## 值得精读

1. **When to Align, When to Predict: A Phase Diagram for Multimodal Learning**  
   本文首次为跨模态学习提供统一的理论框架，明确对齐与预测两种范式的适用边界，对多模态研究的长远发展有奠基意义。

2. **Attention Amnesia in Hybrid LLMs: When CoT Fine-Tuning Breaks Long-Range Recall, and How to Fix It**  
   揭示了 CoT 微调的系统性副作用，并提出修复方法，对当前主流推理模型的实践有直接警示和改进价值。

3. **Does Reasoning Preserve Alignment? On the Trustworthiness of Large Reasoning Models**  
   系统评估了推理模型对齐行为的变化，结果具有强预警性，对于负责任地部署推理增强模型不可或缺。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*