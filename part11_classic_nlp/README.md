# Part 11 · 经典 NLP / Classic NLP

> 进入文本世界。从分词/清洗、词袋与 TF-IDF、词向量(Word2Vec 从零)，到文本分类、情感分析、主题模型、命名实体识别、序列标注(HMM 从零)、文本相似度。这是**深度学习之前**(也是至今仍大量使用)的 NLP 主干——理解它们才能真正读懂现代 NLP/LLM 为何而来。
> Entering the text world. From tokenization/cleaning, Bag-of-Words & TF-IDF, word embeddings (Word2Vec from scratch), to text classification, sentiment analysis, topic modeling, NER, sequence labeling (HMM from scratch), and text similarity. This is the **pre-deep-learning** (and still widely used) NLP backbone — understanding it is key to grasping why modern NLP/LLMs exist.

每个 notebook 都遵循全仓统一标准：逐句中英双语、直觉优先讲解、丰富代码注释、💡面试速查 + 💼实战视角，**大量动手实验 + 可视化**，所有代码单元实跑验证。
Every notebook follows the repo-wide standards: line-by-line bilingual, intuition-first, richly commented code, 💡 interview cheat-sheets + 💼 practical angles, **experiment-heavy with visualizations**, all cells validated.

## 工具与数据 / Tools & Data
- **库**：`scikit-learn`(向量化/分类/LDA-NMF)、`nltk`(分词/停用词/词形还原/语料)、`torch`(从零 Word2Vec)、`numpy/scipy`。
  **Libraries:** `scikit-learn`, `nltk`, `torch` (from-scratch Word2Vec), `numpy/scipy`.
- **数据**：`20 Newsgroups`(sklearn 自带)、`nltk` 自带语料 `movie_reviews`(2000 条带标注影评→情感)、`treebank`(带词性标注句子→HMM)、停用词表等。首次运行自动下载(很小很快)。
  **Data:** `20 Newsgroups` (sklearn), `nltk` corpora `movie_reviews` (2000 labeled reviews → sentiment), `treebank` (PoS-tagged → HMM), stopwords. Auto-downloaded on first run (small/fast).

> 安装：`pip install nltk`，notebook 内用 `nltk.download(...)` 自动取数据。本仓秉持"from scratch"理念：Word2Vec、TF-IDF、编辑距离、BM25、HMM-Viterbi 等都**从零实现**，同时演示 sklearn/nltk 的实战用法。
> Install: `pip install nltk`; notebooks fetch data via `nltk.download(...)`. True to the "from scratch" spirit, Word2Vec, TF-IDF, edit distance, BM25, HMM-Viterbi are **implemented from scratch**, alongside practical sklearn/nltk usage.

## 目录 / Contents
| # | 主题 / Topic | 数据 / Data | 关键概念 / Key Concepts |
|---|---|---|---|
| 11.1 | 文本预处理 / Text Preprocessing | 20NG/影评 | 分词, 归一化, 停用词, 词干vs词形还原, Zipf 定律 |
| 11.2 | 词袋与 TF-IDF / BoW & TF-IDF | 20NG | one-hot, BoW, n-gram, 稀疏, 从零TF-IDF |
| 11.3 | 词向量 / Word Embeddings | 文本语料 | 分布假设, 从零 Skip-gram+负采样, 词类比, 可视化 |
| 11.4 | 文本分类 / Text Classification | 20NG | TF-IDF+逻辑回归/朴素贝叶斯, 管道, 误差分析 |
| 11.5 | 情感分析 / Sentiment Analysis | movie_reviews | 词典法 vs 机器学习, 否定处理 |
| 11.6 | 主题模型 / Topic Modeling | 20NG | LDA, NMF, 主题可视化, 一致性 |
| 11.7 | 命名实体识别 / NER | 合成/小样本 | BIO 标注, 特征, 序列模型思想 |
| 11.8 | 序列标注 / Sequence Labeling | treebank | 词性标注, **HMM+Viterbi 从零**, BiLSTM 思想 |
| 11.9 | 文本相似度 / Text Similarity | 例句/20NG | 编辑距离, 余弦, Jaccard, **BM25 从零** |

## 学习路径 / Path
11.1 → 11.2 → 11.3 是表示文本的三步进阶（清洗→计数向量→稠密向量）。
11.1 → 11.2 → 11.3 are three steps of representing text (clean → count vectors → dense vectors).
11.4–11.6 是核心应用；11.7–11.8 是序列任务；11.9 贯穿检索与匹配。
11.4–11.6 are core applications; 11.7–11.8 are sequence tasks; 11.9 underpins retrieval/matching.
