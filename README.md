# -End-to-End-Credit-Risk-Scoring-Explainable-ML-System
Project Overview

This project implements an end-to-end credit risk scoring system to predict the probability of customer default within a two-year horizon. The solution is designed from a real-world banking and financial risk perspective, emphasizing data quality, model reliability, explainability, and production readiness rather than accuracy alone.

The pipeline processes raw financial data, applies advanced preprocessing and feature engineering, evaluates multiple machine learning models, calibrates predicted probabilities, and provides explainable risk insights suitable for business and regulatory use.

Business Problem

Financial institutions must identify customers who are likely to default in order to:

Reduce credit losses

Optimize approval and rejection decisions

Prioritize high-risk customers for monitoring or intervention

Since defaults are rare events, the problem is highly imbalanced. The objective is therefore to rank customers by risk and capture the maximum number of defaulters in the highest-risk segments, rather than maximizing accuracy.

Dataset Description

Approximately 150,000 training records and 100,000 test records

Each record represents a single customer

Features include:

Credit utilization

Delinquency history (30–59, 60–89, 90+ days past due)

Income and debt ratios

Number of credit lines and loans

Demographic information

The target variable indicates whether a customer experienced serious delinquency within two years.

Methodology & Pipeline
1. Data Quality Analysis

Identified missing values, invalid entries, and extreme outliers

Detected heavy skewness in financial variables

Verified target imbalance (~6–7% default rate)

2. Missing Value Imputation

Compared Mean, Median, KNN, MICE, and Random Forest imputation

Evaluated methods using distribution similarity metrics

Selected Random Forest–based imputation to preserve realistic income distributions

3. Outlier Treatment

Applied two-sided winsorization (1st–99th percentile)

Preserved high-risk customers while controlling extreme noise

Created capped-value indicator flags to retain risk signals

4. Feature Engineering

Aggregated delinquency behavior into total past-due measures

Created income-normalized and debt-based risk indicators

Added behavioral flags such as high utilization and zero income

5. Train–Validation Strategy

Stratified 80–20 split to preserve default distribution

Strict prevention of data leakage across preprocessing steps

Model Development

Multiple algorithms were evaluated:

Logistic Regression

Random Forest

Extra Trees

Gradient Boosting

XGBoost (standard and weighted)

LightGBM

CatBoost

KNN

Models were compared using business-oriented metrics:

ROC-AUC

Recall at top risk percentiles

Precision at top risk percentiles

Lift

Random Forest delivered the best balance between predictive performance and high-risk capture.

Probability Calibration & Threshold Optimization

Applied isotonic regression to calibrate predicted probabilities

Selected optimal decision thresholds based on F1-score and business trade-offs

Ensured probabilities are reliable for real credit decisions

Explainability & Risk Interpretation

Used SHAP (SHapley Additive exPlanations) for model interpretability

Provided:

Global feature importance

Customer-level risk driver explanations

Enabled transparent, auditable, and regulator-friendly decisions

Results Summary

ROC-AUC: ~0.89

Lift in top 5% risk segment: ~7×

Captured a significant share of defaulters with minimal customer coverage

Calibrated probabilities suitable for deployment

Production Readiness

Modular and reproducible pipeline

Saved model and configuration artifacts

Configurable decision thresholds

Ready for batch or real-time scoring

Easily extensible for monitoring and retraining

Technology Stack

Python

Pandas, NumPy

Scikit-learn

XGBoost, LightGBM, CatBoost

SHAP

Matplotlib, Seaborn

Future Improvements
