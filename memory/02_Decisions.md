# Decisions Log

## 2026-10-26: Project Setup
- **Created folder structure**: notebooks/, results/(metrics, confusion_matrices, curves), data_info/, memory/
- **Git repo**: Initialized at C:\BSM Project 3, pushed to https://github.com/uppu123/BSM-Project-3.git (Note: user requested holisticNoobda/BSM-Project-3 but repo didn't exist; created under authenticated account uppu123. Can transfer later.)
- **Memory vault**: Created 00_Index.md, 01_Paper_Summary.md, 07_Next_Steps.md
- **Collaborator**: uppu123 is the repo owner (authenticated account)

## 2026-10-26: Training Configuration Decisions
- **Batch size**: Paper uses 1028 (full training set). **Decision**: Use batch size = 32 (standard mini-batch). Reason: 1028 is effectively batch gradient descent, unusual for DL, may cause memory issues and poor generalization.
- **Optimizer**: Paper mentions both Adam and SGD without clear per-model choice. **Decision**: Default to Adam (lr=1e-4) for all models; can tune later. Reason: Adam generally more robust for transfer learning.
- **Pretrained weights**: **Decision**: Use ImageNet-pretrained weights for all models (default). Reason: Standard practice for small datasets (367 images); from-scratch training would need more data/epochs.
- **Epochs**: 60 (matching paper)
- **Seed**: 42 everywhere (PyTorch, NumPy, Python random, CUDA)
- **Image size**: 224×224×3 (matching paper)
- **Normalization**: ImageNet mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]

## 2026-10-26: Data Pipeline Decisions
- **Primary split**: Combine all (original + augmented), then 70/15/15 stratified (paper-faithful). **Risk**: Data leakage - augmented copies of same original can appear in train and test.
- **Supplementary split**: Leak-free - split 367 originals first (70/15/15), then augment ONLY training set. Report both.
- **Augmentation target**: ~1468 total images (4x original), roughly balanced per class.
- **Extra augmentation**: Add random pixel translation (±10-15% shift) as requested.
- **Combined dataset storage**: Save as Kaggle dataset / notebook output for reproducibility across notebooks.

## 2026-10-26: Metrics Decisions
- **Precision formula**: Use TP/(TP+FP) (paper's TN/(TN+FP) is a typo = specificity)
- **RMSE**: Compute between one-hot labels and softmax probabilities (document exact definition)
- **Per-class tables**: Match paper Tables 3, 6, 7, 8 format
- **Save formats**: CSV + JSON + PNG for all metrics

## 2026-10-26: GPU Quota
- **Limit**: 30 hours/week (Kaggle free GPU)
- **Safety threshold**: 25 hours (stop and ask before exceeding)
- **Tracking**: Log every notebook run time in 06_Kaggle_Quota.md