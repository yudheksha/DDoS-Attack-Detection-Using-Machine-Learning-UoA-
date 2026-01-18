# DDoS Attack Detection Using Machine Learning (CICDDoS2019)

A multiclass DDoS detection and classification project built using the **CICDDoS2019** network-traffic dataset.  
This work was completed as part of my **research work at the University of Auckland**.

## Project goal
Build a machine learning pipeline that can **detect and classify multiple DDoS attack types vs. benign traffic** using flow-based network features.

Attack labels covered include:
- Syn, UDP, UDPLag, Portmap, MSSQL, NetBIOS, LDAP, and Benign traffic

## What’s inside
- `ddos-detection-using-machine-learning.ipynb` — end-to-end notebook:
  - data loading (training/testing parquet files)
  - cleaning (duplicates, low-variance columns)
  - correlation-based feature reduction
  - label encoding + feature scaling
  - model training + evaluation + ROC curves
  - model export (`random_forest_model.pkl`)
- `README.md` — project overview (this file)

## Approach (high level)
1. **Load CICDDoS2019 parquet files** (training + testing)
2. **Preprocess**
   - remove duplicates
   - drop columns with a single unique value
   - drop highly correlated features (corr ≥ 0.8)
3. **Feature engineering**
   - encode target labels
   - scale features (Min-Max scaling)
   - train/validation split (random_state=42)
4. **Model training and evaluation**
   - Random Forest, KNN, Extra Trees, MLP, XGBoost
   - metrics: Accuracy, Precision, Recall, F1, ROC AUC, CV score

## Key results (validation set)
- Best overall balanced model: **Random Forest**
  - Accuracy ≈ **99.33%**
  - F1 Score ≈ **99.32%**
- A trained Random Forest model is exported as: `random_forest_model.pkl`

## How to run
1. Install dependencies (typical):
   - Python 3.x
   - pandas, numpy, scikit-learn, matplotlib, seaborn, tqdm, xgboost

2. Open and run the notebook:
   - `ddos-detection-using-machine-learning.ipynb`

3. Dataset path
   - The notebook was originally run in a Kaggle-style structure (e.g., `/kaggle/input/...`).
   - If running locally, download/prep the CICDDoS2019 data and update the dataset directory in the notebook’s `os.walk(...)` section to point to your local folder containing:
     - `*-training.parquet`
     - `*-testing.parquet`

## Output artifacts
- Model comparison table (metrics across models)
- ROC curves (multiclass)
- `random_forest_model.pkl` (exported best model)
