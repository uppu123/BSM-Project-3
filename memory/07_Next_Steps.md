# Next Steps - BSM Project 3

## Current Status: STEP 5 - METRICS & COMPARISON (ALL MODEL NOTEBOOKS CREATED)

### ✅ Completed (STEP 0 - Setup)
- [x] Create folder structure (notebooks/, results/, data_info/, memory/)
- [x] Initialize git repository
- [x] Create GitHub repo (https://github.com/uppu123/BSM-Project-3.git)
- [x] Write memory/00_Index.md
- [x] Write memory/01_Paper_Summary.md
- [x] Write memory/02_Decisions.md
- [x] Write memory/03_Progress_Log.md
- [x] Write memory/04_Errors_and_Fixes.md
- [x] Write memory/05_Results.md
- [x] Write memory/06_Kaggle_Quota.md
- [x] Write memory/07_Next_Steps.md (this file)
- [x] First commit and push to GitHub

### ✅ Completed (STEP 1 - EDA Notebook Creation)
- [x] Create `notebooks/01_eda_and_dataset.ipynb` with full EDA pipeline
- [x] Commit and push to GitHub

### ✅ Completed (Dataset Verification - Local)
- [x] Downloaded dataset via Kaggle CLI (OAuth authenticated as `kiramada`)
- [x] Verified 367 total images across 6 classes
- [x] **Found per-class count mismatch vs paper** (folders appear swapped):
  - Garnet: 60, Ilmenite: 62, Monazite: 60, Rutile: 66, Sillimanite: 60, Zircon: 59
- [x] Updated `01_Paper_Summary.md` with actual counts

### ✅ Completed (STEP 2 - Augmentation Notebook Creation)
- [x] Create `notebooks/02_augmentation.ipynb` with full augmentation pipeline
- [x] Paper's augmentation: horizontal flip + 6 rotations
- [x] Extension: pixel translation (±15% shift)
- [x] Target: ~1468 total (4x), balanced ~244/class
- [x] Commit and push to GitHub

### ✅ Completed (STEP 3 - Split Notebook Creation)
- [x] Create `notebooks/03_split.ipynb` with primary + supplementary splits
- [x] Leakage analysis included
- [x] Commit and push to GitHub

### ✅ Completed (STEP 4 - Model Training Notebooks Creation)
- [x] `03_resnet18.ipynb` - ResNet-18 (paper target: Acc=0.78)
- [x] `04_resnet34.ipynb` - ResNet-34 (paper target: Acc=0.83)
- [x] `05_dresnet50.ipynb` - D-ResNet-50 (paper target: Acc=0.89)
- [x] `06_vgg16.ipynb` - VGG-16 (paper target: Acc=0.83)
- [x] All: PyTorch, ImageNet pretrained, 6-class head, 60 epochs, batch=32, Adam, seed=42
- [x] All include: confusion matrix, per-class metrics, RMSE, prediction grids
- [x] All have EPOCHS=1 for smoke test
- [x] Commit and push to GitHub

### 🔄 Ready to Run (STEP 1-4 Execution on Kaggle GPU)
- [ ] Run `01_eda_and_dataset.ipynb` on Kaggle GPU (smoke test + full)
- [ ] Run `02_augmentation.ipynb` on Kaggle GPU (generates combined dataset)
- [ ] Run `03_split.ipynb` on Kaggle GPU (generates split files)
- [ ] Run each model notebook with EPOCHS=1 (smoke test) on Kaggle GPU
- [ ] If smoke tests pass, change EPOCHS=60 and run full training for each model
- [ ] Save results to `results/` and commit after each

### 📋 Next: STEP 5 - Metrics (already in each model notebook)
- [ ] Confusion matrix heatmaps
- [ ] Per-class precision/recall/specificity/F1
- [ ] RMSE (one-hot vs softmax)
- [ ] Prediction grids

### 📋 Next: STEP 6 - Smoke Tests (critical - in each notebook)
- [ ] Run EPOCHS=1 for each model notebook on Kaggle
- [ ] Fix any errors, log in 04_Errors_and_Fixes.md
- [ ] Only then set EPOCHS=60 and run full training

### 📋 Next: STEP 7 - Comparison (notebook 07_comparison.ipynb)
- [ ] Create comparison table vs paper (Table 9, Fig 9 equivalent)
- [ ] Include RMSE comparison
- [ ] Leak-free supplementary results

### 📋 Next: STEP 8 - Hyperparameter Tuning (if needed)
- [ ] Only for models >2 points below paper
- [ ] Optuna on validation set, 8-10 epochs/trial, 15-20 trials max

### 📋 Next: STEP 9 - Final Deliverables
- [ ] README.md with overview, setup, results, deviations, leakage caveat
- [ ] Update all memory notes
- [ ] Push everything to GitHub

## GPU Quota Tracking
- **Weekly limit**: 30 hours (Kaggle free GPU)
- **Safety limit**: 25 hours (stop and ask before exceeding)
- **Used so far**: 0 hours
- **Remaining**: 30 hours

---

## Blockers / Questions
- [ ] Need to configure Kaggle MCP server (requires kaggle.json credentials) - will need user to provide
- [ ] Verify dataset download works on Kaggle
- [ ] User may want to transfer repo to holisticNoobda/BSM-Project-3