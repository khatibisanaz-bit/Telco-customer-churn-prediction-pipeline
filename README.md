# Telco Customer Churn Prediction Pipeline

End‑to‑end machine learning pipeline for predicting customer churn, including data preprocessing, feature engineering, model development, evaluation, and a lightweight API for real‑time predictions.

This project analyzes telecom customer behavior using the Telco Customer Churn dataset and builds a predictive pipeline to identify subscribers who are at high risk of leaving the service. The goal is to support data‑driven retention strategies and enable proactive business actions.

## Project Overview

Customer churn is a critical problem for subscription-based businesses such as telecom companies. In this project, machine learning models are used to analyze customer behavior and predict the probability of churn.

The project includes the full machine learning pipeline: data exploration, preprocessing, feature engineering, model training, evaluation, and prediction.

## Business Problem

These days customer churn is a critical challenge for subscription‑based and service‑driven businesses because losing existing customers directly impacts recurring revenue and long‑term growth. In addition, acquiring new customers is significantly more expensive than retaining current ones, and if high‑value customers leave, the company not only loses immediate revenue but also their future lifetime value. The objective of this project is to develop a predictive model that identifies customers at high risk of churn before they leave. By enabling early intervention through targeted retention strategies, the business can improve customer retention and protect long‑term revenue.

## Project Architecture

End‑to‑end ML pipeline:

1. Data ingestion
2. Data cleaning and preprocessing
3. Feature engineering
4. Model training and evaluation
5. Saving the best model
6. Real‑time prediction API (FastAPI)

## How to Run

Train the model:
python src/train_model.py

text

Make predictions:
python src/predict.py --input sample_input.json

text

Run API:
uvicorn api.main:app --reload

text

## Model Performance

The best model achieved:
- Accuracy: XX%
- F1 Score: XX%
- ROC‑AUC: XX%

(Replace with your real results when ready.)

## Key Insights

Top churn indicators:
- MonthlyCharges
- Contract type
- Tenure
- Internet service type

## Future Improvements

- Hyperparameter tuning with Optuna
- Experiment tracking using MLflow
- Deploying with Docker
- Adding a Streamlit UI dashboard
- Real‑time monitoring

## Architecture / ML Pipeline Diagram
                        ┌────────────────────────┐
                        │      Raw Dataset       │
                        │  (Telco Customer Data) │
                        └─────────────┬──────────┘
                                      │
                                      ▼
                         ┌────────────────────────┐
                         │   Data Ingestion       │
                         │  (load CSV → dataframe)│
                         └─────────────┬──────────┘
                                      │
                                      ▼
                    ┌───────────────────────────────────┐
                    │      Data Cleaning & Preprocessing │
                    │ - Handle missing values            │
                    │ - Encode categorical features      │
                    │ - Scale numerical features         │
                    └─────────────────────┬─────────────┘
                                          │
                                          ▼
                    ┌───────────────────────────────────┐
                    │        Feature Engineering         │
                    │ - Create new variables             │
                    │ - Remove irrelevant features       │
                    │ - Train/Test split                 │
                    └─────────────────────┬─────────────┘
                                          │
                                          ▼
                    ┌───────────────────────────────────┐
                    │         Model Training             │
                    │ - Logistic Regression              │
                    │ - Random Forest                    │
                    │ - XGBoost                          │
                    └─────────────────────┬─────────────┘
                                          │
                                          ▼
                    ┌───────────────────────────────────┐
                    │        Model Evaluation            │
                    │ - Accuracy / F1 / AUC              │
                    │ - Confusion Matrix                 │
                    │ - Select best model                │
                    └─────────────────────┬─────────────┘
                                          │
                                          ▼
                    ┌───────────────────────────────────┐
                    │         Model Export               │
                    │ Save best model → models/*.pkl     │
                    └─────────────────────┬─────────────┘
                                          │
                                          ▼
                    ┌───────────────────────────────────┐
                    │      Prediction API (FastAPI)      │
                    │ - Load model                       │
                    │ - Predict churn (JSON input)       │
                    └───────────────────────────────────┘
