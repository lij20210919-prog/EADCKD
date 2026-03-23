
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


## 主要特性 | Key Features

- 基于原始 SAM (ViT-B) 作为教师，提供高质量伪标签
- 双学生网络（UNet + VNet） + 可学习融合头，实现互补预测
- 熵驱动的软加权机制，避免硬阈值过滤导致的信息丢失
- 支持 ACDC、SegTHOR、多源结肠镜数据集等多任务验证

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
```

注意：请确保下载预训练 SAM 权重并放置在项目目录下：sam_vit_b_01ec64.pth

## 快速开始 | Quick Start

```bash

python train_semi_SAM_ACDC.py \
    --data_path ./SampleData \
    --dataset /ACDC \
    --sam_checkpoint ./sam_vit_b_01ec64.pth \
    --max_iterations 50000 \
    --batch_size 12 \
    --labeled_bs 6
```
训练结果保存在 ./Results/results_ACDC_xxx/fold_X/ 目录下，包括模型权重、log.txt 和 coverage_history.txt。

## 测试 / 推理
```bash

python test.py \
    --SGDL_model_path ./Results/.../SGDL_best_model.pth
```

更多结果和对比见论文 Table 1 & Table 2。
## 可视化示例 | Visualization ExamplesPrediction Examples


## 引用 | Citation
如果我们的工作对你的研究有帮助，请考虑引用：bibtex
```bash

```





# 安装额外工具（用于评估、计算成本等）
pip install medpy thop torchsummary scikit-image scipy
