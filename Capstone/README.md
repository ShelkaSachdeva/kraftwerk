NEW 

## Overview

This project predicts loan default risk to help financial institutions make smarter lending decisions. Using advanced machine learning techniques, it classifies borrowers into three risk tiers—Low, Medium, 
and High—so the business can reduce bad loans, protect profits, and serve customers more effectively.

## Business Problem

Predicting loan defaults is a critical challenge for banks and financial institutions, as it directly impacts profitability, risk management, and the ability to offer future credit. 
When too many borrowers fail to repay their loans, lenders face financial losses, reduced liquidity, and increased lending restrictions. These defaults can also damage investor confidence and weaken customer trust.

## **Goal:** Identify borrowers likely to default that are in 'High Risk' category before loan approval.

This project applies machine learning models to borrower data—like income, spending, credit behavior etc. to classify loan applicants as:
- Low Risk 
- Medium Risk 
- High risk
    
## **Business Value:**
- This data-driven approach helps lenders reduce losses, improve efficiency, and ensure fair, consistent, and inclusive lending decisions.
  - Reduce financial losses from defaults.
  - Approve more good loans confidently.
  - Optimize pricing strategies for medium-risk borrowers.
  - Comply with regulatory requirements using explainable models.

## 📊 Dataset Overview

Key features used for modeling include:
- Debt-to-Income Ratio
- Interest Rate
- Credit Utilization Rate
- Total Credit Used and Limits
- Annual Income
- Public Records (Bankruptcies, Collections, Historical Failures to Pay)
- Loan Terms (amount, duration)

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

**Best Model:**  
Ensemble pipeline (M9) with:
- Macro F1 ~0.91
- High recall and precision for high-risk borrowers
- Excellent balance across all classes

---

## Model Performance

| Model | Macro F1 | High F1 | Medium F1 | Low F1 |
|-------|----------|---------|-----------|--------|
| Random Forest + SMOTE | 0.91 | 0.86 | 0.88 | 0.99 |
| XGBoost Ensemble | 0.91 | 0.86 | 0.88 | 0.99 |
| Keras Baseline | 0.83 | 0.73 | 0.77 | 0.98 |

---

## Business Interpretation of Risk

| **Risk Level** | **Description** | **Business Approach** |
|----------------|-----------------|-----------------------|
| **Low Risk** | Strong credit history, stable income, low debt. Very likely to repay. | Approve confidently at competitive rates. |
| **Medium Risk** | Some warning signs like higher debt or recent credit inquiries. | Lend with safeguards: higher rates, smaller loans, collateral. |
| **High Risk** | Significant red flags (e.g. high debt, past defaults, bankruptcy). | Decline or approve only with strict conditions. |

---

## Communication to Stakeholders

Model results are communicated as:
- **Risk Scores** (0–100)
- **Probability of Default** (e.g. “17% chance of default”)
- **Risk Tiers** (Low, Medium, High)
- **Key Factors Driving Risk** via SHAP explanations
- **Actionable Recommendations** for lending strategies
