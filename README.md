# Salifort Motors HR Analytics: Employee Attrition Prediction

## Project Overview

[cite_start]This project is a capstone for a data analytics program, focusing on providing data-driven insights for the Human Resources (HR) department of Salifort Motors, a large consulting firm[cite: 3, 5]. [cite_start]The HR department is seeking to improve employee satisfaction and retention but lacks direction on how to use the data they have collected[cite: 16, 17].

[cite_start]The primary business question is: **"What's likely to make the employee leave the company?"** [cite: 19]

[cite_start]The goal of this project is to analyze the provided HR dataset, build a predictive model to identify employees likely to leave, and offer actionable suggestions to the HR department to help increase employee retention[cite: 18, 21, 23].

## Dataset

[cite_start]The project utilizes an HR dataset containing 15,000 employee records and 10 features (prior to cleaning)[cite: 25]. The features include:

* [cite_start]`satisfaction_level`: Employee-reported job satisfaction (0-1) [cite: 28]
* [cite_start]`last_evaluation`: Score from the last performance review [cite: 28]
* [cite_start]`number_project`: Number of projects contributed to [cite: 28]
* [cite_start]`average_monthly_hours`: Average hours worked per month [cite: 28]
* [cite_start]`time_spend_company`: Number of years with the company [cite: 28]
* [cite_start]`Work_accident`: Whether the employee had a work accident (0 or 1) [cite: 28]
* [cite_start]`left`: Whether the employee left the company (0 or 1) - **This is the target variable.** [cite: 28]
* [cite_start]`promotion_last_5years`: Whether the employee was promoted in the last 5 years (0 or 1) [cite: 28]
* [cite_start]`Department`: The employee's department [cite: 28]
* [cite_start]`salary`: The employee's salary (low, medium, or high) [cite: 28]

## Project Workflow (PACE Methodology)

[cite_start]This project follows the PACE (Plan, Analyze, Construct, Execute) data analytics framework[cite: 12].

### 1. Plan

[cite_start]The initial stage involved understanding the business scenario and the needs of the primary stakeholder, the Salifort Motors HR department[cite: 15, 16, 30]. [cite_start]The objective was clearly defined: to identify key factors driving employee attrition to inform retention strategies[cite: 19, 21].

### 2. Analyze (Data Cleaning & EDA)

This stage focused on data exploration, cleaning, and visualization.

**Data Cleaning:**
* [cite_start]**Column Renaming:** Column names were standardized to `snake_case` for consistency (e.g., `average_montly_hours` became `avg_monthly_hours`, `left` became `left_company`)[cite: 140, 148, 153].
* [cite_start]**Missing Values:** A check confirmed there were no missing values in the dataset [cite: 160, 162-181].
* [cite_start]**Duplicates:** The dataset contained 3,008 duplicate rows [cite: 189][cite_start], which were subsequently removed[cite: 329].
* [cite_start]**Final Dataset:** The cleaned dataset (`df1`) consists of 11,991 unique employee records[cite: 351].
* [cite_start]**Outliers:** Outliers were examined using boxplots, particularly for the `years_at_company` variable[cite: 354, 359].

**Exploratory Data Analysis (EDA):**
* [cite_start]**Attrition Rate:** In the cleaned dataset, 1,991 employees (16.6%) left the company, while 10,000 (83.4%) stayed[cite: 451, 456, 458, 463].
* **Visualizations:** Various plots were generated to understand variable relationships:
    * [cite_start]A scatterplot of `avg_monthly_hours` vs. `satisfaction_level`, segmented by `left_company` [cite: 468-471].
    * [cite_start]Histograms comparing salary levels (`low`, `medium`, `high`) for short-tenured (<7 years) and long-tenured (>=7 years) employees [cite: 490-501].
    * [cite_start]Bar plots showing the relationship between `left_company` and variables like `promotion_last_five_years` [cite: 556][cite_start], `work_accident` [cite: 568-570][cite_start], and `department`[cite: 601, 603].
* [cite_start]**Initial Insight:** The strongest initial correlation observed was between `satisfaction_level` and whether an employee `left_company`[cite: 623].

### 3. Construct (Modeling & Evaluation)

[cite_start]This phase involved feature engineering and building predictive models for the binary classification task[cite: 644].

**Preprocessing:**
* [cite_start]**Ordinal Encoding:** The `salary` feature was ordinally encoded (`low`: 1, `medium`: 2, `high`: 3) [cite: 723-725].
* [cite_start]**One-Hot Encoding:** The categorical `department` feature was one-hot encoded[cite: 757, 1072].
* [cite_start]**Scaling:** For the Logistic Regression model, all features were scaled using `MinMaxScaler` [cite: 758-760].

**Models & Tuning:**
[cite_start]Two models were built and tuned using `GridSearchCV` to optimize for the F1-score[cite: 47, 895, 900, 1092, 1098]:

1.  **Logistic Regression:**
    * [cite_start]**Best F1-Score:** 0.54 [cite: 928]
    * [cite_start]**Best Parameters:** `{'C': 1.0, 'class_weight': {0: 0.2, 1: 0.8}, 'l1_ratio': 0.5, 'penalty': 'l1', 'solver': 'saga'}` [cite: 930-935]
    * [cite_start]**Confusion Matrix:** The model produced 380 True Positives, 120 False Negatives, 470 False Positives, and 2000 True Negatives[cite: 1043, 1044, 1050, 1051].

2.  **Random Forest Classifier:**
    * [cite_start]**Best F1-Score:** 0.94 [cite: 1118]
    * [cite_start]**Best Parameters:** `{'criterion': 'gini', 'max_depth': 8, 'max_features': 'sqrt', 'min_samples_leaf': 1, 'min_samples_split': 5, 'n_estimators': 350}` [cite: 1120-1125]
    * [cite_start]**Confusion Matrix:** This model performed exceptionally well, yielding 460 True Positives, 40 False Negatives, 6 False Positives, and 2500 True Negatives[cite: 1154, 1156, 1160, 1161].

### 4. Execute (Results & Recommendations)

The final stage involved interpreting the best-performing model (Random Forest) and deriving actionable insights.

**Feature Importance:**
[cite_start]The Random Forest model identified the following features as the most predictive of employee attrition, in descending order of importance[cite: 1167, 1175, 1187]:
1.  [cite_start]`satisfaction_level` [cite: 1188]
2.  [cite_start]`projects` [cite: 1189]
3.  [cite_start]`years_at_company` [cite: 1190]
4.  [cite_start]`avg_monthly_hours` [cite: 1191]
5.  [cite_start]`last_eval_score` [cite: 1192]

## Key Findings & Recommendations

Based on the model results, the following key recommendations were proposed to the HR department:

1.  [cite_start]**Prioritize Employee Satisfaction:** `satisfaction_level` is the single most predictive feature[cite: 1231]. [cite_start]The company should immediately invest in understanding and improving the factors that contribute to employee satisfaction to boost retention[cite: 1231].
2.  **Optimize Project Workload:** The number of projects (`projects`) is the second most important factor. [cite_start]Further analysis suggests that assigning 3-4 projects per employee may be the "best middle ground" to balance productivity and prevent burnout[cite: 1232].

## Tools & Libraries Used

* [cite_start]**Data Manipulation:** `pandas` [cite: 43][cite_start], `numpy` [cite: 42]
* [cite_start]**Data Visualization:** `matplotlib` [cite: 45][cite_start], `seaborn` [cite: 46]
* [cite_start]**Machine Learning:** `scikit-learn` (specifically `LogisticRegression` [cite: 48][cite_start], `RandomForestClassifier` [cite: 48][cite_start], `train_test_split` [cite: 47][cite_start], `GridSearchCV` [cite: 47][cite_start], `MinMaxScaler` [cite: 47][cite_start], `OneHotEncoder` [cite: 47][cite_start], and `metrics` [cite: 47])
