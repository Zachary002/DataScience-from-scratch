# Part 7 · 模型评估与优化 / Model Evaluation & Tuning

> 模型建好之后，怎么**正确评估**、**调到最好**、**讲清楚为什么这样预测**、并保证它**公平、稳健、不随时间失效**？这一部分把散落在前几章的评估/调参知识系统化，并加入工业界与面试越来越看重的可解释性、校准、公平性、鲁棒性、概念漂移。
> Once a model is built: how do you **evaluate it correctly**, **tune it to its best**, **explain its predictions**, and ensure it's **fair, robust, and doesn't decay over time**? This part consolidates evaluation/tuning and adds interpretability, calibration, fairness, robustness, and drift — increasingly valued in industry and interviews.

## 内容清单 / Contents

| # | Notebook | 主题 / Topic | 状态 |
|---|---|---|---|
| 7.1 | [`01_regression_metrics.ipynb`](01_regression_metrics.ipynb) | 回归评估指标 / Regression Metrics | ✅ |
| 7.2 | [`02_classification_metrics.ipynb`](02_classification_metrics.ipynb) | 分类评估指标 / Classification Metrics | ✅ |
| 7.3 | [`03_bias_variance.ipynb`](03_bias_variance.ipynb) | 偏差-方差权衡 / Bias-Variance | ✅ |
| 7.4 | [`04_cross_validation.ipynb`](04_cross_validation.ipynb) | 交叉验证策略 / CV Strategies | ✅ |
| 7.5 | [`05_hyperparameter_tuning.ipynb`](05_hyperparameter_tuning.ipynb) | 网格/随机/贝叶斯调参 / Tuning | ✅ |
| 7.6 | [`06_multiobjective.ipynb`](06_multiobjective.ipynb) | 多目标与帕累托 / Multi-objective | ✅ |
| 7.7 | [`07_feature_selection.ipynb`](07_feature_selection.ipynb) | 特征选择 / Feature Selection | ✅ |
| 7.8 | [`08_interpretability.ipynb`](08_interpretability.ipynb) | 模型解释 / Interpretability (SHAP/LIME) | ✅ |
| 7.9 | [`09_calibration.ipynb`](09_calibration.ipynb) | 概率校准 / Calibration | ✅ |
| 7.10 | [`10_fairness.ipynb`](10_fairness.ipynb) | 公平性 / Fairness | ✅ |
| 7.11 | [`11_robustness.ipynb`](11_robustness.ipynb) | 鲁棒性与对抗样本 / Robustness | ✅ |
| 7.12 | [`12_concept_drift.ipynb`](12_concept_drift.ipynb) | 概念漂移 / Concept Drift | ✅ |

## 数据集 / Datasets

| 数据集 | 来源 | 用在 |
|---|---|---|
| California Housing | `sklearn.datasets.fetch_california_housing` | 7.1, 7.3 |
| Breast Cancer | `sklearn.datasets.load_breast_cancer` | 7.2 |
| Iris / Wine | `sklearn.datasets` | 7.4, 7.5 |
| Madelon 风格 (synthetic) | `make_classification` | 7.7 |
| Adult Income (synthetic) | inline `numpy.default_rng` | 7.8 |
| 信用违约 (synthetic) | inline | 7.9 |
| COMPAS 风格累犯 (synthetic) | inline | 7.10 |
| Digits | `sklearn.datasets.load_digits` | 7.11 |
| 流式数据 (synthetic) | inline | 7.6, 7.12 |

## 工具栈 / Tools

`scikit-learn` + `optuna`(贝叶斯调参) + `shap` / `lime`(可解释性) + `torch`(对抗样本)。
每个主题**先讲直觉/数学, 再代码演示**, 标注 💡 面试要点与 💼 实战视角。
