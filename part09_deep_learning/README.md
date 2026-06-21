# Part 9 · 深度学习基础 / Deep Learning Foundations

> 前面都是经典机器学习。这一部分进入**深度学习**——从单个感知器到多层网络、从零用 NumPy 实现反向传播、再到 PyTorch/Keras 框架，以及训练一个深度网络真正需要的全部"内功"：激活、损失、优化器、学习率调度、初始化、正则化、训练技巧、分布式、迁移学习、可视化。
> Beyond classic ML lies **deep learning** — from a single perceptron to multilayer nets, backprop from scratch in NumPy, then PyTorch/Keras, plus everything needed to actually train a deep net: activations, losses, optimizers, LR schedules, initialization, regularization, training tricks, distributed training, transfer learning, and visualization.

## 内容清单 / Contents

| # | Notebook | 主题 / Topic | 状态 |
|---|---|---|---|
| 9.1 | [`01_perceptron_mlp.ipynb`](01_perceptron_mlp.ipynb) | 感知器 & MLP / Perceptron & MLP | ✅ |
| 9.2 | [`02_nn_from_scratch.ipynb`](02_nn_from_scratch.ipynb) | 神经网络从零实现 / NN from Scratch | ✅ |
| 9.3 | [`03_pytorch_basics.ipynb`](03_pytorch_basics.ipynb) | PyTorch 入门 / PyTorch Basics | ✅ |
| 9.4 | [`04_keras_basics.ipynb`](04_keras_basics.ipynb) | Keras 入门 / Keras Basics | ✅ |
| 9.5 | [`05_activations.ipynb`](05_activations.ipynb) | 激活函数 / Activations | ✅ |
| 9.6 | [`06_loss_functions.ipynb`](06_loss_functions.ipynb) | 损失函数 / Loss Functions | ✅ |
| 9.7 | [`07_optimizers.ipynb`](07_optimizers.ipynb) | 优化器 / Optimizers | ✅ |
| 9.8 | [`08_lr_schedulers.ipynb`](08_lr_schedulers.ipynb) | 学习率调度 / LR Schedulers | ✅ |
| 9.9 | [`09_initialization.ipynb`](09_initialization.ipynb) | 初始化 / Initialization | ✅ |
| 9.10 | [`10_regularization.ipynb`](10_regularization.ipynb) | 正则化 / Regularization | ✅ |
| 9.11 | [`11_training_tricks.ipynb`](11_training_tricks.ipynb) | 训练技巧 / Training Tricks | ✅ |
| 9.12 | [`12_distributed_training.ipynb`](12_distributed_training.ipynb) | 分布式训练 / Distributed Training | ✅ |
| 9.13 | [`13_transfer_learning.ipynb`](13_transfer_learning.ipynb) | 迁移学习 / Transfer Learning | ✅ |
| 9.14 | [`14_nn_visualization.ipynb`](14_nn_visualization.ipynb) | 神经网络可视化 / NN Visualization | ✅ |

## 数据集 / Datasets

| 数据集 | 来源 | 用在 |
|---|---|---|
| XOR | inline | 9.1 |
| Digits (MNIST 替身, 8×8) | `sklearn.datasets.load_digits` | 9.1-9.4, 9.7-9.14 |
| Synthetic | inline `numpy.default_rng` | 9.5, 9.6, 9.9 |

> 注：CIFAR/Flowers/真 MNIST 需联网下载且较大；为保证**每个单元秒级可跑、离线可用**，用 sklearn Digits(8×8) 作 MNIST 替身、合成数据演示机制，并注明生产中的真实数据集。
> Note: CIFAR/Flowers/full MNIST need large downloads; to keep every cell **fast and offline**, we use sklearn Digits (8×8) as a MNIST stand-in and synthetic data, noting the real datasets used in production.

## 工具栈 / Tools

`numpy`(从零实现) + `torch`(主框架) + `keras`(Keras 3, torch 后端) + `torchvision`。
每个主题**先讲数学/直觉, 再从零实现(可行时), 再用框架**, 标注 💡 面试要点与 💼 实战视角。
