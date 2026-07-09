# Part 18 · 贝叶斯方法 / Bayesian Methods

> 前面所有机器学习给的都是**点估计**——一组"最好的"参数。贝叶斯方法根本不同:它求参数的**整个概率分布**,于是每个预测都自带**不确定性**——模型会诚实地说"这里我没见过数据、我不确定"。这是**可信、可解释、数据高效**机器学习的基石(风控、医疗、自动驾驶、科学实验、AutoML 都离不开它)。本部分从共轭闭式一路**从零实现**到高斯过程与贝叶斯优化。
> All prior ML gives a **point estimate** — one "best" set of parameters. Bayesian methods are fundamentally different: they seek the **entire probability distribution** over parameters, so every prediction carries **uncertainty** — the model honestly says "I haven't seen data here, I'm unsure." This is the foundation of **trustworthy, interpretable, data-efficient** ML (risk, medicine, self-driving, scientific experiments, AutoML all rely on it). This part goes from conjugate closed forms to Gaussian processes and Bayesian optimization, **all implemented from scratch**.

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results**.

## 工具与数据 / Tools & Data
- **库**:`numpy/scipy`(分布、线性代数、优化)、`matplotlib`、`scikit-learn`(对照)。
  **Libraries:** `numpy/scipy` (distributions, linear algebra, optimization), `matplotlib`, `scikit-learn` (comparisons).
- **全部从零实现**:`pymc`/`stan`/`emcee`/`arviz` 本机未装 → 我们**手写所有推断**——共轭后验、Laplace 近似、Metropolis-Hastings/Gibbs、变分推断(CAVI)、层次模型 MCMC、高斯过程、贝叶斯优化。这把"后验到底怎么算/近似"讲得最透。
  **All from scratch**: `pymc`/`stan`/`emcee`/`arviz` not installed → we **hand-code all inference** — conjugate posteriors, Laplace approximation, Metropolis-Hastings/Gibbs, variational inference (CAVI), hierarchical-model MCMC, Gaussian processes, Bayesian optimization. This makes "how the posterior is actually computed/approximated" crystal clear.
- **数据**:多为**合成数据**(以便对比估计与真值), 加经典教学案例(Beta-Binomial 抛硬币、层次打击率、1D 高斯过程回归)。
  **Data:** mostly **synthetic** (to compare estimates against ground truth), plus classic teaching cases (Beta-Binomial coin flips, hierarchical batting averages, 1D GP regression).

## 目录 / Contents
| # | 主题 / Topic | 关键概念 / Key Concepts |
|---|---|---|
| 18.1 | 贝叶斯线性回归 | 共轭先验, 闭式后验, 预测不确定性, 岭回归=MAP |
| 18.2 | 贝叶斯逻辑回归 | Laplace 近似(MAP+Hessian), probit 预测, 缓解过度自信 |
| 18.3 | **MCMC** | Metropolis-Hastings, Gibbs, 证据约掉, 步长/诊断 |
| 18.4 | 变分推断 / VI | ELBO, 平均场, KL(q‖p), 低估方差+mode-seeking |
| 18.5 | 概率编程 / 层次模型 | 部分合并/收缩, PyMC 声明式建模, 经验贝叶斯 |
| 18.6 | **高斯过程 / GP** | 核, 函数上的分布, 闭式后验, 边际似然选超参 |
| 18.7 | **贝叶斯优化 / BO** | GP 代理, 采集函数(EI/UCB), 探索vs利用, AutoML |

## 学习路径 / Path
18.1→18.2 是**从共轭到近似的过渡**(闭式高斯后验 → 无共轭时用 Laplace 近似)。18.3→18.4 是**两大通用近似推断**主线:MCMC(采样, 渐近精确但慢)vs 变分(优化, 快但有偏)——这是贝叶斯计算的核心权衡。
18.1→18.2 is the **conjugate-to-approximate transition** (closed-form Gaussian posterior → Laplace when non-conjugate). 18.3→18.4 are the **two general approximate-inference** spines: MCMC (sampling, asymptotically exact but slow) vs VI (optimization, fast but biased) — the core trade-off of Bayesian computation.
18.5 层次模型/概率编程展示贝叶斯最实用的形态(收缩)。18.6→18.7 是**非参数贝叶斯**主线:高斯过程(函数上的分布)→ 贝叶斯优化(用 GP 做昂贵黑箱优化), 收束到 AutoML/实验设计。
18.5 (hierarchical models / PPL) shows Bayes' most practical form (shrinkage). 18.6→18.7 are the **non-parametric Bayes** spine: Gaussian processes (distributions over functions) → Bayesian optimization (using a GP for expensive black-box optimization), landing on AutoML/experiment design.

## 贯穿全部的诚实主线 / Honest threads throughout
- **岭回归其实是"偷偷的贝叶斯"**:贝叶斯线性回归的后验均值精确等于岭回归解(λ=α/β)(18.1)。
  **Ridge is "secretly Bayesian"**: the Bayesian posterior mean exactly equals the ridge solution (λ=α/β) (18.1).
- **贝叶斯量化"知道自己不知道"**:预测不确定性在数据外自动张开(18.1/18.2/18.6)。
  **Bayes quantifies "knowing what you don't know"**: predictive uncertainty auto-widens outside data (18.1/18.2/18.6).
- **MCMC 的魔法=证据约掉**:MH 接受率只用后验比值, 绕开最难算的归一化常数, 从而能还原真后验(18.3)。
  **MCMC's magic = the evidence cancels**: MH's acceptance uses only the posterior ratio, bypassing the intractable normalizer to recover the true posterior (18.3).
- **VI 的两大天生偏差**:平均场低估方差 72%(过度自信)、反向KL mode-seeking(多峰塌到单峰)——快但有偏(18.4)。
  **VI's two inherent biases**: mean-field underestimates variance by 72% (overconfident), reverse-KL is mode-seeking — fast but biased (18.4).
- **收缩两头都赢**:层次模型的部分合并(RMSE 0.020)同时打败不合并(0.079)与完全合并(0.048)——Stein 悖论的实践(18.5)。
  **Shrinkage wins both ways**: hierarchical partial pooling (RMSE 0.020) beats both no-pooling (0.079) and complete-pooling (0.048) — Stein's paradox in practice (18.5).
- **BO 少评估找最优**:GP 代理 + 采集函数用 15 次评估精确命中最优, 随机搜索差一个数量级(18.7)。
  **BO finds the optimum in few evaluations**: GP surrogate + acquisition hits the optimum in 15 evals, an order of magnitude better than random search (18.7).
