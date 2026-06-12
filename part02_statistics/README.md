# Part 2 · 统计学与概率 / Statistics & Probability

> **DS 面试第二关**。0.9 节打了概率地基；这一部分把"推断统计"完整走一遍——从描述统计到假设检验、贝叶斯、Bootstrap、蒙特卡洛。**A/B 测试（Part 19）的全部统计学根基都在这里**。
> Interview round two. Part 0.9 laid the probability foundation; this part covers inferential statistics end-to-end — the statistical bedrock of A/B testing (Part 19).

## 内容清单 / Contents

| # | Notebook | 主题 / Topic | 状态 / Status |
|---|---|---|---|
| 2.1 | [`01_descriptive_stats.ipynb`](01_descriptive_stats.ipynb) | 描述统计 / Descriptive Stats | ✅ Done |
| 2.2 | [`02_distributions_in_practice.ipynb`](02_distributions_in_practice.ipynb) | 分布实战：拟合与选择 / Distributions in Practice | ✅ Done |
| 2.3 | [`03_lln_clt.ipynb`](03_lln_clt.ipynb) | 大数定律 & 中心极限定理 / LLN & CLT | ✅ Done |
| 2.4 | [`04_sampling.ipynb`](04_sampling.ipynb) | 抽样方法 / Sampling Methods | ✅ Done |
| 2.5 | [`05_confidence_intervals.ipynb`](05_confidence_intervals.ipynb) | 置信区间 / Confidence Intervals | ✅ Done |
| 2.6 | [`06_hypothesis_testing.ipynb`](06_hypothesis_testing.ipynb) | 假设检验 / Hypothesis Testing | ✅ Done |
| 2.7 | [`07_multiple_testing.ipynb`](07_multiple_testing.ipynb) | 多重比较 / Multiple Testing | ✅ Done |
| 2.8 | [`08_power_sample_size.ipynb`](08_power_sample_size.ipynb) | 功效与样本量 / Power & Sample Size | ✅ Done |
| 2.9 | [`09_mle.ipynb`](09_mle.ipynb) | 最大似然估计 / MLE | ✅ Done |
| 2.10 | [`10_bayesian_estimation.ipynb`](10_bayesian_estimation.ipynb) | 贝叶斯估计 / Bayesian Estimation | ✅ Done |
| 2.11 | [`11_bootstrap_jackknife.ipynb`](11_bootstrap_jackknife.ipynb) | Bootstrap & Jackknife | ✅ Done |
| 2.12 | [`12_monte_carlo.ipynb`](12_monte_carlo.ipynb) | 蒙特卡洛方法 / Monte Carlo | ✅ Done |

## 数据集 / Datasets

| 数据集 / Dataset | 来源 / Source | 用在 / Used in |
|---|---|---|
| Tips | `seaborn.load_dataset("tips")` | 2.1, 2.6 |
| Synthetic（模拟为主）| `numpy.default_rng` | 其余各节 |

## 工具栈 / Tools

`numpy` + `scipy.stats` + `statsmodels` + `matplotlib/seaborn`。所有重要量都**先手写公式实现，再和库函数对照**。
Everything important is implemented from formulas first, then cross-checked against library functions.
