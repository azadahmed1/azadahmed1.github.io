# 📊 Credit Risk Classification & Default Prediction System

[![Streamlit App](https://img.shields.io/badge/Streamlit-Demo-FF4B4B?style=for-the-badge&logo=Streamlit&logoColor=white)](https://share.streamlit.io/azadahmed1/Credit-Risk-Model-Azad)
[![GitHub License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)
[![Python Version](https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=Python&logoColor=white)](https://python.org)

An end-to-end Machine Learning classification system designed to predict credit default risk for retail lending underwriters. Using a historical dataset of **50,000+ loan records**, this pipeline integrates rigorous feature engineering, multicollinearity elimination, weight-of-evidence (WOE) encoding, and class imbalance handling to train robust classifiers (XGBoost, Random Forest, Logistic Regression). 

By implementing custom decision threshold tuning, the final deployed solution achieves a **94% default prediction Recall rate**, successfully exceeding the target business SLA of **90%**.

---

## 📈 Deployed Streamlit Application

The final model has been packaged and deployed as a real-time interactive credit scoring interface. Lending officers can input applicant demographics, loan details, and bureau history to receive instant default risk evaluations.

👉 **[Launch the Live Underwriting Platform](https://share.streamlit.io/azadahmed1/Credit-Risk-Model-Azad)**

---

## 🎯 Business Problem & Objective

For financial institutions, loan defaults represent major revenue leakages. A credit risk model must strike a delicate balance:
1.  **Minimize False Negatives (Maximize Recall):** Flagging high-risk borrowers who would default (SLA Requirement: >90% Recall).
2.  **Maintain Acceptable Precision:** Avoiding over-rejection of credit-worthy applicants to preserve lending volume.

This project implements an end-to-end data-driven underwriter assistant that predicts the probability of default and highlights key risk drivers (e.g., Credit Score, Debt-to-Income, and Utilization rates).

---

## ⚙️ Data Engineering & Preprocessing Pipeline

Tabular financial datasets are notoriously noisy, highly correlated, and heavily imbalanced. The preprocessing pipeline consists of:

### 1. Multi-Source Integration & Cleaning
*   Merged raw datasets containing customer credit histories, bureau metrics, and historical loan terms (50,000+ records).
*   Resolved missing values and handled data-entry anomalies.

### 2. Multi-Collinearity Elimination (VIF Analysis)
*   Computed the **Variance Inflation Factor (VIF)** for all numerical features to detect high multi-collinearity.
*   Iteratively dropped highly redundant features (VIF > 5), stabilizing the linear coefficient estimates of baseline models.

### 3. Feature Selection (WOE & IV Analysis)
*   Applied **Weight of Evidence (WOE)** encoding to categorical variables to measure the strength of individual feature bins in separating defaults from non-defaults.
*   Computed the **Information Value (IV)** for each feature. Handled selection by retaining medium-to-strong predictors ($0.1 \le IV \le 0.5$) and dropping weak or highly volatile features.

### 4. Class Imbalance Resolution
*   The dataset exhibited a classic default class skew.
*   Handled the imbalance by designing a hybrid sampling approach utilizing **Random Under-Sampling (RUS)** on the majority class and **Synthetic Minority Over-sampling Technique (SMOTE)** on the minority class to prevent classifier bias.

---

## 🤖 Model Exploration & Hyperparameter Tuning

We evaluated three separate classifier architectures:
*   **Logistic Regression:** Serving as a highly interpretable statistical baseline.
*   **Random Forest Classifier:** Capturing non-linear interactions across tabular fields.
*   **XGBoost (eXtreme Gradient Boosting):** Our champion ensemble method.

### 🔬 Hyperparameter Optimization with Optuna
We built a highly targeted search space using **Optuna** to optimize tree depth, learning rates, regularization parameters (L1/L2), and class weight ratios. 

---

## 📊 Key Evaluation Metrics

Standard accuracy is a deceptive metric for imbalanced fraud/default classification. Instead, we evaluated our systems using:
*   **ROC-AUC Score:** Evaluated general class separation capacity.
*   **KS (Kolmogorov-Smirnov) Statistic:** Measured the maximum separation between the cumulative distribution of defaults vs. non-defaults.
*   **Precision-Recall Curve & Threshold Tuning:** By shifting the classification decision boundary from `0.5` to a tuned threshold, we achieved a **94% Recall rate** on the holdout test set, capturing bad borrowers aggressively.

---

## 🛠️ Installation & Local Usage

To run this project and the Streamlit interface locally:

### 1. Clone the Repository
```bash
git clone https://github.com/azadahmed1/Credit-Risk-Model-Azad.git
cd Credit-Risk-Model-Azad
```

### 2. Set Up Virtual Environment & Dependencies
```bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Run the Streamlit App
```bash
streamlit run app.py
```

---

## 📂 Repository Structure

```text
├── data/                    # Sample data assets
├── notebooks/               # Jupyter Notebooks for VIF, WOE, IV, & Training
├── models/                  # Serialized XGBoost/scaler joblib assets
├── src/                     # Source pipeline components (preprocessing, encoding)
├── app.py                   # Streamlit underwriting application file
├── requirements.txt         # Production dependencies
└── README.md                # Project documentation
```
