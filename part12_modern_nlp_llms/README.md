# Part 12 · 现代 NLP 与大语言模型 / Modern NLP & LLMs ⭐⭐⭐

> 当下数据科学/AI 岗位的**核心竞争力**。从 RNN/LSTM、注意力、**从零实现 Transformer**，到 BERT/GPT/T5、分词(BPE)、预训练与微调、**LoRA**、RLHF/DPO、Prompt 工程、**RAG**、向量数据库、Agent、LLM 评估与推理优化。**全部从零用 PyTorch 实现**(本机无 transformers/HF)，把"黑盒大模型"拆开讲透——这正是面试最看重的深度。
> The **core competency** for today's DS/AI roles. From RNN/LSTM, attention, **a Transformer built from scratch**, to BERT/GPT/T5, tokenization (BPE), pretraining & fine-tuning, **LoRA**, RLHF/DPO, prompt engineering, **RAG**, vector databases, agents, LLM evaluation and inference optimization. **All implemented from scratch in PyTorch** (no transformers/HF here), opening up the "black box" — exactly the depth interviews reward.

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results**.

## 工具与数据 / Tools & Data
- **只用 `torch` + `numpy`**(本机未装 transformers/tiktoken/faiss)——所有模型、分词、检索、LoRA 等**从零实现**，更利于理解。
  **Only `torch` + `numpy`** (no transformers/tiktoken/faiss here) — everything from scratch, best for understanding.
- 数据用**小型/合成语料**(玩具翻译、字符级文本、TinyShakespeare 风格)以便 CPU 上快速训练；概念型主题(RLHF/Prompt/Agent)用**小演示**说明机制，并指明生产做法。
  Tiny/synthetic corpora (toy translation, char-level text) for fast CPU training; conceptual topics (RLHF/prompt/agent) use small demos plus notes on production practice.

## 目录 / Contents
| # | 主题 / Topic | 关键概念 / Key Concepts |
|---|---|---|
| 12.1 | RNN, LSTM, GRU | 序列建模, 梯度消失, 门控 |
| 12.2 | Seq2Seq & 注意力 / Attention | 编码器-解码器, Bahdanau/Luong 注意力 |
| 12.3 | **Transformer 从零** / from Scratch | Q/K/V, 多头注意力, 位置编码, 残差+LN |
| 12.4 | BERT & 编码器模型 | MLM 掩码语言模型, 双向, 微调 |
| 12.5 | **GPT & 解码器模型** | 因果LM, 自回归生成, 字符级 GPT |
| 12.6 | T5 & 编码器-解码器 | text-to-text 统一框架 |
| 12.7 | **分词 / Tokenization** | BPE(从零), WordPiece, subword |
| 12.8 | 预训练 vs 微调 | 自监督预训练 + 下游微调 |
| 12.9 | **参数高效微调 / LoRA** | 低秩适配(从零), 冻结主干 |
| 12.10 | RLHF / DPO | 奖励模型, PPO, DPO |
| 12.11 | Prompt 工程 | few-shot, 思维链CoT, ReAct, 自洽 |
| 12.12 | **RAG / 检索增强生成** | 嵌入+检索+生成 |
| 12.13 | 向量数据库 / Vector DB | 近邻搜索, HNSW, 量化 |
| 12.14 | LLM 智能体 / Agents | 工具调用, 规划, ReAct 循环 |
| 12.15 | LLM 评估 | 困惑度, BLEU, ROUGE, LLM-as-judge |
| 12.16 | LLM 推理优化 | KV cache, 量化, 投机解码 |

## 学习路径 / Path
12.1 → 12.2 → 12.3 是通往 Transformer 的主线(循环→注意力→自注意力)。
12.1 → 12.2 → 12.3 is the road to the Transformer (recurrence → attention → self-attention).
12.4–12.6 是三大架构家族(编码器/解码器/编码-解码)；12.7–12.10 是训练 LLM 的关键工程；12.11–12.16 是用好 LLM 的实战(Prompt/RAG/Agent/评估/部署)。
12.4–12.6 are the three architecture families; 12.7–12.10 are key LLM-training engineering; 12.11–12.16 are applying LLMs in practice.
