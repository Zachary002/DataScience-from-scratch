# Part 19 · 因果推断与实验 / Causal Inference & Experimentation

> 数据科学最值钱的问题往往是**因果**的:"改了 X 真的会让 Y 变吗?"——而不只是"X 和 Y 相关"。**相关≠因果**是这一部分的灵魂。回答因果问题的黄金标准是**随机实验(A/B 测试)**;当无法随机化时,一整套**准实验/观测因果方法**(倾向匹配、双重差分、工具变量、回归断点)退而求其次地逼近随机实验;再进一步,**异质效应(因果森林/提升建模)** 回答"对谁有效",**网络实验**处理社交溢出。这是数据科学从"预测"跨向"决策"的关键一部分,也是产品/增长/策略岗面试的核心。
> Data science's most valuable questions are often **causal**: "will changing X actually change Y?" — not just "are X and Y correlated." **Correlation ≠ causation** is the soul of this part. The gold standard for causal questions is the **randomized experiment (A/B test)**; when randomization is impossible, a whole toolkit of **quasi-experimental / observational methods** (propensity matching, difference-in-differences, instrumental variables, regression discontinuity) approximates it as a second best; further, **heterogeneous effects (causal forests / uplift modeling)** answer "for whom," and **network experiments** handle social spillover. This is the crucial leap from "prediction" to "decision," and a core topic in product/growth/strategy interviews.

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results**.

## 工具与数据 / Tools & Data
- **库**:`numpy/scipy/pandas`、`statsmodels`(回归/2SLS)、`scikit-learn`(元学习器基模型)、`networkx`(网络实验)、`matplotlib`。
  **Libraries:** `numpy/scipy/pandas`, `statsmodels` (regression/2SLS), `scikit-learn` (meta-learner base models), `networkx` (network experiments), `matplotlib`.
- **全部从零实现**:`dowhy`/`econml`/`linearmodels` 本机未装 → 手写功效分析、CUPED、倾向匹配/IPW、DiD、2SLS、RDD 局部回归、因果森林、S/T/X-learner、聚类随机化。**合成数据**是主力(因为我们【知道】真实因果效应, 能验证每种方法能否还原它); 另用经典真实数据 **LaLonde**(倾向匹配)与 **Card-Krueger**(双重差分)。
  **All from scratch**: `dowhy`/`econml`/`linearmodels` not installed → hand-coded power analysis, CUPED, propensity matching/IPW, DiD, 2SLS, RDD local regression, causal forest, S/T/X-learners, cluster randomization. **Synthetic data** dominates (we KNOW the true causal effect, so we can verify each method recovers it); plus the classic real datasets **LaLonde** (propensity matching) and **Card-Krueger** (DiD).

## 目录 / Contents
| # | 主题 / Topic | 数据 / Data | 关键概念 / Key Concepts |
|---|---|---|---|
| 19.1 | A/B 测试设计 | Synthetic | 随机化消混杂, 功效分析, MDE, 样本量 |
| 19.2 | A/B 测试分析 | Synthetic | t检验, bootstrap CI, **CUPED 减方差** |
| 19.3 | 赌博机 vs A/B | Synthetic | learn vs earn, 何时用哪个 |
| 19.4 | **因果图 & do-演算** | — | 混杂/中介/对撞, 后门准则, 控制越多≠越准 |
| 19.5 | 倾向得分匹配 | LaLonde | e(x), 匹配/IPW, 无未观测混杂假设 |
| 19.6 | 双重差分 DiD | Card-Krueger | 平行趋势, 消时间趋势+群体差异 |
| 19.7 | 工具变量 2SLS | Synthetic | 未观测混杂, 排他性, 弱工具, LATE |
| 19.8 | 回归断点 RDD | Synthetic | 阈值分配, 局部随机, McCrary 检验 |
| 19.9 | **因果森林** | Synthetic | CATE 异质效应, 诚实分裂, 精准投放 |
| 19.10 | 提升建模 Uplift | Synthetic | 四类人(睡狗!), S/T/X-learner, Qini |
| 19.11 | 网络效应实验 | Social graph | SUTVA 违反, 溢出, 聚类随机化 |

## 学习路径 / Path
19.1→19.2→19.3 是**实验(随机化)主线**——能随机就用 A/B, 会设计会分析。19.4 因果图是**观测因果的思维地基**(哪些变量该控制)。19.5→19.6→19.7→19.8 是**四大准实验方法**:倾向匹配(测得到混杂)、DiD(时间维度)、IV(未观测混杂)、RDD(阈值分配)——**不能随机化时逼近实验的四条路**。19.9→19.10 从"平均效应"走向"**异质效应/对谁有效**"(因果森林、提升建模),是精准运营的核心。19.11 处理**网络溢出**这个社交平台的头号实验陷阱。
19.1→19.2→19.3 are the **experimentation (randomization) spine** — use A/B when you can; design and analyze it. 19.4 (causal DAGs) is the **conceptual foundation of observational causal inference** (what to control). 19.5→19.6→19.7→19.8 are the **four quasi-experimental methods**: propensity matching (measured confounders), DiD (time dimension), IV (unobserved confounding), RDD (threshold assignment) — **four routes to approximate an experiment when you can't randomize**. 19.9→19.10 move from "average effect" to "**heterogeneous effect / for whom**" (causal forest, uplift), the core of precision operations. 19.11 handles **network spillover**, the #1 experimentation trap on social platforms.

## 贯穿全部的诚实主线 / Honest threads throughout
- **相关≠因果, 随机化是解药**:非随机估计把 +3% 的真效应估成 +13%, 随机 A/B 还原真值(19.1)。
  **Correlation ≠ causation; randomization is the cure**: a non-random estimate turns a +3% effect into +13%, while a randomized A/B recovers the truth (19.1).
- **控制变量越多越准是错的**:同一个"控制某变量"的动作, 在混杂/中介/对撞三种结构里分别是必须/不该/绝不能——对撞偏差能凭空造出 −0.9 的相关(19.4)。
  **"More controls = more accurate" is wrong**: the same "control a variable" action is mandatory/wrong/forbidden across confounder/mediator/collider — collider bias conjures a −0.9 correlation from nothing (19.4).
- **观测法能救回观测数据**:LaLonde 上朴素估计 −$8498(符号都反), 倾向匹配纠回实验真值 +$1794(19.5)。
  **Observational methods can rescue observational data**: on LaLonde the naive estimate is −$8498 (wrong sign), propensity matching corrects it to the experimental truth +$1794 (19.5).
- **每种方法都有致命且不可检验的假设**:PSM 假设无未观测混杂、DiD 假设平行趋势、IV 假设排他性、RDD 假设无操纵——都无法从数据验证(19.5–19.8)。
  **Every method has a fatal, untestable assumption**: PSM assumes no unobserved confounding, DiD parallel trends, IV exclusion, RDD no manipulation — none verifiable from data (19.5–19.8).
- **平均数掩盖异质性**:ATE +3 掩盖了真实效应 0~6 的巨大差异; 因果森林估 CATE(corr 0.99), 精准投放比随机多 71% 收益(19.9)。
  **Averages hide heterogeneity**: an ATE of +3 hides true effects ranging 0–6; a causal forest estimates CATE (corr 0.99), and targeting beats random by +71% (19.9).
- **uplift≠响应**:营销要找"因发券才买"的可劝说者、避开"发券反而烦"的睡狗——平均 uplift≈0 掩盖了这两群相反的人(19.10)。
  **Uplift ≠ response**: marketing must find Persuadables (buy because of the coupon) and avoid Sleeping Dogs (annoyed by it) — an average uplift ≈0 hides these two opposite groups (19.10).
- **社交溢出让黄金标准 A/B 也骗人**:个体级 A/B 把 3.0 的总效应估成 1.0(对照吃溢出), 聚类随机化才还原(19.11)。
  **Social spillover fools even gold-standard A/B**: individual-level A/B estimates a 3.0 total effect as 1.0 (control absorbs spillover); cluster randomization recovers it (19.11).
