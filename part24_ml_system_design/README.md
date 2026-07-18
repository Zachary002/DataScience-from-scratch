# Part 24 · ML 系统设计与面试 / ML System Design & Interviews  ⭐⭐⭐

> **整个仓库的收官**——直接对准大厂 senior DS / MLE 面试。前面 24 个部分教你"懂技术",这一部分教你"拿 offer":8 道经典 ML 系统设计题(推荐/搜索/feed/广告/欺诈/ETA/审核/RAG)+ 4 个面试硬技能(案例题/行为面/SQL/ML 概念)。每道系统设计题都遵循同一套框架(澄清需求→指标→架构→数据特征→模型→服务扩展→监控陷阱)并附一个**可跑的核心机制 demo**;面试技能部分用真实 DuckDB/sklearn 现场演示。这是把整个仓库的知识"变现"成 offer 的最后一跃。
> **The finale of the whole repo** — aimed directly at senior DS / MLE interviews at big tech. The prior 24 parts taught you to "understand the tech"; this part teaches you to "land the offer": 8 classic ML system-design questions (recommendation/search/feed/ads/fraud/ETA/moderation/RAG) + 4 interview hard skills (case questions/behavioral/SQL/ML concepts). Each system-design question follows the same framework (clarify → metrics → architecture → data & features → models → serving & scaling → monitoring & pitfalls) with a **runnable core-mechanism demo**; the interview-skills part demonstrates live with real DuckDB/sklearn. This is the final leap turning the whole repo's knowledge into an offer.

每个 notebook 遵循全仓标准：逐句中英双语、💡面试速查（含"面试金句"答题模板）、💼实战视角、可跑 demo、所有代码验证、**诚实呈现**。
Every notebook follows the repo standards: line-by-line bilingual, 💡 cheat-sheets (with "interview one-liner" answer templates), 💼 practical angles, runnable demos, all cells validated, **honest presentation**.

## 目录 / Contents
| # | 主题 / Topic | 核心洞察 / Core Insight（可跑 demo） |
|---|---|---|
| 24.1 | 设计推荐系统 / Recommender | **多阶段漏斗**(检索→精排→重排): 深度精排全部100万物品 401ms vs 漏斗 12ms |
| 24.2 | 设计搜索排序 / Search Ranker | **混合检索**: BM25 词汇(精确)+ 语义向量(同义), 互补缺一漏召回 |
| 24.3 | 设计信息流 / News Feed | 多目标价值模型 + **MMR 多样性重排**(1作者刷屏→4作者)+ fan-out 推/拉 |
| 24.4 | 设计广告 CTR / Ads CTR | **校准**: eCPM=bid×pCTR 需真实概率, AUC 不变但 ECE 降 6x(排序好≠概率准) |
| 24.5 | 设计欺诈检测 / Fraud | 准确率陷阱(98%抓0欺诈)+ **成本敏感阈值**(最优0.02≠0.5, 成本 150k→30k) |
| 24.6 | 设计 ETA / ETA Prediction | **分位数回归**: P50 只 51% 准时, P90 达 91%(误差不对称迟到>早到) |
| 24.7 | 设计内容审核 / Moderation | **分级/级联**: 高置信自动、不确定送人审(自动错误 6000→400) |
| 24.8 | 设计 RAG / RAG System | 检索决定答案质量; 检索不到应说"不知道"防幻觉(mini RAG demo) |
| 24.9 | 案例面试题型 / Case Patterns | 指标设计+根因分析框架; **辛普森悖论**分段分解(整体降但每段没变) |
| 24.10 | 行为面试 / Behavioral (STAR) | 把"AUC 0.87"翻译成"+\$8.6M/年"; end-to-end ownership |
| 24.11 | SQL 面试速通 / SQL Cram | **7 大可跑 DuckDB 模式**: 窗口排名/LAG/累计/自连接/漏斗/gaps-islands/留存 |
| 24.12 | ML 概念速通 / ML Concepts | 偏差-方差(degree15 测试MSE爆4322)、L1稀疏vs L2缩小、18题 Q&A 速查 |

## 学习路径 / Path
24.1→24.8 是 **8 道系统设计题**——都遵循同一框架, 但每题突出一个决定性洞察:推荐的漏斗、搜索的混合检索、feed 的多样性、广告的校准、欺诈的成本阈值、ETA 的分位数、审核的分级、RAG 的检索为王。24.9→24.12 是 **4 个面试硬技能**——案例题(结构化拆解)、行为面(STAR+量化影响)、SQL(7 大模式)、ML 概念(理解本质)。
24.1→24.8 are the **8 system-design questions** — all following the same framework but each highlighting one decisive insight: the recommender's funnel, search's hybrid retrieval, the feed's diversity, ads' calibration, fraud's cost threshold, ETA's quantiles, moderation's tiering, RAG's retrieval-is-king. 24.9→24.12 are the **4 interview hard skills** — case questions (structured decomposition), behavioral (STAR + quantified impact), SQL (7 patterns), ML concepts (understand the essence).

## 系统设计通用框架 / The universal system-design framework
**澄清需求 → 定指标(离线+在线+护栏)→ 架构(多阶段漏斗)→ 数据与特征 → 模型 → 服务与扩展 → 监控与陷阱**。别急着上模型, 先问问题; 主动提冷启动/反馈回路/位置偏差/离线-在线差异/伦理。
**Clarify → metrics (offline + online + guardrails) → architecture (multi-stage funnel) → data & features → models → serving & scaling → monitoring & pitfalls**. Don't jump to models; ask questions first; proactively raise cold start / feedback loops / position bias / offline-online gap / ethics.

## 贯穿全部的诚实主线 / Honest threads throughout
- **漏斗让大规模+精准+低延迟同时成立**: 没法用重模型给百万物品打分, 检索便宜粗筛 + 精排昂贵精选(24.1)。
  **The funnel makes large-scale + accurate + low-latency simultaneous**: can't score millions with a heavy model, so cheap retrieval coarse-filters + expensive ranking fine-selects (24.1).
- **排序好 ≠ 概率准**: 广告 AUC 高但系统性高估 pCTR 会毁掉竞价, 校准让 ECE 降 6x 而 AUC 不变(24.4)。
  **Good ranking ≠ accurate probability**: high ad AUC but systematically overestimated pCTR wrecks the auction; calibration cuts ECE 6x with AUC unchanged (24.4).
- **准确率是欺诈检测的垃圾指标**: 全预测正常 98% 准确抓 0 欺诈; 阈值由业务成本决定不是 0.5(24.5)。
  **Accuracy is garbage for fraud detection**: predict-all-legit is 98% accurate catching 0 fraud; threshold set by business cost not 0.5 (24.5).
- **回归不一定预测均值**: ETA 误差不对称, 用分位数回归 P90 给可靠承诺(P50 一半迟到)(24.6)。
  **Regression needn't predict the mean**: ETA errors are asymmetric, use quantile regression P90 for a reliable promise (P50 is late half the time) (24.6).
- **整体指标变化先分段**: 辛普森悖论——整体转化率降但每段没变, 真因是流量结构变化(24.9)。
  **Segment before concluding on aggregate changes**: Simpson's paradox — overall conversion drops but each segment unchanged, the true cause is a traffic mix shift (24.9).
- **数据科学家最易栽在只说技术不说价值**: 把"AUC 0.87"翻译成"+\$8.6M/年", 决定 offer 级别(24.10)。
  **Data scientists most fail by stating tech not value**: translate "AUC 0.87" into "+\$8.6M/year," which decides offer level (24.10).
- **理解 > 记忆**: 概念题能演示/连接业务才是深度; 这也是整个仓库"从零实现、诚实求真"的核心理念(24.12)。
  **Understanding > memorization**: concept questions demand demonstrating/connecting to the business for depth; also the whole repo's core idea of "implement from scratch, honestly seek truth" (24.12).
