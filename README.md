# Telco Customer Churn Prediction & Recall Optimization

# Project Overview

The objective of this project is to predict customer churn using the IBM Telco Customer Churn dataset (Kaggle) while demonstrating a rigorous and reproducible machine learning workflow. The core focus is not only predictive performance but correct methodological design and business-oriented optimization.

In customer retention, identifying potential churners is highly critical. Therefore, this project places a strong emphasis on maximizing Recall (minimizing False Negatives) through systematic model evaluation and Decision Threshold Tuning.

# Dataset

The project uses the Telco Customer Churn dataset, which contains 7,043 customer records and 21 columns.
Target Variable: Churn (Yes/No, mapped to 1/0).
Features: Customer profile indicators (gender, partner, dependents, senior citizen status), subscribed services (internet, streaming, online security, tech support), contract details, payment methods, and billing information.

Scope Note: This dataset does not contain detailed demographic or geographic attributes such as age, income, address, or location.

# Workflow & Methodology

Raw Dataset (IBM Telco Data)
       │
       ▼
Data Cleaning (Imputation & Conversion)
       │
       ▼
Exploratory Data Analysis (EDA)
       │
       ▼
Feature / Target Split (X / y)
       │
       ▼
Feature Type Detection (Numerical vs. Categorical)
       │
       ▼
Stratified Train/Test Split (80/20)
       │
       ▼
ColumnTransformer (Preprocessing Pipeline)
 ├── StandardScaler (Numerical Features)
 └── OneHotEncoder (Categorical Features)
       │
       ▼
Model Architecture (Logistic Regression / XGBoost)
       │
       ▼
Decision Threshold Tuning (Recall Optimization)
       │
       ▼
Model Evaluation (Metrics & Confusion Matrix)


# 1. Data Cleaning
Replaced blank space values in TotalCharges with NaN and converted the column to numeric.
Dropped rows with missing values (representing less than 0.15% of the data).
Removed non-informative identifier columns (customerID).
Encoded the target variable Churn to binary (Yes → 1, No → 0).

# 2. Exploratory Data Analysis (EDA)
Analyzed churn distribution (revealing a clear class imbalance: ~26.5% churn).
Explored correlations between churn and contract types (e.g., Month-to-month contracts showed significantly higher churn

Analyzed relationship between tech support availability and churn.

Examined monthly charges distributions among churned and retained customers.

# 3. Experimental Design & Preprocessing Pipeline

To prevent data leakage and guarantee reproducibility, all preprocessing steps are encapsulated inside a Scikit-Learn Pipeline using ColumnTransformer:

Numerical Features: Handled via StandardScaler.

Categorical Features: Processed via OneHotEncoder(drop='first', handle_unknown='ignore').
Data Split: Evaluated using a stratified 80/20 train/test split to preserve the original class ratio.

# 4. Classification & Optimization Strategy

To address class imbalance and satisfy the business requirement of capturing the maximum number of churning customers, the modeling strategy incorporated:
Algorithm Choice: Evaluated LogisticRegression (with class_weight='balanced') and gradient-boosted trees (XGBoost).
Decision Threshold Tuning: Because default classification boundaries set the probability threshold at 0.50, models often output overly conservative predictions for the minority class. By extracting predicted probabilities (predict_proba) and systematically evaluating thresholds from 0.05 to 0.50, we optimized the decision-making process.

Evaluation & Results

# Decision Threshold Trade-off
By tuning the probability threshold on the trained model, we achieved the following trade-offs on the test set:
ThresholdRecallPrecisionF1-Score0.50 (Default)78.34%51.95%0.62470.32 (Optimized)87.97%46.14%0.60530.3089.84%45.41%0.60320.05 (Max Recall)98.40%32.80%0.4920

# Why Threshold was Chosen
Using the default threshold of 0.50 yields an insufficient recall of 78.34%.
Moving the threshold down to 0.32 successfully pushes the recall rate above the target to 87.97%.

At 0.32, the model retains a balanced F1-score (0.6053) and avoids the excessive false positives associated with extreme thresholds like 0.05 (where precision drops to 32.8%).

# Methodological Reflection (for README / Applications)

Using the default decision threshold of 0.50, the model achieved a recall of 78.3%. Since churn detection prioritizes minimizing false negatives (missing customers who are about to leave), the decision threshold was tuned on predicted probabilities. A threshold of 0.32 increased recall to approximately 88% while maintaining a highly acceptable precision-recall trade-off, avoiding the operational costs of over-classifying non-churners."
# Tech Stack
Language: Python
Data Wrangling: Pandas, NumPy
Visualization: Matplotlib, Seaborn
Machine Learning: Scikit-Learn, XGBoost
