# Part 20 · 高级专题 / Advanced Topics

> 这一部分收录数据科学中**高价值但常被入门课跳过**的进阶专题——它们要么对应特定行业(生存分析→医疗/风控, 地理空间→出行/零售, 音频→语音), 要么是现代 ML 的前沿范式(元学习、联邦学习、差分隐私、多任务、排序学习)。共同点:**在真实工作和高级面试中反复出现, 却很少有人真正从零讲透**。本部分坚持从零实现每个核心算法, 并把重点放在**诚实呈现每种方法的边界与陷阱**——很多专题的最大价值恰恰是"它什么时候不奏效"。
> This part collects **high-value topics that intro courses skip** — either domain-specific (survival → healthcare/risk, geospatial → mobility/retail, audio → speech) or frontier ML paradigms (meta-learning, federated learning, differential privacy, multi-task, learning-to-rank). What they share: **they recur in real work and senior interviews, yet are rarely taught from scratch**. This part implements every core algorithm from scratch and focuses on **honestly presenting each method's limits and pitfalls** — for many topics the greatest value is precisely "when it does NOT work."

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results**.

## 工具与数据 / Tools & Data
- **库**:`numpy/scipy/pandas`、`scikit-learn`、`torch`(深度方法)、`torchvision`(MNIST/FashionMNIST)、`matplotlib`。
  **Libraries:** `numpy/scipy/pandas`, `scikit-learn`, `torch` (deep methods), `torchvision` (MNIST/FashionMNIST), `matplotlib`.
- **大量从零实现**:`lifelines`(生存)、`geopandas/shapely/h3`(地理)、`librosa`(音频)本机未装 → 手写 Kaplan-Meier/Cox、空间自相关/点模式、STFT/梅尔谱/MFCC。深度专题(MAML、ProtoNet、FedAvg、DP-SGD、RankNet/LambdaRank)全部用 `torch` 从零搭建。**合成数据**为主(可控、能验证方法能否还原真值), 图像专题复用缓存的 **MNIST/FashionMNIST**。
  **Much from scratch**: `lifelines` (survival), `geopandas/shapely/h3` (geospatial), `librosa` (audio) not installed → hand-coded Kaplan-Meier/Cox, spatial autocorrelation/point patterns, STFT/mel-spectrogram/MFCC. Deep topics (MAML, ProtoNet, FedAvg, DP-SGD, RankNet/LambdaRank) all built from scratch in `torch`. **Synthetic data** dominates (controllable, verifiable against ground truth); image topics reuse cached **MNIST/FashionMNIST**.

## 目录 / Contents
| # | 主题 / Topic | 数据 / Data | 关键概念 / Key Concepts |
|---|---|---|---|
| 20.1 | 生存分析 Survival | Synthetic | 删失, Kaplan-Meier, 风险函数, Cox 比例风险 |
| 20.2 | 地理空间分析 Geospatial | Synthetic | 空间自相关(Moran's I), 点模式, 克里金直觉 |
| 20.3 | 音频与语音 Audio | Synthetic | 波形→STFT→梅尔谱→MFCC, 频域特征 |
| 20.4 | 高级异常检测 Anomaly | Synthetic | Isolation Forest, LOF, 自编码器重构误差 |
| 20.5 | 半监督学习 Semi-supervised | Synthetic | 自训练, 一致性, **确认偏差会自我崩溃** |
| 20.6 | 主动学习 Active Learning | Synthetic | 不确定性采样, **策略选错反而不如随机** |
| 20.7 | 元学习 Meta-Learning | Synthetic | MAML(学会快速适应), ProtoNet(原型) |
| 20.8 | 联邦学习 Federated | MNIST | FedAvg, **non-IID 是头号难题**, 隐私≠安全 |
| 20.9 | 隐私保护 ML Privacy | MNIST | 差分隐私, DP-SGD, **隐私-效用硬权衡** |
| 20.10 | 合成数据 Synthetic Data | Synthetic | SMOTE, TSTR, **合成≠隐私**, 精度-召回权衡 |
| 20.11 | 多任务学习 Multi-task | Synthetic | 硬共享, **正迁移 vs 负迁移**, 损失加权 |
| 20.12 | 排序学习 Learning to Rank | Synthetic | NDCG, RankNet, LambdaRank, **匹配问题难度** |

## 学习路径 / Path
20.1–20.4 是**领域/任务专题**(生存、地理、音频、异常)——各对应一类行业问题, 可按需取用。20.5–20.7 是**"标注稀缺"三兄弟**:半监督(用无标注数据)、主动学习(挑最该标的数据)、元学习(学会用极少样本快速学新任务)——现实里数据多、标注贵, 这三招是核心。20.8–20.10 是**隐私与数据主线**:联邦学习(数据不动模型动)、差分隐私(数学化隐私保证)、合成数据(造数据解决不平衡/隐私)——三者常组合使用, 是合规时代的关键技能。20.11 多任务与 20.12 排序学习是**工业系统主力**(推荐/搜索/广告的精排、多目标建模)。
20.1–20.4 are **domain/task topics** (survival, geospatial, audio, anomaly) — each maps to an industry problem, pick as needed. 20.5–20.7 are the **"labels are scarce" trio**: semi-supervised (use unlabeled data), active learning (pick the most-worth-labeling data), meta-learning (learn to learn new tasks from very few samples) — in reality data is plentiful but labels expensive, so these three are core. 20.8–20.10 are the **privacy & data spine**: federated learning (data stays put, model moves), differential privacy (mathematical privacy guarantee), synthetic data (generate data for imbalance/privacy) — often combined, key skills in the compliance era. 20.11 multi-task and 20.12 learning-to-rank are **industrial-system workhorses** (fine-ranking and multi-objective modeling in recommendation/search/ads).

## 贯穿全部的诚实主线 / Honest threads throughout
- **半监督不是免费加数据**:朴素自训练把自己的错误当真值反复强化(确认偏差), 逻辑回归自训练一路崩到 0.50——"用无标注数据"必须有置信度门槛和一致性约束(20.5)。
  **Semi-supervised isn't free data**: naive self-training reinforces its own errors as truth (confirmation bias), collapsing to 0.50 — "using unlabeled data" needs confidence thresholds and consistency constraints (20.5).
- **主动学习选错策略比随机还差**:熵/最小置信度采样因采样偏差跑输随机, 只有边际采样(margin)以 −46% 标注量达标——"挑数据"的策略本身至关重要(20.6)。
  **The wrong active-learning strategy loses to random**: entropy/least-confidence underperform random due to sampling bias; only margin sampling hits target with −46% labels — the querying strategy itself is decisive (20.6).
- **原型网络的威力来自度量而非魔法**:在混入大量噪声维度时, 朴素最近中心崩到 0.38, ProtoNet 在学到的度量空间里做同样的事却达 0.99——表示学习是关键(20.7)。
  **ProtoNet's power is the metric, not magic**: with many nuisance dimensions, raw nearest-centroid drops to 0.38, while ProtoNet does the same in a learned metric space at 0.99 — representation learning is the key (20.7).
- **联邦学习:IID 近乎免费, non-IID 是头号难题**:FedAvg 在 IID 上达 0.874(逼近集中式 0.905), 但每个客户端只有少数类时崩到 0.582——且"不传数据"≠隐私(梯度可反推), 需叠加差分隐私(20.8)。
  **Federated learning: IID nearly free, non-IID is the #1 challenge**: FedAvg reaches 0.874 on IID (near centralized 0.905) but collapses to 0.582 when each client holds few classes — and "not sending data" ≠ privacy (gradients can reconstruct it), needing differential privacy (20.8).
- **隐私是可证明的, 但要拿精度换**:DP-SGD(逐样本裁剪+加噪)给出 (ε,δ)-DP 数学保证, 噪声越大隐私越强、精度从 0.86 一路降到 0.66——没有既完全隐私又完全准确的模型(20.9)。
  **Privacy is provable, but paid for in accuracy**: DP-SGD (per-example clipping + noise) gives an (ε,δ)-DP guarantee; more noise = stronger privacy, accuracy dropping 0.86→0.66 — no model is both fully private and fully accurate (20.9).
- **SMOTE 是精度-召回权衡, 合成≠隐私**:SMOTE 主要提升召回(F1 涨不涨看模型); 而纯合成数据能训出 95.7% 效用的模型(TSTR), 但合成数据默认不保证隐私(可能记忆真实样本), 要隐私必须叠加 DP(20.10)。
  **SMOTE is a precision-recall tradeoff; synthetic ≠ private**: SMOTE mainly boosts recall (F1 depends on the model); purely synthetic data trains a model at 95.7% utility (TSTR), but synthetic data doesn't guarantee privacy by default (may memorize real samples) — for privacy add DP (20.10).
- **多任务学习不是免费午餐**:数据多的相关辅助任务能救数据少的主任务(+10%, 正迁移), 但无关任务共享主干反而互相拖累(负迁移)——共享只在任务相关时有益(20.11)。
  **Multi-task learning isn't a free lunch**: a data-rich related auxiliary task rescues a data-poor main task (+10%, positive transfer), but sharing a trunk with unrelated tasks drags them down (negative transfer) — sharing helps only when tasks are related (20.11).
- **精巧的方法要匹配问题难度**:排序学习让 NDCG@1 从随机的 0.12 飙到 0.9+; 但在干净、近饱和的数据上, 理论更优的 LambdaRank(0.904)反而输给简单的 RankNet(0.928)——复杂损失只在指标远未饱和的难问题上兑现价值(20.12)。
  **Sophisticated methods must match problem difficulty**: LTR lifts NDCG@1 from random's 0.12 to 0.9+; but on clean, near-saturated data the theoretically superior LambdaRank (0.904) loses to the simpler RankNet (0.928) — complex losses pay off only on hard problems far from metric saturation (20.12).
