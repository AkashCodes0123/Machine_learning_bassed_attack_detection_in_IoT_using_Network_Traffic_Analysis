# Machine Learning-Based Attack Detection in IoT Using Network Traffic Analysis

This project presents a machine learning-based Intrusion Detection System (IDS) for IoT network traffic using the **NF-UQ-NIDS-v2** dataset. The goal is to classify traffic as **Benign (0)** or **Attack (1)** using multiple machine learning models and compare their performance on a large-scale, imbalanced dataset.

## Overview

IoT devices are resource-constrained and often cannot run traditional security tools. This project addresses that challenge by building a scalable ML-based IDS that can detect malicious network traffic using flow-based features.

The project includes:

- Data preprocessing and cleaning
- Feature scaling and correlation analysis
- Model training and evaluation
- Explainability using SHAP
- Model saving for future reuse

## Dataset

**Dataset Name:** NF-UQ-NIDS-v2  
**Source:** University of Queensland eSpace  
**Link:** https://espace.library.uq.edu.au/view/UQ:631a24a

### Dataset Details

- **Total Records:** 1,048,575
- **Raw Features:** 46
- **Features Used:** 39
- **Train/Test Split:** 80% / 20%
- **Problem Type:** Binary classification
- **Class Distribution:**
  - Benign (0): 347,249
  - Attack (1): 701,326

The dataset is imbalanced, so class weighting is used during model training.

## Methodology

The pipeline followed in this project is:

1. **Data Collection**
   - NF-UQ-NIDS-v2 network flow records are used for training and testing.

2. **Preprocessing**
   - IP and port columns are removed
   - Missing and infinite values are replaced with zero
   - Features are scaled using `StandardScaler`
   - Data is converted to `float32` for memory efficiency
   - Outliers are clipped to reduce instability

3. **Exploratory Data Analysis**
   - Class distribution is analyzed
   - Feature correlation heatmap is generated

4. **Model Training**
   - Random Forest
   - XGBoost
   - LightGBM
   - SVM using `Nystroem` approximation + `SGDClassifier`

5. **Evaluation**
   - Accuracy
   - Precision
   - Recall
   - F1-score
   - Confusion Matrix
   - Learning Curve

6. **Explainability**
   - SHAP is applied to XGBoost to identify important features

7. **Model Saving**
   - All trained models and the scaler are saved using `joblib`

## Models Used

### Random Forest
- Uses 200 decision trees
- `class_weight='balanced'`
- Strong generalization on tabular network data

### XGBoost
- Gradient boosting model
- `scale_pos_weight` used to handle class imbalance
- Best false positive performance among the tested models

### LightGBM
- Leaf-wise tree growth strategy
- Fast and efficient on large datasets
- Strong speed-accuracy tradeoff

### SVM
- Implemented using `MinMaxScaler`, `Nystroem`, and `SGDClassifier`
- Useful for large-scale approximation of kernel-based classification
- Lower performance compared to tree-based models

## Results

| Model | Accuracy | Precision | Recall | F1-Score |
|------|----------:|----------:|-------:|---------:|
| Random Forest | 98% | 0.98 | 0.98 | 0.98 |
| XGBoost | 98% | 0.98 | 0.98 | 0.98 |
| LightGBM | 98% | 0.98 | 0.97 | 0.97 |
| SVM | 88% | 0.90 | 0.88 | 0.88 |

### Key Observations

- **Random Forest** gave the best overall balance of precision, recall, and generalization.
- **XGBoost** achieved the lowest false positives.
- **LightGBM** offered the best speed-accuracy tradeoff.
- **SVM** underperformed because the kernel approximation had limited capacity for this large dataset.

## Explainability

SHAP analysis on XGBoost showed that the most important attack indicators include:

- `DURATION_IN`
- `L7_PROTO`
- `TCP_WIN_MAX_IN`
- `IN_BYTES`
- `TCP_FLAGS`

These features help explain how the model distinguishes between benign and malicious traffic.

## Requirements

```bash
numpy
pandas
scikit-learn
xgboost
lightgbm
shap
matplotlib
seaborn
joblib


git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
pip install -r requirements.txt

Usage
Open the notebook files in Jupyter Notebook or JupyterLab.
Run the preprocessing cells.
Train the models.
Evaluate the results.
Load the saved models for inference if needed.

.
├── intrusion-runned_akashnaik_final_file(2).ipynb
├── Model test_akashnaik_final(1).ipynb
├── Machine_Learning_Based_Attack_Detection_in_IoT.pdf
├── README.md
└── models/
    ├── random_forest_model.pkl
    ├── xgboost_model.pkl
    ├── lightgbm_model.pkl
    ├── svm_model.pkl
    └── scaler.joblib


Conclusion
This project demonstrates that tree-based machine learning models are highly effective for IoT intrusion detection on tabular network traffic data. With proper preprocessing, class imbalance handling, and explainability, the system becomes suitable for practical security applications.
Future Work


Multi-class attack classification


Real-time traffic detection


Deep learning models such as LSTM or CNN


Edge deployment for IoT devices


Federated learning across distributed networks


Reference
[1] University of Queensland, “NF-UQ-NIDS-v2 Dataset,” UQ eSpace. Available: https://espace.library.uq.edu.au/view/UQ:631a24a
[2] A. Naik et al., “Machine Learning-Based Attack Detection in IoT Using Network Traffic Analysis,” M.Sc. Computer Science, Sambalpur University, 2026.



