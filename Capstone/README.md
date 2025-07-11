---
## Overview

This project predicts loan default risk to help financial institutions make smarter lending decisions. Using advanced machine learning techniques, it classifies borrowers into three risk tiers—Low, Medium, 
and High—so the business can reduce bad loans, protect profits, and serve customers more effectively.
---
## Business Problem

Predicting loan defaults is a critical challenge for banks and financial institutions, as it directly impacts profitability, risk management, and the ability to offer future credit. 
When too many borrowers fail to repay their loans, lenders face financial losses, reduced liquidity, and increased lending restrictions. These defaults can also damage investor confidence and weaken customer trust.
---
## **Goal:** Identify borrowers likely to default that are in 'High Risk' category before loan approval.

This project applies machine learning models to borrower data—like income, spending, credit behavior etc. to classify loan applicants as:
- Low Risk 
- Medium Risk 
- High risk
---    
## **Business Value:**
- This data-driven approach helps lenders reduce losses, improve efficiency, and ensure fair, consistent, and inclusive lending decisions.
  - Reduce financial losses from defaults.
  - Approve more good loans confidently.
  - Optimize pricing strategies for medium-risk borrowers.
  - Comply with regulatory requirements using explainable models.
---

## Data Overview

- **Dataset Size:** ~10 K records
- **Features Used:** 41
- **Target Variable:** `risk_category` (High, Medium, Low)

---

## Data Preprocessing

- Applied extensive **feature engineering** to create meaningful new variables for modeling.
- Dropped columns with **more than 85% missing values** to reduce noise and improve data quality.
- Handled missing values using **mode imputation, fill NA, or -1 placeholders** depending on feature type and business logic.
- Applied **logarithmic transformations** to features such as income, installment, and interest rate to reduce skewness and improve model performance.
- Performed **feature scaling** using StandardScaler to normalize numeric variables.
- Conducted **data visualization** to understand distributions and relationships among variables.
- Calculated a new **Risk Category** column by consolidating five different statuses from the original 'Loan Status' field.
- Applied both **One-Hot Encoding** and **Label Encoding** to convert categorical variables into numerical format suitable for machine learning.
- Performed **feature selection** to retain the most relevant variables for modeling.
- Addressed dataset imbalance using **Synthetic Minority Oversampling Technique (SMOTE)** to improve model sensitivity to minority classes.


## Dataset Overview

Dataset has following features and additionally feature engineering created additional features
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
---
### Feature Engineering
- installment_to_income
- credit_utilization_rate
- credit_history_length
- high_utilization_flag
- verified_income_flag
- delinq_ratio
- balance_to_loan_ratio
- paid_pct

---
Key features used for modeling include:
- balance_to_loan_ratio
- interest_rate
- log_interest_rate
- total_credit_utilized
- debt_to_income
- credit_utilization_rate
- total_credit_limit
- annual_income
- total_debit_limit
- months_since_last_credit_inquiry
- public_record_bankrupt
- num_collections_last_12m
- num_historical_failed_to_pay

---

## Models Implemented

- Random Forest with SMOTE
- XGBoost with Class Weights and Threshold Tuning
- Keras Neural Network Baseline
- Ensemble Pipelines combining:
  - XGBoost
  - Keras Neural Networks
  - Class balancing (SMOTE)
  - Threshold Grid Search
  - Hyperparameter Tuning
---
**Best Model:**  
Ensemble pipeline (M9) with:
- Macro F1 ~0.91
- High recall and precision for high-risk borrowers
- Excellent balance across all classes

---

## Model Performance

### Summary table comparing key models:

| **Model** | **Accuracy** | **Macro F1** | **High Recall** | **Low Recall** | **Medium Recall** |
|-----------|-------------:|-------------:|----------------:|---------------:|------------------:|
| M1 – Random Forest Baseline + SMOTE                   | 0.96 | 0.91 | 0.77 | 1.00 | 0.95 |
| M2 – XGBoost Baseline + Class Weights + Threshold Tuning            | 0.93 | 0.86 | 0.89 | 0.99 | 0.72 |
| M3 – Keras Baseline               | 0.91 | 0.83 | 0.64 | 0.99 | 0.85 |
| M4 – Ensemble: XGBoost + Keras Neural Network + class weights                   | 0.90 | 0.78 | 0.93 | 0.98 | 0.48 |
| M5 – Ensemble: XGBoost + Keras Neural Network + class weights & soft voting                   | 0.82 | 0.72 | 0.92 | 0.86 | 0.53 |
| M6 – Ensemble: XGBoost + Keras Neural Network + SMOTETomek        | 0.79 | 0.67 | 0.93 | 0.83 | 0.44 |
| M7 – Ensemble (XGB + Keras)       | 0.95 | 0.91 | 0.78 | 1.00 | 0.93 |
| M8 – Full Ensemble Pipeline: XGBoost + Keras + SMOTE + Class Weights + Grid Search     | 0.95 | 0.91 | 0.79 | 1.00 | 0.93 |
| M9 – Full Ensemble Pipeline: XGB + Keras + SMOTE + Grid Search + Hyperparameter Tuning **(BEST MODEL)**  | 0.96 | 0.91 | 0.79 | 1.00 | 0.93 |

---

## Business Interpretation of Risk

| **Risk Level** | **Description** | **Business Approach** |
|----------------|-----------------|-----------------------|
| **Low Risk** | Strong credit history, stable income, low debt. Very likely to repay. | Approve confidently at competitive rates. |
| **Medium Risk** | Some warning signs like higher debt or recent credit inquiries. | Lend with safeguards: higher rates, smaller loans, collateral. |
| **High Risk** | Significant red flags (e.g. high debt, past defaults, bankruptcy). | Decline or approve only with strict conditions. |

---

## Communication to Stakeholders

Model insights are presented in business-friendly formats to support decision-making:

- **Risk Scores** expressed on a 0–100 scale for easy interpretation.
- **Probability of Default**, providing a clear percentage risk estimate (e.g. “17% chance of default”).
- **Risk Tiers** categorizing borrowers into Low, Medium, or High risk for streamlined policy decisions.
- **Key Drivers of Risk**, explained using SHAP values to show which factors influence individual predictions.
- **Actionable Recommendations**, offering practical next steps such as adjusting loan amounts, interest rates, or collateral requirements based on predicted risk.

