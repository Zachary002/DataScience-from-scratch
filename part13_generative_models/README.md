# Part 13 · 生成模型 / Generative Models

> 不止"判别"(分类/回归), 而是**生成**全新数据——画图、写字、合成人脸。从自编码器、**VAE**、**GAN**、流模型, 到当今最火的**扩散模型(Diffusion)** 和 **Stable Diffusion** 原理。生成模型是 AIGC 时代的核心, 也是面试热点。**全部用 PyTorch 从零实现**, 在 MNIST 上**亲手训练出会生成数字的模型**, 配大量可视化。
> Beyond "discriminating" (classification/regression), **generate** brand-new data — images, text, faces. From autoencoders, **VAE**, **GAN**, normalizing flows, to today's hottest **diffusion models** and **Stable Diffusion** internals. Generative models are the core of the AIGC era and an interview hotspot. **All implemented from scratch in PyTorch**, training digit-generating models on MNIST with rich visualization.

每个 notebook 遵循全仓标准：逐句中英双语、直觉优先、丰富注释、💡面试速查 + 💼实战视角、**大量动手实验+可视化**、所有代码实跑验证、**诚实呈现结果**(生成质量受 CPU/小模型/小数据限制时如实说明)。
Every notebook follows the repo standards: line-by-line bilingual, intuition-first, richly commented, 💡 cheat-sheets + 💼 practical angles, **experiment-heavy with visualization**, all cells validated, **honest results** (noting when quality is limited by CPU/small models/small data).

## 工具与数据 / Tools & Data
- **只用 `torch` + `numpy` + `matplotlib`**——所有生成模型从零实现。
  **Only `torch` + `numpy` + `matplotlib`** — all models from scratch.
- 数据用 **MNIST**(手写数字, 28×28, torchvision 自动下载, 缓存到 `~/.cache/dsfs_cv`); 流模型用 2D 玩具数据便于可视化。
  Data: **MNIST** (handwritten digits, 28×28, auto-downloaded, cached); flows use 2D toy data for visualization.
- 为在 CPU 上快速训练, 用**小子集 + 小模型 + 少步数**; 生成质量"可辨认但不完美", 重点在**讲清原理**, 并指明放大到 GPU/大数据的真实做法。
  For fast CPU training: **small subsets + small models + few steps**; generations are "recognizable but imperfect" — the focus is the principle, noting how to scale up.

## 目录 / Contents
| # | 主题 / Topic | 关键概念 / Key Concepts |
|---|---|---|
| 13.1 | 自编码器 / Autoencoder | 编码-解码, 重建, 隐空间 |
| 13.2 | 变分自编码器 / VAE | ELBO, 重参数化, 从隐空间采样生成 |
| 13.3 | GAN 基础 / GAN | 生成器-判别器博弈, minimax, 模式坍塌 |
| 13.4 | DCGAN / WGAN | 卷积 GAN, Wasserstein 损失, 训练稳定性 |
| 13.5 | 条件 GAN / cGAN | 可控生成(指定数字) |
| 13.6 | 流模型 / Normalizing Flows | 可逆网络, 变量变换, RealNVP |
| 13.7 | **扩散模型 / Diffusion (DDPM)** | 前向加噪/反向去噪, 当今主流 |
| 13.8 | Stable Diffusion 原理 | 潜空间扩散, U-Net, CLIP 条件 |
| 13.9 | 生成模型评估 / Eval | FID, Inception Score, 多样性vs保真 |

## 学习路径 / Path
13.1 → 13.2 是"压缩+生成"的入门(AE→VAE)。13.3→13.5 是 GAN 家族(对抗生成)。
13.1 → 13.2 are the gateway (AE → VAE). 13.3 → 13.5 are the GAN family.
13.6 流模型是另一条路(精确似然)。13.7→13.8 是当今主流的扩散模型。13.9 讲怎么评估生成质量。
13.6 (flows) is another route (exact likelihood). 13.7 → 13.8 are today's dominant diffusion models. 13.9 covers evaluation.
