# Part 17 · 强化学习 / Reinforcement Learning

> 强化学习和前面所有"从固定数据学映射"的机器学习都不同——一个**智能体**在**环境**里**试错行动**、观察奖励、学会**最大化长期回报**。没有标准答案,只有奖励信号。下棋、打游戏、机器人、推荐、自动驾驶、以及**用 RLHF 对齐大模型**,都是 RL。本部分按经典教学主线,从数学地基(MDP/贝尔曼)一路**从零实现**到 PPO,建立"价值 vs 策略、有模型 vs 无模型、on-policy vs off-policy、探索 vs 利用"的完整直觉。
> Reinforcement learning differs from every prior "learn a mapping from fixed data" method — an **agent** acts by **trial-and-error** in an **environment**, observes rewards, and learns to **maximize long-term return**. No ground-truth labels, only a reward signal. Games, robotics, recommendation, self-driving, and **aligning LLMs via RLHF** are all RL. This part follows the classic curriculum, **implementing from scratch** from the mathematical foundation (MDP/Bellman) up to PPO, building full intuition for value vs policy, model-based vs model-free, on- vs off-policy, and exploration vs exploitation.

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results**.

## 工具与环境 / Tools & Environments
- **库**:`numpy`(表格法与环境)、`torch`(DQN/策略梯度/AC/PPO 的神经网络)、`matplotlib`。
  **Libraries:** `numpy` (tabular methods & environments), `torch` (neural nets for DQN/policy-gradient/AC/PPO), `matplotlib`.
- **环境全部从零实现**:`gymnasium`/`gym` 本机未装 → 我们**手写所有经典环境**——GridWorld、湿滑冰湖、悬崖行走、21点 Blackjack、Taxi(500状态)、CartPole(连续物理)、新闻推荐上下文赌博机。这反而把"环境的转移与奖励到底怎么定义"讲得更透。
  **All environments implemented from scratch**: `gymnasium`/`gym` not installed → we **hand-code every classic environment** — GridWorld, slippery FrozenLake, Cliff Walking, Blackjack, Taxi (500 states), CartPole (continuous physics), and a news-recommendation contextual bandit. This makes "how transitions and rewards are actually defined" crystal clear.

## 目录 / Contents
| # | 主题 / Topic | 环境 / Env | 关键概念 / Key Concepts |
|---|---|---|---|
| 17.1 | MDP 与贝尔曼 | GridWorld | 状态/动作/奖励/策略/价值, 贝尔曼方程 |
| 17.2 | 动态规划 / DP | 湿滑 GridWorld | 策略迭代, 价值迭代, 已知模型规划 |
| 17.3 | 蒙特卡洛 / Monte Carlo | Blackjack | 无模型, 首次/每次访问, MC 控制 |
| 17.4 | TD 学习 | 随机游走 + 悬崖 | TD(0), 自举, TD 误差, SARSA(on-policy) |
| 17.5 | **Q-Learning** | Taxi + 悬崖 | off-policy, max 目标, SARSA-vs-Q 对决 |
| 17.6 | **DQN** | CartPole | 神经网络近似Q, 经验回放, 目标网络 |
| 17.7 | 策略梯度 / REINFORCE | CartPole | 直接优化策略, 策略梯度定理, 基线 |
| 17.8 | Actor-Critic / A2C | CartPole | 演员+评论家, 优势估计, n步/GAE 偏差-方差 |
| 17.9 | **PPO** | CartPole | 裁剪替代目标, 数据复用, 软信任域, RLHF |
| 17.10 | 赌博机 & 上下文赌博机 | 新闻推荐 | 一步 RL, LinUCB, 离线(反事实)评估 |

## 学习路径 / Path
17.1→17.2 是**基础与规划**(MDP/贝尔曼 → 动态规划, 已知模型)。17.3→17.4→17.5 是**无模型表格法主线**(MC → TD/SARSA → Q-learning), RL 的真正入门。
17.1→17.2 cover **foundations & planning** (MDP/Bellman → DP, known model). 17.3→17.4→17.5 are the **model-free tabular spine** (MC → TD/SARSA → Q-learning), the real entry to RL.
17.6→17.7→17.8→17.9 是**深度 RL 主线**(DQN 值方法 → REINFORCE 策略方法 → Actor-Critic 合流 → PPO 集大成), 现代 RL 的核心。17.10 用赌博机把整个 Part 收束到"一步 RL + 落地评估"。
17.6→17.7→17.8→17.9 are the **deep-RL spine** (DQN value method → REINFORCE policy method → Actor-Critic merger → PPO synthesis), the core of modern RL. 17.10 closes the part with bandits: "one-step RL + deployment evaluation."

## 贯穿全部的诚实主线 / Honest threads throughout
- **随机环境让最优策略学会避险**:湿滑冰湖上,最优策略会主动"撞墙/绕路"降低打滑掉洞的风险(17.2)。
  **Stochasticity teaches risk-aversion**: on slippery ice the optimal policy deliberately bumps walls / detours to reduce slip risk (17.2).
- **无需公式,从"纯玩"里学策略**:MC 不写一行概率公式,就在 21点上学出赌场级基本策略(17.3)。
  **Learn from pure play, no formulas**: MC recovers the casino basic strategy on Blackjack without a single probability formula (17.3).
- **最优 ≠ 训练时表现好**:悬崖行走里 Q-learning 学到最优贴崖路但训练在线回报更差, SARSA 更安全(17.4/17.5)。
  **Optimal ≠ good while training**: on Cliff Walking, Q-learning's optimal cliff-edge path has worse online reward; SARSA is safer (17.4/17.5).
- **消融见真章**:DQN 去掉经验回放或目标网络任一都彻底崩溃(280→~10)——证明两个技巧结构性必需(17.6)。
  **Ablation reveals truth**: removing either replay or the target network makes DQN collapse (280→~10) — both are structurally essential (17.6).
- **没有免费午餐**:REINFORCE 减基线把全正回报变成围绕0的优势(无偏降方差, 193→487)(17.7);Actor-Critic 里纯1步TD因 critic 偏差反而失败, 中间 n步才是甜点(17.8)。
  **No free lunch**: REINFORCE's baseline centers all-positive returns into a zero-mean advantage (unbiased variance reduction, 193→487) (17.7); in Actor-Critic pure 1-step TD fails from critic bias, the middle n-step wins (17.8).
- **裁剪是 PPO 的灵魂**:同批多轮复用时,无裁剪会冲过头崩溃, 裁剪稳到满分(17.9)。
  **Clipping is PPO's soul**: with multi-epoch reuse, no-clip overshoots and collapses; clipping steadily maxes out (17.9).
- **离线评估是落地命门**:Replay 方法不上线就几乎无偏地估准新策略 CTR(误差 0.005)(17.10)。
  **Offline evaluation is the crux of deployment**: the Replay method estimates a new policy's CTR nearly unbiasedly without deploying (error 0.005) (17.10).
