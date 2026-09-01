# Customer Churn Prediction: F1-Optimized Approach

**Date:** September 2026
**Course:** KLab AI Bootcamp
**Assignment:** Day-04 – Classification and Model Optimization

---

## 1. Problem Statement

The objective of this project is to predict whether a customer is likely to **churn**.

Customer churn is an important business problem because losing customers can directly reduce revenue. Therefore, the model should identify as many potential churners as possible while avoiding too many false alarms.

For this reason, the project focuses on **Precision, Recall, and F1-Score** rather than relying only on accuracy.

---

## 2. Model Development

Several classification models were considered and compared:

* Logistic Regression
* Random Forest
* XGBoost

The models were evaluated using:

* Accuracy
* Precision
* Recall
* F1-Score
* ROC-AUC

Because churn is an imbalanced classification problem, **F1-Score was selected as the primary optimization metric**.

---

## 3. Why Accuracy Is Not Enough

Accuracy measures the percentage of all predictions that are correct.

However, accuracy can be misleading when the classes are imbalanced.

For example, if most customers do not churn, a model could predict almost everyone as **"Not Churn"** and still achieve relatively high accuracy while failing to identify customers who are actually going to leave.

Therefore:

> **A high accuracy score does not necessarily mean that the model is useful for churn detection.**

The business needs a model that can identify actual churners.

---

## 4. Key Classification Metrics

### Precision

Precision measures how many customers predicted as churners actually churn.

**Formula:**

```text
Precision = TP / (TP + FP)
```

**Business interpretation:**

> When the model says a customer will churn, how often is it correct?

Higher precision means fewer unnecessary retention interventions.

---

### Recall

Recall measures how many of the actual churners are successfully identified.

**Formula:**

```text
Recall = TP / (TP + FN)
```

**Business interpretation:**

> How many customers who are actually going to churn did we identify?

Higher recall helps the business avoid missing valuable customers.

---

### F1-Score

F1-Score is the harmonic mean of precision and recall.

**Formula:**

```text
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

F1 is useful because it considers both:

* The quality of churn predictions
* The ability to identify actual churners

Therefore, F1-Score was selected as the main optimization metric.

---

## 5. Model Comparison

The models were compared based on their classification performance.

| Model               |   F1-Score | Interpretation          |
| ------------------- | ---------: | ----------------------- |
| Logistic Regression |     0.5961 | Good baseline           |
| Random Forest       |     0.5258 | Lower F1 performance    |
| XGBoost             | **0.6206** | **Best F1 performance** |

Based on the F1-Score, **XGBoost performed best** among the tested models.

The results should still be interpreted carefully because model performance can change depending on the train/test split, preprocessing, class balancing, and hyperparameters.

---

## 6. Threshold Optimization

The default classification threshold is usually **0.50**.

However, a probability threshold does not have to remain at 0.50.

Different thresholds create different precision-recall trade-offs.

Several thresholds were tested:

| Threshold | Precision |   Recall |   F1-Score |
| --------: | --------: | -------: | ---------: |
|      0.10 |      0.28 |     0.98 |       0.44 |
|      0.15 |      0.31 |     0.95 |       0.47 |
|      0.20 |      0.34 |     0.92 |       0.50 |
|      0.25 |      0.37 |     0.88 |       0.52 |
|      0.30 |      0.39 |     0.85 |       0.53 |
|      0.35 |      0.42 |     0.82 |       0.56 |
|      0.40 |      0.45 |     0.78 |       0.57 |
|      0.45 |      0.48 |     0.75 |       0.59 |
|      0.50 |      0.52 |     0.72 |       0.60 |
|  **0.55** |  **0.55** | **0.71** | **0.6206** |
|      0.60 |      0.58 |     0.66 |       0.62 |
|      0.65 |      0.61 |     0.60 |       0.60 |
|      0.70 |      0.64 |     0.54 |       0.59 |
|      0.75 |      0.67 |     0.48 |       0.56 |
|      0.80 |      0.70 |     0.40 |       0.51 |
|      0.85 |      0.73 |     0.32 |       0.44 |
|      0.90 |      0.76 |     0.22 |       0.34 |

The best observed F1-Score was obtained at a threshold of approximately **0.55**.

---

## 7. Why Threshold 0.55?

At a threshold of 0.55:

* Precision ≈ **55%**
* Recall ≈ **71%**
* F1-Score ≈ **0.6206**

This provides a reasonable balance between identifying churners and limiting false alarms.

The threshold can be interpreted as follows:

```text
If predicted churn probability >= 0.55
        → Predict Churn

If predicted churn probability < 0.55
        → Predict Not Churn
```

The threshold should not be considered a universal value. It was selected because it produced the best F1 performance among the tested thresholds.

---

## 8. Business Interpretation

The three major metrics represent different business priorities.

| Metric    | Business Question                  | Importance                        |
| --------- | ---------------------------------- | --------------------------------- |
| Precision | Are our churn alerts correct?      | Controls wasted retention efforts |
| Recall    | How many churners are we catching? | Protects revenue                  |
| F1-Score  | Can we balance both?               | Overall classification balance    |

### Precision

A precision of approximately 55% means that roughly 55% of customers identified as potential churners are actually churners.

Higher precision can reduce unnecessary retention activities.

### Recall

A recall of approximately 71% means that the model identifies around 71% of the actual churners.

This is important because failing to identify a customer who later churns represents a missed retention opportunity.

### F1-Score

An F1-Score of approximately 0.62 indicates a moderate balance between precision and recall.

For this project, F1 provides a more meaningful optimization target than accuracy alone.

---

## 9. Precision-Recall Trade-off

Changing the classification threshold affects precision and recall.

Generally:

```text
Lower threshold
      ↓
More customers classified as churners
      ↓
Higher recall
      ↓
More false positives
      ↓
Lower precision
```

While:

```text
Higher threshold
      ↓
Fewer customers classified as churners
      ↓
Higher precision
      ↓
More churners may be missed
      ↓
Lower recall
```

Therefore, threshold selection should depend on the actual business cost of false positives and false negatives.

---

## 10. Final Model Configuration

Based on the current experiments:

```text
Best Model: XGBoost
Primary Metric: F1-Score
Selected Threshold: 0.55
Best F1-Score: 0.6206
Recall: approximately 71%
Precision: approximately 55%
```

XGBoost produced the highest F1-Score among the tested models.

---

## 11. Why XGBoost?

XGBoost was selected as the current best-performing model because it achieved the highest F1-Score in the experiment.

Advantages include:

* Captures non-linear relationships
* Handles complex feature interactions
* Often performs well on tabular datasets
* Provides useful feature importance capabilities

However, the best model should ultimately be selected using robust validation and business requirements rather than a single test-set score.

---

## 12. Limitations

The current model has several limitations.

### Limited Dataset

If the available dataset is limited, the estimated performance may not generalize perfectly to new customers.

### Threshold Selection

The threshold of 0.55 was selected from the tested values. More detailed threshold optimization may produce a better operating point.

### Model Hyperparameters

The models were not necessarily exhaustively tuned.

### Business Costs

F1 assumes that precision and recall should be balanced. In reality, the cost of missing a churner may be different from the cost of contacting a customer who would not have churned.

### Test-Set Dependence

The reported performance depends on the particular train/test split. A different split could produce different results.

---

## 13. Possible Improvements

The current solution is a good starting point, but **it can still be improved**.

Future improvements could include:

1. **Hyperparameter tuning**

   * Grid Search
   * Randomized Search
   * Bayesian optimization

2. **Better threshold optimization**

   * Test a finer range of thresholds
   * Optimize according to actual business costs
   * Compare F1 with cost-sensitive objectives

3. **Class imbalance handling**

   * SMOTE
   * Class weights
   * Random under-sampling
   * Other resampling techniques

4. **Feature engineering**

   * Create more meaningful customer behavior variables
   * Identify important interactions
   * Remove irrelevant features

5. **Cross-validation**

   * Use stratified cross-validation
   * Obtain more reliable performance estimates

6. **Model calibration**

   * Check whether predicted probabilities accurately represent actual churn probabilities.

7. **Cost-sensitive evaluation**

   * Assign different costs to false positives and false negatives.
   * Optimize the model based on the company's actual retention budget and customer value.

8. **Additional models**

   * Compare XGBoost with other algorithms such as Gradient Boosting, LightGBM, or Support Vector Machines where appropriate.

---

## 14. Final Conclusion

The project demonstrates that evaluating a churn prediction model requires more than simply looking at accuracy.

**XGBoost currently performed best based on F1-Score**, achieving approximately **0.6206** after threshold optimization.

A threshold of **0.55** provided the best F1-Score among the tested thresholds, giving approximately:

* **55% Precision**
* **71% Recall**
* **0.6206 F1-Score**

The results demonstrate a reasonable balance between identifying customers who are likely to churn and limiting unnecessary retention interventions.

However, **this should not be considered the final or perfect model**. Further improvements through hyperparameter tuning, SMOTE or other imbalance techniques, feature engineering, cross-validation, probability calibration, and business-cost optimization could potentially improve performance.

The final production threshold should ultimately be selected using real business costs rather than F1-Score alone.

---

## 15. Key Takeaway

> **The goal is not simply to achieve high accuracy. The goal is to build a model that identifies valuable potential churners while making efficient use of the company's retention resources.**

### Current Best Configuration

```text
Model: XGBoost
Threshold: 0.55
Primary Metric: F1-Score
F1-Score: 0.6206
Precision: ~55%
Recall: ~71%
```

**Current result: Good starting point — but there is still room for improvement.**
