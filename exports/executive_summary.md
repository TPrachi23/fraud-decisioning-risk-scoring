# Fraud Decisioning & Risk Scoring Framework (Credit Card / Customer Fraud)

## What this does
This project builds a production-style fraud decisioning framework:
- Train a supervised model to estimate fraud probability for transactions
- Convert probability into a **0–1000 risk score**
- Apply thresholds to produce decisions: **APPROVE / REVIEW / DECLINE**

## Dataset
Synthetic but realistic credit card transactions including:
- Amount, merchant category, country
- Card present vs not present
- Velocity (1h/24h), device change
- Failed logins (ATO proxy), travel flag
- Customer tenure and prior chargebacks

## Model
- Logistic Regression (interpretable baseline)
- Class imbalance handled via `class_weight="balanced"`

## Test Performance (probability model)
- ROC-AUC: **0.7705**
- Average Precision (PR-AUC): **0.5974**

## Decisioning Logic (risk score thresholds)
- 0–300: APPROVE
- 301–700: REVIEW
- 701–1000: DECLINE

## Precision-based decline calibration (optional)
A probability threshold targeting precision ~0.80 produced:
- Threshold: **0.8650**
- Achieved precision: **0.8000**
- Achieved recall: **0.1012**

## Outputs
- `outputs/scored_test_transactions.csv`
- `outputs/decision_summary.csv`
- `outputs/fraud_rate_by_decision.csv`
- Charts: ROC, PR, confusion matrix, risk score distribution
