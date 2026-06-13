# Part 3 · EDA 与数据预处理 / EDA & Preprocessing

> 模型再好，garbage in = garbage out。Part 0-2 打好了工具和统计地基；这一部分是**真实脏数据的实战车间**——探索、清洗、变换、防泄漏。
> No model survives bad data. This part is the hands-on workshop on real dirty data: explore, clean, transform, prevent leakage.

## 内容清单 / Contents

| # | Notebook | 主题 / Topic | 状态 / Status |
|---|---|---|---|
| 3.1 | [`01_eda.ipynb`](01_eda.ipynb) | 探索性数据分析 / EDA | ✅ Done |
| 3.2 | [`02_missing_values.ipynb`](02_missing_values.ipynb) | 缺失值处理 / Missing Values | ✅ Done |
| 3.3 | [`03_outliers.ipynb`](03_outliers.ipynb) | 异常值检测 / Outliers | ✅ Done |
| 3.4 | [`04_feature_scaling.ipynb`](04_feature_scaling.ipynb) | 特征缩放 / Feature Scaling | ✅ Done |
| 3.5 | [`05_categorical_encoding.ipynb`](05_categorical_encoding.ipynb) | 类别变量编码 / Categorical Encoding | ✅ Done |
| 3.6 | [`06_feature_engineering.ipynb`](06_feature_engineering.ipynb) | 特征工程 / Feature Engineering | ✅ Done |
| 3.7 | [`07_text_features.ipynb`](07_text_features.ipynb) | 文本特征工程 / Text Features | ✅ Done |
| 3.8 | [`08_image_features.ipynb`](08_image_features.ipynb) | 图像特征基础 / Image Features | ✅ Done |
| 3.9 | [`09_data_leakage.ipynb`](09_data_leakage.ipynb) | 数据泄漏 / Data Leakage | ✅ Done |
| 3.10 | [`10_splitting_cv.ipynb`](10_splitting_cv.ipynb) | 划分与交叉验证 / Splitting & CV | ✅ Done |
| 3.11 | [`11_imbalanced_data.ipynb`](11_imbalanced_data.ipynb) | 不平衡数据 / Imbalanced Data | ✅ Done |
| 3.12 | [`12_pipelines.ipynb`](12_pipelines.ipynb) | 流水线 / Pipelines | ✅ Done |

## 数据集 / Datasets

| 数据集 / Dataset | 来源 / Source | 用在 / Used in |
|---|---|---|
| Titanic | `seaborn.load_dataset("titanic")` | 3.1, 3.2, 3.12 |
| California Housing | `sklearn.datasets.fetch_california_housing` | 3.3, 3.6 |
| Wine | `sklearn.datasets.load_wine` | 3.4 |
| Synthetic (adult-income style / fraud / credit) | inline `numpy.default_rng` | 3.5, 3.9, 3.11 |
| SMS Spam (mini) | inline | 3.7 |
| Digits | `sklearn.datasets.load_digits` | 3.8 |
| Iris | `sklearn.datasets.load_iris` | 3.10 |

## 工具栈 / Tools

`pandas` + `scikit-learn`（预处理 / Pipeline / ColumnTransformer）+ `imbalanced-learn`（SMOTE）+ `scikit-image`（HOG）。
所有变换都**先讲数学/直觉，再用 sklearn 实现，并强调防泄漏的正确姿势**（fit 只在 train，transform 全程）。
