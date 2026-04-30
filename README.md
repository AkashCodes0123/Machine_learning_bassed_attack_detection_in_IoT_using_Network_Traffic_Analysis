# Network Intrusion Detection System (IDS) using Machine Learning

## Overview

This project implements a machine learning-based Network Intrusion Detection System (IDS) for classifying network traffic as **benign** or **attack**. It is built using the **NF-UQ-NIDS-v2** dataset and follows an end-to-end workflow that includes data cleaning, feature scaling, model training, evaluation, explainability, and model saving.

The notebook compares multiple machine learning models for intrusion detection, including **Random Forest**, **XGBoost**, **LightGBM**, and an **SVM-based pipeline** using **Nystroem kernel approximation** with **SGDClassifier**.

## Key Features

- Data preprocessing and cleaning
- Removal of non-informative network fields such as IP addresses and ports
- Handling of missing and infinite values
- Feature scaling with `StandardScaler`
- Correlation analysis using a heatmap
- Class imbalance handling using balanced class weights and `scale_pos_weight`
- Multiple model training and comparison
- Confusion matrix and classification report evaluation
- Learning curve analysis
- SHAP-based explainability for XGBoost
- Model and scaler saving using `joblib`
- Chunk-based dataset handling for large-scale data

## Models Used

### 1. Random Forest
A tree-based ensemble model trained with balanced class weights and multiple estimators.

### 2. XGBoost
An optimized gradient boosting model trained with class imbalance support using `scale_pos_weight`.

### 3. LightGBM
A fast gradient boosting model trained with balanced class weights for efficient classification.

### 4. SVM Pipeline
A scalable SVM approach built with:
- `MinMaxScaler`
- `Nystroem` kernel approximation
- `SGDClassifier`

## Workflow

1. Load the NF-UQ-NIDS-v2 dataset  
2. Drop irrelevant columns  
3. Separate features and target label  
4. Clean missing and infinite values  
5. Scale the feature values  
6. Analyze feature correlation  
7. Split data into training and testing sets  
8. Train and evaluate multiple models  
9. Plot confusion matrices and learning curves  
10. Apply SHAP for feature explainability  
11. Save trained models and scaler for reuse  

## Repository Contents

- `intrusion-runned_akashnaik_final_file(2).ipynb` — Main notebook
- `random_forest_model.joblib` — Saved Random Forest model
- `xgb_model.joblib` — Saved XGBoost model
- `lgb_model.joblib` — Saved LightGBM model
- `svm_model.joblib` — Saved SVM pipeline model
- `scaler.joblib` — Saved preprocessing scaler
- `dataset_heatmap.png` — Feature correlation heatmap

## Requirements

- Python 3.8+
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- xgboost
- lightgbm
- shap
- joblib

## Installation

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost lightgbm shap joblib
```

## Usage

Open the notebook and run the cells in order:

```bash
jupyter notebook
```

Then open the main notebook file and execute all cells to reproduce preprocessing, model training, evaluation, and saved outputs.

## Output

The project generates:
- Classification reports
- Confusion matrices
- Learning curves
- SHAP summary plot
- Saved trained models
- Saved scaler file

## Notes

- The dataset is large, so the project includes memory-conscious processing.
- The notebook also uses separate test chunks for additional evaluation.
- The code is focused on practical IDS classification and model comparison.

## Author

Akash Naik
