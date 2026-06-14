# Part 4 · 监督学习：回归 / Supervised Learning — Regression

> Part 0-3 把工具、统计、数据预处理全部备齐；从这一部分起**正式建模**。回归 = 预测连续值。我们从线性回归的数学推导一路走到 XGBoost、分位数/稳健/等张回归。
> Now we model. Regression predicts continuous targets — from the OLS derivation all the way to XGBoost and quantile/robust/isotonic variants.

## 内容清单 / Contents

| # | Notebook | 主题 / Topic | 状态 |
|---|---|---|---|
| 4.1 | [`01_linear_regression.ipynb`](01_linear_regression.ipynb) | 线性回归 / Linear Regression | ✅ |
| 4.2 | [`02_regression_diagnostics.ipynb`](02_regression_diagnostics.ipynb) | 回归诊断 / Diagnostics | ✅ |
| 4.3 | [`03_polynomial_regression.ipynb`](03_polynomial_regression.ipynb) | 多项式回归 / Polynomial | ✅ |
| 4.4 | [`04_ridge.ipynb`](04_ridge.ipynb) | 岭回归 / Ridge (L2) | ✅ |
| 4.5 | [`05_lasso.ipynb`](05_lasso.ipynb) | Lasso (L1) | ✅ |
| 4.6 | [`06_elastic_net.ipynb`](06_elastic_net.ipynb) | 弹性网 / Elastic Net | ✅ |
| 4.7 | [`07_glm.ipynb`](07_glm.ipynb) | 广义线性模型 / GLM | ✅ |
| 4.8 | [`08_nonlinear_regression.ipynb`](08_nonlinear_regression.ipynb) | 非线性回归 / Nonlinear | ✅ |
| 4.9 | [`09_svr.ipynb`](09_svr.ipynb) | 支持向量回归 / SVR | ✅ |
| 4.10 | [`10_knn_regression.ipynb`](10_knn_regression.ipynb) | KNN 回归 / KNN | ✅ |
| 4.11 | [`11_decision_tree_regressor.ipynb`](11_decision_tree_regressor.ipynb) | 决策树回归 / Decision Tree | ✅ |
| 4.12 | [`12_random_forest_regressor.ipynb`](12_random_forest_regressor.ipynb) | 随机森林回归 / Random Forest | ✅ |
| 4.13 | [`13_gradient_boosting_regressor.ipynb`](13_gradient_boosting_regressor.ipynb) | 梯度提升 / GBDT + XGBoost | ✅ |
| 4.14 | [`14_quantile_regression.ipynb`](14_quantile_regression.ipynb) | 分位数回归 / Quantile | ✅ |
| 4.15 | [`15_robust_regression.ipynb`](15_robust_regression.ipynb) | 稳健回归 / Robust | ✅ |
| 4.16 | [`16_isotonic_regression.ipynb`](16_isotonic_regression.ipynb) | 等张回归 / Isotonic | ✅ |

## 数据集 / Datasets

| 数据集 | 来源 | 用在 |
|---|---|---|
| California Housing | `sklearn.datasets.fetch_california_housing` | 4.1, 4.2, 4.4, 4.5, 4.6 |
| Diamonds | `seaborn.load_dataset("diamonds")` | 4.10, 4.11, 4.12, 4.13 |
| Synthetic | inline `numpy.default_rng` | 4.3, 4.7, 4.8, 4.9, 4.14, 4.15, 4.16 |

## 工具栈 / Tools

`numpy` + `scikit-learn` + `statsmodels`(GLM/诊断) + `scipy.optimize`(非线性) + `xgboost`(GBDT)。
每个模型都**先推数学/讲直觉, 再从零实现(可行时), 再对照 sklearn**, 并标注 💡 面试要点。
