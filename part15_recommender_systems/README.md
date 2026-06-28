# Part 15 · 推荐系统 / Recommender Systems

> 推荐系统是互联网最赚钱的机器学习应用——电商、短视频、音乐、新闻、广告的核心引擎。本部分按工业界真实的**召回→排序→重排→在线探索→评估**链路，从最直观的基于内容/协同过滤，一路讲到矩阵分解、FM 系、Wide&Deep/DeepFM/DCN 排序模型、双塔召回、序列推荐、赌博机在线探索，最后系统讲透离线评估。
> Recommender systems are the internet's most lucrative ML application — the core engine of e-commerce, short video, music, news, and ads. This part follows the real industrial pipeline **retrieval → ranking → re-ranking → online exploration → evaluation**, from intuitive content-based / collaborative filtering through matrix factorization, the FM family, Wide&Deep/DeepFM/DCN rankers, two-tower retrieval, sequential recommendation, bandit-based online exploration, and finally rigorous offline evaluation.

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results**.

## 工具与数据 / Tools & Data
- **库**:`numpy/scipy/pandas`、`scikit-learn`、`torch`(深度模型)、`matplotlib`。
  **Libraries:** `numpy/scipy/pandas`, `scikit-learn`, `torch` (deep models), `matplotlib`.
- **数据**:经典的 **MovieLens-100k**(943 用户 × 1682 电影 × 10 万评分 + 类型/人口学特征, 首次运行自动下载并缓存到 `~/.cache/dsfs_recsys`)；**Census/Adult** 收入数据(Wide&Deep 经典数据)；以及多份**合成数据**用于干净地证明机制。
  **Data:** the classic **MovieLens-100k** (943 users × 1682 movies × 100k ratings + genre/demographic features, auto-downloaded to `~/.cache/dsfs_recsys` on first run); **Census/Adult** income data (the canonical Wide&Deep dataset); plus several **synthetic datasets** to prove mechanisms cleanly.
- `surprise`/`implicit`/`lightfm` 等推荐库本机未装 → 所有模型(CF/MF/BPR/iALS/FM/FFM/DeepFM/DCN/双塔/SASRec/LinUCB)均**从零实现**, 反而把原理讲得更透。
  `surprise`/`implicit`/`lightfm` not installed → every model (CF/MF/BPR/iALS/FM/FFM/DeepFM/DCN/two-tower/SASRec/LinUCB) is **implemented from scratch**, which makes the mechanics clearer.

## 目录 / Contents
| # | 主题 / Topic | 关键概念 / Key Concepts |
|---|---|---|
| 15.1 | 基于内容 / Content-based | TF-IDF + 余弦, 用户画像, 冷启动 |
| 15.2 | 协同过滤 / Collaborative Filtering | user-user / item-item KNN, RMSE, 评分预测≠排序 |
| 15.3 | 矩阵分解 / Matrix Factorization | FunkSVD(SGD), ALS-WR, 偏置, 隐空间语义 |
| 15.4 | 隐式反馈 / Implicit Feedback | BPR 两两排序, iALS 置信度加权 MF, 负采样 |
| 15.5 | **FM & FFM** | 二阶交叉, O(kF) 技巧, 场感知 |
| 15.6 | **Wide & Deep** | 记忆 vs 泛化, 叉乘特征, 联合训练 |
| 15.7 | **DeepFM, DCN** | 共享 embedding, 自动交叉, cross 层=多项式阶 |
| 15.8 | 双塔模型 / Two-Tower | 召回, in-batch softmax, **logQ 采样偏差校正**, ANN |
| 15.9 | 序列推荐 / Sequential | GRU4Rec, SASRec(因果), BERT4Rec(双向 Cloze) |
| 15.10 | 多臂赌博机 / Bandits | ε-greedy, UCB, Thompson, 上下文 LinUCB, 遗憾 |
| 15.11 | 评估 / Evaluation | precision@k/recall@k/HR/MAP/MRR/NDCG, 覆盖率/多样性, 采样评估陷阱 |

## 学习路径 / Path
15.1→15.2→15.3→15.4 是**基础主线**(内容→协同→矩阵分解→隐式反馈), 理解推荐的核心思想与"召回"。
15.1→15.2→15.3→15.4 are the **foundational spine** (content → collaborative → matrix factorization → implicit feedback) — the core ideas and "retrieval."
15.5→15.6→15.7 是**排序模型**演进(FM→Wide&Deep→DeepFM/DCN), CTR 预估主线。
15.5→15.6→15.7 are the **ranking-model** evolution (FM → Wide&Deep → DeepFM/DCN), the CTR-prediction spine.
15.8 召回(双塔)、15.9 序列、15.10 在线探索(赌博机)、15.11 评估是现代工业推荐的专题。
15.8 (two-tower retrieval), 15.9 (sequential), 15.10 (online exploration / bandits), 15.11 (evaluation) cover modern industrial topics.

## 贯穿全部的诚实主线 / Honest threads throughout
> 几乎每个 notebook 都设计了**合成数据证明机制 + 真实数据诚实检验**的双实验，并反复强调：
> Nearly every notebook pairs **a synthetic experiment proving the mechanism** with **an honest check on real data**, repeatedly stressing:
- **永远和 popularity 基线比**——这是推荐离线评估的"及格线", 纯内容 CF 常常打不过它(15.1/15.2)。
  **Always compare to the popularity baseline** — the "pass line"; pure content-based often loses to it (15.1/15.2).
- **评分预测最优 ≠ 排序最优**(Cremonesi 2010)——低 RMSE 的模型按预测分排序反而输给热门(15.2)。
  **RMSE-optimal ≠ ranking-optimal** (Cremonesi 2010) — ranking by predicted rating can lose to popularity (15.2).
- **训练目标要对齐评估目标**——为排序训练(BPR/iALS)才能赢排序(15.4)。
  **Align training with evaluation** — train for ranking (BPR/iALS) to win at ranking (15.4).
- **结构的增益依赖数据**——FM/DeepFM/DCN 在 ID 主导或干净数据上未必胜过更简单模型, MLP 万能(15.5/15.7)。
  **Structural gains are data-dependent** — FM/DeepFM/DCN may not beat simpler models on ID-dominated/clean data; the MLP is universal (15.5/15.7).
- **采样偏差与采样评估都会害死你**——双塔必须 logQ 校正(15.8); 采样评估会高估并**颠倒模型排名**(15.11)。
  **Sampling bias and sampled evaluation will bite you** — two-tower needs logQ correction (15.8); sampled eval inflates and **reorders models** (15.11).
- **MovieLens 是弱序列数据**——打乱顺序几乎不掉点, SASRec 的收益主要来自协同而非顺序(15.9)。
  **MovieLens is weakly sequential** — shuffling barely hurts; SASRec's gain is mostly collaborative, not order (15.9).
