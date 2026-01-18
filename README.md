# DDoS Attack Detection Using Machine Learning (CICDDoS2019)

A multiclass DDoS detection and classification project built using the CICDDoS2019 network-traffic dataset.
This work was completed as part of my research work at the University of Auckland.

## Project goal
Build a machine learning pipeline that can detect and classify multiple DDoS attack types vs. benign traffic using flow-based network features.

Attack labels covered include:
- Syn, UDP, UDPLag, Portmap, MSSQL, NetBIOS, LDAP, and Benign traffic

## Repository contents
- `ddos-detection-using-machine-learning.ipynb` - end-to-end notebook (data prep, training, evaluation, export)
- `README.md` - project overview

## Approach (high level)
1. Load CICDDoS2019 parquet files (training and testing)
2. Preprocess
   - remove duplicates
   - drop columns with a single unique value
   - drop highly correlated features (corr >= 0.8)
3. Feature preparation
   - encode target labels
   - scale features (Min-Max scaling)
   - train/validation split (random_state=42)
4. Model training and evaluation
   - Random Forest, KNN, Extra Trees, MLP, XGBoost
   - metrics: Accuracy, Precision, Recall, F1, ROC AUC, cross-validation score

## Key results (validation set)
- Best overall balanced model: Random Forest
  - Accuracy: ~99.33%
  - F1 Score: ~99.32%
- Exported model file: `random_forest_model.pkl`

## How to run
1. Install dependencies (typical)
   - Python 3.x
   - pandas, numpy, scikit-learn, matplotlib, seaborn, tqdm, xgboost

2. Open and run the notebook
   - `ddos-detection-using-machine-learning.ipynb`

## Dataset notes
- The notebook was originally run in a Kaggle-style directory structure (for example, `/kaggle/input/...`).
- If running locally, download and place CICDDoS2019 parquet files on your machine and update the dataset path in the notebook to point to the folder containing:
  - `*-training.parquet`
  - `*-testing.parquet`

## Outputs
- Model comparison metrics across algorithms
- Multiclass ROC curves
- Saved model: `random_forest_model.pkl`
