# Bank Customer Churn Prediction With Ensemble Learning

---

## Overview

This project applies ensemble learning techniques to predict whether a bank customer will churn (exit) or stay, using a cleaned real-world dataset of 10,000 bank customers. Four classifiers are built and compared: a baseline Decision Tree, Random Forest, AdaBoost, and a Stacking ensemble.

---

## Dataset

**Source:** [Bank Customer Churn Prediction — Kaggle](https://www.kaggle.com/datasets/murilozangari/customer-churn-from-a-bank)

The original dataset contains 10,000 rows and 14 columns. The version used in this project has been pre-cleaned as follows:

- Removed non-predictive columns: `RowNumber`, `CustomerId`, `Surname`
- One-hot encoded `Geography` and `Gender` into numeric columns

**Final shape:** 10,000 rows × 12 columns (11 features + 1 target)

**Target variable:** `Exited` — `0` = Stayed (7,963), `1` = Exited (2,037)


---

### Ensemble Models, Evaluation & Comparison
- Split data: 80% train / 20% test, with stratification
- The ensemble models were trained with the following configurations:

| Model | Key Parameters |
|---|---|
| Decision Tree | `max_depth=4`, `random_state=42` |
| Random Forest | `n_estimators=200`, `random_state=42` |
| AdaBoost | `n_estimators=200`, `learning_rate=0.8`, `random_state=42` |
| Stacking | RF (150 trees) + AdaBoost (100 trees) → Logistic Regression meta-learner, `cv=5` |

### Model Comparison

| Model | Test Accuracy | F1 Score |
|---|---|---|
| Decision Tree | 0.8515 | 0.5367 |
| Random Forest | 0.8630 | 0.5772 |
| AdaBoost | 0.8600 | 0.5692 |
| **Stacking** | **0.8660** | **0.5988** |

### Key Insight

The Stacking model achieved the best accuracy (0.8660) and F1 score (0.5988). Ensemble methods outperform a single decision tree because they combine multiple weak learners, reducing variance and improving predictive stability. By aggregating diverse models, each capturing different patterns in the data, ensembles make more robust predictions than any individual classifier.

---

## Top Features (Random Forest)

The most important features for predicting churn, ranked by importance score:

1. Age
2. EstimatedSalary
3. Balance
4. CreditScore
5. NumOfProducts
6. Tenure
7. IsActiveMember
8. Geography_Germany

---
