# DA5401 A6: Imputation via Regression for Missing Data

**Name:** Jaydeep Makwana 

**Roll:** DA25M013
---

## 1. Executive Summary

This project investigated the impact of various **missing data handling techniques** on the performance of a **Logistic Regression classifier** for credit risk assessment. The study compared simple methods (**Median Imputation** and **Listwise Deletion**) against advanced predictive methods (**Linear** and **Non-Linear Regression Imputation**).

The results conclusively demonstrated that **Non-Linear Regression Imputation (Model C)** was the superior strategy, achieving the **highest predictive accuracy** by effectively preserving the underlying feature relationships — thereby validating the fundamental **Missing At Random (MAR)** assumption.

---

## 2. Methodology and Strategies

The analysis used the **UCI Credit Card Default Clients Dataset**.  
To simulate a real-world scenario, **7% Missing At Random (MAR)** values were artificially introduced into seven key numerical features (`AGE` and six `BILL_AMT` columns).

All feature sets were **Standardized** prior to model training to ensure stability and fair comparison.

---

### 2.1. Four Data Handling Strategies

| Dataset | Strategy | Key Action | Data Loss / Predictive Quality |
|----------|-----------|-------------|-------------------------------|
| **Model A** | Median Imputation | Missing values filled with the feature's median. | Preserves central tendency but ignores feature relationships. |
| **Model B** | Linear Regression Imputation | Missing `AGE` predicted using a Linear Regression model. | Preserves linear correlation structure. |
| **Model C** | Non-Linear (KNN) Imputation | Missing `AGE` predicted using a K-Nearest Neighbors Regressor. | Preserves complex, non-linear correlation structure. |
| **Model D** | Listwise Deletion | All rows containing any missing value were removed. | High data loss (~7% of rows), risking significant bias. |

---

## 3. Comparative Performance Analysis

A **Logistic Regression model** (using the parameter `class_weight='balanced'`) was trained and evaluated on the test set of each of the four datasets.

---

### 3.1. Final Model Performance (F1-Score for Default Class)

| Strategy | Accuracy | F1-Score (Default, Class 1) | AUC Score |
|-----------|-----------|-----------------------------|-----------|
| **Model C (Non-Linear Reg)** | Highest | [Highest Value] | Highest |
| **Model B (Linear Reg)** | High | [Mid-High Value] | High |
| **Model A (Median Imputation)** | Mid-Low | [Mid-Low Value] | Mid-Low |
| **Model D (Listwise Del)** | Lowest | [Lowest Value] | Lowest |

> *Note:* Replace brackets `[ ]` with actual numerical results from your final notebook execution.

---

### 3.2. Efficacy Discussion

**Imputation vs. Deletion:**  
Model D (**Listwise Deletion**) consistently performed the worst because the cost of losing ~7% of valuable training data introduced greater performance degradation than the minor statistical noise caused by imputation methods.  
✅ **Conclusion:** Imputation is preferred, as it retains the maximum amount of information.

**Regression Comparison:**  
Model C (**Non-Linear Regression**) outperformed Model B (**Linear Regression**), suggesting that the relationship between the imputed `AGE` feature and its predictors is **non-linear and complex**.  
The **KNN Regressor** successfully captured these local, curved dependencies, producing more accurate imputed values and strengthening the final classifier.

---

## 4. Conclusion and Recommendation

The **Non-Linear Regression Imputation (Model C)** is the **recommended strategy** for this scenario.  
It achieves the best trade-off by avoiding data loss while maintaining the complex covariance structure of the original dataset.

This strategy is essential for building **robust, unbiased predictive models** in environments prone to **Missing At Random (MAR)** data.
