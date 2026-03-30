
# EADCKD: Entropy-Driven Adaptive Dual-Level Contrastive Knowledge Distillation for Semi-Supervised Medical Image Segmentation

[![Python](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-orange)](https://pytorch.org/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

![Framework Overview](figures/framework.png)  
*Figure: Overall architecture of the EADCKD framework*
Official code for "EADCKD: Entropy-Driven Adaptive Dual-Level Contrastive Knowledge Distillation for Semi-Supervised Medical Image Segmentation"
##  Introduction

EADCKD is an efficient semi-supervised medical image segmentation framework designed for clinical scenarios with extremely scarce labeled data. It significantly improves the utilization rate of unlabeled data and enhances segmentation accuracy.

## Installation

```bash
# 
git clone https://github.com/yourusername/EADCKD.git
cd EADCKD

# 
conda create -n eadckd python=3.8
conda activate eadckd

# 
pip install -r requirements.txt
```

Note: Please ensure that you download the pretrained SAM weight file and place it in the project directory: [sam_vit_b_01ec64.pth](https://www.kaggle.com/datasets/sacuscreed/sam-vit-b-01ec64-pth)



## Training

```bash

python train_EADCKD_SAM_ACDC.py \
    --data_path ./SampleData \
    --dataset /ACDC \
    --sam_checkpoint ./sam_vit_b_01ec64.pth \
    --max_iterations 50000 \
    --batch_size 12 \
    --labeled_bs 6
```
The training results are saved in the ./Results/results_ACDC_xxx/fold_X/ directory, including model checkpoints, log.txt, and coverage_history.txt.

## Test 
```bash

python test.py \
    --EADCKD_model_path ./Results/.../EADCKD_best_model.pth
```

More results and comparisons can be found in Table 1 and Table 2 of the paper.
##  Visualization ExamplesPrediction Examples

##  Acknowledgements

Our code is based on [SSL4MIS](https://github.com/HiLab-git/SSL4MIS).

##  Questions

If you have any questions, welcome contact me at 'lij20210919@gmail.com'

##  Citation

```bash

```


