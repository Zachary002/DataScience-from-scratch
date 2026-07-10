# Part 23 · 云计算与数据科学 / Cloud for Data Science

> 现代数据科学几乎都在**云**上跑。这一部分不背服务名,而是抓**云的底层思想**:存算分离、无服务器、按量计费、访问控制、工作负载隔离、DAG 编排。核心洞察是——**三大云本质同构**(S3=GCS=Blob、SageMaker=Vertex=AzureML……),掌握心智模型就能在任意云上工作。贯穿全程的诚实主线:**云省钱靠用对(分区/Spot/自动挂起/最小权限),用错比自建更贵**。这是数据科学从"能建模"到"能在生产云环境落地"的必备一环。
> Modern data science almost all runs in the **cloud**. This part memorizes no service names but grasps the **cloud's underlying ideas**: storage-compute separation, serverless, pay-per-use, access control, workload isolation, DAG orchestration. The core insight: **the three clouds are fundamentally isomorphic** (S3=GCS=Blob, SageMaker=Vertex=AzureML…), so mastering the mental model lets you work on any cloud. The honest thread throughout: **the cloud saves money only when used right (partitioning/Spot/auto-suspend/least-privilege) — misused, it's pricier than self-hosting**. This is essential for data science moving from "can model" to "can ship in a production cloud environment."

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **hands-on experiments + visualization**, all cells validated, **honest results**.

## 工具与数据 / Tools & Data
- **真实可跑**:`duckdb`、`pyarrow`、`pandas`、`numpy`、`matplotlib`(23.2 用真实 Parquet 测 BigQuery 成本模型)。
  **Really-runnable**: `duckdb`, `pyarrow`, `pandas`, `numpy`, `matplotlib` (23.2 uses real Parquet to measure BigQuery's cost model).
- **从零复现云机制**:云 SDK 不可用 → 手写 **mini-S3 + mini-Lambda**(事件驱动)、**RBAC 访问控制引擎**、**Medallion 流水线**、**Snowflake 虚拟仓库模拟**、**DAG 编排器**(拓扑执行+重试+失败传播)。真实的服务对应表、Dockerfile 概念、YAML 作为参考。
  **From-scratch cloud mechanisms**: cloud SDKs unavailable → hand-coded **mini-S3 + mini-Lambda** (event-driven), **RBAC access-control engine**, **Medallion pipeline**, **Snowflake virtual-warehouse simulation**, **DAG orchestrator** (topological execution + retries + failure propagation). Real service-mapping tables and YAML as reference.

## 目录 / Contents
| # | 主题 / Topic | 方式 / Approach | 关键概念 / Key Concepts |
|---|---|---|---|
| 23.1 | AWS for DS | 从零 mini-S3+Lambda | 对象存储、无服务器、存算分离(按需省 24x)、服务地图 |
| 23.2 | GCP for DS | **真实 Parquet 成本测量** | BigQuery 无服务器数仓、**按扫描计费(分区+列裁剪省 61x)** |
| 23.3 | Azure for DS | 从零 RBAC 引擎 | 三云 Rosetta 对应表、**最小权限/默认拒绝**、托管身份、爆炸半径 |
| 23.4 | Databricks | 从零 Medallion 流水线 | 湖仓平台、**bronze→silver→gold** 逐层提质、Delta/Unity |
| 23.5 | Snowflake | 从零虚拟仓库模拟 | 三层架构、**虚拟仓库工作负载隔离**、按秒计费、零拷贝克隆 |
| 23.6 | 编排 Airflow/Prefect/Dagster | 从零 DAG 编排器 | **拓扑执行+重试+失败传播**、幂等性、调度回填、vs cron |

## 学习路径 / Path
23.1→23.2→23.3 是**三大云巡礼**(AWS 对象存储/无服务器 → GCP BigQuery 成本模型 → Azure + RBAC 访问控制),每个聚焦一个跨云通用概念,最后用 Rosetta 表看穿"三云同构"。23.4→23.5 是**两大数据平台之争**(Databricks 湖仓+Medallion vs Snowflake 虚拟仓库),它们把 Part 21/22 的开源工具打包成托管平台。23.6 工作流编排是**把所有管道串起来的调度层**(DAG+重试+回填)。
23.1→23.2→23.3 is the **three-cloud tour** (AWS object storage/serverless → GCP BigQuery cost model → Azure + RBAC access control), each focused on one cross-cloud concept, ending with the Rosetta table seeing through "the three clouds are isomorphic." 23.4→23.5 is the **two-data-platform war** (Databricks lakehouse + Medallion vs Snowflake virtual warehouses), packaging Part 21/22's open-source tools into managed platforms. 23.6 workflow orchestration is the **scheduling layer tying all pipelines together** (DAG + retries + backfill).

## 贯穿全部的诚实主线 / Honest threads throughout
- **存算分离让按需计算省几十倍**:每天只用 1 小时算力, 24 小时开机 $720 vs 按需 $30(24x)——只为实际使用付费(23.1)。
  **Storage-compute separation makes on-demand compute tens of times cheaper**: 1 hr/day compute costs $720 always-on vs $30 on-demand (24x) — pay only for actual use (23.1).
- **按扫描计费一个疏忽烧几十倍钱**:同样结果, SELECT * 扫描全表比分区+列裁剪贵 61 倍(真实 Parquet 测量)——别 SELECT *(23.2)。
  **Pay-per-scan burns tens of times on one oversight**: for the same result, SELECT * scans the whole table 61x more than partition + column pruning (real Parquet measurement) — never SELECT * (23.2).
- **权限配错是云事故头号原因**:RBAC 默认拒绝+最小权限, 让凭证泄漏的爆炸半径从 100% 缩到 15%(23.3)。
  **Misconfigured permissions are the #1 cloud incident cause**: RBAC deny-by-default + least-privilege shrinks a credential leak's blast radius from 100% to 15% (23.3).
- **三大云本质同构**:一张 Rosetta 表看穿(S3=GCS=Blob、SageMaker=Vertex=AzureML)——求职别被"某家经验"门槛吓住(23.3)。
  **The three clouds are fundamentally isomorphic**: one Rosetta table sees through it (S3=GCS=Blob, SageMaker=Vertex=AzureML) — job-seekers shouldn't fear "vendor X experience" gates (23.3).
- **虚拟仓库让工作负载互不干扰**:ETL 满载跑时, 分析师查询在自己的仓库上照样秒回——存算分离最有价值的实际收益(23.5)。
  **Virtual warehouses keep workloads non-interfering**: while ETL runs at full load, analyst queries return in seconds on their own warehouse — the most valuable practical benefit of storage-compute separation (23.5).
- **编排把脚本升级为可靠管道**:DAG 拓扑执行 + 重试(暂时性故障自愈)+ 失败传播(训练失败绝不部署), 前提是任务幂等(23.6)。
  **Orchestration upgrades scripts into reliable pipelines**: DAG topological execution + retries (self-heal transient failures) + failure propagation (never deploy after training fails), premised on idempotent tasks (23.6).
