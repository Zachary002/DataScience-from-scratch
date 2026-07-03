# Part 16 · 图数据与图神经网络 / Graph Data & Graph Neural Networks

> 现实世界充满**关系**——社交网络、引文网络、网页链接、交易网络、知识图谱、分子。这类数据的核心不是"每个样本长什么样"，而是"**谁和谁相连**"。本部分从图论基础(遍历、中心性、社区、PageRank)一路讲到现代**图神经网络**(GCN/GraphSAGE/GAT)与**知识图谱嵌入**(TransE/RotatE)，覆盖搜索、推荐、反欺诈、分子性质预测等主战场。
> The real world is full of **relationships** — social networks, citation graphs, web links, transaction networks, knowledge graphs, molecules. What matters is not "what each sample looks like" but "**who connects to whom**." This part goes from graph-theory basics (traversal, centrality, communities, PageRank) to modern **Graph Neural Networks** (GCN/GraphSAGE/GAT) and **Knowledge Graph embeddings** (TransE/RotatE), covering search, recommendation, fraud detection, and molecular property prediction.

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results**.

## 工具与数据 / Tools & Data
- **库**:`networkx`(图分析)、`torch`(所有 GNN 从零实现)、`numpy/scipy`、`scikit-learn`、`matplotlib`。
  **Libraries:** `networkx` (graph analysis), `torch` (all GNNs from scratch), `numpy/scipy`, `scikit-learn`, `matplotlib`.
- **数据**:**Zachary 空手道俱乐部**(networkx 内置, 16.1–16.3)、小型有向**网页图**(16.4)、**Cora 引文网络**(2708 论文 × 1433 特征 × 7 类, 首次运行自动下载缓存到 `~/.cache/dsfs_recsys/cora`, 用于 16.5–16.8)、合成 KG(16.9)。
  **Data:** **Zachary's Karate Club** (built into networkx, 16.1–16.3), a small directed **web graph** (16.4), the **Cora citation network** (2708 papers × 1433 features × 7 classes, auto-downloaded to `~/.cache/dsfs_recsys/cora`, used in 16.5–16.8), and synthetic KGs (16.9).
- `torch_geometric` / `dgl` 本机未装 → **所有 GNN(GCN/GraphSAGE/GAT)与 KGE(TransE/RotatE)均从零用 torch 实现**，把消息传递、注意力、旋转嵌入的原理讲透。
  `torch_geometric`/`dgl` not installed → **every GNN (GCN/GraphSAGE/GAT) and KGE (TransE/RotatE) is implemented from scratch in torch**, laying bare message passing, attention, and rotation embeddings.

## 目录 / Contents
| # | 主题 / Topic | 关键概念 / Key Concepts |
|---|---|---|
| 16.1 | 图基础与 NetworkX | 节点/边/度, 邻接矩阵 vs 邻接表, 稀疏, 小世界 |
| 16.2 | 图算法 / Graph Algorithms | BFS/DFS, Dijkstra, 度/接近/介数/特征向量中心性 |
| 16.3 | 社区发现 / Community Detection | 模块度 Q, Louvain(从零), Girvan-Newman |
| 16.4 | PageRank & HITS | 随机冲浪者, 幂迭代, PageRank≠入度, 权威/枢纽 |
| 16.5 | 节点嵌入 / Node Embeddings | DeepWalk(游走+skip-gram), node2vec(p/q 偏置) |
| 16.6 | **GCN** | 归一化邻接消息传递, 半监督, **过平滑** |
| 16.7 | **GraphSAGE** | 归纳式(嵌入未见节点), 邻居采样, mean/pool |
| 16.8 | **GAT** | 图注意力, 多头, 自适应权重 vs 固定权重 |
| 16.9 | 知识图谱 / Knowledge Graphs | TransE(平移), RotatE(旋转), 链接预测 MRR/Hits@k |

## 学习路径 / Path
16.1→16.2→16.3→16.4 是**经典图论主线**(表示→遍历/中心性→社区→PageRank), 只用 networkx/numpy, 无需深度学习。
16.1→16.2→16.3→16.4 are the **classical graph-theory spine** (representation → traversal/centrality → communities → PageRank), using only networkx/numpy, no deep learning.
16.5 节点嵌入是**桥梁**(把图变向量, 复用 Word2Vec), 直接引出 16.6→16.7→16.8 的**三大 GNN**(GCN 谱/固定权重 → GraphSAGE 归纳/采样 → GAT 注意力/自适应)。
16.5 (node embeddings) is the **bridge** (graph → vectors, reusing Word2Vec), leading into the **three core GNNs** 16.6→16.7→16.8 (GCN spectral/fixed-weight → GraphSAGE inductive/sampling → GAT attention/adaptive).
16.9 知识图谱嵌入是**有类型边**的专题(TransE/RotatE), 收官。
16.9 (KG embeddings) is the **typed-edge** finale (TransE/RotatE).

## 贯穿全部的诚实主线 / Honest threads throughout
- **结构=命运**:空手道俱乐部的两派分裂, 仅凭社交结构就能 ~94% 预测(16.3); 纯引用结构嵌入(~0.78)胜过纯文本特征(~0.74)(16.5)。
  **Structure is destiny**: the karate split is ~94% predictable from structure alone (16.3); citation-structure embeddings (~0.78) beat text features (~0.74) (16.5).
- **PageRank≠入度**:重要页面的一个链接胜过一堆垃圾链接(16.4)。
  **PageRank ≠ in-degree**: one link from an important page beats many junk links (16.4).
- **GNN 头号坑——过平滑**:GCN 层数从 2 增到 16, 准确率从 0.77 崩到 ~0.15(≈随机)(16.6)。
  **The #1 GNN pitfall — over-smoothing**: GCN from 2 to 16 layers collapses from 0.77 to ~0.15 (≈ random) (16.6).
- **注意力不总是更强**:同质图 Cora 上 GAT≈GCN, 学到的注意力近乎均匀——诚实揭示注意力的价值取决于数据(16.8)。
  **Attention isn't always better**: on homophilous Cora GAT≈GCN with near-uniform learned attention — honestly showing attention's value is data-dependent (16.8).
- **每个模型都有软肋**:TransE 数学上无法建模对称关系(Hits@1≈0), RotatE 用旋转解决(Hits@1≈0.56)(16.9)。
  **Every model has a weakness**: TransE mathematically cannot model symmetric relations (Hits@1≈0), RotatE fixes it via rotation (Hits@1≈0.56) (16.9).
- **归纳 vs 直推**:GraphSAGE 能给训练时完全没见过的新节点算嵌入(~0.78), 这是 GCN/DeepWalk 做不到的生产刚需(16.7)。
  **Inductive vs transductive**: GraphSAGE embeds nodes never seen at training (~0.78) — a production necessity GCN/DeepWalk can't meet (16.7).
