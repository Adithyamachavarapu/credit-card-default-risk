# Credit Card Default Risk Analysis

A Python analysis of 30,000 credit card customers from a Taiwanese bank to find who is most likely to miss next month's payment. Includes data cleaning, segment analysis with statistical tests, and a logistic regression model scored on a held-out test set.

## What it does

The project answers three questions a card issuer's risk team would ask:
1. **Who defaults most?** — default rates by repayment status, credit limit, utilisation, age
2. **What warns early?** — which signals go with default, tested with chi-square and Mann-Whitney
3. **Who do we call first?** — a ranked list using 10 risk bands from a logistic regression model

## Data

- **Name:** Default of Credit Card Clients (Yeh and Lien, 2009)
- **Source:** UCI Machine Learning Repository
- **Licence:** CC BY 4.0
- **Size:** 30,000 customers, 25 columns
- **Period:** April to September 2005, plus October default flag
- **Currency:** New Taiwan dollars (NT$)

## Key results

| Metric | Value |
|--------|-------|
| Overall default rate | 22.1% (6,636 of 30,000) |
| 2+ months late in Sep default rate | 69.6% |
| Test AUC | 0.751 |
| Top 3 risk bands capture | 60.4% of all defaults (from 30% of customers) |
| Repayment status Cramer's V | 0.422 (strong) |
| Education Cramer's V | 0.073 (very weak) |

## Model details

- **Type:** Logistic regression (statsmodels)
- **Inputs (5):** September repayment status, months late out of 6, utilisation, credit limit (log2), age
- **Left out on purpose:** sex, education, marital status — they add almost nothing and using gender in credit decisions is unfair
- **Split:** 70/30 stratified (both have 22.12% default rate)

### Odds ratios

| Input | Odds ratio | Meaning |
|-------|-----------|---------|
| 2 months late in Sep | 4.2 | ~4x the odds vs paid in full |
| Each extra late month | 1.3 | +30% odds per month |
| Doubling credit limit | 0.83 | -17% odds |
| +10 points utilisation | 1.01 | Almost no effect once payment history is in |
| +10 years age | 1.06 | Small rise |

## Tools used

- pandas, NumPy — loading, cleaning, group-by tables
- SciPy — chi-square, Mann-Whitney U, Spearman correlation
- statsmodels — logistic regression with p-values and confidence intervals
- scikit-learn — train/test split, AUC, confusion matrix
- matplotlib — 8 charts, one shared colour file

## Limitations

- Taiwan, 2005 — behaviour and products have changed
- Six months of history only. No income, job, other loans or credit bureau data
- Some repayment status codes are undocumented
- Simple five-input model, no tuning, one split
- Correlation, not cause

## Dataset

UCI Machine Learning Repository. CC BY 4.0.
