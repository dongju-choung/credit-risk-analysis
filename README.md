# Credit Risk Analysis

[View the analysis notebook](./credit_risk_grading.ipynb)

This project examines two decisions in lending: which credit card accounts to review when capacity is limited, and whether a proposed secured corporate loan fills a genuine funding need.

## 1. Credit Card Default Monitoring

I compared logistic regression and gradient boosting on the same evaluation sample, ranking accounts by predicted next-month default risk.

| Share of accounts reviewed | Logistic regression | Gradient boosting | Additional defaults captured |
|---|---:|---:|---:|
| 5% | 215 | 227 | +12 |
| 10% | 409 | 413 | +4 |
| 15% | 539 | 560 | +21 |

At the 10% cutoff, gradient boosting replaced 91 of the 600 accounts on the review list. The accounts it added included 57 defaults, while the accounts it removed included 53. It captured 28 more defaults among accounts with one to three months of recorded delinquency and 24 fewer among accounts with four to six months. Both models left all 504 defaults with no recorded delinquency in the prior six months outside their top 600.

I would validate these patterns on a later cohort before recommending a model change. The results also prompted a question from my lending experience: what can we learn about a borrower's ability to repay before missed payments appear?

## 2. Corporate Credit Underwriting

Using Fastenal’s FY2025 Form 10-K, I evaluated a hypothetical USD 250M secured term loan. I modeled how a collection delay would affect first-year repayment coverage and near-term liquidity, then separately estimated recovery from receivables under assumed collateral conditions.

I recommended deferring approval until a 13-week cash-flow forecast showed whether a funding gap remained after accounting for available capacity under the existing revolver. The case illustrates how a borrower can have modeled capacity to repay while the need for a new loan remains unproven.

## Data Sources

- [UCI Default of Credit Card Clients dataset](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients)
- [Fastenal FY2025 Form 10-K](https://www.sec.gov/Archives/edgar/data/815556/000081555626000009/fast-20251231.htm)
