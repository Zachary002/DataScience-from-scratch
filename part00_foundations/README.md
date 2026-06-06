# Part 0 · Foundations 基础准备

> Python 语言本身 + NumPy / pandas / 可视化 + 必要的数学。所有后续章节的地基。
> The Python language itself + NumPy / pandas / viz + essential math. Foundation for everything else.

## 内容清单 / Contents

| # | Notebook | 主题 / Topic | 状态 / Status |
|---|---|---|---|
| 0.1 | [`01_python_for_data_science.ipynb`](01_python_for_data_science.ipynb) | Python for Data Science 数据科学中的 Python | ✅ Done |
| 0.2 | [`02_numpy_deep_dive.ipynb`](02_numpy_deep_dive.ipynb) | NumPy 全面解析 / NumPy Deep Dive | ✅ Done |
| 0.3 | [`03_pandas_deep_dive.ipynb`](03_pandas_deep_dive.ipynb) | Pandas 全面解析 / Pandas Deep Dive | ✅ Done |
| 0.4 | `04_polars_intro.ipynb` | Polars 入门 / Polars Intro | ⏳ TODO |
| 0.5 | `05_matplotlib_seaborn.ipynb` | Matplotlib & Seaborn | ⏳ TODO |
| 0.6 | `06_plotly_interactive.ipynb` | Plotly & 交互可视化 / Interactive Viz | ⏳ TODO |
| 0.7 | `07_linear_algebra.ipynb` | 线性代数 / Linear Algebra | ⏳ TODO |
| 0.8 | `08_calculus.ipynb` | 微积分 / Calculus | ⏳ TODO |
| 0.9 | `09_probability.ipynb` | 概率论 / Probability | ⏳ TODO |
| 0.10 | `10_numerical_optimization.ipynb` | 数值优化 / Numerical Optimization | ⏳ TODO |
| 0.11 | `11_information_theory.ipynb` | 信息论 / Information Theory | ⏳ TODO |
| 0.12 | `12_engineering_basics.ipynb` | 工程化 / Git, venv, Jupyter, VSCode | ⏳ TODO |

## 数据集 / Datasets used in this part

| 数据集 / Dataset | 来源 / Source | 用在 / Used in |
|---|---|---|
| Iris | `sklearn.datasets.load_iris` | 0.1 |
| California Housing | `sklearn.datasets.fetch_california_housing` | 0.2 |
| Titanic | `seaborn.load_dataset("titanic")` | 0.3 |
| (later additions...) | | |

## 怎么运行 / How to Run

仓库根目录已经有 `requirements.txt`。建议用虚拟环境：
Use the root `requirements.txt` in a virtualenv:

```bash
cd ..                                # back to repo root
python3 -m venv .venv
source .venv/bin/activate            # macOS / Linux
.venv\Scripts\activate               # Windows
pip install -r requirements.txt
jupyter lab                          # 或 jupyter notebook
```

打开本目录下任一 `.ipynb` 即可运行。
Open any `.ipynb` in this folder to start.
