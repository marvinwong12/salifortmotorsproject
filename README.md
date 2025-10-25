# Salifort Motors HR Analytics: Employee Attrition Prediction

## Project Overview

This project is a capstone for a data analytics program, focusing on providing data-driven insights for the Human Resources (HR) department of Salifort Motors, a large consulting firm. The HR department is seeking to improve employee satisfaction and retention but lacks direction on how to use the data they have collected.

The primary business question is: **"What's likely to make the employee leave the company?"**

The goal of this project is to analyze the provided HR dataset, build a predictive model to identify employees likely to leave, and offer actionable suggestions to the HR department to help increase employee retention.

## Dataset

The project utilizes an HR dataset containing 15,000 employee records and 10 features (prior to cleaning). The features include:

* `satisfaction_level`: Employee-reported job satisfaction (0-1)
* `last_evaluation`: Score from the last performance review
* `number_project`: Number of projects contributed to
* `average_monthly_hours`: Average hours worked per month
* `time_spend_company`: Number of years with the company
* `Work_accident`: Whether the employee had a work accident (0 or 1)
* `left`: Whether the employee left the company (0 or 1) - **This is the target variable.**
* `promotion_last_5years`: Whether the employee was promoted in the last 5 years (0 or 1)
* `Department`: The employee's department
* `salary`: The employee's salary (low, medium, or high)

## Project Workflow (PACE Methodology)

This project follows the PACE (Plan, Analyze, Construct, Execute) data analytics framework.

### 1. Plan

The initial stage involved understanding the business scenario and the needs of the primary stakeholder, the Salifort Motors HR department. The objective was clearly defined: to identify key factors driving employee attrition to inform retention strategies.

### 2. Analyze (Data Cleaning & EDA)

This stage focused on data exploration, cleaning, and visualization.

**Data Cleaning:**
* **Column Renaming:** Column names were standardized to `snake_case` for consistency (e.g., `average_montly_hours` became `avg_monthly_hours`, `left` became `left_company`).
* **Missing Values:** A check confirmed there were no missing values in the dataset.
* **Duplicates:** The dataset contained 3,008 duplicate rows, which were subsequently removed.
* **Final Dataset:** The cleaned dataset (`df1`) consists of 11,991 unique employee records.
* **Outliers:** Outliers were examined using boxplots, particularly for the `years_at_company` variable.

**Exploratory Data Analysis (EDA):**
* **Attrition Rate:** In the cleaned dataset, 1,991 employees (16.6%) left the company, while 10,000 (83.4%) stayed.
* **Visualizations:** Various plots were generated to understand variable relationships:
    * A scatterplot of `avg_monthly_hours` vs. `satisfaction_level`, segmented by `left_company`.
    * Histograms comparing salary levels (`low`, `medium`, `high`) for short-tenured (<7 years) and long-tenured (>=7 years) employees.
    * Bar plots showing the relationship between `left_company` and variables like `promotion_last_five_years`, `work_accident`, and `department`.
* **Initial Insight:** The strongest initial correlation observed was between `satisfaction_level` and whether an employee `left_company`.

### 3. Construct (Modeling & Evaluation)

This phase involved feature engineering and building predictive models for the binary classification task.

**Preprocessing:**
* **Ordinal Encoding:** The `salary` feature was ordinally encoded (`low`: 1, `medium`: 2, `high`: 3).
* **One-Hot Encoding:** The categorical `department` feature was one-hot encoded.
* **Scaling:** For the Logistic Regression model, all features were scaled using `MinMaxScaler`.

**Models & Tuning:**
Two models were built and tuned using `GridSearchCV` to optimize for the F1-score:

1.  **Logistic Regression:**
    * **Best F1-Score:** 0.54
    * **Best Parameters:** `{'C': 1.0, 'class_weight': {0: 0.2, 1: 0.8}, 'l1
