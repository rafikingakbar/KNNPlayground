# KNN Playground – Heart Failure Clinical Records

This repository contains a small project aimed at understanding how the **K-Nearest Neighbors (KNN)** algorithm works on a heart failure clinical dataset. The main purpose of this project is exploratory in nature, focusing on the data analysis process and model evaluation, rather than building a production-ready medical prediction system.

---

## Introduction

The dataset used is the **Heart Failure Clinical Records Dataset**, which contains data from 299 patients with 13 clinical variables such as age, blood pressure, ejection fraction, serum creatinine, diabetes status, smoking habits, and follow-up time.  
The predicted target variable is `DEATH_EVENT` (0 = survived, 1 = died).

This project covers the complete workflow from data cleaning and exploration to KNN modeling and evaluation using **5-Fold Cross Validation**.

---

## Analysis Workflow

### 1. Data Loading
- The dataset is loaded using pandas.
- The data structure is inspected using `df.info()`.
- Three columns (`age`, `platelets`, `serum_creatinine`) were initially read as object type due to the use of commas as decimal separators.

### 2. Preprocessing
- Commas are replaced with dots in columns containing decimal values.
- The three columns are converted to numeric data types.
- Missing values are checked after conversion.
- The dataset is then ready for modeling.

### 3. Exploratory Data Analysis (EDA)
- The distribution of `DEATH_EVENT` is imbalanced:
  - 203 patients survived
  - 96 patients died
- Key feature correlations:
  - `serum_creatinine` has the strongest positive correlation with mortality.
  - `time` shows the strongest negative correlation, indicating that longer follow-up time is associated with lower mortality risk.

### 4. Modeling – KNN with Pipeline
- The pipeline consists of:
  - `StandardScaler` for feature normalization.
  - `KNeighborsClassifier` for modeling.
- Tested K values: `3, 4, 5, 6, 7, 8, 9, 11, 13, 15`.
- Model evaluation uses **5-Fold Cross Validation**.

### 5. Modeling Results
- The best K value is **K = 7**.
- The average cross-validation accuracy is **74.57%**.
- Accuracy across folds is relatively stable.
- Additional evaluation for K = 7:
  - Precision is fairly good.
  - Recall is low due to the imbalanced class distribution.
  - The F1-score follows the low recall trend.

### 6. Insights and Recommendations
- Key factors associated with mortality risk include age, `serum_creatinine`, and `time`.
- Very small K values tend to cause overfitting, while large K values lead to overly generalized models.
- Recommendations:
  - Apply data balancing techniques such as oversampling or SMOTE.
  - Use **Stratified K-Fold Cross Validation**.
  - Try other algorithms that are more suitable for imbalanced datasets.

### 7. Conclusion
- KNN with the optimal parameter K = 7 achieved an accuracy of approximately **74.6%**.
- Precision is acceptable, but recall is low, making the model less effective at detecting high-risk patients.
- Class imbalance significantly impacts model performance.
- This project serves as a useful baseline for understanding the end-to-end KNN analysis and evaluation workflow on clinical data.
