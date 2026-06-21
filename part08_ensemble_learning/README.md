# Part 8 · 集成学习 / Ensemble Learning

> "三个臭皮匠顶个诸葛亮"——把多个模型**组合**起来，往往比任何单个模型都强。这是表格数据竞赛和工业实战的**制胜法宝**。本部分系统讲两大范式(bagging 降方差、boosting 降偏差)的原理与从零实现，三大 boosting 库的对比，以及把不同模型组合的 voting/stacking。
> "Many weak learners make a strong one" — **combining** models often beats any single one. The winning recipe in tabular competitions and industry. This part covers the two paradigms (bagging for variance, boosting for bias) with from-scratch derivations, the three boosting libraries compared, and voting/stacking to combine heterogeneous models.
>
> 注：随机森林(5.7)、GBDT(5.8)、XGBoost/LightGBM/CatBoost(5.9-5.11)在 Part 5 已用过；本部分从**集成原理**角度深入并补全 AdaBoost、GBDT 数学推导、Stacking 等新内容。
> Note: RF (5.7), GBDT (5.8), the boosting trio (5.9-5.11) appeared in Part 5; this part goes deeper from the **ensemble-theory** angle and adds AdaBoost, the GBDT derivation, and Stacking.

## 内容清单 / Contents

| # | Notebook | 主题 / Topic | 状态 |
|---|---|---|---|
| 8.1 | [`01_bagging.ipynb`](01_bagging.ipynb) | Bagging | ✅ |
| 8.2 | [`02_random_forest_deep.ipynb`](02_random_forest_deep.ipynb) | 随机森林深入 / RF Deep Dive | ✅ |
| 8.3 | [`03_adaboost.ipynb`](03_adaboost.ipynb) | AdaBoost | ✅ |
| 8.4 | [`04_gradient_boosting_derivation.ipynb`](04_gradient_boosting_derivation.ipynb) | 梯度提升推导 / GB Derivation | ✅ |
| 8.5 | [`05_boosting_libraries.ipynb`](05_boosting_libraries.ipynb) | XGBoost/LightGBM/CatBoost 对比 | ✅ |
| 8.6 | [`06_voting_averaging.ipynb`](06_voting_averaging.ipynb) | Voting & Averaging | ✅ |
| 8.7 | [`07_stacking_blending.ipynb`](07_stacking_blending.ipynb) | Stacking & Blending | ✅ |

## 数据集 / Datasets

| 数据集 | 来源 | 用在 |
|---|---|---|
| Titanic | `seaborn.load_dataset("titanic")` | 8.1, 8.2, 8.3 |
| Synthetic | inline `numpy.default_rng` | 8.4 |
| Adult Income (synthetic) | inline | 8.5 |
| Wine | `sklearn.datasets.load_wine` | 8.6 |
| California Housing (House-Prices 替身) | `sklearn.datasets.fetch_california_housing` | 8.7 |

## 工具栈 / Tools

`scikit-learn` + `xgboost` + `lightgbm` + `catboost`。
每个方法**先讲原理/数学, 再从零实现(可行时), 再对照库**, 标注 💡 面试要点与 💼 实战视角。
