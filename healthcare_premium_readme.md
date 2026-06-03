# 🏥 Healthcare Insurance Premium Prediction Engine

[![Streamlit App](https://img.shields.io/badge/Streamlit-Demo-FF4B4B?style=for-the-badge&logo=Streamlit&logoColor=white)](https://share.streamlit.io/azadahmed1/ml-project-premium-prediction)
[![GitHub License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)
[![Python Version](https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=Python&logoColor=white)](https://python.org)

An end-to-end Machine Learning regression platform designed to automate and optimize actuarial insurance underwriting. Trained on **50,000+ consumer records**, this system leverages advanced data preprocessing, outlier detection, multicollinearity elimination, and specialized **age-based dataset segmentation** to train highly accurate cost-prediction models (XGBoost, Ridge Regression, Linear Regression). 

Through rigorous tuning and cohort segmentation, the final models achieve an exceptional **98-99% prediction accuracy ($R^2$ score)**.

---

## 📈 Deployed Streamlit Application

The predictive model is fully serialized and deployed as an intuitive web calculator, allowing underwriters or customers to immediately estimate annual premium costs by inputting risk metrics (Age, BMI, Smoker status, and demographic flags).

👉 **[Launch the Live Premium Estimation Tool](https://share.streamlit.io/azadahmed1/ml-project-premium-prediction)**

---

## 🎯 Business Case & Impact

In the health insurance sector, underwriting premium pricing must be extremely precise:
*   **Under-pricing** leads to massive financial losses on high-risk policy claims.
*   **Over-pricing** drives customers to competitor platforms, hurting customer acquisition.

This project implements an automated, real-time premium pricing engine that accurately maps historical risk factors (like obesity and high-risk habits) to actual policy pricing, reducing administrative overhead and human pricing bias.

---

## ⚙️ Advanced Data Engineering Pipeline

Tabular healthcare datasets often suffer from extreme outliers, skewed distributions, and highly correlated variables. The engineering pipeline is structured as follows:

### 1. Robust Outlier Handling & Cleaning
*   Analyzed insurance charges and demographic distributions.
*   Implemented statistical outlier boundaries (Interquartile Range - IQR) to isolate and clean anomaly records that would otherwise bias linear models.

### 2. Multi-Collinearity Elimination (VIF Analysis)
*   Calculated **Variance Inflation Factor (VIF)** across demographic features to identify and eliminate highly redundant variables.

### 3. High-Fidelity Categorical Encoding & Scaling
*   Implemented One-Hot Encoding for categorical features (Region, Sex, Smoker status).
*   Applied Robust/Standard Scaling to continuous variables (BMI, Age) to prevent neural/linear model bias toward high-magnitude features.

### 4. Specialized Age-Based Segment Models (Our Competitive Edge)
*   **The Problem:** Actuarial costs exhibit highly non-linear volatility in older age brackets, leading to high prediction errors (RMSE) for standard global regression fits.
*   **The Solution:** Segmented the primary dataset by age cohorts and trained custom segment-specific sub-models. This approach significantly stabilized prediction variance and dramatically increased prediction accuracy in the 50+ age demographic.

---

## 🤖 Model Exploration & Actuarial Tuning

We evaluated multiple regression architectures to compare linear baseline interpretations against tree-based ensembles:
*   **Linear Regression:** Serving as a baseline statistical control.
*   **Ridge Regression (L2 Regularization):** Preventing overfitting by penalizing high-magnitude coefficients.
*   **XGBoost Regressor:** Our champion model, capturing complex non-linear actuarial hazards.

### 🔬 Hyperparameter Optimization
Model tuning was performed using **RandomizedSearchCV** to locate the optimal balance of tree depth, learning rate, and estimator counts, yielding up to **99% test set validation**.

### 📦 Production-Ready Serialization
Optimized scalers and pre-trained segment models were exported utilizing **Joblib**, enabling instant pipeline deserialization for low-latency web applications.

---

## 🛠️ Installation & Local Usage

To clone and run this predictive calculator locally:

### 1. Clone the Repository
```bash
git clone https://github.com/azadahmed1/ml-project-premium-prediction.git
cd ml-project-premium-prediction
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
├── data/                    # Historical actuarial datasets
├── notebooks/               # EDA, Outlier cleaning, & Model tuning notebooks
├── saved_models/            # Serialized joblib pipelines (scalers, encoders, estimators)
├── src/                     # Core python preprocessors
├── app.py                   # Deployed Streamlit frontend calculator
├── requirements.txt         # Production libraries
└── README.md                # Project documentation
```
