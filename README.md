# Data Science from Scratch — 数据科学完整学习路线

> 一份覆盖数据科学全栈知识的项目式学习仓库。
> 每一个知识点配一个独立的 Jupyter Notebook，使用经典公开数据集，含中英双语讲解、数学公式推导和完整代码流程。
>
> A project-based curriculum covering the full data-science stack.
> Each topic has its own Jupyter notebook with a classic dataset, bilingual (Chinese / English) explanations, math derivations, and end-to-end code.

> 📐 **统一符号约定 / Unified math notation**：本仓库所有 notebook **共用同一套数学符号**，定义见 [`NOTATION.md`](NOTATION.md)。如果你以前学过 Bishop / ESL / Andrew Ng / Goodfellow，那个文件最后有一张对照表。
> All notebooks share **one consistent set of math symbols**, defined in [`NOTATION.md`](NOTATION.md). If you've used Bishop / ESL / Ng / Goodfellow before, there's a translation table at the bottom.

---

## 仓库结构 / Repository Layout

```
DataScience-from-scratch/
├── README.md                          ← 本文件 / this file
├── part00_foundations/                ← Python / NumPy / Pandas / Polars / 可视化 / 数学
├── part01_sql_databases/              ← SQL / NoSQL / 数据仓库
├── part02_statistics/                 ← 概率 + 推断统计
├── part03_eda_preprocessing/          ← EDA + 数据清洗 + 特征工程
├── part04_supervised_regression/
├── part05_supervised_classification/
├── part06_unsupervised/
├── part07_model_evaluation/
├── part08_ensemble/
├── part09_deep_learning/
├── part10_computer_vision/
├── part11_classic_nlp/
├── part12_modern_nlp_llms/
├── part13_generative_models/          ← GAN / VAE / Diffusion / Flow
├── part14_time_series/
├── part15_recommender/
├── part16_graph_gnn/
├── part17_reinforcement_learning/
├── part18_bayesian/
├── part19_causal_inference/
├── part20_advanced_topics/            ← survival / geospatial / audio / anomaly
├── part21_big_data/                   ← Spark / Dask / Polars at scale
├── part22_mlops/
├── part23_cloud_for_ds/
└── part24_ml_system_design/           ← 大厂 ML System Design + 案例面试
```

每个章节文件夹内含：
- `README.md` — 本章导读 / chapter intro
- 每个知识点一个 `XX_topic_name.ipynb`
- `data/` — 数据集 (或下载脚本)

---

## Part 0 · 基础准备 / Foundations

数据科学家工具箱与数学基础。
The toolbox + math.

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 0.1 | Python for Data Science | — | list comp, generator, decorator, OOP, typing, pathlib |
| 0.2 | NumPy 全面解析 | — | ndarray, broadcasting, vectorization, einsum, memory layout |
| 0.3 | Pandas 全面解析 | Titanic | Series/DataFrame, groupby, merge, pivot, MultiIndex, window |
| 0.4 | Polars 入门 | NYC Taxi (subset) | lazy frames, expressions, vs pandas performance |
| 0.5 | Matplotlib & Seaborn | Iris, Tips | figure/axes, subplot grid, styling |
| 0.6 | Plotly & 交互可视化 / Interactive Viz | COVID time series | Plotly Express, Dash basics |
| 0.7 | 线性代数 / Linear Algebra | — | vector, matrix, rank, eigen-decomp, SVD, projection |
| 0.8 | 微积分 / Calculus | — | derivative, gradient, chain rule, Jacobian, Hessian, Taylor |
| 0.9 | 概率论 / Probability | — | distributions, conditional, Bayes, joint/marginal, expectation |
| 0.10 | 数值优化 / Numerical Optimization | — | GD, Newton's, BFGS, convexity, KKT, Lagrangian |
| 0.11 | 信息论 / Information Theory | — | entropy, cross-entropy, KL, mutual information |
| 0.12 | 工程化：Git / venv / Jupyter / VSCode | — | reproducibility, environments, notebook hygiene |

---

## Part 1 · SQL 与数据库 / SQL & Databases  ⭐⭐⭐ (面试核心)

**几乎所有 DS / DA 面试第一关都是 SQL。** 单独成一大块。
**Almost every DS/DA interview starts with SQL.** Treated as a first-class section.

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 1.1 | SQL 基础 / SQL Basics | Chinook | SELECT, WHERE, ORDER BY, LIMIT |
| 1.2 | 多表 JOIN | Chinook | INNER / LEFT / RIGHT / FULL / CROSS / SELF |
| 1.3 | 聚合 & GROUP BY | Sakila | aggregate funcs, HAVING, ROLLUP, CUBE |
| 1.4 | 子查询 & CTE | Sakila | scalar, correlated, WITH RECURSIVE |
| 1.5 | 窗口函数 / Window Functions | Sales | ROW_NUMBER, RANK, LAG/LEAD, running totals |
| 1.6 | 高级 SQL 题型 / Advanced Patterns | LeetCode-style | nth-highest, pivot, sessionization, funnel |
| 1.7 | 索引与执行计划 / Indexes & EXPLAIN | Custom | B-tree, hash, EXPLAIN ANALYZE |
| 1.8 | Python + SQL 集成 | any | SQLAlchemy, pandas.read_sql, duckdb |
| 1.9 | NoSQL 速览 / NoSQL Overview | Movies JSON | MongoDB (document), Redis (KV), Cassandra (wide) |
| 1.10 | 数据仓库 / Data Warehouse | TPC-H | star vs snowflake schema, fact/dim, SCD |
| 1.11 | dbt 入门 / dbt Basics | toy warehouse | models, refs, tests, lineage |

---

## Part 2 · 统计学与概率 / Statistics & Probability

DS 面试第二关——统计基础题。
DS interview round two — stats.

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 2.1 | 描述统计 / Descriptive Stats | Tips | mean/median/mode, variance, skewness, kurtosis |
| 2.2 | 常见分布 / Distributions | Synthetic | Bernoulli, Binomial, Poisson, Normal, Exp, Gamma, Beta |
| 2.3 | 大数定律 & 中心极限定理 / LLN & CLT | Simulated | convergence, sampling distribution |
| 2.4 | 抽样方法 / Sampling | Census | SRS, stratified, cluster, reservoir sampling |
| 2.5 | 置信区间 / Confidence Intervals | Heights | t-CI, bootstrap CI, coverage |
| 2.6 | 假设检验 / Hypothesis Testing | Tips | t-test, z-test, chi-square, ANOVA, Wilcoxon, KS |
| 2.7 | 多重比较 / Multiple Testing | Microarray | Bonferroni, BH-FDR |
| 2.8 | 功效与样本量 / Power & Sample Size | Synthetic | type I/II error, MDE, power curves |
| 2.9 | 最大似然 / MLE | Coin flips, Gaussian | likelihood, log-likelihood, Fisher info |
| 2.10 | 贝叶斯估计 / Bayesian Estimation | Beta-Binomial | prior, posterior, conjugate, MAP |
| 2.11 | Bootstrap & Jackknife | Boston-like | resampling, percentile, BCa |
| 2.12 | 蒙特卡洛 / Monte Carlo | — | importance sampling, MCMC primer |

---

## Part 3 · EDA 与数据预处理 / EDA & Preprocessing

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 3.1 | 探索性数据分析 / EDA | Titanic | univariate / bivariate / multivariate |
| 3.2 | 缺失值处理 / Missing Values | Titanic | MCAR/MAR/MNAR, mean/median/KNN/MICE |
| 3.3 | 异常值检测 / Outliers | House Prices | z-score, IQR, Isolation Forest, LOF, Mahalanobis |
| 3.4 | 特征缩放 / Feature Scaling | Wine | standardization, normalization, robust, quantile |
| 3.5 | 类别变量编码 / Categorical Encoding | Adult Income | label, one-hot, ordinal, target, frequency, hashing |
| 3.6 | 特征工程 / Feature Engineering | House Prices (Ames) | interaction, polynomial, binning, datetime, geo |
| 3.7 | 文本特征工程 / Text Features | SMS Spam | tf-idf, n-gram, embeddings |
| 3.8 | 图像特征基础 / Image Features | Digits | HOG, SIFT, color histograms |
| 3.9 | 数据泄漏 / Data Leakage | Credit | target leak, train-test contamination, pipeline fix |
| 3.10 | 训练/验证/测试与 CV / Splitting & CV | Iris | hold-out, K-fold, stratified, group, time-series |
| 3.11 | 不平衡数据 / Imbalanced Data | Fraud | SMOTE, ADASYN, class weight, threshold tuning |
| 3.12 | 流水线 / Pipelines | Titanic | sklearn Pipeline, ColumnTransformer, FeatureUnion |

---

## Part 4 · 监督学习：回归 / Supervised Regression

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 4.1 | 线性回归 / Linear Regression | California Housing | OLS, normal equation, GD, Gauss-Markov |
| 4.2 | 回归诊断 / Regression Diagnostics | Same | residual plots, heteroscedasticity, multicollinearity, VIF |
| 4.3 | 多项式回归 / Polynomial Regression | Salary–Position | basis expansion, underfit/overfit |
| 4.4 | 岭回归 / Ridge (L2) | California Housing | L2 penalty, bias-variance |
| 4.5 | Lasso 回归 / Lasso (L1) | California Housing | L1 sparsity, coordinate descent, LARS |
| 4.6 | 弹性网 / Elastic Net | California Housing | L1+L2 hybrid |
| 4.7 | 广义线性模型 / GLM | Insurance Claims | link function, exp family, Poisson, Gamma |
| 4.8 | 非线性回归 / Nonlinear Regression | Curve-fitting | Levenberg-Marquardt, scipy.optimize |
| 4.9 | 支持向量回归 / SVR | Boston-like | kernel trick, ε-insensitive |
| 4.10 | KNN 回归 / KNN Regression | Diamonds | weighted average, distance metric |
| 4.11 | 决策树回归 / Decision Tree Regressor | Diamonds | CART, MSE split, pruning |
| 4.12 | 随机森林回归 / Random Forest Regressor | Diamonds | bagging, OOB, importance |
| 4.13 | 梯度提升回归 / Gradient Boosting Regressor | House Prices | additive model, learning rate |
| 4.14 | 分位数回归 / Quantile Regression | Engel curves | pinball loss, prediction interval |
| 4.15 | 稳健回归 / Robust Regression | Outlier data | Huber, RANSAC, Theil-Sen |
| 4.16 | 等张回归 / Isotonic Regression | Calibration | PAV algorithm |

---

## Part 5 · 监督学习：分类 / Supervised Classification

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 5.1 | 逻辑回归 / Logistic Regression | Breast Cancer | sigmoid, log-loss, decision boundary |
| 5.2 | Softmax 回归 / Softmax Regression | Iris | multinomial logit, cross-entropy |
| 5.3 | K 近邻 / KNN | Iris | distance metric, K choice, curse of dim |
| 5.4 | 朴素贝叶斯 / Naive Bayes | SMS Spam | Gaussian / Multinomial / Bernoulli NB |
| 5.5 | 支持向量机 / SVM | MNIST (subset) | hinge loss, kernels, C, gamma, SMO |
| 5.6 | 决策树分类器 / Decision Tree | Titanic | Gini, entropy, max_depth |
| 5.7 | 随机森林分类器 / Random Forest | Titanic | bootstrapping, randomness |
| 5.8 | 梯度提升 / GBDT | Adult Income | functional gradient |
| 5.9 | XGBoost | Adult Income | second-order Taylor, regularization |
| 5.10 | LightGBM | Adult Income | leaf-wise growth, histogram, categorical |
| 5.11 | CatBoost | Adult Income | ordered boosting, native categoricals |
| 5.12 | LDA & QDA | Wine | Bayes-optimal under Gaussian |
| 5.13 | 多类与多标签 / Multi-class & Multi-label | 20 Newsgroups | OvR, OvO, classifier chains |
| 5.14 | 不平衡分类 / Imbalanced Classification | Credit Card Fraud | SMOTE, class_weight, threshold |
| 5.15 | 在线学习 / Online Learning | Streaming | SGD partial_fit, perceptron, Vowpal Wabbit |

---

## Part 6 · 无监督学习 / Unsupervised Learning

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 6.1 | K-Means | Mall Customers | Lloyd's, K-means++, elbow, silhouette |
| 6.2 | Mini-batch K-Means | Large synthetic | scalable clustering |
| 6.3 | 层次聚类 / Hierarchical Clustering | Mall Customers | linkage, dendrogram |
| 6.4 | DBSCAN | Synthetic moons | ε, minPts, density |
| 6.5 | HDBSCAN | Geo points | hierarchical density |
| 6.6 | 高斯混合 / GMM | Old Faithful | EM, soft assignment |
| 6.7 | 谱聚类 / Spectral Clustering | Synthetic graph | graph Laplacian |
| 6.8 | 主成分分析 / PCA | Iris, MNIST | eigen-decomp, explained variance |
| 6.9 | 核 PCA / Kernel PCA | Swiss roll | kernel trick for nonlinear DR |
| 6.10 | 因子分析 / Factor Analysis | Psych data | latent variable model |
| 6.11 | ICA | Audio mixing | source separation |
| 6.12 | t-SNE | MNIST | perplexity, KL divergence |
| 6.13 | UMAP | MNIST, single-cell | manifold learning, fast |
| 6.14 | LDA 作为降维 / LDA as DR | Wine | supervised dim reduction |
| 6.15 | 自编码器 / Autoencoder | Fashion-MNIST | encoder-decoder, reconstruction |
| 6.16 | 异常检测 / Anomaly Detection | KDD subset | One-Class SVM, Isolation Forest, LOF |
| 6.17 | 关联规则 / Association Rules | Online Retail | Apriori, FP-Growth, support/confidence/lift |
| 6.18 | NMF | Documents | non-negative matrix factorization |

---

## Part 7 · 模型评估与优化 / Model Evaluation & Tuning

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 7.1 | 回归评估指标 / Regression Metrics | California | MAE, MSE, RMSE, R², adj R², MAPE, sMAPE |
| 7.2 | 分类评估指标 / Classification Metrics | Breast Cancer | accuracy, precision, recall, F1, ROC-AUC, PR-AUC, MCC |
| 7.3 | 偏差-方差权衡 / Bias-Variance | Synthetic | learning curves, validation curves |
| 7.4 | 交叉验证策略 / CV Strategies | Iris | K-fold, stratified, group, time-series, nested |
| 7.5 | 网格 / 随机 / 贝叶斯调参 | Wine | GridSearchCV, Randomized, Optuna (TPE), Hyperopt |
| 7.6 | 多目标 / 帕累托 / Multi-objective | Custom | trade-off frontiers |
| 7.7 | 特征选择 / Feature Selection | Madelon | filter, wrapper, embedded, RFE |
| 7.8 | 模型解释 / Model Interpretability | Adult Income | SHAP, LIME, permutation importance, PDP/ICE |
| 7.9 | 校准 / Calibration | Credit | Platt, isotonic, reliability diagram |
| 7.10 | 公平性 / Fairness | COMPAS | demographic parity, equalized odds, debiasing |
| 7.11 | 鲁棒性 / Robustness | Image classifier | adversarial examples, FGSM |
| 7.12 | 概念漂移 / Concept Drift | Streaming | drift detection (DDM, ADWIN) |

---

## Part 8 · 集成学习 / Ensemble Learning

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 8.1 | Bagging | Titanic | bootstrap aggregation |
| 8.2 | Random Forest 深入 / RF Deep Dive | Titanic | feature randomness, OOB |
| 8.3 | AdaBoost | Titanic | exponential loss, weighted samples |
| 8.4 | Gradient Boosting 推导 / Derivation | Synthetic | functional gradient descent |
| 8.5 | XGBoost / LightGBM / CatBoost 对比 | Adult | implementation differences, when to use |
| 8.6 | Voting & Averaging | Wine | hard / soft voting |
| 8.7 | Stacking & Blending | House Prices | meta-learner, OOF predictions |

---

## Part 9 · 深度学习基础 / Deep Learning Foundations

完整覆盖，不依赖外部仓库。
Standalone, full coverage.

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 9.1 | 感知器 & 多层感知器 / Perceptron & MLP | XOR, MNIST | activation, layer |
| 9.2 | 神经网络从零实现 / NN from Scratch (NumPy) | MNIST | forward, backprop, SGD |
| 9.3 | PyTorch 入门 / PyTorch Basics | MNIST | tensor, autograd, nn.Module, DataLoader |
| 9.4 | TensorFlow / Keras 入门 | MNIST | Sequential, Functional API |
| 9.5 | 激活函数 / Activations | Synthetic | sigmoid, tanh, ReLU, GELU, Swish, leaky |
| 9.6 | 损失函数 / Loss Functions | various | MSE, CE, focal, contrastive, triplet |
| 9.7 | 优化器 / Optimizers | MNIST | SGD, momentum, NAG, Adam, AdamW, RMSProp, Adagrad |
| 9.8 | 学习率调度 / LR Schedulers | MNIST | step, cosine, warmup, ReduceLROnPlateau, one-cycle |
| 9.9 | 初始化 / Initialization | MNIST | Xavier, He, orthogonal |
| 9.10 | 正则化 / Regularization | CIFAR-10 (subset) | dropout, BN, LN, weight decay, early stopping, mixup |
| 9.11 | 训练技巧 / Training Tricks | CIFAR | gradient clipping, accumulation, AMP/half precision |
| 9.12 | 分布式训练 / Distributed Training | CIFAR | DataParallel, DDP, ZeRO 基础 |
| 9.13 | 迁移学习 / Transfer Learning | Flowers | feature extraction, fine-tuning |
| 9.14 | 神经网络可视化 / NN Visualization | MNIST | activation, filter, Grad-CAM |

---

## Part 10 · 计算机视觉 / Computer Vision

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 10.1 | 图像处理基础 / Image Processing | any | OpenCV, PIL, color spaces, filters |
| 10.2 | 卷积神经网络 / CNN | CIFAR-10 | conv, pooling, receptive field |
| 10.3 | 经典 CNN 架构 / Classic CNNs | CIFAR | LeNet, AlexNet, VGG, GoogLeNet |
| 10.4 | ResNet & Skip Connections | CIFAR | residual block, identity mapping |
| 10.5 | 数据增强 / Data Augmentation | CIFAR | flip/crop, mixup, cutout, AutoAugment |
| 10.6 | 目标检测 / Object Detection | Pascal VOC (subset) | sliding window, R-CNN family, YOLO, SSD |
| 10.7 | 语义 & 实例分割 / Segmentation | Cityscapes (subset) | FCN, U-Net, Mask R-CNN |
| 10.8 | 关键点检测 / Pose Estimation | COCO (subset) | heatmap regression |
| 10.9 | Vision Transformer / ViT | CIFAR | patch embedding, class token |
| 10.10 | 多模态 / Multimodal (CLIP) | Custom image-text | contrastive learning |
| 10.11 | 自监督学习 / Self-Supervised | CIFAR | SimCLR, MoCo, MAE |

---

## Part 11 · 经典 NLP / Classic NLP

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 11.1 | 文本预处理 / Text Preprocessing | 20 Newsgroups | tokenize, stopwords, stem/lemma, regex |
| 11.2 | 词袋与 TF-IDF / BoW & TF-IDF | SMS Spam | n-gram, sparse |
| 11.3 | 词向量 / Word Embeddings | Text8 | Word2Vec (CBOW, Skip-gram), GloVe, FastText |
| 11.4 | 文本分类 / Text Classification | IMDB | logistic + TF-IDF, FastText |
| 11.5 | 情感分析 / Sentiment Analysis | Twitter | lexicon + ML |
| 11.6 | 主题模型 / Topic Modeling | NYT | LDA, NMF |
| 11.7 | 命名实体识别 / NER | CoNLL-2003 | BIO tagging, CRF, spaCy |
| 11.8 | 序列标注 / Sequence Labeling | PoS | HMM, CRF, BiLSTM-CRF |
| 11.9 | 文本相似度 / Text Similarity | Quora pairs | edit distance, cosine, Jaccard, BM25 |

---

## Part 12 · 现代 NLP 与大语言模型 / Modern NLP & LLMs  ⭐⭐⭐

LLM 是当下数据科学家的必备能力，完整覆盖一遍。
LLMs are table stakes today — full coverage here.

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 12.1 | RNN, LSTM, GRU | IMDB | sequence modeling, vanishing gradient |
| 12.2 | Seq2Seq & Attention | Translation toy | encoder-decoder, Bahdanau, Luong |
| 12.3 | Transformer 从零实现 / Transformer from Scratch | Toy translation | Q/K/V, multi-head, positional encoding |
| 12.4 | BERT & Encoder Models | GLUE (subset) | MLM, NSP, fine-tuning |
| 12.5 | GPT & Decoder Models | TinyStories | causal LM, autoregressive |
| 12.6 | T5 & Encoder-Decoder | Summarization | text-to-text framework |
| 12.7 | 分词 / Tokenization | — | BPE, WordPiece, SentencePiece, tiktoken |
| 12.8 | 预训练 vs 微调 / Pretraining vs Fine-tuning | — | concepts + when to use |
| 12.9 | 参数高效微调 / PEFT | small LLM | LoRA, QLoRA, prefix tuning |
| 12.10 | RLHF / DPO | Preference data | reward model, PPO, DPO |
| 12.11 | Prompt Engineering | — | few-shot, CoT, ReAct, self-consistency |
| 12.12 | RAG / Retrieval-Augmented Generation | Wiki | embeddings + vector DB + reranker |
| 12.13 | 向量数据库 / Vector Databases | — | FAISS, Chroma, Pinecone, HNSW |
| 12.14 | LLM Agents | — | tool use, function calling, planning |
| 12.15 | 评估 LLM / LLM Evaluation | MT-Bench style | perplexity, BLEU, ROUGE, LLM-as-judge |
| 12.16 | LLM 推理优化 / LLM Inference Optimization | — | KV cache, quantization, vLLM, speculative decoding |

---

## Part 13 · 生成模型 / Generative Models

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 13.1 | 自编码器回顾 / AE Recap | MNIST | reconstruction |
| 13.2 | 变分自编码器 / VAE | MNIST | ELBO, reparameterization |
| 13.3 | GAN 基础 / GAN | MNIST | minimax, mode collapse |
| 13.4 | DCGAN / WGAN | CelebA (subset) | conv GAN, Wasserstein loss |
| 13.5 | 条件 GAN / cGAN, pix2pix | edges→shoes | conditional generation |
| 13.6 | 流模型 / Normalizing Flows | Toy 2D | invertible NN, RealNVP |
| 13.7 | 扩散模型 / Diffusion | MNIST | forward/reverse process, DDPM |
| 13.8 | Stable Diffusion 工作原理 / SD Internals | — | latent diffusion, U-Net, CLIP cond |
| 13.9 | 评估生成模型 / Generative Eval | — | FID, IS, perceptual metrics |

---

## Part 14 · 时间序列 / Time Series

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 14.1 | 时间序列基础 / TS Basics | Air Passengers | trend, seasonality, stationarity, ACF/PACF |
| 14.2 | 分解 / Decomposition | Air Passengers | additive vs multiplicative, STL |
| 14.3 | 平滑法 / Smoothing | Sales | MA, EWMA, Holt-Winters |
| 14.4 | ARIMA / SARIMA / SARIMAX | Air Passengers | AR, MA, I, seasonal, exogenous |
| 14.5 | Prophet | Wikipedia pageviews | Bayesian additive |
| 14.6 | LSTM / GRU for TS | Stock prices | sequence-to-one, windowing |
| 14.7 | Temporal CNN / TCN | Energy load | dilated conv |
| 14.8 | Transformers for TS | Electricity | Informer, PatchTST 概念 |
| 14.9 | 多变量 & 多步预测 / Multivariate & Multi-step | M5 (subset) | VAR, direct vs recursive |
| 14.10 | 异常检测 in TS / TS Anomaly Detection | NAB | STL residual, Twitter ESD |
| 14.11 | 因果性检验 / Granger Causality | Macro | VAR, Granger test |

---

## Part 15 · 推荐系统 / Recommender Systems

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 15.1 | 基于内容 / Content-based | MovieLens | TF-IDF + cosine |
| 15.2 | 协同过滤 / Collaborative Filtering | MovieLens | user-user, item-item, KNN |
| 15.3 | 矩阵分解 / Matrix Factorization | MovieLens | SVD, ALS, SGD |
| 15.4 | 隐式反馈 / Implicit Feedback | Last.fm | BPR, weighted MF |
| 15.5 | FM & FFM | Avazu (subset) | factorization machines |
| 15.6 | Wide & Deep | Census | memorization + generalization |
| 15.7 | DeepFM, DCN | Criteo (subset) | feature interactions |
| 15.8 | 双塔模型 / Two-Tower | MovieLens | sampled softmax, retrieval |
| 15.9 | 序列推荐 / Sequential | MovieLens | SASRec, GRU4Rec, BERT4Rec |
| 15.10 | 多臂赌博机 / Multi-armed Bandits | Synthetic | ε-greedy, UCB, Thompson |
| 15.11 | 评估 / Evaluation | MovieLens | precision@k, recall@k, NDCG, MAP, hit rate |

---

## Part 16 · 图数据与图神经网络 / Graph Data & GNN

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 16.1 | 图基础与 NetworkX / Graph Basics | Karate | nodes, edges, degree, paths |
| 16.2 | 图算法 / Graph Algorithms | Karate | BFS/DFS, shortest path, centrality |
| 16.3 | 社区发现 / Community Detection | Karate | modularity, Louvain |
| 16.4 | PageRank & HITS | Web graph | random walk |
| 16.5 | 节点嵌入 / Node Embeddings | Cora | DeepWalk, node2vec |
| 16.6 | GCN | Cora | spectral GNN |
| 16.7 | GraphSAGE | Reddit (subset) | inductive learning |
| 16.8 | GAT | Citation | attention on graphs |
| 16.9 | 知识图谱 / Knowledge Graphs | FB15k-237 | TransE, RotatE |

---

## Part 17 · 强化学习 / Reinforcement Learning

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 17.1 | MDP 与贝尔曼方程 / MDP & Bellman | GridWorld | state, action, reward, policy, value |
| 17.2 | 动态规划 / Dynamic Programming | GridWorld | policy iter, value iter |
| 17.3 | 蒙特卡洛方法 / Monte Carlo | Blackjack | every-visit, first-visit |
| 17.4 | TD 学习 / TD Learning | GridWorld | TD(0), SARSA |
| 17.5 | Q-Learning | Taxi-v3 | off-policy, ε-greedy |
| 17.6 | DQN | CartPole | replay buffer, target net |
| 17.7 | 策略梯度 / Policy Gradient | CartPole | REINFORCE, baseline |
| 17.8 | Actor-Critic, A2C, A3C | CartPole | advantage estimation |
| 17.9 | PPO | LunarLander | clipped surrogate |
| 17.10 | Bandits & Contextual Bandits | News rec | exploration vs exploitation |

---

## Part 18 · 贝叶斯方法 / Bayesian Methods

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 18.1 | 贝叶斯线性回归 / Bayesian Linear Regression | Synthetic | conjugate prior, posterior |
| 18.2 | 贝叶斯逻辑回归 / Bayesian Logistic | Synthetic | Laplace approximation |
| 18.3 | MCMC | Beta-Binomial | Metropolis-Hastings, Gibbs |
| 18.4 | 变分推断 / Variational Inference | Mixture | ELBO, mean-field |
| 18.5 | PyMC / Stan / NumPyro 实战 | Hierarchical model | probabilistic programming |
| 18.6 | 高斯过程 / Gaussian Processes | 1D regression | kernel, posterior over functions |
| 18.7 | 贝叶斯优化 / Bayesian Optimization | Hyperparam tuning | acquisition functions |

---

## Part 19 · 因果推断与实验 / Causal Inference & Experimentation

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 19.1 | A/B 测试设计 / A/B Test Design | Synthetic | randomization, MDE, power |
| 19.2 | A/B 测试分析 / A/B Test Analysis | Synthetic | t-test, CUPED, bootstrap CI |
| 19.3 | 多臂赌博机 vs A/B / Bandits vs AB | Synthetic | when to use which |
| 19.4 | 因果图 / DAGs & do-calculus | — | confounding, mediation, collider |
| 19.5 | 倾向得分匹配 / PSM | LaLonde | propensity, matching |
| 19.6 | 双重差分 / DiD | Card-Krueger | parallel trends |
| 19.7 | 工具变量 / IV | Education–wage | 2SLS |
| 19.8 | 回归断点 / RDD | Election | sharp / fuzzy |
| 19.9 | 因果森林 / Causal Forest | Synthetic | heterogeneous treatment effects |
| 19.10 | 提升模型 / Uplift Modeling | Marketing | T-learner, S-learner, X-learner, R-learner |
| 19.11 | 网络效应实验 / Network Experiments | Social graph | SUTVA violation, cluster randomization |

---

## Part 20 · 高级 / 专门主题 / Advanced Topics

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 20.1 | 生存分析 / Survival Analysis | Lung | Kaplan-Meier, Cox PH |
| 20.2 | 地理空间分析 / Geospatial | NYC Taxi, GeoJSON | GeoPandas, H3, shapely |
| 20.3 | 音频与语音 / Audio | UrbanSound8K | spectrogram, MFCC, CNN audio |
| 20.4 | 异常检测进阶 / Advanced Anomaly Detection | NAB, MVTec | autoencoder, deep SVDD, PaDiM |
| 20.5 | 半监督学习 / Semi-supervised | CIFAR | label propagation, self-training, FixMatch |
| 20.6 | 主动学习 / Active Learning | MNIST | uncertainty sampling |
| 20.7 | 元学习 / Meta-Learning | Omniglot | MAML, prototypical net |
| 20.8 | 联邦学习 / Federated Learning | MNIST partitioned | FedAvg |
| 20.9 | 隐私保护机器学习 / Privacy-Preserving ML | MNIST | differential privacy, DP-SGD |
| 20.10 | 数据合成 / Synthetic Data Generation | Tabular | SMOTE, CTGAN |
| 20.11 | 多任务学习 / Multi-task Learning | Multi-output | shared backbone |
| 20.12 | 排序学习 / Learning to Rank | LETOR | RankNet, LambdaMART |

---

## Part 21 · 大数据 / Big Data  ⭐⭐ (大厂必备)

数据量上 TB / PB 后单机搞不定，必须懂这些。
Single-machine pandas dies above TB scale — must-know.

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 21.1 | PySpark 入门 / PySpark Basics | NYC Taxi | RDD, DataFrame, SparkSession |
| 21.2 | Spark SQL & 优化 / Spark SQL & Tuning | NYC Taxi | partitioning, broadcast join, catalyst |
| 21.3 | Spark MLlib | Titanic-scale | pipeline, distributed training |
| 21.4 | Spark Streaming / Structured Streaming | Kafka topic | micro-batch, watermark |
| 21.5 | Dask | Large CSV | task graph, dask.dataframe, dask.delayed |
| 21.6 | Polars (Lazy) at Scale | Multi-GB | streaming engine |
| 21.7 | DuckDB | Parquet | analytical SQL on local data |
| 21.8 | 数据存储格式 / Storage Formats | various | CSV, Parquet, Avro, ORC, Arrow |
| 21.9 | Hadoop 生态速览 / Hadoop Overview | — | HDFS, YARN, Hive |
| 21.10 | Kafka 入门 / Kafka Basics | Toy stream | producer, consumer, topic |
| 21.11 | Lakehouse: Delta / Iceberg / Hudi | — | ACID on object storage |
| 21.12 | 分布式 ML 训练 / Distributed Training at Scale | — | Horovod, Ray, DeepSpeed 概念 |

---

## Part 22 · MLOps 与部署 / MLOps & Deployment  ⭐⭐

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 22.1 | 模型持久化 / Model Persistence | any | pickle, joblib, ONNX |
| 22.2 | Scikit-learn Pipelines | Titanic | ColumnTransformer, end-to-end fit |
| 22.3 | FastAPI 部署 / Deployment with FastAPI | Iris | REST API, pydantic |
| 22.4 | Streamlit 仪表板 / Dashboards | any | quick UI |
| 22.5 | Docker 入门 / Docker Basics | model service | image, container, compose |
| 22.6 | Kubernetes 入门 / K8s Basics for ML | — | pod, service, deployment, KServe |
| 22.7 | CI/CD for ML | GitHub Actions | lint, test, model release |
| 22.8 | 实验追踪 / Experiment Tracking | any | MLflow, Weights & Biases |
| 22.9 | 特征平台 / Feature Store | toy | Feast 基础 |
| 22.10 | 模型监控 & 漂移 / Monitoring & Drift | Synthetic | data drift, concept drift, PSI, KS, Evidently |
| 22.11 | A/B 测试基础设施 / A/B Infra | — | bucketing, traffic split, shadow deploy |
| 22.12 | 边缘部署 / Edge Deployment | TFLite/ONNX | quantization, pruning, distillation |

---

## Part 23 · 云计算与数据科学 / Cloud for Data Science

| # | 主题 / Topic | 数据集 / Dataset | 关键概念 / Key Concepts |
|---|---|---|---|
| 23.1 | AWS for DS | — | S3, EC2, SageMaker, Lambda, Athena, Redshift |
| 23.2 | GCP for DS | — | GCS, BigQuery, Vertex AI, Dataflow |
| 23.3 | Azure for DS | — | Blob, Synapse, Azure ML |
| 23.4 | Databricks | — | notebooks, Delta Lake, jobs |
| 23.5 | Snowflake | — | warehouse, Snowpark |
| 23.6 | Airflow / Prefect / Dagster | toy DAG | scheduling, task graph |

---

## Part 24 · ML 系统设计与面试 / ML System Design & Interviews  ⭐⭐⭐

终极阶段——大厂 senior DS / MLE 面试。
The final boss — senior DS / MLE interviews.

| # | 主题 / Topic | 内容 / Content |
|---|---|---|
| 24.1 | 设计推荐系统 / Design a Recommender | YouTube / Netflix 级别 |
| 24.2 | 设计搜索系统 / Design a Search Ranker | Google / Amazon 搜索 |
| 24.3 | 设计 feed / 时间线 / Design a News Feed | Facebook / Twitter |
| 24.4 | 设计广告系统 / Design an Ads CTR System | Meta / Google Ads |
| 24.5 | 设计欺诈检测 / Design Fraud Detection | Stripe / Visa |
| 24.6 | 设计 ETA / 路径预测 / Design ETA Prediction | Uber / DoorDash |
| 24.7 | 设计内容审核 / Design Content Moderation | Reddit / TikTok |
| 24.8 | 设计 RAG 系统 / Design a RAG System | 企业知识库 |
| 24.9 | 案例面试题型 / Case Interview Patterns | metric design, root cause analysis |
| 24.10 | 行为面试与 DS 故事 / Behavioral & DS Storytelling | STAR framework |
| 24.11 | SQL 面试速通 / SQL Interview Cram | LeetCode hard SQL |
| 24.12 | 机器学习概念速通 / ML Concepts Cram | classic interview Q&A |

---

## 进度追踪 / Progress Tracker

- [x] Part 0: Foundations
- [x] Part 1: SQL & Databases
- [x] Part 2: Statistics & Probability
- [x] Part 3: EDA & Preprocessing
- [x] Part 4: Regression
- [x] Part 5: Classification
- [x] Part 6: Unsupervised
- [x] Part 7: Evaluation & Tuning
- [x] Part 8: Ensemble
- [x] Part 9: Deep Learning
- [x] Part 10: Computer Vision
- [x] Part 11: Classic NLP
- [x] Part 12: Modern NLP & LLMs
- [x] Part 13: Generative Models
- [x] Part 14: Time Series
- [x] Part 15: Recommender Systems
- [x] Part 16: Graph & GNN
- [ ] Part 17: Reinforcement Learning
- [ ] Part 18: Bayesian Methods
- [ ] Part 19: Causal Inference
- [ ] Part 20: Advanced Topics
- [ ] Part 21: Big Data
- [ ] Part 22: MLOps & Deployment
- [ ] Part 23: Cloud for DS
- [ ] Part 24: ML System Design & Interviews

---

## 每个 Notebook 的标准结构 / Standard Notebook Template

每个 notebook 都遵循同一套结构，确保体验一致：
Every notebook follows the same flow for consistency:

1. **背景与问题定义 / Background & Problem Statement** — 中英双语
2. **数学原理推导 / Math Derivation** — LaTeX 公式
3. **数据加载与 EDA / Data Loading & EDA**
4. **从零实现 / From-scratch Implementation** — 仅 NumPy（适用时）
5. **使用标准库 / Using Standard Libraries** — sklearn / PyTorch / etc.
6. **模型评估 / Evaluation** — 多指标对比
7. **结果可视化 / Visualization** — 图表化结论
8. **小结 / Summary** — 知识点回顾 + 真实工作场景中怎么用

