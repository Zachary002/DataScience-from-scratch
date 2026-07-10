# Part 21 · 大数据 / Big Data

> 数据量上 TB / PB 后单机 pandas 会崩,必须懂**分布式计算**和**现代数据栈**。但这部分最大的诚实主线是:*"分布式不是越大越好——先问数据到底多大,用对规模的工具。"* 我们既讲清 Spark / Hadoop / Kafka 这些**分布式系统的思想**(从零实现 MiniSpark、MapReduce、流引擎、Kafka 日志、Ring-AllReduce、Lakehouse 事务日志),也用**真实基准**证明:很多"以为要上集群"的活,单机的 Polars / DuckDB 就能秒级搞定。这是数据工程和 ML 系统面试的核心,也是从"会算法"到"会造系统"的关键一跃。
> Above TB/PB, single-machine pandas dies — you must understand **distributed computing** and the **modern data stack**. But this part's biggest honest thread is: *"distributed isn't always better — first ask how big the data really is, and use the right tool for the scale."* We explain the **ideas of distributed systems** (Spark/Hadoop/Kafka) by building from scratch a MiniSpark, MapReduce, a stream engine, a Kafka log, Ring-AllReduce, and a Lakehouse transaction log — and use **real benchmarks** to prove that many "you thought you needed a cluster" jobs are done in seconds on a single machine with Polars/DuckDB. This is core to data-engineering and ML-systems interviews, and the key leap from "knows algorithms" to "builds systems."

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results**.

## 工具与数据 / Tools & Data
- **真实可跑的库**:`polars`、`duckdb`、`pyarrow`、`pandas`、`numpy`、`torch`、`matplotlib`。21.6/21.7/21.8 是**真实基准测试**(不是模拟)。
  **Really-runnable libraries**: `polars`, `duckdb`, `pyarrow`, `pandas`, `numpy`, `torch`, `matplotlib`. 21.6/21.7/21.8 are **real benchmarks** (not simulations).
- **从零实现的分布式系统**:`pyspark`/`dask`/`kafka`/`deltalake` 本机未装 → 手写 **MiniSpark**(惰性 RDD/DAG/shuffle)、**MiniSQL 优化器**(谓词下推/broadcast join)、**分布式梯度聚合**、**流引擎**(事件时间/watermark)、**mini-Dask**(任务图)、**MapReduce**、**mini-Kafka**(分区日志/消费者组)、**mini-Lakehouse**(事务日志/时间旅行)、**Ring-AllReduce**。这些从零实现把抽象的分布式概念变成能亲手运行、亲眼看到的东西。
  **From-scratch distributed systems**: `pyspark`/`dask`/`kafka`/`deltalake` not installed → hand-coded **MiniSpark** (lazy RDD/DAG/shuffle), **MiniSQL optimizer** (predicate pushdown/broadcast join), **distributed gradient aggregation**, a **stream engine** (event time/watermark), **mini-Dask** (task graph), **MapReduce**, **mini-Kafka** (partitioned log/consumer groups), **mini-Lakehouse** (transaction log/time travel), **Ring-AllReduce**. These turn abstract distributed concepts into things you can run and see.

## 目录 / Contents
| # | 主题 / Topic | 方式 / Approach | 关键概念 / Key Concepts |
|---|---|---|---|
| 21.1 | PySpark 入门 | 从零 MiniSpark | 惰性求值, 分区并行, 窄/宽依赖, Shuffle, 血缘容错 |
| 21.2 | Spark SQL & 优化 | MiniSQL + 真实 DuckDB EXPLAIN | Catalyst, 谓词下推, broadcast vs shuffle join, 数据倾斜/AQE |
| 21.3 | Spark MLlib | 从零分布式训练 | 数据并行, 梯度可加, treeAggregate(=单机 1e-16) |
| 21.4 | 结构化流处理 | 从零流引擎 | 事件时间, 窗口, **watermark 处理迟到数据**, exactly-once |
| 21.5 | Dask | 从零任务图 | delayed DAG, 并行调度(3x), 分区 pandas |
| 21.6 | Polars | **真实基准** | 列式+多线程+惰性优化器, 比 pandas 快 **5-6x** |
| 21.7 | DuckDB | **真实基准** | 进程内 OLAP, SQL 直查 Parquet 比 pandas 快 **10x**, Arrow 零拷贝 |
| 21.8 | 存储格式 | **真实基准** | 行式 vs 列式, CSV→Parquet 快 **17x/34x**, Arrow, 谓词下推 |
| 21.9 | Hadoop & MapReduce | 从零 MapReduce | map→shuffle→reduce, 为何 Spark 快 14x(内存 vs 落盘) |
| 21.10 | Kafka 入门 | 从零 mini-Kafka | 分区日志, offset, 消费者组, 键序保证, 重放 |
| 21.11 | 湖仓一体 | 从零 mini-Lakehouse | 事务日志=文件级 MVCC, ACID, 时间旅行, copy-on-write |
| 21.12 | 分布式训练 | 从零 Ring-AllReduce | 数据/张量/流水线/ZeRO 并行, AllReduce 可扩展性 |

## 学习路径 / Path
21.1→21.2→21.3→21.4 是 **Spark 主线**(批处理引擎、SQL 优化、分布式 ML、流处理)——理解分布式计算的思维模型(惰性 DAG、分区、shuffle、数据并行)。21.5→21.6→21.7→21.8 是**现代单机数据栈**——Dask(扩展 Python)、Polars/DuckDB(单机极速, 真实基准打脸"必须上集群")、存储格式(列式为什么快)。21.9→21.10→21.11 是**数据基础设施**——Hadoop/MapReduce(思想源头)、Kafka(实时数据中枢)、Lakehouse(数据湖有了数据库可靠性)。21.12 分布式训练是 **ML 系统深水区**(训 LLM 的工程核心)。
21.1→21.2→21.3→21.4 is the **Spark spine** (batch engine, SQL optimization, distributed ML, streaming) — understanding distributed computing's mental model (lazy DAG, partitions, shuffle, data parallelism). 21.5→21.6→21.7→21.8 is the **modern single-machine stack** — Dask (scale Python), Polars/DuckDB (single-machine speed, real benchmarks debunking "must go to a cluster"), storage formats (why columnar is fast). 21.9→21.10→21.11 is **data infrastructure** — Hadoop/MapReduce (the source of ideas), Kafka (real-time data hub), Lakehouse (a data lake with a database's reliability). 21.12 distributed training is the **deep end of ML systems** (the engineering core of training LLMs).

## 贯穿全部的诚实主线 / Honest threads throughout
- **数据能进单机内存就别上 Spark**:真实基准——Polars 比 pandas 快 5-6x、DuckDB 直查 Parquet 快 10x, 一台笔记本秒杀"以为要集群"的几千万行数据(21.6/21.7)。
  **If data fits single-machine memory, skip Spark**: real benchmarks — Polars 5-6x faster than pandas, DuckDB 10x on Parquet; a laptop crushes the tens-of-millions-of-rows data "you thought needed a cluster" (21.6/21.7).
- **分布式 ML 与单机数学等价, 不是玄学**:从零的分布式逻辑回归(梯度可加→各分区算局部梯度再聚合)与单机结果差 1e-16(21.3)。
  **Distributed ML is mathematically equivalent to single-machine, not magic**: from-scratch distributed logistic regression (additive gradients → partitions compute partial gradients then aggregate) differs from single-machine by 1e-16 (21.3).
- **流处理的难点是时间不是速度**:按事件时间开窗必遇乱序迟到, watermark 是延迟 vs 完整性的权衡(21.4)。
  **Streaming's difficulty is time, not speed**: event-time windowing inevitably meets out-of-order/late data; the watermark is a latency-vs-completeness tradeoff (21.4).
- **存储格式常比算法优化更能提速**:仅 CSV→Parquet 就读快 17-34x、体积小 3x, 没改一行分析逻辑(21.8)。
  **Storage format often speeds things up more than algorithm optimization**: CSV→Parquet alone is 17-34x faster and 3x smaller, no logic change (21.8).
- **Spark 比 Hadoop 快的本质是内存 vs 磁盘**:真实测量迭代任务 Spark 快 14x, 因为 MR 每轮落盘 HDFS 而 Spark 留内存(21.9)。
  **Spark beats Hadoop fundamentally via memory vs disk**: measured 14x on iterative jobs because MR spills to HDFS each round while Spark stays in memory (21.9).
- **湖仓的魔法朴素得惊人**:Delta/Iceberg 的 ACID+时间旅行, 本质只是"一个记录每版本文件构成的事务日志"(文件级 MVCC), 几十行可复现(21.11)。
  **The Lakehouse magic is astonishingly plain**: Delta/Iceberg's ACID + time travel is essentially "a transaction log recording each version's file composition" (file-level MVCC), reproducible in dozens of lines (21.11).
- **分布式训练瓶颈永远是通信**:Ring-AllReduce 每卡通信量与卡数无关(而朴素 master 汇聚线性爆炸), 这才是能扩展千卡的原因; 但先榨干单卡再谈分布式(21.12)。
  **Distributed training's bottleneck is always communication**: Ring-AllReduce's per-card communication is independent of card count (while a naive master gather explodes linearly), the real reason it scales to thousands; but exhaust single-GPU before distributing (21.12).
