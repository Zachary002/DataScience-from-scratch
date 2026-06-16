# Part 6 · 无监督学习 / Unsupervised Learning

> Part 4-5 有标签(监督)。这一部分**没有标签**——从数据自身结构里发现聚类、低维表示、潜在因子、异常和关联。聚类(K-Means→DBSCAN→GMM→谱聚类)、降维(PCA→核PCA→t-SNE→UMAP→自编码器)、异常检测、关联规则、矩阵分解。
> No labels here. We discover structure: clusters, low-dimensional representations, latent factors, anomalies, and associations.

## 内容清单 / Contents

| # | Notebook | 主题 / Topic | 状态 |
|---|---|---|---|
| 6.1 | [`01_kmeans.ipynb`](01_kmeans.ipynb) | K-Means | ✅ |
| 6.2 | [`02_minibatch_kmeans.ipynb`](02_minibatch_kmeans.ipynb) | Mini-batch K-Means | ✅ |
| 6.3 | [`03_hierarchical_clustering.ipynb`](03_hierarchical_clustering.ipynb) | 层次聚类 / Hierarchical | ✅ |
| 6.4 | [`04_dbscan.ipynb`](04_dbscan.ipynb) | DBSCAN | ✅ |
| 6.5 | [`05_hdbscan.ipynb`](05_hdbscan.ipynb) | HDBSCAN | ✅ |
| 6.6 | [`06_gmm.ipynb`](06_gmm.ipynb) | 高斯混合 / GMM (EM) | ✅ |
| 6.7 | [`07_spectral_clustering.ipynb`](07_spectral_clustering.ipynb) | 谱聚类 / Spectral | ✅ |
| 6.8 | [`08_pca.ipynb`](08_pca.ipynb) | 主成分分析 / PCA | ✅ |
| 6.9 | [`09_kernel_pca.ipynb`](09_kernel_pca.ipynb) | 核 PCA / Kernel PCA | ✅ |
| 6.10 | [`10_factor_analysis.ipynb`](10_factor_analysis.ipynb) | 因子分析 / Factor Analysis | ✅ |
| 6.11 | [`11_ica.ipynb`](11_ica.ipynb) | 独立成分分析 / ICA | ✅ |
| 6.12 | [`12_tsne.ipynb`](12_tsne.ipynb) | t-SNE | ✅ |
| 6.13 | [`13_umap.ipynb`](13_umap.ipynb) | UMAP | ✅ |
| 6.14 | [`14_lda_dimensionality.ipynb`](14_lda_dimensionality.ipynb) | LDA 作为降维 / LDA as DR | ✅ |
| 6.15 | [`15_autoencoder.ipynb`](15_autoencoder.ipynb) | 自编码器 / Autoencoder | ✅ |
| 6.16 | [`16_anomaly_detection.ipynb`](16_anomaly_detection.ipynb) | 异常检测 / Anomaly Detection | ✅ |
| 6.17 | [`17_association_rules.ipynb`](17_association_rules.ipynb) | 关联规则 / Association Rules | ✅ |
| 6.18 | [`18_nmf.ipynb`](18_nmf.ipynb) | NMF | ✅ |

## 数据集 / Datasets

| 数据集 | 来源 | 用在 |
|---|---|---|
| Mall Customers (synthetic) | inline `numpy.default_rng` | 6.1, 6.3 |
| 大规模合成 blobs | `sklearn.datasets.make_blobs` | 6.2 |
| make_moons / make_circles | `sklearn.datasets` | 6.4, 6.7 |
| 地理点 (synthetic) | inline | 6.5 |
| Old Faithful (inline) | inline | 6.6 |
| Iris / Digits | `sklearn.datasets` | 6.8, 6.12, 6.13 |
| Swiss roll | `sklearn.datasets.make_swiss_roll` | 6.9 |
| 心理测量 (synthetic) | inline | 6.10 |
| 混合音频信号 (synthetic) | inline | 6.11 |
| Wine | `sklearn.datasets.load_wine` | 6.14 |
| Digits (Fashion-MNIST 替身) | `sklearn.datasets.load_digits` | 6.15 |
| 网络入侵 (synthetic, KDD 风格) | inline | 6.16 |
| 零售购物篮 (synthetic) | inline | 6.17 |
| 20 Newsgroups subset | `sklearn.datasets.fetch_20newsgroups` | 6.18 |

## 工具栈 / Tools

`scikit-learn`(聚类/降维/异常) + `scipy`(层次/信号) + `umap-learn` + `mlxtend`(Apriori/FP-Growth) + `torch`(自编码器)。
每个方法**先讲数学/直觉, 再从零实现(可行时), 再对照库**, 标注 💡 面试要点。无监督评估贯穿: 没有标签时如何衡量(silhouette / 重构误差 / 解释方差)。
