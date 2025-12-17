# A-Machine-Learning-Approach-for-Predicting-Familial-Sporadic-Disease-Cases-Using-Clinical-Symptoms

1. # Project Overview

This project builds and evaluates machine learning models that classify disease cases as Familial or Sporadic based on routinely collected clinical features. The goal is to support early risk stratification and guide clinical decision-making, especially in settings where genetic testing is limited or delayed.

2. Problem Statement

Identifying whether a case is familial or sporadic can influence:

genetic counseling and family screening,

monitoring intensity and follow-up,

interpretation of clinical risk.

However, this distinction is not always obvious from clinical presentation. This project uses supervised ML to learn patterns from symptom combinations and clinical context.

3. Objectives
Main Objective

Develop a robust ML classifier to predict Case Type (Familial vs Sporadic) from symptoms and clinical characteristics.

Specific Objectives

Prepare and clean the dataset for modeling (missing values, encoding, scaling).

Train baseline and advanced models and compare performance.

Evaluate using clinically meaningful metrics (ROC-AUC, recall, precision, F1).

Explain model decisions using feature importance (and optionally SHAP).

Produce a reproducible pipeline suitable for deployment.

4. Dataset Description

File: dataset-uci.xlsx
Target column: Case Type
Columns (features):

Identifier: Unnamed: 0 (drop)

Clinical context: Tumour Case, Age of Mother, Age of Father, Age at First Diagnosis

Symptoms (binary/clinical):
Café au lait (CLS), Axillary Freckles, Inguinal Freckles, Lisch Nodules,
Dermal Neurofibromins, Plexiform Neurofibromins, Optic Glioma, Skeletal Dysplasia,
Learning Disability, Hypertension, Astrocytoma, Hamartoma, Scoliosis, Other Symptoms

5. Methodology
5.1 Data Preprocessing

Drop Unnamed: 0

Separate target y = Case Type

Handle missing values:

numeric ages → median imputation

binary symptoms → most frequent (mode) imputation (if needed)

Scaling:

scale numeric columns: Age of Mother, Age of Father, Age at First Diagnosis

keep binary symptom features as-is

Train/Test split:

stratified split (e.g., 80/20) to preserve class distribution

5.2 Model Development

Baseline (interpretable):

Logistic Regression (class_weight="balanced")

Stronger (performance-focused):

Random Forest

Gradient Boosting (HistGradientBoostingClassifier)

Probability calibration (optional but recommended for clinical scoring):

CalibratedClassifierCV (isotonic or sigmoid)

5.3 Evaluation Metrics

Report (test set + CV):

ROC-AUC

F1-score

Recall (Sensitivity) for Familial class (often most important)

Precision

Confusion Matrix

(Optional) Calibration metrics: Brier Score

5.4 Explainability

Logistic Regression: coefficients (direction + magnitude)

Tree/boosting: permutation importance

Optional: SHAP for global + patient-level explanations

6. Deliverables

Cleaned ML pipeline (preprocessing + model)

Model comparison table (CV and test performance)

Confusion matrix + ROC curve

Feature importance/explainability output

Final report (Methods, Results, Discussion, Limitations)

Reproducible codebase (notebook + scripts)

7. Tools & Tech Stack

Python, pandas, numpy

scikit-learn

matplotlib

8. Project Structure (recommended)
familial-vs-sporadic-ml/
│── data/
│   └── dataset-uci.xlsx
│── notebooks/
│   └── 01_modeling.ipynb
│── src/
│   ├── train.py
│   ├── evaluate.py
│   └── utils.py
│── outputs/
│   ├── models/
│   └── figures/
│── README.md
│── requirements.txt
