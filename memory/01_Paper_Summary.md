# Paper Summary: D-ResNet for Beach Sand Minerals

## Paper Reference
**Title**: D-Resnet: deep residual neural network for exploration, identification, and classification of beach sand minerals
**Journal**: Multimedia Tools and Applications (2024) 83:14539-14563
**DOI**: https://doi.org/10.1007/s11042-024-18702-4

## Key Facts from Paper

### Dataset
- **Source**: Beach Sand Mineral (BSM) dataset
- **Classes** (6): Ilmenite, Rutile, Zircon, Garnet, Monazite, Sillimanite
- **Reported counts**: 60, 62, 60, 66, 60, 59 = **367 total** (paper text says 357 - inconsistency)
- **Augmented total**: 1,468 images (4x original)
- **Split**: 70/15/15 = 1028 train / 220 val / 220 test (on augmented set)

### Augmentation (Paper)
- Horizontal flip
- Rotations: 0°, 30°, 45°, 90°, 180°, 270°
- Resize to 224×224×3
- Normalize with ImageNet mean/std

### Models Tested
| Model | Architecture | Paper Accuracy |
|-------|-------------|----------------|
| D-ResNet-50 | ResNet-50 bottleneck, 3-4-6-3 blocks | 0.89 |
| VGG-16 | Standard VGG-16 | 0.83 |
| ResNet-34 | Standard ResNet-34 | 0.83 |
| ResNet-18 | Standard ResNet-18 | 0.78 |

### Training Settings (Paper)
- Epochs: 60
- Batch size: 1028 (full training set - unusual)
- Optimizer: Adam or SGD (not clearly specified)
- Loss: Cross-entropy
- Input: 224×224×3
- Output: 6 classes (softmax)

### Reported Metrics
- **Overall Accuracy**: D-ResNet50=0.89, VGG16=0.83, ResNet34=0.83, ResNet18=0.78
- **Precision** (weighted): 0.90, 0.89, 0.89, 0.87
- **Recall/Sensitivity**: 0.89, 0.83, 0.83, 0.78
- **Per-class tables**: Tables 3, 6, 7, 8
- **Confusion matrices**: Figures 8, 10-12
- **Training curves**: Figures 6, 7
- **Prediction grids**: Figures 13, 14

## Inconsistencies & Issues to Verify

1. **Dataset count discrepancy**: Paper text says 357 images, but class counts sum to 367. The 1468 augmented total is consistent with 367×4.

2. **Precision formula typo**: Paper writes "TN/(TN+FP)" for precision - this is specificity. Correct precision = TP/(TP+FP).

3. **Batch size**: 1028 (entire training set) is effectively batch gradient descent, unusual for deep learning. We'll use 32 as default.

4. **Optimizer ambiguity**: Paper mentions both Adam and SGD without clear choice per model.

5. **Data leakage risk**: The paper splits AFTER augmentation, meaning augmented copies of the same original image can appear in both train and test sets, inflating accuracy.

6. **D-ResNet-50 architecture**: Paper Table 2 says "ResNet-50 bottleneck, 3-4-6-3 blocks" - this IS standard ResNet-50. The "D-" prefix meaning is unclear (possibly "Deep" or "Dense" but architecture matches standard).

7. **RMSE definition**: Paper mentions RMSE between one-hot labels and softmax probabilities - need to verify exact computation.

## Our Extensions
- Add **random pixel translation** (±10-15% shift) to augmentation pipeline
- Run **leak-free split**: split original 367 images first, then augment only training set
- Use standard batch size (32) with proper mini-batch SGD/Adam
- Fixed seed (42) everywhere for reproducibility