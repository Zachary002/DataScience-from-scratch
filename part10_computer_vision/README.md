# Part 10 · 计算机视觉 / Computer Vision

> 让机器"看懂"图像。从图像处理基础、卷积神经网络(CNN)、经典架构(LeNet→ResNet)，到目标检测、分割、Vision Transformer、多模态与自监督学习。本部分**大量动手实验 + 丰富可视化**，帮你把抽象概念"看"明白。
> Teaching machines to "see." From image-processing basics, CNNs, classic architectures (LeNet→ResNet), to detection, segmentation, Vision Transformers, multimodal and self-supervised learning. This part is **experiment-heavy with rich visualizations** to make abstract ideas visible.

每个 notebook 都遵循全仓统一标准：逐句中英双语、直觉优先的讲解、丰富代码注释、💡面试速查 + 💼实战视角，所有代码单元均实跑验证。
Every notebook follows the repo-wide standards: line-by-line bilingual, intuition-first, richly commented code, 💡 interview cheat-sheets + 💼 practical angles, all code cells validated to run.

## 数据 / Data
- **图像处理**：用 `skimage.data` 自带样例图（astronaut/camera/coins…），无需下载。
  **Image processing:** uses `skimage.data` built-in samples (astronaut/camera/coins…), no download.
- **分类/CNN**：用 **FashionMNIST / MNIST**（28×28，torchvision 自动下载，约 30MB，快），部分用 **CIFAR-10**（32×32 彩色）。数据缓存到 `~/.cache/dsfs_cv`，多个 notebook 共享、跨天复用。
  **Classification/CNN:** **FashionMNIST / MNIST** (28×28, torchvision auto-download, ~30MB, fast); some use **CIFAR-10** (32×32 color). Cached to `~/.cache/dsfs_cv`, shared across notebooks.
- 检测/分割/姿态等需要大数据集的主题，用**小规模合成数据或单图**做可视化演示，并指明真实数据集与生产做法。
  Detection/segmentation/pose (needing big datasets) use **small synthetic data or single images** for visualization, noting the real datasets and production practice.

> 注：本机未装 OpenCV(cv2)，图像处理用 `skimage` + `PIL` 实现（API 思想相通，会标注 OpenCV 对应写法）。
> Note: OpenCV (cv2) isn't installed here; image processing uses `skimage` + `PIL` (same ideas; OpenCV equivalents noted).

## 目录 / Contents
| # | 主题 / Topic | 数据 / Data | 关键概念 / Key Concepts |
|---|---|---|---|
| 10.1 | 图像处理基础 / Image Processing | skimage samples | 像素/通道/色彩空间, 滤波, 卷积, 边缘检测 |
| 10.2 | 卷积神经网络 / CNN | FashionMNIST | 卷积/池化, 感受野, 特征图可视化, 从零卷积 |
| 10.3 | 经典 CNN 架构 / Classic CNNs | FashionMNIST | LeNet/AlexNet/VGG/GoogLeNet, 1×1 卷积 |
| 10.4 | ResNet & 跳连 / ResNet | FashionMNIST | 残差块, 退化问题, 恒等映射 |
| 10.5 | 数据增强 / Data Augmentation | CIFAR-10 | flip/crop/rotate, Mixup, Cutout, 对比实验 |
| 10.6 | 目标检测 / Object Detection | 合成/单图 | bbox, IoU, NMS(从零), R-CNN/YOLO/SSD 思想 |
| 10.7 | 图像分割 / Segmentation | 合成/单图 | FCN, U-Net(搭建), Dice loss, 语义vs实例 |
| 10.8 | 关键点检测 / Pose Estimation | 合成 | 热图回归, 关键点 |
| 10.9 | Vision Transformer / ViT | FashionMNIST | patch embedding, class token, 自注意力 |
| 10.10 | 多模态 / Multimodal (CLIP) | 合成图文 | 对比学习, 图文对齐, 零样本 |
| 10.11 | 自监督学习 / Self-Supervised | FashionMNIST | SimCLR/对比学习, MoCo/MAE 思想 |

## 学习路径 / Path
10.1 → 10.2 → 10.3 → 10.4 是核心主线（图像→卷积→架构→残差）。
10.1 → 10.2 → 10.3 → 10.4 is the core spine (image → conv → architectures → residual).
10.5 数据增强贯穿实战；10.6–10.8 是 CV 三大下游任务；10.9–10.11 是现代前沿。
10.5 (augmentation) is practical throughout; 10.6–10.8 are the three downstream tasks; 10.9–10.11 are the modern frontier.
