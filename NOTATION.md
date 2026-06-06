# 数学符号约定 / Mathematical Notation Convention

> 本仓库**所有 notebook** 一律遵循下面的符号约定。如果某一节出于教学原因不得不偏离（例如对照某本教材的特殊记号），文件**开头会显式说明**。
> Every notebook in this repo follows the conventions below. When a notebook must deviate (e.g. matching a specific textbook), it will say so **explicitly at the top**.

---

## 1. 标量、向量、矩阵 / Scalars, Vectors, Matrices

| 对象 / Object | 本仓库写法 / Our notation | 例子 / Example | 不用 / Avoid |
|---|---|---|---|
| 标量 / Scalar | 普通小写斜体 / italic lowercase | $x,\; n,\; \eta$ | — |
| 向量 / Vector | **粗体小写** / **bold** lowercase，**默认列向量** / column by default | $\mathbf{x} \in \mathbb{R}^d$ | $\vec{x}$, $\underline{x}$ |
| 矩阵 / Matrix | **粗体大写** / **bold** uppercase | $\mathbf{X} \in \mathbb{R}^{n \times d}$ | $\mathbb{X}$, $\boldsymbol{X}$ |
| 张量 / Tensor (≥3维) | 花体大写 / calligraphic | $\mathcal{X}$ | — |
| 转置 / Transpose | 上标 $\top$ | $\mathbf{X}^\top$ | $X^T,\; X'$ |
| 逆 / Inverse | 上标 $-1$ | $\mathbf{X}^{-1}$ | — |
| 伪逆 / Pseudo-inverse | 上标 $\dagger$ | $\mathbf{X}^\dagger$ | $X^+$ |
| 实数集 / Reals | 黑板体 / blackboard | $\mathbb{R},\; \mathbb{R}^d$ | $\mathbf{R}$ |

---

## 2. 数据集相关 / Dataset Notation

| 量 / Quantity | 符号 / Symbol | 含义 / Meaning |
|---|---|---|
| 样本数 / number of samples | $n$ | 训练集行数。**不用** $N$、不用 $m$。 |
| 特征数 / number of features | $d$ | 特征维度。**不用** $p$、不用 $n$。 |
| 类别数 / number of classes | $K$ | 分类任务的标签数 |
| 训练集 / training set | $\mathcal{D} = \{(\mathbf{x}_i, y_i)\}_{i=1}^{n}$ | 大小为 $n$ 的 i.i.d. 样本 |
| 设计矩阵 / design matrix | $\mathbf{X} \in \mathbb{R}^{n \times d}$ | 行是样本，列是特征 |
| 标签向量 / label vector | $\mathbf{y} \in \mathbb{R}^n$ 或 $\{0,1,\dots,K-1\}^n$ | |
| 第 $i$ 个样本 / i-th sample | $\mathbf{x}_i \in \mathbb{R}^d$ | $\mathbf{X}$ 的第 $i$ 行 |
| 第 $j$ 个特征 / j-th feature | $\mathbf{x}_{:,j}$ | $\mathbf{X}$ 的第 $j$ 列 |
| 标量元素 / scalar element | $X_{ij} = (\mathbf{x}_i)_j$ | $\mathbf{X}$ 的第 $i$ 行第 $j$ 列 |

> ⚠ **常见冲突 / Common clash**
> Andrew Ng 用 $x^{(i)}$ 表示第 $i$ 个样本（上标加括号），$m$ 表示样本数。
> **本仓库**统一用 $\mathbf{x}_i$ 和 $n$。
> Andrew Ng uses $x^{(i)}$ for the $i$-th sample and $m$ for sample count; we standardize on $\mathbf{x}_i$ and $n$.

---

## 3. 模型与参数 / Models & Parameters

| 量 / Quantity | 符号 / Symbol | 含义 / Meaning |
|---|---|---|
| 模型参数 / parameters | $\boldsymbol{\theta}$ 或 $\mathbf{w}$ | $\mathbf{w}$ 专指线性模型的权重 / weight vector |
| 偏置 / bias / intercept | $b$ | 标量 |
| 真值 / ground truth | $y_i$ | 第 $i$ 个样本的真实标签 |
| 预测值 / prediction | $\hat{y}_i$ | 模型输出，戴 hat |
| 假设函数 / hypothesis | $f_{\boldsymbol{\theta}}(\mathbf{x}),\; h(\mathbf{x})$ | 模型 |
| 真实参数 / true parameter | $\boldsymbol{\theta}^\star$ | 数据生成过程中的真值 |
| 估计量 / estimator | $\hat{\boldsymbol{\theta}}$ | 训练得到的估计 |
| 残差 / residual | $r_i = y_i - \hat{y}_i$ | |

---

## 4. 概率与统计 / Probability & Statistics

| 量 / Quantity | 符号 / Symbol | 含义 / Meaning |
|---|---|---|
| 概率 / probability | $\Pr(A)$ | **不用** $P(A)$（避免和后面的预测函数 $P$ 混淆） |
| 概率密度 / density | $p(x),\; p_X(x)$ | 小写 $p$ |
| 期望 / expectation | $\mathbb{E}[X],\; \mathbb{E}_{p}[f(X)]$ | 黑板体 $\mathbb{E}$ |
| 方差 / variance | $\mathrm{Var}(X)$ | |
| 协方差 / covariance | $\mathrm{Cov}(X, Y)$ | |
| 协方差矩阵 / cov matrix | $\boldsymbol{\Sigma}$ | $d \times d$ |
| 样本均值 / sample mean | $\bar{x}$ | |
| 样本方差 / sample variance | $s^2$ | 无偏估计用 $n-1$ |
| 独立同分布 / i.i.d. | $\overset{\text{iid}}{\sim}$ | |
| 服从分布 / distribution | $X \sim \mathcal{N}(\mu, \sigma^2)$ | 分布用花体 $\mathcal{N}, \mathcal{U}$ 等 |
| 似然 / likelihood | $\mathcal{L}(\boldsymbol{\theta}; \mathcal{D})$ | 花体 $\mathcal{L}$ |
| 对数似然 / log-likelihood | $\ell(\boldsymbol{\theta})$ | 普通 $\ell$ |
| 指示函数 / indicator | $\mathbb{1}\{A\}$ | |

> ⚠ **似然 vs 损失的命名冲突 / Likelihood-vs-loss clash**
> 有些教材把损失函数也写成 $\mathcal{L}$，**本仓库**：
> - 似然 → $\mathcal{L}(\boldsymbol{\theta})$
> - 损失（单样本）→ $\ell(\hat{y}, y)$
> - 经验风险 / 目标函数 / cost → $J(\boldsymbol{\theta}) = \frac{1}{n}\sum_i \ell(\hat{y}_i, y_i)$
>
> Some books use $\mathcal{L}$ for loss too. We reserve $\mathcal{L}$ for likelihood, $\ell$ for per-sample loss, and $J$ for the cost.

---

## 5. 损失与优化 / Loss & Optimization

| 量 / Quantity | 符号 / Symbol | 含义 / Meaning |
|---|---|---|
| 单样本损失 / per-sample loss | $\ell(\hat{y}, y)$ | |
| 目标函数 / cost (经验风险) | $J(\boldsymbol{\theta}) = \frac{1}{n}\sum_{i=1}^n \ell(\hat{y}_i, y_i)$ | |
| 正则化项 / regularization | $\Omega(\boldsymbol{\theta})$ 或 $R(\boldsymbol{\theta})$ | |
| 正则化强度 / reg strength | $\lambda \ge 0$ | |
| 学习率 / learning rate | $\eta$ | **不用** $\alpha$（保留给统计显著性水平） |
| 梯度 / gradient | $\nabla_{\boldsymbol{\theta}} J,\; \nabla J$ | 对 $\boldsymbol{\theta}$ 求梯度 |
| 偏导 / partial derivative | $\partial J / \partial \theta_j$ | |
| Hessian | $\mathbf{H} = \nabla^2 J$ | |
| epoch / iteration | $t = 0, 1, 2, \dots$ | 迭代步用上标 $\boldsymbol{\theta}^{(t)}$ |

---

## 6. 范数与距离 / Norms & Distances

| 量 / Quantity | 符号 / Symbol | 含义 / Meaning |
|---|---|---|
| 默认范数 / default norm | $\|\mathbf{x}\|$ | 即 $\ell_2$ 范数 |
| $\ell_p$ 范数 | $\|\mathbf{x}\|_p = \left(\sum_j \lvert x_j \rvert^p\right)^{1/p}$ | $p=1,2,\infty$ |
| Frobenius | $\|\mathbf{X}\|_F$ | 矩阵的"L2" |
| 内积 / inner product | $\langle \mathbf{x}, \mathbf{y} \rangle = \mathbf{x}^\top \mathbf{y}$ | |
| 欧氏距离 / Euclidean dist | $d(\mathbf{x}, \mathbf{y}) = \|\mathbf{x} - \mathbf{y}\|_2$ | |

---

## 7. 神经网络专属 / Neural Network Specific

| 量 / Quantity | 符号 / Symbol | 含义 / Meaning |
|---|---|---|
| 层数 / layer count | $L$ | |
| 第 $\ell$ 层权重 / layer-$\ell$ weights | $\mathbf{W}^{(\ell)}$ | 上标加括号 |
| 第 $\ell$ 层偏置 / layer-$\ell$ bias | $\mathbf{b}^{(\ell)}$ | |
| 第 $\ell$ 层激活前 / pre-activation | $\mathbf{z}^{(\ell)}$ | $\mathbf{z}^{(\ell)} = \mathbf{W}^{(\ell)} \mathbf{a}^{(\ell-1)} + \mathbf{b}^{(\ell)}$ |
| 第 $\ell$ 层激活 / activation | $\mathbf{a}^{(\ell)} = \phi(\mathbf{z}^{(\ell)})$ | $\phi$ 是激活函数 |
| Sigmoid | $\sigma(z) = 1/(1+e^{-z})$ | $\sigma$ 在 NN 章节默认是 sigmoid |

---

## 8. 评估指标专属 / Evaluation Metrics

| 量 / Quantity | 符号 / Symbol |
|---|---|
| 准确率 / accuracy | $\mathrm{Acc}$ |
| 精确率 / precision | $\mathrm{Prec}$ |
| 召回率 / recall | $\mathrm{Rec}$ |
| F1 分数 | $F_1$ |
| ROC 曲线下面积 | $\mathrm{AUC}$ |
| 显著性水平 / significance level | $\alpha$ |
| 检验功效 / power | $1 - \beta$ |
| p 值 / p-value | $p$ |

---

## 9. 常见缩写表 / Acronym Cheat Sheet

| 缩写 / Abbreviation | 全称 / Full |
|---|---|
| MSE | Mean Squared Error 均方误差 |
| RMSE | Root Mean Squared Error 均方根误差 |
| MAE | Mean Absolute Error 平均绝对误差 |
| CE / BCE | (Binary) Cross-Entropy 交叉熵 |
| NLL | Negative Log-Likelihood 负对数似然 |
| MLE | Maximum Likelihood Estimation 极大似然估计 |
| MAP | Maximum A Posteriori 最大后验 |
| ERM | Empirical Risk Minimization 经验风险最小化 |
| SGD | Stochastic Gradient Descent 随机梯度下降 |
| CV | Cross-Validation 交叉验证 |
| OOB | Out-Of-Bag 袋外（用于 Random Forest） |
| i.i.d. | independent and identically distributed 独立同分布 |

---

## 10. 速查：和常见教材的对照表 / Cross-Reference with Major Textbooks

| 概念 / Concept | 本仓库 / Ours | Bishop *PRML* | Hastie *ESL* | Andrew Ng *CS229* | Goodfellow *DL* |
|---|---|---|---|---|---|
| 样本数 | $n$ | $N$ | $N$ | $m$ | $m$ |
| 特征数 | $d$ | $D$ | $p$ | $n$ | $n$ |
| 设计矩阵 | $\mathbf{X}$ | $\mathbf{X}$ | $\mathbf{X}$ | $X$ | $\mathbf{X}$ |
| 第 $i$ 样本 | $\mathbf{x}_i$ | $\mathbf{x}_n$ | $x_i$ | $x^{(i)}$ | $\mathbf{x}^{(i)}$ |
| 权重 | $\mathbf{w}$ | $\mathbf{w}$ | $\beta$ | $\theta$ | $\mathbf{w}$ |
| 偏置 | $b$ | $w_0$ | $\beta_0$ | $\theta_0$ | $b$ |
| 学习率 | $\eta$ | $\eta$ | — | $\alpha$ | $\epsilon$ |
| 损失 | $\ell$ / $J$ | $E$ | RSS | $J$ | $L$ / $J$ |

> 如果你以前学过其中一本，看本仓库时**对照这一栏即可**。
> Use this row to translate between this repo and the textbook you already know.

---

**最后**：每个 notebook 顶部都会有"📐 符号约定 / Notation"小框，提醒你本节用到的关键符号；它们都遵循上表。
**Lastly**: every notebook starts with a tiny "📐 Notation" box reminding you of the key symbols used in that lesson — all consistent with this file.
