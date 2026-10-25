# Next Steps - BSM Project 3

## Current Status: STEP 3 - SPLIT NOTEBOOK (AUGMENTATION NOTEBOOK CREATED)

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

### 🔄 Ready to Run (STEP 1-2 Execution)
- [ ] Run `01_eda_and_dataset.ipynb` on Kaggle GPU
- [ ] Run `02_augmentation.ipynb` on Kaggle GPU
- [ ] Generate combined dataset (~1468 images)
- [ ] Save records to `data_info/`

### 📋 Next: STEP 3 - Split (notebook 03_split.ipynb)
- [ ] Primary: 70/15/15 stratified on combined set (1028/220/220)
- [ ] Supplementary: leak-free split on originals first, then augment train only
- [ ] Save split file lists to data_info/

### 📋 Upcoming Steps (in order)

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