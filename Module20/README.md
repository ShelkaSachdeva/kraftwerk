# Capstone Project - Loan Default Prediction

**Credit Risk Modeling with ML and AI (Module 20.1)**

---

## Project Overview

This project focuses on predicting credit risk categories for loan applicants, aiming to classify loans as **High, Medium, or Low Risk**. 
It leverages machine learning techniques, feature engineering, and handling class imbalance to support financial institutions in assessing
lending risk effectively.

---

## Data Overview

- **Dataset Size:** ~10 K records
- **Features Used:** 41
- **Target Variable:** `risk_category` (High, Medium, Low)

---

## Data Preprocessing

- Applied Feature Engineering
- Missing values handled via mode imputation
- Dropped columns that were > 75 % null
- Outliers capped using IQR technique.
- Feature scaling applied using StandardScaler.
- Synthetic Minority Oversampling Technique (SMOTE) applied to balance the dataset.
- Visualized data
- Calculated Risk Catefory column using 5 different statuses from 'Loan Status' column
- Performed One Hot Encoding and Label Encoding
---

## Features Used

The following 41 features were included for model building initially:

- balance
- balance_to_loan_ratio
- paid_pct
- paid_total
- paid_principal
- paid_interest
- log_installment
- installment
- annual_income
- total_credit_limit
- loan_amount
- total_credit_utilized
- installment_to_income
- debt_to_income
- total_debit_limit
- paid_late_fees
- log_annual_income
- log_interest_rate
- credit_utilization_rate
- interest_rate
- total_credit_lines
- num_satisfactory_accounts
- open_credit_lines
- months_since_last_credit_inquiry
- num_cc_carrying_balance
- num_total_cc_accounts
- inquiries_last_12m
- credit_history_length
- num_open_cc_accounts
- earliest_credit_line
- accounts_opened_24m
- num_active_debit_accounts
- account_never_delinq_percent
- emp_length
- months_since_last_delinq
- months_since_90d_late
- current_installment_accounts
- issue_month_Jan-2018
- num_mort_accounts
- term
Note: Plan is to further reduce these features using Logistic Regression - L1 Regularization as next steps.
---

## Models Tested with SNOTE ((Synthetic Minority Over-sampling Technique)) and/or Class Weights

- Logistic Regression
- Random Forest
- SVC
- Decision Tree
- Gradient Boosting
- AdaBoost
- Voting Classifier Ensemble

---
### Class Distribution Before SMOTE:

| Class   | Count |
|---------|-------|
| Low     | 6,562 |
| Medium  | 74    |
| High    | 51    |

Due to significant imbalance, SMOTE was used to balance classes for model training.

## Voting Classifier Performance

Example result (Voting Classifier with SMOTE and class weights):

| Class   | Precision | Recall | F1-Score | Support | Summary |
|---------|-----------|--------|----------|---------|---------|
| High    | 0.58      | 0.64   | 0.61     | 22      | Model moderately detects High risk but misses some cases. |
| Low     | 0.99      | 0.98   | 0.98     | 2813    | Excellent detection of Low risk cases. |
| Medium  | 0.06      | 0.13   | 0.08     | 31      | Medium risk remains difficult to detect effectively. |
| **Accuracy** |           |        | **0.96** | 2866    | Overall high accuracy, mainly driven by Low class performance. |

**Macro Avg F1:** 0.56  
**Weighted Avg F1:** 0.97

---

## Challenges

- Extreme Class Imbalance:** Medium and High classes were severely underrepresented.
- Medium Class Performance: Despite resampling and weighting, Medium class remains challenging to predict.

---

## Next Steps

- Advanced sampling strategies (e.g. SMOTE-ENN).
- Ensemble methods tuned specifically for minority class detection.
- Feature engineering to create variables highlighting Medium risk patterns.

---


## Author

- Shelka Sachdeva
- Capstone Project - Credit Risk Modeling with ML and AI 

---
