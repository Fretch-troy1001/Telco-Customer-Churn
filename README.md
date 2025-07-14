# Predicting Customer Churn: From Gut Feel to Data-Driven Precision

“For every new customer we gain, another quietly leaves.”

This was the pattern ConnectTel noticed in its quarterly reports. Growth was stagnant—not because of poor acquisition, but due to silent attrition. Customers weren't complaining. They were simply leaving.

Rather than treating this as a marketing issue, we reframed it as a predictive modeling challenge:

## What if we could know in advance who’s likely to churn—and why?

---

## Project Overview

This project uses machine learning to proactively identify customers most at risk of churn. The goal is not just prediction, but strategic intervention—empowering the business to act before customers leave.

**Business Value:**
- Focus retention campaigns only where it matters
- Avoid wasteful blanket discounts
- Improve customer lifetime value and operational efficiency

---

## Problem

- ConnectTel lacked insight into why customers were leaving.
- Traditional marketing was reactive, offering discounts too late or to the wrong people.
- The company needed a way to predict churn risk and understand what factors drive it.

---

## Approach

We followed a clean ML workflow using Python, Scikit-learn, and Pandas.

### 1. Data Inspection & Cleaning
- Loaded 1,000+ telecom customer records.
- Cleaned and converted `TotalCharges` from object to float.
- Mapped binary columns (like `Partner`, `Churn`) to numeric.
- Applied one-hot encoding to multi-category fields (e.g., `Contract`, `InternetService`).

### 2. Baseline Model – Logistic Regression
- Built a pipeline with scaling and logistic regression.
- Evaluated performance using precision, recall, and F1-score.
- Found major weakness in identifying churners (True class):
  - Recall (True): Only 52% – meaning 48% of churners were missed
  - Precision (True): 62% – 38% false alarms when targeting for retention

We needed better recall for churners to prevent customer loss.

### 3. Model Improvement – Random Forest with Grid Search
- Replaced the baseline with a RandomForestClassifier
- Used GridSearchCV to optimize hyperparameters for recall
- Final model performance:
  - Recall (True) improved to 81%
  - Precision dropped to 50%, but this was acceptable since the business goal was to catch as many churners as possible, even at the cost of some false positives

---

## Key Features Driving Churn

These features had the highest importance in predicting customer churn:

| Feature                           | Importance |
|----------------------------------|------------|
| `num__tenure`                    | 18.4%      |
| `Contract_Two year`              | 15.6%      |
| `InternetService_Fiber optic`    | 12.7%      |
| `num__TotalCharges`              | 10.8%      |
| `MonthlyCharges`                 | 8.1%       |
| `PaymentMethod_Electronic check`| 6.9%       |

Tenure was the strongest predictor. Short-term customers were far more likely to churn.  
Contracts and fiber-optic plans also contributed to churn risk—likely due to pricing or service experience.

---

## Result & Business Impact

- Recall on churners (True) jumped from 52% to 81%
- Reduced missed churners from nearly half to less than 1 in 5
- Enabled targeted retention actions (e.g., personalized offers or support calls)

---

## Strategic Value

This project isn’t just about plugging churn—it’s about shifting from reaction to prediction.

- Identify customers before they leave  
- Reduce churn costs  
- Focus retention budgets efficiently  

Instead of chasing lost customers, ConnectTel can now keep the ones who matter most.
