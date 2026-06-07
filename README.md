# Telecom Customer Churn Prediction

An end-to-end data science project predicting customer churn for a telecom company — from raw data exploration to machine learning predictions on 24,000+ unseen records.

---

## Project Overview

Customer churn is one of the most critical business problems in the telecom industry. Acquiring a new customer costs significantly more than retaining an existing one. This project builds a complete churn prediction pipeline — from data cleaning and feature engineering to model training, evaluation, and deployment on a new dataset.

**Business Question:** Which customers are likely to leave, and what are the key drivers of churn?

---

## Project Structure

```
├── notebooks/
│   ├── BigDataProject-Part-A.ipynb   # EDA, feature engineering, model training
│   └── BigDataProject-Part-B.ipynb   # MongoDB pipeline + churn prediction
├── data/
│   ├── churn.csv                      # Original dataset (7,043 customers)
│   └── Part-B-Churn-Prediction.csv    # Final predictions (24,218 customers)
├── presentation/
│   └── Presentation-BigData.ppsx      # Project presentation with business insights
└── README.md
```

---

## Part A — EDA, Feature Engineering & Model Training

**Dataset:** 7,043 telecom customers with 26 features including demographics, services, contract details, and billing information.

### Key Steps

**Data Cleaning**
- Identified and resolved `total_charges` misclassification (string → numeric)
- Imputed missing values based on business logic: new customers (`tenure = 0`) received `total_charges = 0`
- Unified inconsistent categorical values (`No internet service` / `No phone service` → `No`)

**Feature Engineering**
- Created `tenure_segment` groups (0–12, 13–24, 25–36, 37–48, 49–60, 61–72 months)
- Applied three encoding strategies:
  - One-Hot Encoding: gender, internet service, payment method
  - Ordinal Encoding: tenure segment, contract type
  - Label Encoding: all binary yes/no features

**Models Trained & Compared**

| Model | Test Accuracy |
|---|---|
| Benchmark (majority class) | ~73% |
| Decision Tree | ~79% |
| Random Forest | ~79% |
| KNN | ~78% |

**Winner:** Random Forest (`n_estimators=9`, `max_depth=7`) — best test accuracy with lowest overfitting gap.

---

## Part B — MongoDB Pipeline & Prediction on Unseen Data

**Dataset:** 24,218 customer records stored in a MongoDB collection with nested `Services` documents.

### Key Steps

- Connected to MongoDB and queried all valid documents using MQL
- Flattened nested `Services` subdocuments into separate feature columns
- Applied identical preprocessing pipeline as Part A
- Applied trained Random Forest model to predict churn on unseen data
- Exported results to CSV for business use

### Prediction Results

| Outcome | Count | Percentage |
|---|---|---|
| Predicted to Stay | 18,288 | ~75.5% |
| Predicted to Churn | 5,930 | ~24.5% |

---

## Key Business Insights

**1. Contract type is the strongest churn predictor**
Customers on month-to-month contracts churn significantly more than those on one- or two-year contracts.
→ Offer incentives to migrate short-term customers to longer contracts.

**2. Fiber optic users show the highest churn rate**
Despite being a premium service, fiber optic customers are more likely to leave than DSL users.
→ Investigate service quality and pricing satisfaction among fiber optic users.

**3. New customers are the highest-risk segment**
Customers with tenure under 12 months represent the most vulnerable group.
→ Invest in onboarding experience and early retention programs.

---

## Tech Stack

| Tool | Usage |
|---|---|
| Python | Core language |
| pandas | Data manipulation and cleaning |
| scikit-learn | Machine learning models |
| matplotlib / seaborn | Data visualization |
| MongoDB / pymongo | NoSQL database and querying |
| Jupyter Notebook | Development environment |

---

## Dataset

Based on the [IBM Telco Customer Churn dataset](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) — a widely used benchmark for churn prediction tasks.

---

## Author

**Valeria Barabanova**
Junior Data Analyst | Tel Aviv, Israel
[LinkedIn](https://linkedin.com/in/valeriabarabanova) · [GitHub](https://github.com/barabanovalera1-ui)
