Fraud Decisioning & Risk Scoring Framework
Credit Card / Customer Fraud Analytics (Machine Learning – Python)
📌 Overview

This project implements a production-style fraud decisioning and risk scoring framework for credit card transactions.
It simulates how real-world fraud systems score transactions, apply decision thresholds, and balance fraud prevention vs customer experience.

The framework combines:

Transaction-level behavioral risk features

Supervised machine learning for fraud probability estimation

Risk score calibration (0–1000 scale)

Operational decisioning: APPROVE / REVIEW / DECLINE

🎯 Business Problem

Credit card fraud teams must make real-time decisions under uncertainty:

Decline fraudulent transactions quickly

Minimize false positives that frustrate customers

Route ambiguous cases for manual review

This project demonstrates how a fraud risk engine supports these decisions using data-driven scoring and policy thresholds.

🧠 Framework Architecture
Raw Transactions
      ↓
Feature Engineering
(amount, velocity, device change,
 failed logins, geo risk, tenure)
      ↓
Fraud Probability Model
(Logistic Regression)
      ↓
Risk Score (0–1000)
      ↓
Decisioning Engine
APPROVE | REVIEW | DECLINE

📊 Dataset

Synthetic but realistic credit card transaction data, generated to avoid privacy or compliance issues.

Key Features

Transaction amount

Merchant category (MCC-like)

Transaction country (geo risk)

Card-present vs card-not-present

Device change indicator

Velocity (1-hour & 24-hour)

Failed login attempts (ATO proxy)

Account tenure

Prior chargeback history

Target variable:

is_fraud (binary, imbalanced)

🤖 Model & Techniques

Model: Logistic Regression (interpretable baseline)

Class imbalance: Handled via class_weight="balanced"

Feature preprocessing:

Standard scaling (numeric)

One-hot encoding (categorical)

Evaluation metrics:

ROC-AUC

Precision-Recall AUC

Confusion Matrix

Decision-bucket analysis

🔢 Risk Scoring & Decisioning
Risk Score

Fraud probability converted into a 0–1000 risk score

Higher score → higher fraud risk

Decision Thresholds
Risk Score	Decision
0–300	APPROVE
301–700	REVIEW
701–1000	DECLINE

This mirrors real fraud operations where only the riskiest transactions are hard-declined.

📈 Model Performance (Test Set)

ROC-AUC: ~0.77

PR-AUC: ~0.60

Decisioning evaluation shows:

High precision for declined transactions

Majority of legitimate transactions correctly approved

Review bucket absorbs uncertainty to reduce customer friction

📂 Repository Structure
fraud-decisioning-risk-scoring/
│
├── data/
│   └── synthetic_fraud_transactions.csv
│
├── outputs/
│   ├── scored_test_transactions.csv
│   ├── decision_summary.csv
│   ├── fraud_rate_by_decision.csv
│   ├── risk_score_distribution.png
│   ├── confusion_matrix_decline_vs_actual.png
│   ├── roc_curve.png
│   └── pr_curve.png
│
├── fraud_decisioning_framework.ipynb
├── requirements.txt
└── README.md

📁 Key Outputs

Scored transactions: risk score + decision per transaction

Decision summary: fraud counts by decision bucket

Fraud rate by decision: validates risk separation

Visualizations: ROC, PR curve, confusion matrix, score distribution

🛠️ Tech Stack

Python

Pandas, NumPy

Scikit-learn

Matplotlib

Jupyter Notebook / Google Colab

🚀 How to Run

Open the notebook in Jupyter or Google Colab

Run all cells sequentially

Outputs will be saved automatically to the data/ and outputs/ folders

💡 Extensions (Future Work)

Cost-based optimization (fraud loss vs customer friction)

Gradient Boosting / Tree-based models

Realistic fraud rate calibration (<1%)

Customer-level risk aggregation

Real-time streaming simulation

👩‍💼 Use Case Alignment

This project is relevant for roles in:

Fraud Analytics

Risk Strategy

Financial Crimes / AML

Trust & Safety

Payments & Credit Risk
