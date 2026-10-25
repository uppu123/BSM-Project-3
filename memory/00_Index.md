# BSM Project 3 - Memory Index

## Project Overview
Reproduction and extension of the paper: **"D-Resnet: deep residual neural network for exploration, identification, and classification of beach sand minerals"** (Multimedia Tools and Applications, 2024, 83:14539-14563)

- **Dataset**: Kaggle `prasannavenkatesant/beach-sand-mineral-bsm` (6 classes, ~367 images)
- **Models**: ResNet-18, ResNet-34, D-ResNet-50, VGG-16
- **Framework**: PyTorch on Kaggle GPU (T4/P100)
- **GitHub**: https://github.com/uppu123/BSM-Project-3.git (created under authenticated account; can transfer to holisticNoobda later)

## Memory Notes
- [[01_Paper_Summary]] - Key paper facts and inconsistencies
- [[02_Decisions]] - All decisions with rationale (dated)
- [[03_Progress_Log]] - Chronological log of work done
- [[04_Errors_and_Fixes]] - Errors encountered and resolutions
- [[05_Results]] - Metrics tables for every model/run
- [[06_Kaggle_Quota]] - GPU hours used/remaining tracking
- [[07_Next_Steps]] - Current TODO list for crash recovery

## Notebooks (in order)
1. `01_eda_and_dataset.ipynb` - EDA and dataset exploration
2. `02_augmentation.ipynb` - Augmentation and combined dataset creation
3. `03_split.ipynb` - Train/val/test split (primary + leak-free supplementary)
4. `03_resnet18.ipynb` - ResNet-18 training (paper target: 0.78 acc)
5. `04_resnet34.ipynb` - ResNet-34 training (paper target: 0.83 acc)
6. `05_dresnet50.ipynb` - D-ResNet-50 training (paper target: 0.89 acc)
7. `06_vgg16.ipynb` - VGG-16 training (paper target: 0.83 acc)
8. `07_comparison.ipynb` - Comparison with paper results
9. `08_hyperparameter_tuning.ipynb` - Hyperparameter tuning (if needed)

## Results Structure
- `results/metrics/` - CSV/JSON metrics files
- `results/confusion_matrices/` - Heatmap PNGs
- `results/curves/` - Loss/accuracy curves

## Data Info
- `data_info/` - Split file lists (train/val/test) for reproducibility