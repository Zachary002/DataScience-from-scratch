# Part 22 · MLOps 与部署 / MLOps & Deployment

> 训好一个模型只是 20% 的工作,剩下 80% 是**把它可靠地送上生产并持续运营**。这一部分覆盖模型从"能跑"到"上线、监控、迭代"的全生命周期:持久化、Pipeline、API 部署、容器/编排、CI/CD、实验追踪、特征平台、漂移监控、A/B 基础设施、边缘压缩。贯穿全程的诚实主线是:**代码能跑 ≠ 系统可靠**——真正的工程性在于防泄漏、防训练-服务偏差、防静默退化、限制上线风险。这是数据科学从"会建模"跨到"能落地"的分水岭,也是高级 DS/MLE 面试的核心。
> Training a model is only 20% of the work; the other 80% is **reliably shipping it to production and continuously operating it**. This part covers the model's full lifecycle from "runs" to "deployed, monitored, iterated": persistence, pipelines, API deployment, containers/orchestration, CI/CD, experiment tracking, feature stores, drift monitoring, A/B infrastructure, edge compression. The honest thread throughout: **code running ≠ system reliable** — real engineering is preventing leakage, training-serving skew, silent degradation, and limiting deployment risk. This is the divide from "can model" to "can ship," and the core of senior DS/MLE interviews.

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results**.

## 工具与数据 / Tools & Data
- **真实可跑的库**:`scikit-learn`、`joblib`、`torch`、`scipy`、`numpy`、`pandas`、`matplotlib`。
  **Really-runnable libraries**: `scikit-learn`, `joblib`, `torch`, `scipy`, `numpy`, `pandas`, `matplotlib`.
- **从零复现的基础设施**:`fastapi`/`mlflow`/`streamlit`/`onnx` 本机未装 → 手写 **mini 模型服务**(校验/健康检查)、**Streamlit 反应式引擎**、**Docker 分层缓存**、**K8s 调和循环**、**CI/CD 流水线+质量门**、**mini MLflow 追踪器**、**特征平台 point-in-time join**、**A/B 哈希分桶**。真实的 Dockerfile/K8s YAML/GitHub Actions/FastAPI/MLflow 代码作为参考产物给出。
  **From-scratch infrastructure**: `fastapi`/`mlflow`/`streamlit`/`onnx` not installed → hand-coded **mini model service** (validation/health), **Streamlit reactive engine**, **Docker layer cache**, **K8s reconciliation loop**, **CI/CD pipeline + quality gate**, **mini MLflow tracker**, **feature store point-in-time join**, **A/B hash bucketing**. Real Dockerfile/K8s YAML/GitHub Actions/FastAPI/MLflow code is given as reference artifacts.

## 目录 / Contents
| # | 主题 / Topic | 方式 / Approach | 关键概念 / Key Concepts |
|---|---|---|---|
| 22.1 | 模型持久化 Persistence | 真实 joblib + 演示 | 模型=权重+计算图; pickle RCE 安全; 版本漂移; 训练-服务偏差 |
| 22.2 | Sklearn Pipelines | 真实(泄漏实验) | **纯噪声上泄漏造 0.78 假准确率**; ColumnTransformer; 机制防泄漏 |
| 22.3 | FastAPI 部署 | 从零 mini 服务 | 请求校验(422)、健康检查、模型加载一次、请求生命周期 |
| 22.4 | Streamlit 仪表板 | 从零反应式引擎 | 反应式重跑 + @st.cache; 模型探索器; vs Gradio/Dash |
| 22.5 | Docker 入门 | 从零分层缓存 | 镜像vs容器; **指令顺序=构建速度**; 多阶段; 真实 Dockerfile |
| 22.6 | Kubernetes 入门 | 从零调和循环 | **声明式+调和循环**(自愈+扩缩); Pod/Deployment/Service/HPA; KServe |
| 22.7 | ML 的 CI/CD | 从零流水线+质量门 | **模型质量门拦退化模型**(0.70 被 0.88 阻断); 数据校验; 持续训练 |
| 22.8 | 实验追踪 Tracking | 从零 mini MLflow | 记录 params/metrics/model; 比较 run; **可复现**; 模型注册表 |
| 22.9 | 特征平台 Feature Store | 真实 point-in-time | **朴素 join 泄漏未来值**; as-of join; 在线离线一致; Feast |
| 22.10 | 监控与漂移 Drift | 真实 PSI+KS | 数据漂移(PSI/KS)vs **概念漂移**(输入没变准确率崩); 标签延迟 |
| 22.11 | A/B 基础设施 | 从零哈希分桶 | 确定性分桶(一致/无状态/独立); 影子/金丝雀/蓝绿限爆炸半径 |
| 22.12 | 边缘部署 Edge | 真实 torch 压缩 | **量化 int8 免费 4x**; 剪枝 80%; 蒸馏(诚实:难任务才有效) |

## 学习路径 / Path
22.1→22.2 是**可信建模的地基**(持久化、Pipeline 防泄漏)。22.3→22.4→22.5→22.6 是**部署主线**(FastAPI API → Streamlit UI → Docker 打包 → K8s 编排)。22.7→22.8 是**工程化交付**(CI/CD 质量门 + 实验追踪的可复现)。22.9→22.10→22.11 是**生产运营闭环**(特征平台一致性 → 漂移监控 → A/B 安全上线)。22.12 边缘部署是**把 AI 送上十亿设备**的压缩技术。
22.1→22.2 is the **foundation of trustworthy modeling** (persistence, Pipeline anti-leakage). 22.3→22.4→22.5→22.6 is the **deployment spine** (FastAPI API → Streamlit UI → Docker packaging → K8s orchestration). 22.7→22.8 is **engineered delivery** (CI/CD quality gate + experiment-tracking reproducibility). 22.9→22.10→22.11 is the **production operations loop** (feature-store consistency → drift monitoring → safe A/B rollout). 22.12 edge deployment is the compression to **bring AI to billions of devices**.

## 贯穿全部的诚实主线 / Honest threads throughout
- **代码能跑 ≠ 结果可信**:纯噪声数据上, 一个划分前做特征选择的泄漏, 凭空造出 0.78 假准确率(真实=0.5)——Pipeline 从机制上杜绝它(22.2)。
  **Code running ≠ trustworthy results**: on pure noise, feature-selection leakage before the split manufactures 0.78 fake accuracy (truth = 0.5) — a Pipeline mechanically eliminates it (22.2).
- **训练-服务偏差是隐形杀手**:模型只存权重、线上手写预处理必然偏差; 存整条 Pipeline、在线离线共用同一特征定义才根治(22.1/22.2/22.9)。
  **Training-serving skew is an invisible killer**: saving only weights and hand-writing online preprocessing inevitably skews; save the whole Pipeline and share one feature definition online/offline to cure it (22.1/22.2/22.9).
- **代码能跑 ≠ 模型变好**:CI/CD 的模型质量门拦下一个准确率 0.70 的退化候选(生产基线 0.88), 防止它悄悄上线(22.7)。
  **Code running ≠ model improved**: the CI/CD quality gate blocks a degraded 0.70 candidate (baseline 0.88), preventing it from silently shipping (22.7).
- **特征平台防的是最隐蔽的未来泄漏**:朴素 join 取用户余额最新值(标签之后才发生)造成泄漏, point-in-time join 取标签时刻已知值才正确(22.9)。
  **Feature stores prevent the most insidious future leakage**: a naive join takes the latest balance (occurring after the label) → leakage; a point-in-time join takes the value known at the label's moment (22.9).
- **模型会静默退化**:概念漂移下输入分布 PSI 仅 0.004(看似正常)但准确率从 0.996 崩到 0.512——只监控输入不够, 必须也监控性能(22.10)。
  **Models degrade silently**: under concept drift the input-distribution PSI is just 0.004 (looks fine) but accuracy collapses 0.996→0.512 — monitoring inputs alone is insufficient, monitor performance too (22.10).
- **安全上线靠限制爆炸半径**:新模型 3% 故障率, 全量切换波及全站 3%, 金丝雀 5% 流量只波及 0.13%——渐进发布+秒级回滚(22.11)。
  **Safe deployment limits blast radius**: a new model with 3% failure rate affects 3% of the site on full switch, but only 0.13% with 5% canary traffic — progressive rollout + seconds rollback (22.11).
- **压缩非越复杂越好**:量化 int8 几乎免费 4x 压缩(精度 0.886→0.886), 而理论更优的知识蒸馏在简单任务上反而没赢过从零训小模型——方法要匹配任务难度(22.12)。
  **Compression isn't "more complex is better"**: int8 quantization is almost-free 4x compression (accuracy 0.886→0.886), while the theoretically-superior knowledge distillation didn't beat a from-scratch small model on an easy task — match the method to task difficulty (22.12).
