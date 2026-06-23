# Part 14 · 时间序列 / Time Series

> 数据带着**时间顺序**就不一样了——昨天影响今天, 有趋势、有季节性、不能随便打乱。时间序列预测是销量预测、金融、运维监控、需求规划的核心。本部分从**经典统计方法**(分解、平滑、ARIMA/SARIMA)到**深度学习方法**(LSTM、TCN、Transformer), 再到多变量预测、异常检测、因果检验, 完整覆盖。
> Data with **temporal order** is different — yesterday affects today, with trends, seasonality, and no shuffling allowed. Time-series forecasting is core to sales prediction, finance, monitoring, and demand planning. This part covers from **classical statistics** (decomposition, smoothing, ARIMA/SARIMA) to **deep learning** (LSTM, TCN, Transformer), plus multivariate forecasting, anomaly detection, and causality testing.

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results**.

## 工具与数据 / Tools & Data
- **库**:`statsmodels`(分解/ARIMA/SARIMAX/VAR/Granger/ACF)、`torch`(LSTM/TCN/Transformer)、`pandas/numpy/scipy`、`scikit-learn`。
  **Libraries:** `statsmodels`, `torch`, `pandas/numpy/scipy`, `scikit-learn`.
- **数据**:经典的 **AirPassengers**(1949-1960 月度航空客运量, 趋势+季节性教科书案例, 内嵌于 notebook)、statsmodels 自带的 **macrodata**(宏观经济多变量, 用于 VAR/Granger)等。
  **Data:** the classic **AirPassengers** (monthly airline passengers 1949-1960, the textbook trend+seasonality case, embedded in notebooks); statsmodels' bundled **macrodata** (macro multivariate, for VAR/Granger), etc.
- `pmdarima`(auto_arima)、`prophet`、`sktime` 本机未装 → 相关思想**从零/用 statsmodels 实现**, 并指明这些库的实战用法。
  `pmdarima`/`prophet`/`sktime` not installed → their ideas implemented from scratch/with statsmodels, noting the libraries' practical use.

## 目录 / Contents
| # | 主题 / Topic | 关键概念 / Key Concepts |
|---|---|---|
| 14.1 | 时间序列基础 | 趋势/季节性/平稳性, ACF/PACF, 差分, ADF 检验 |
| 14.2 | 分解 / Decomposition | 加法vs乘法, 经典分解, STL |
| 14.3 | 平滑法 / Smoothing | 移动平均, EWMA, Holt-Winters 指数平滑 |
| 14.4 | **ARIMA / SARIMA / SARIMAX** | AR/I/MA, 季节项, 外生变量, 定阶 |
| 14.5 | Prophet 思想 | 可分解加法模型(趋势+季节+节假日), Fourier 季节 |
| 14.6 | LSTM / GRU 预测 | 滑窗, seq-to-one, 缩放, 防泄漏 |
| 14.7 | 时序 CNN / TCN | 因果卷积, 空洞卷积, 感受野 |
| 14.8 | Transformer 预测 | patch, 注意力, Informer/PatchTST 思想 |
| 14.9 | 多变量 & 多步预测 | VAR, 直接vs递归多步 |
| 14.10 | 时序异常检测 | STL 残差, z-score, ESD |
| 14.11 | 因果性检验 | VAR, Granger 因果检验 |

## 学习路径 / Path
14.1→14.2→14.3→14.4 是经典统计预测主线(理解数据→分解→平滑→ARIMA)。
14.1→14.2→14.3→14.4 are the classical-stats spine (understand → decompose → smooth → ARIMA).
14.5 Prophet 与 14.6-14.8 深度学习是现代方法; 14.9-14.11 是多变量/异常/因果等专题。
14.5 (Prophet) and 14.6-14.8 (deep learning) are modern; 14.9-14.11 cover multivariate/anomaly/causality.

> ⚠️ 时间序列的头号大坑(贯穿全部): **绝不能随机打乱或用未来预测过去**——划分训练/测试必须**按时间顺序**(过去训练、未来测试), 任何"未来信息泄漏"都会让评估虚高。
> ⚠️ The #1 pitfall (throughout): **never shuffle or use the future to predict the past** — train/test splits must be **chronological** (train on past, test on future); any future leakage inflates evaluation.
