# Profit-Optimized Credit Risk Model

End-to-end credit risk modeling project that predicts borrower default probability and optimizes loan approvals using expected profit. Integrates PD, LGD, EAD, amortized loan cash flows, and financial feature engineering to simulate real-world lending decisions.

---

## Overview

This project builds a credit underwriting model that predicts borrower default risk and determines loan approval decisions based on **expected profitability rather than simple default prediction**.

The model integrates core financial risk modeling concepts used in real lending systems:

- **Probability of Default (PD)**
- **Loss Given Default (LGD)**
- **Exposure at Default (EAD)**
- **Amortized loan cash flow modeling**

Instead of rejecting borrowers purely based on predicted default risk, the system evaluates whether issuing a loan is **expected to generate positive profit after accounting for potential credit losses**.

---

## Project Goals

- Predict borrower **probability of default**
- Model **expected credit losses**
- Simulate **real-world lending decisions**
- Optimize loan approvals based on **profitability**

---

## Pipeline

The model follows a simple idea: a loan should be approved if the **expected profit from the loan is positive**.

To estimate this, the system combines three components that are commonly used in credit risk modeling.

| Component | What it represents |
|----------|-------------------|
Probability of Default (PD) | The chance that the borrower will default on the loan |
Loss Given Default (LGD) | The fraction of the loan likely lost if default occurs |
Exposure at Default (EAD) | The amount of money exposed to loss (the loan principal) |

Once these are estimated, the model calculates the expected profit of issuing the loan using the loan’s interest payments and the potential credit loss.

Instead of simply rejecting borrowers with high default risk, the model evaluates whether the interest earned compensates for the risk taken.

---

## Financial Modeling Framework

Expected loan profit is calculated using:

```
Expected Profit =
(1 − PD) × Interest Income
− PD × LGD × Exposure at Default
```

Where:

**PD**  
Predicted probability that the borrower defaults.

**LGD**  
Estimated percentage of the loan lost if default occurs.

**EAD**  
Loan principal exposed to loss.

**Interest Income**  
Interest earned through the amortized payment schedule if the borrower fully repays.

This mirrors simplified versions of models used in **consumer lending, credit cards, and structured finance**.

---

## Feature Engineering

Several financial risk indicators were engineered to improve model performance.

| Feature | Description |
|-------|-------------|
LoanToIncome | Loan size relative to borrower income |
PaymentToIncome | Monthly payment burden relative to income |
CreditScore × DTI | Interaction between credit quality and debt burden |
InterestBurden | Loan interest relative to borrower income |
CreditLinesPerYearEmployed | Credit utilization relative to employment stability |

These features help capture **borrower repayment stress and financial leverage**.

---

## Dataset

The dataset contains borrower-level loan application information including:

- Age
- Income
- Loan Amount
- Credit Score
- Months Employed
- Number of Credit Lines
- Interest Rate
- Loan Term
- Debt-to-Income Ratio
- Education
- Employment Type
- Marital Status
- Mortgage Status
- Dependents
- Loan Purpose
- Co-signer Presence

Each record includes a **Default indicator** showing whether the borrower ultimately defaulted.

---

## Model Performance

| Metric | Value |
|------|------|
AUC | ~0.75 |
KS Statistic | ~0.39 |
Approval Rate | ~75% |
Default Rate (Approved Loans) | ~8% |

The model successfully separates high-risk borrowers while maintaining profitable lending decisions.

---

## Evaluation Metrics

Several evaluation techniques were used:

**ROC Curve (AUC)**  
Measures ranking quality of predicted default probabilities.

**Precision–Recall Curve**  
Evaluates model performance on identifying default events.

**Calibration Curve**  
Checks whether predicted probabilities match actual default rates.

**KS Statistic**  
Measures separation between defaulting and non-defaulting borrowers.

**Profit Curve**  
Shows how total expected profit changes as approval thresholds vary.

---

## Model Comparison

Two models were evaluated:

**Logistic Regression**

- Strong probability calibration
- High interpretability
- Industry standard for credit scoring

**XGBoost**

- Slightly improved predictive power
- More complex model structure
- Less interpretable

Logistic regression was retained as the primary model due to its **interpretability and stability in credit risk modeling**.

---

## Technologies Used

- Python
- Pandas
- NumPy
- NumPy Financial
- Scikit-Learn
- XGBoost
- Matplotlib

---

## Future Improvements

Possible extensions include:

- **Survival analysis for default timing**
- **More sophisticated LGD modeling**
- **Macroeconomic stress testing**
- **Scorecard-style credit model**
- **Web interface for borrower evaluation**

---

## Author

Developed as a personal project exploring **machine learning applications in financial risk modeling and lending decision systems**.
