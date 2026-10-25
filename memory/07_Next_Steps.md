# Next Steps - BSM Project 3

## Current Status: STEP 1 - EDA (READY TO START)

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

### 📋 Upcoming Steps (in order)

#### STEP 1 - EDA (notebook 01_eda_and_dataset.ipynb) - NEXT
- [ ] Load dataset from Kaggle (prasannavenkatesant/beach-sand-mineral-bsm)
- [ ] Print class counts and distribution bar chart (paper Fig. 2)
- [ ] Show sample grid (paper Fig. 3)
- [ ] Check for corrupt/missing/duplicate images
- [ ] Log actual counts vs paper's 367 in memory
- [ ] Save dataset info to data_info/

#### STEP 2 - Augmentation (notebook 02_augmentation.ipynb)
- [ ] Implement paper's augmentation (horizontal flip + 6 rotations: 0, 30, 45, 90, 180, 270)
- [ ] Add pixel translation (±10-15% shift)
- [ ] Resize to 224×224×3, normalize with ImageNet stats
- [ ] Generate ~1468 total images (4x), roughly balanced per class
- [ ] Save combined dataset for reuse (Kaggle dataset or notebook output)
- [ ] Fixed seed (42)

#### STEP 3 - Split
- [ ] Primary: 70/15/15 stratified on combined set (1028/220/220)
- [ ] Supplementary: leak-free split on originals first, then augment train only
- [ ] Save split file lists to data_info/

#### STEP 4 - Model Training (4 notebooks)
- [ ] 03_resnet18.ipynb
- [ ] 04_resnet34.ipynb
- [ ] 05_dresnet50.ipynb
- [ ] 06_vgg16.ipynb
- Each: PyTorch, pretrained ImageNet, 6-class head, 60 epochs, batch=32, seed=42

#### STEP 5 - Metrics (in each model notebook)
- [ ] Confusion matrix heatmap
- [ ] Accuracy, per-class & weighted precision/recall/specificity/F1
- [ ] RMSE (one-hot vs softmax)
- [ ] Per-class tables (paper Tables 3, 6, 7, 8 format)
- [ ] Predicted vs actual image grid

#### STEP 6 - Smoke Tests
- [ ] 1-epoch test for EACH notebook on Kaggle before full training
- [ ] Fix errors, log in 04_Errors_and_Fixes.md
- [ ] Only then run full 60 epochs

#### STEP 7 - Comparison
- [ ] 07_comparison.ipynb with table vs paper (Table 9, Fig 9 equivalent)
- [ ] Include RMSE comparison

#### STEP 8 - Hyperparameter Tuning (if needed)
- [ ] Only for models >2 points below paper
- [ ] Optuna on validation set, 8-10 epochs/trial, 15-20 trials max
- [ ] Retrain best config for 60 epochs

#### STEP 9 - Final Deliverables
- [ ] README.md with overview, setup, results, deviations, leakage caveat
- [ ] Update all memory notes
- [ ] Push everything to GitHub

---

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