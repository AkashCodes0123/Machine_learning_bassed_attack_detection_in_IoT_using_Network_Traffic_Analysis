# Machine Learning-Based Attack Detection in IoT Using Network Traffic Analysis

> An intelligent, machine learning-driven Intrusion Detection System (IDS) designed to identify and classify cyber threats in resource-constrained Internet of Things (IoT) network environments.

## 📖 Overview

The rapid proliferation of IoT devices has expanded the attack surface for cyber threats. Because IoT devices are often resource-constrained, deploying traditional on-device security tools is impractical. This project addresses that challenge by building a scalable, machine learning-based IDS that analyzes NetFlow traffic to classify network behavior as either **Benign (0)** or **Attack (1)**. 

### Key Features
*   Robust data preprocessing and feature scaling pipelines.
*   Comparative analysis of state-of-the-art tree-based models and SVMs.
*   Advanced handling of severe class imbalance in network traffic.
*   Model interpretability and feature importance extraction using SHAP.

---

## 📊 Dataset

The models are trained and evaluated using the **NF-UQ-NIDS-v2** dataset, a comprehensive collection of modern, real-world network traffic flows.

*   **Source:** [University of Queensland eSpace](https://espace.library.uq.edu.au/view/UQ:631a24a)
*   **Total Records:** 1,048,575
*   **Raw Features:** 46
*   **Features Utilized:** 39
*   **Problem Type:** Binary Classification
*   **Train/Test Split:** 80% / 20%

### Class Distribution
The dataset is inherently imbalanced, reflecting real-world network threat landscapes. Algorithmic class weighting is applied during training to mitigate bias.
*   **Benign (0):** 347,249 samples (33.1%)
*   **Attack (1):** 701,326 samples (66.9%)

---

## ⚙️ Methodology

The end-to-end machine learning pipeline consists of the following stages:

1.  **Data Ingestion:** Processing raw NF-UQ-NIDS-v2 network flow records.
2.  **Preprocessing & Engineering:** 
    *   Removal of topology-specific identifiers (IP addresses, ports) to prevent overfitting.
    *   Replacement of missing (`NaN`) and infinite (`Inf`) values with zero.
    *   Feature standardization using `StandardScaler`.
    *   Data type conversion to `float32` and extreme outlier clipping for computational efficiency.
3.  **Exploratory Data Analysis (EDA):** Class distribution tracking and feature correlation mapping.
4.  **Model Training:** Parallelized training across four distinct algorithms.
5.  **Evaluation:** Multi-metric performance validation (Accuracy, Precision, Recall, F1-score) and learning curve analysis.
6.  **Explainability:** Utilizing SHAP (SHapley Additive exPlanations) to interpret model decisions.

---

## 🧠 Models Evaluated

*   **Random Forest:** An ensemble of 200 decision trees utilizing `class_weight='balanced'` to establish a strong, generalized baseline for tabular network data.
*   **XGBoost:** A highly scalable gradient boosting framework configured with `scale_pos_weight` to manage class imbalance, achieving the lowest false positive rate.
*   **LightGBM:** A gradient boosting model utilizing a leaf-wise tree growth strategy, providing the optimal trade-off between computational speed and predictive accuracy on large datasets.
*   **Support Vector Machine (SVM):** Implemented via a `Nystroem` kernel approximation and `SGDClassifier` to adapt distance-based margin calculations for a massive dataset.

---

## 📈 Results

| Model | Accuracy | Precision | Recall | F1-Score |
| :--- | :---: | :---: | :---: | :---: |
| **Random Forest** | 98% | 0.98 | 0.98 | 0.98 |
| **XGBoost** | 98% | 0.98 | 0.98 | 0.98 |
| **LightGBM** | 98% | 0.98 | 0.97 | 0.97 |
| **SVM (Nystroem)** | 88% | 0.90 | 0.88 | 0.88 |

**Key Findings:**
*   **Random Forest** and **XGBoost** delivered the highest overall accuracy and generalization, effectively minimizing critical false negatives.
*   **LightGBM** demonstrated near-identical predictive performance while drastically reducing training times.
*   **SVM** underperformed relative to the ensemble models, as the necessary kernel approximation restricted its capacity to capture highly complex, non-linear network patterns.

---

## 🔍 Model Explainability (SHAP)

To ensure the IDS is transparent and actionable for security analysts, SHAP analysis was applied to the XGBoost model. The top five most critical features driving the detection of malicious traffic were identified as:

1.  `DURATION_IN`
2.  `L7_PROTO`
3.  `TCP_WIN_MAX_IN`
4.  `IN_BYTES`
5.  `TCP_FLAGS`

---

## 💻 Installation and Usage

### Prerequisites
Ensure you have Python 3.8+ installed. The following libraries are required:
```text
numpy
pandas
scikit-learn
xgboost
lightgbm
shap
matplotlib
seaborn
joblib
