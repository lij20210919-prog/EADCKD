
# EADCKD: Entropy-Driven Adaptive Dual-Level Contrastive Knowledge Distillation for Semi-Supervised Medical Image Segmentation

[![Python](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-orange)](https://pytorch.org/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

![Framework Overview](figures/framework.png)  
*Figure: Overall architecture of the EADCKD framework*

## 简介 | Introduction

EADCKD 是一个高效的半监督医学图像分割框架，针对标注数据极度稀缺的临床场景，显著提升未标记数据的利用率和分割精度。核心创新包括：

- 像素级熵作为统一不确定性度量，同时指导伪标签过滤、Mixup 区域选择和对比蒸馏加权
- 双层对比知识蒸馏（DCKD）：同时在特征层和 logits 层对齐 SAM 教师与学生网络
- 双重归一化知识蒸馏（DNKD）：解决多类医学分割中的尺度不一致与类别不平衡
- 熵优化的目标 Mixup：仅混合高置信区域，强力抑制伪标签噪声传播

在 ACDC 数据集 10% 标注设置下，Dice 达到 **90.11%**，显著超越主流半监督方法。

## 主要特性 | Key Features

- 基于原始 SAM (ViT-B) 作为教师，提供高质量伪标签
- 双学生网络（UNet + VNet） + 可学习融合头，实现互补预测
- 熵驱动的软加权机制，避免硬阈值过滤导致的信息丢失
- 支持 ACDC、SegTHOR、多源结肠镜数据集等多任务验证
- 训练吞吐量 ≈ 0.051 iters/sec（RTX 4090，batch=12），推理速度 ≈ 35 ms/图像

## 安装 | Installation

```bash
# 克隆仓库
git clone https://github.com/yourusername/EADCKD.git
cd EADCKD

# 创建虚拟环境（推荐 conda）
conda create -n eadckd python=3.8
conda activate eadckd

# 安装依赖
pip install -r requirements.txt

# 安装额外工具（用于评估、计算成本等）
pip install medpy thop torchsummary scikit-image scipy
