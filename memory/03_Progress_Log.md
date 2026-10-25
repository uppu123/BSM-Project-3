# Progress Log

## 2026-10-26
- **STEP 0 - Setup**: COMPLETED
  - Created folder structure: notebooks/, results/, data_info/, memory/
  - Initialized git repository
  - Created GitHub repo at https://github.com/uppu123/BSM-Project-3.git (note: user requested holisticNoobda/BSM-Project-3 but it didn't exist)
  - Pushed initial commit with memory files:
    - 00_Index.md - project overview and links
    - 01_Paper_Summary.md - key paper facts and inconsistencies
    - 07_Next_Steps.md - TODO list
  - Created 02_Decisions.md with all configuration decisions
  - Next: STEP 1 - EDA notebook

## 2026-10-26 (continued)
- **STEP 1 - EDA Notebook**: CREATED
  - Created `notebooks/01_eda_and_dataset.ipynb` with:
    - Dataset loading from Kaggle
    - Class counts verification vs paper (367 total)
    - Distribution bar chart (paper Fig. 2)
    - Sample image grid (paper Fig. 3)
    - Image properties analysis (sizes, modes, aspect ratios)
    - Corrupt/missing/duplicate detection
    - Saves image lists to `data_info/` for later steps
  - Committed and pushed to GitHub
  - **Waiting for Kaggle MCP server configuration to run notebook**

## 2026-10-26 (continued)
- **Dataset Downloaded & Verified Locally**:
  - Downloaded `prasannavenkatesant/beach-sand-mineral-bsm` via Kaggle CLI (OAuth authenticated as `kiramada`)
  - **Actual class counts** (total=367, matches paper total but per-class differs):
    - Garnet: 60 (paper: 66)
    - Ilmenite: 62 (paper: 60)
    - Monazite: 60 (paper: 60)
    - Rutile: 66 (paper: 62)
    - Sillimanite: 60 (paper: 59)
    - Zircon: 59 (paper: 60)
  - Class folders appear swapped vs paper labels - will use folder names as ground truth
  - Updated `01_Paper_Summary.md` with verified counts
  - EDA notebook ready to run on Kaggle (or locally for verification)

## 2026-10-26 (continued)
- **STEP 2 - Augmentation Notebook**: CREATED
  - Created `notebooks/02_augmentation.ipynb` with:
    - Paper's augmentation: horizontal flip + 6 rotations (0, 30, 45, 90, 180, 270)
    - Extension: pixel translation (±15% shift)
    - Resize to 224×224, ImageNet normalization
    - Target: ~1468 total images (4x), balanced ~244 per class
    - Deterministic seeding (42) for reproducibility
    - Saves combined dataset + records to `/kaggle/working/combined_dataset/` and `data_info/`
  - Committed and pushed to GitHub
  - Ready to run on Kaggle GPU

## 2026-10-26 (continued)
- **STEP 3 - Split Notebook**: CREATED
  - Created `notebooks/03_split.ipynb` with:
    - Primary split: 70/15/15 stratified on combined dataset (paper-faithful)
    - Supplementary split: Leak-free split on originals first, then augment train only
    - Leakage analysis to quantify train-test overlap
    - Saves split lists to `data_info/primary_split.json` and `supplementary_split.json`
  - Committed and pushed to GitHub

- **STEP 4 - Model Training Notebooks**: CREATED (4 notebooks)
  - `03_resnet18.ipynb`: ResNet-18 (paper target: Acc=0.78, Prec=0.87, Rec=0.78)
  - `04_resnet34.ipynb`: ResNet-34 (paper target: Acc=0.83, Prec=0.89, Rec=0.83)
  - `05_dresnet50.ipynb`: D-ResNet-50 / ResNet-50 (paper target: Acc=0.89, Prec=0.90, Rec=0.89)
  - `06_vgg16.ipynb`: VGG-16 (paper target: Acc=0.83, Prec=0.89, Rec=0.83)
  - All: PyTorch, ImageNet pretrained, 6-class head, 60 epochs, batch=32, Adam, seed=42
  - Metrics: Confusion matrix, per-class precision/recall/specificity/F1, RMSE, prediction grids
  - Committed and pushed to GitHub
  - All notebooks have EPOCHS=1 for smoke test; change to 60 after verification

## 2026-10-26 (continued)
- **STEP 1 - EDA Execution**: COMPLETED (run locally)
  - Ran `01_eda_and_dataset.ipynb` locally with dataset at `C:\BSM Project 3\data_raw\BSM`
  - **Verified class counts** (total=367, matches paper):
    - Garnet: 60, Ilmenite: 62, Monazite: 60, Rutile: 66, Sillimanite: 60, Zircon: 59
  - **Per-class mismatch vs paper** confirmed (folders swapped vs paper labels)
  - **0 corrupt images, 0 duplicates** found
  - **Image properties**: Variable sizes (148x130 to 561x406), all RGB, mean aspect ratio 1.28
  - Generated outputs in `results/`: class_distribution.png, sample_grid.png, image_properties.png
  - Generated outputs in `data_info/`: class_counts.csv, eda_report.json, original_image_list.json/csv
  - EDA complete - ready for augmentation step

## 2026-10-26 (continued)
- **STEP 2 - Augmentation Execution**: COMPLETED (run locally)
  - Ran `02_augmentation.ipynb` logic locally (CPU)
  - Generated 1464 augmented images (244 per class, 6 classes = 1464 total, close to paper's 1468)
  - Paper's augmentation: horizontal flip + 6 rotations (0, 30, 45, 90, 180, 270)
  - Extension: pixel translation (±15% shift) using Albumentations
  - Resize to 224×224, ImageNet normalization
  - Saved combined dataset to `C:\BSM Project 3\combined_dataset/` (1464 images)
  - Saved records to `data_info/combined_dataset_records.json` and config to `augmentation_config.json`

- **STEP 3 - Split Execution**: COMPLETED (run locally)
  - Ran split logic locally
  - **Primary split** (combined dataset): 1024 train / 220 val / 220 test (69.9%/15.0%/15.0%)
  - **Supplementary split** (leak-free, originals only): 256 train / 55 val / 56 test
  - **Leakage analysis** (primary split): 67 train-test overlapping originals (expected with combined split)
  - Saved splits to `data_info/primary_split.json` and `supplementary_split.json`
  - Saved leakage report to `data_info/leakage_report.json`
  - Ready for model training on Kaggle GPU

## 2026-10-26 (continued)
- **STEP 4 - Smoke Tests**: COMPLETED (all 4 models validated locally)
  - Ran smoke validation for all 4 models locally (GTX 1650)
  - **ResNet-18**: 11.1M params, forward/backward pass OK, loss=1.93
  - **ResNet-34**: 21.3M params, forward/backward pass OK, loss=2.19
  - **D-ResNet-50**: 23.5M params, forward/backward pass OK, loss=1.74
  - **VGG-16**: 134.3M params, forward/backward pass OK, loss=2.02
  - All 5 validations passed: data loading, batch, model creation, forward pass, backward pass
  - All models ready for full training on Kaggle GPU (T4/P100)
  - Next: Update notebooks with EPOCHS=60 and push to Kaggle for full training

## 2026-10-26 (continued)
- **STEP 5 - Full Training on Kaggle GPU**: IN PROGRESS
  - Pushed all 4 model notebooks to Kaggle with EPOCHS=60:
    - **ResNet-18**: `kiramada/bsm-resnet-18-training` - ERROR (re-pushed v11)
    - **ResNet-34**: `kiramada/bsm-resnet-34-training` - **RUNNING** (T4 GPU)
    - **D-ResNet-50**: `kiramada/bsm-d-resnet-50-training` - ERROR (re-pushed v1)
    - **VGG-16**: `kiramada/bsm-vgg-16-training` - ERROR (re-pushed v3)
  - ResNet-34 currently RUNNING on Kaggle T4 GPU (60 epochs)
  - ResNet-18 re-pushed as version 11
  - D-ResNet-50 re-pushed as version 1
  - VGG-16 re-pushed as version 3
  - Kaggle GPU limit: 2 concurrent sessions (ResNet-34 running, 1 slot available)
  - Need to wait for ResNet-34 to complete or slot to free up
  - Will re-push errored kernels after slot frees up