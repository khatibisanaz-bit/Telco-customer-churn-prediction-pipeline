# Telco Customer Churn Prediction Kaggel Data Set

## Project Overview
The objective of this project is to predict customer churn using the IBM Telco Customer Churn dataset (Kaggle) while demonstrating a rigorous and reproducible machine learning workflow. The focus is not only predictive performance, but correct methodological design.

## Dataset

The project uses the **Telco Customer Churn** dataset, which contains **7,043 customer records** and **21 columns**.  
The target variable is **Churn**.  
The features include customer profile indicators, subscribed services, contract details, and billing information.  
This dataset does **not** contain detailed demographic or geographic attributes such as age, income, address, or location.

## Workflow
1. Data cleaning
   - replaced blank values in `TotalCharges`
   - converted `TotalCharges` to numeric
   - removed missing values
   - dropped `customerID`
   - encoded `Churn` as binary

2. Exploratory Data Analysis
   - churn distribution
   - churn by contract type
   - churn by tech support
   - monthly charges distribution by churn

3. Feature preparation
   - split data into features (`X`) and target (`y`)
   - detected numerical and categorical columns

4. Train/test split
   - used stratified split to preserve class proportions

5. Preprocessing and modeling
   - scaled numerical features with `StandardScaler`
   - encoded categorical features with `OneHotEncoder`
   - trained `LogisticRegression` with `class_weight='balanced'`

6. Evaluation
   - classification report
   - confusion matrix
   - ROC-AUC score
   - F1 score
   - recall
   - precision

## Methodology
1. Data Cleaning
Converted TotalCharges to numeric
Removed missing values
Dropped non-informative identifier (customerID)
Encoded target variable (Churn → 0/1)

2. Exploratory Analysis
Identified class imbalance
Analyzed churn across:
Contract type
Tech support
Monthly charges
This step guided modeling decisions (e.g., imbalance handling).

3. Experimental Design
To ensure methodological correctness:

Stratified Train/Test Split (80/20)
Clear separation of features (X) and target (y)
Automatic detection of numerical and categorical variables

4. Reproducible ML Pipeline
All preprocessing steps are encapsulated inside a Scikit‑Learn Pipeline to prevent data leakage.

Preprocessing (ColumnTransformer):

StandardScaler → numerical features
OneHotEncoder(drop='first', handle_unknown='ignore') → categorical features
Model:

Logistic Regression
class_weight='balanced' (handles class imbalance)
solver='liblinear'
random_state=42
This ensures that transformations are learned only from training data.

## Tech Stack
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-Learn

## Evaluation Metrics
Performance is evaluated using:

Classification Report
Confusion Matrix
ROC-AUC
F1 Score
Recall
Precision
Using multiple metrics ensures robust assessment under class imbalance.

## Architecture / ML Pipeline Diagram

Raw Dataset (IBM Telco Data)
        │
        ▼
Data Cleaning
        │
        ▼
Exploratory Data Analysis
        │
        ▼
Feature / Target Split
        │
        ▼
Feature Type Detection
        │
        ▼
Stratified Train/Test Split
        │
        ▼
ColumnTransformer
   ├── StandardScaler (Numerical)
   └── OneHotEncoder (Categorical)
        │
        ▼
Logistic Regression (Balanced)
        │
        ▼
Model Evaluation

