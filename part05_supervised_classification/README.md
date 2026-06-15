# Part 5 · 监督学习：分类 / Supervised Classification

> Part 4 预测连续值, Part 5 预测**类别**。从逻辑回归的数学推导到 XGBoost/LightGBM/CatBoost 三巨头, 完整的评估指标体系(ROC/PR/F1), 不平衡, 多类多标签, 校准, 在线学习。很多概念(正则/树/boosting/校准)从 Part 4 直接迁移。
> Regression predicts numbers, classification predicts classes. From logistic regression to the GBDT big-three, full metrics (ROC/PR/F1), imbalance, multiclass, calibration, online learning. Much carries over from Part 4.

## 内容清单 / Contents

| # | Notebook | 主题 / Topic | 状态 |
|---|---|---|---|
| 5.1 | [`01_logistic_regression.ipynb`](01_logistic_regression.ipynb) | 逻辑回归 + 评估指标 / Logistic Regression + Metrics | ✅ |
| 5.2 | [`02_softmax_regression.ipynb`](02_softmax_regression.ipynb) | Softmax 回归 / Softmax | ✅ |
| 5.3 | [`03_knn_classifier.ipynb`](03_knn_classifier.ipynb) | K 近邻 / KNN | ✅ |
| 5.4 | [`04_naive_bayes.ipynb`](04_naive_bayes.ipynb) | 朴素贝叶斯 / Naive Bayes | ✅ |
| 5.5 | [`05_svm.ipynb`](05_svm.ipynb) | 支持向量机 / SVM | ✅ |
| 5.6 | [`06_decision_tree_classifier.ipynb`](06_decision_tree_classifier.ipynb) | 决策树分类器 / Decision Tree | ✅ |
| 5.7 | [`07_random_forest_classifier.ipynb`](07_random_forest_classifier.ipynb) | 随机森林分类器 / Random Forest | ✅ |
| 5.8 | [`08_gbdt_classifier.ipynb`](08_gbdt_classifier.ipynb) | 梯度提升分类 / GBDT | ✅ |
| 5.9 | [`09_xgboost.ipynb`](09_xgboost.ipynb) | XGBoost | ✅ |
| 5.10 | [`10_lightgbm.ipynb`](10_lightgbm.ipynb) | LightGBM | ✅ |
| 5.11 | [`11_catboost.ipynb`](11_catboost.ipynb) | CatBoost | ✅ |
| 5.12 | [`12_lda_qda.ipynb`](12_lda_qda.ipynb) | LDA & QDA | ✅ |
| 5.13 | [`13_multiclass_multilabel.ipynb`](13_multiclass_multilabel.ipynb) | 多类与多标签 / Multi-class & Multi-label | ✅ |
| 5.14 | [`14_imbalanced_classification.ipynb`](14_imbalanced_classification.ipynb) | 不平衡分类 / Imbalanced | ✅ |
| 5.15 | [`15_online_learning.ipynb`](15_online_learning.ipynb) | 在线学习 + 校准收官 / Online Learning + Calibration | ✅ |

## 数据集 / Datasets

| 数据集 | 来源 | 用在 |
|---|---|---|
| Breast Cancer Wisconsin | `sklearn.datasets.load_breast_cancer` | 5.1, 5.15 |
| Iris | `sklearn.datasets.load_iris` | 5.2, 5.3 |
| SMS Spam (mini) | inline | 5.4 |
| Digits (MNIST-like) | `sklearn.datasets.load_digits` | 5.5 |
| Titanic | `seaborn.load_dataset("titanic")` | 5.6, 5.7 |
| Adult Income (synthetic) | inline `numpy.default_rng` | 5.8-5.11 |
| Wine | `sklearn.datasets.load_wine` | 5.12 |
| 20 Newsgroups (subset) | `sklearn.datasets.fetch_20newsgroups` | 5.13 |
| Credit Card Fraud (synthetic) | inline | 5.14 |

## 工具栈 / Tools

`scikit-learn` + `xgboost` + `lightgbm` + `catboost` + `imbalanced-learn` + `statsmodels`。
每个模型**先推数学/讲直觉, 再从零实现(可行时), 再对照库**, 标注 💡 面试要点。
