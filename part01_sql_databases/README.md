# Part 1 · SQL & Databases

> **几乎所有 DS / DA 面试第一关都是 SQL**。这一部分把 SELECT 到窗口函数到数据仓库一气讲完。
> **Nearly every DS/DA interview opens with SQL.** This part covers SELECT through window functions through warehousing.

## 内容清单 / Contents

| # | Notebook | 主题 / Topic | 状态 / Status |
|---|---|---|---|
| 1.1 | [`01_sql_basics.ipynb`](01_sql_basics.ipynb) | SQL 基础 / SQL Basics | ✅ Done |
| 1.2 | [`02_joins.ipynb`](02_joins.ipynb) | 多表 JOIN | ✅ Done |
| 1.3 | [`03_groupby_aggregation.ipynb`](03_groupby_aggregation.ipynb) | 聚合 & GROUP BY | ✅ Done |
| 1.4 | [`04_subquery_cte.ipynb`](04_subquery_cte.ipynb) | 子查询 & CTE | ✅ Done |
| 1.5 | [`05_window_functions.ipynb`](05_window_functions.ipynb) | 窗口函数 | ✅ Done |
| 1.6 | [`06_advanced_patterns.ipynb`](06_advanced_patterns.ipynb) | 高级 SQL 题型 / LeetCode-style | ✅ Done |
| 1.7 | [`07_indexes_explain.ipynb`](07_indexes_explain.ipynb) | 索引与执行计划 | ✅ Done |
| 1.8 | `08_python_sql_integration.ipynb` | Python + SQL 集成 | ⏳ TODO |
| 1.9 | `09_nosql_overview.ipynb` | NoSQL 速览 | ⏳ TODO |
| 1.10 | `10_data_warehouse.ipynb` | 数据仓库 / star schema | ⏳ TODO |
| 1.11 | `11_dbt_intro.ipynb` | dbt 入门 | ⏳ TODO |

## 数据集 / Datasets

| 数据集 / Dataset | 来源 / Source | 用在 / Used in |
|---|---|---|
| Mini Music Store (synthetic) | inline (DuckDB) | 1.1 |

## 工具栈 / Tools

**全部 notebook 都用 [DuckDB](https://duckdb.org/)** 跑 SQL：
- 完全在内存、零配置
- 现代 SQL 全支持（窗口函数、CTE、CUBE、PIVOT）
- Python 原生集成，可以直接查 pandas DataFrame
- 语法 95% 兼容 PostgreSQL，转生产无痛
