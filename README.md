## Project Overview & Problem Statement

**Client:** *PowerGrid Central* – a regional electricity provider responsible for maintaining a stable, 24/7 electricity supply to residential, commercial, and industrial sectors.

**Problem:**
PowerGrid Central currently forecasts electricity demand using simple historical averages. While easy to implement, this method often fails to capture non-linear and abrupt demand changes—especially during extreme weather events or behavioral shifts. This leads to:

- Over-generation: Wasted fuel and operational costs.
- Under-generation: Costly emergency power purchases and risk of brownouts.
- Poor outage planning: Maintenance scheduling becomes inefficient and risky.

### Project Goal
Develop a machine learning-based time series forecasting model to:
- Enable smarter generation scheduling aligned with actual demand.
- Reduce reliance on emergency purchases and lower operational costs.
- Improve outage and maintenance planning.
- Avoid over- and under-generation to enhance financial efficiency.
- Provide insights into key demand drivers (time, seasonality, temperature).

![Dashboard Preview](images/churn.gif)

## Setup and Data Loading

**Goal:** Initialize the environment, load the dataset, and inspect for data quality issues.

### Steps:
- Import essential libraries: \`pandas\`, \`numpy\`, \`matplotlib\`, \`seaborn\`, \`sklearn\`.
- Load \`AEP_hourly.csv\` into a DataFrame.
- Perform initial inspection:
  - \`.head()\`, \`.info()\`, \`.describe()\` to explore structure.
  - \`.isnull().sum()\` and \`.duplicated()\` to identify cleaning needs.

## Exploratory Data Analysis (EDA)

**Objective:** Discover temporal patterns like trends, seasonality, and anomalies.

### a. Datetime Preprocessing
- Convert and extract features: \`hour\`, \`day\`, \`weekday\`, \`month\`, \`year\`.

### b. Target Variable Overview (\`MW_Demand\`)
- Plot full time series and demand distribution.
- Spot skewness, spikes, and outliers.

### c. Seasonality Patterns
- Create time-based features for exploration.
- Analyze:
  - Yearly demand shifts.
  - Weekly differences (weekdays vs weekends).
  - Daily/Hourly consumption cycles.

**Outcome:** Clear insight into demand patterns to guide feature engineering and model selection.

## Data Preparation and Feature Engineering

**Objective:** Transform raw time series into a model-ready dataset.

### a. Feature Engineering
Engineered features:
- Time-based: Hour, Day of Week, Month, Year
- Contextual: Season (Winter, Spring, Summer, Fall)
- Aggregated: Daily average demand, optional rolling averages

### b. Feature Preparation and Encoding
- Apply One-Hot Encoding to categorical variables like season and day_of_week.
- Ensure model compatibility and avoid ordinal bias.

**Outcome:** A rich, structured dataset ready for model training.

## Model Training and Evaluation

**Objective:** Train and evaluate forecasting models on future unseen data.

### a. Define Features and Target
- Target (\`y\`): \`MW_Demand\`
- Features (\`X\`): Time and contextual variables

### b. Time-Based Train-Test Split
- Train: Data before 2015
- Test: Data from 2015 onward

### c. Model Training and Comparison
Models:
- Random Forest Regressor – strong baseline, handles non-linearities well
- XGBoost Regressor – gradient boosting model with high performance

### d. Final Evaluation and Model Selection
Metrics:
- R Squared(R2)
- Mean Squared Error
- Root Mean Squared Error(RMSE)
- Mean Absolute Error(MAE)
- Mean Absoulte Percentage Error(MAPE)

The model with the lowest test error will be selected.

**Outcome:** A robust and generalizable model for forecasting energy demand.

## Conclusion and Final Assessment

### a. Summary of Model Performance
After comparing both models on the same test set:
- XGBoost Regressor achieved higher R², lower MSE, and better MAPE on unseen data.
- Random Forest slightly overfitted and had a larger error gap between train and test.

### b. Model Strengths and Limitations
- XGBoost: Excellent at generalizing unseen demand patterns.
- Random Forest: Easier to interpret but prone to overfitting in this case.

### c. Final Recommendation and Business Impact
- Deploy XGBoost for future energy forecasting due to superior generalization.
- Implement monitoring for model drift and periodic retraining.

**Outcome:**
A high-performing forecasting solution ready for deployment. It supports better operational decisions, minimizes cost inefficiencies, and increases the stability of the power grid.
