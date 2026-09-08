# Assignment 3: Linear Regression vs Random Forest

**Author:** Mireille Ingabire  
**Date:** September 2026  
**Course:** KLab AI Bootcamp  

---

## 1. Objective

The objective of this assignment was to build and compare two machine learning models:

- **Linear Regression**
- **Random Forest Regression**

The models were used to predict **MonthlyCharges** using **tenure**, **TotalCharges**, and **SeniorCitizen**.

The models were evaluated using **Mean Squared Error (MSE)** and **R² Score**.

---

## 2. Dataset

The dataset used in this assignment is the cleaned customer churn dataset from Assignment 2.

- **Rows:** 7,043
- **Columns:** 3 (selected features)
- **Features:** `tenure`, `TotalCharges`, `SeniorCitizen`
- **Target:** `MonthlyCharges`

The target variable, `MonthlyCharges`, is numeric, making it suitable for a regression problem.

---

## 3. Methodology

### 3.1 Data Preparation

I loaded the cleaned customer churn dataset from Assignment 2 and explored its structure.

I selected the following features:
- `tenure` — How long the customer has stayed (months)
- `TotalCharges` — Total amount charged
- `SeniorCitizen` — Whether the customer is a senior citizen (0 = No, 1 = Yes)

The target variable was:
- `MonthlyCharges` — Monthly amount charged

The dataset was divided into:
- 80% training data (5,634 rows)
- 20% testing data (1,409 rows)

### 3.2 Linear Regression

Linear Regression was used as the first model.

The model used:
- `tenure`
- `TotalCharges`
- `SeniorCitizen`

to predict `MonthlyCharges`.

The model was evaluated using MSE and R² Score.

### 3.3 Random Forest Regression

Random Forest Regression was used as the second model.

The model was created using **100 decision trees** with `random_state=42`.

It was trained using the same features and target as Linear Regression.

The same evaluation metrics were used to compare both models.

---

## 4. Results

### 4.1 Performance Comparison

| Model | MSE | R² Score |
|-------|-----|----------|
| Linear Regression | 278.84 | 0.693 |
| Random Forest | 9.25 | 0.990 |

### 4.2 Linear Regression Coefficients

| Feature | Coefficient |
|---------|-------------|
| tenure | -0.015 |
| TotalCharges | 0.031 |
| SeniorCitizen | 6.234 |

**Interpretation:**
- `SeniorCitizen` has a large positive impact on `MonthlyCharges` (+6.23)
- `TotalCharges` has a small positive impact (+0.031 per dollar)
- `tenure` has a slight negative impact (-0.015 per month)

### 4.3 Random Forest Feature Importance

| Feature | Importance |
|---------|------------|
| TotalCharges | 0.899 |
| tenure | 0.093 |
| SeniorCitizen | 0.008 |

**Interpretation:**
- `TotalCharges` is the most important feature by far (89.9%)
- `tenure` has moderate importance (9.3%)
- `SeniorCitizen` has almost no impact (0.8%)

### 4.4 Interpretation

Random Forest performed significantly better than Linear Regression.

Random Forest had a much lower MSE of **9.25**, compared with **278.84** for Linear Regression.

It also achieved a much higher R² Score of **0.990**, compared with **0.693** for Linear Regression.

A lower MSE means smaller prediction errors, while a higher R² Score means better performance in explaining the variation in the target variable.

The R² Score of 0.990 means that Random Forest explained about **99% of the variation in MonthlyCharges** on the test data.

---

## 5. Actual vs Predicted Results

The Actual vs Predicted scatter plot supported the evaluation results.

The Random Forest predictions were very close to the actual values, while the Linear Regression predictions were more scattered.

This indicates that Random Forest produced much better predictions for this dataset.

---

## 6. Discussion

### 6.1 Why Random Forest Performed Better

Random Forest performed better because:

1. **Non-linear relationships** — The relationship between features and MonthlyCharges is not perfectly linear
2. **Feature interactions** — Random Forest captures interactions between features
3. **Ensemble learning** — Combining multiple trees reduces variance and improves generalization

### 6.2 Why TotalCharges is the Most Important Feature

`TotalCharges` is the sum of all monthly charges over the customer's tenure. It is strongly correlated with `MonthlyCharges` because:

- `TotalCharges` = `MonthlyCharges` × `tenure`
- The relationship is almost deterministic

This explains why the Random Forest model relies so heavily on this feature.

### 6.3 Why Linear Regression Performed Poorly

Linear Regression struggled because:

1. **Non-linear patterns** — The relationship between features and the target is not linear
2. **Feature dominance** — `TotalCharges` dominates the prediction, but Linear Regression cannot weight it appropriately
3. **Limited complexity** — Linear Regression is too simple for this problem

---

## 7. Conclusion

In this assignment, I built and compared Linear Regression and Random Forest Regression models to predict `MonthlyCharges`.

Based on the evaluation results, **Random Forest performed significantly better than Linear Regression**.

| Model | MSE | R² Score |
|-------|-----|----------|
| Linear Regression | 278.84 | 0.693 |
| Random Forest | 9.25 | 0.990 |

Therefore, Random Forest was the better-performing model for predicting `MonthlyCharges` in this dataset.

---

## 8. Recommendations

For future work, I would:

- Try additional relevant features
- Use cross-validation for more reliable evaluation
- Experiment with different Random Forest parameters
- Try other regression algorithms like XGBoost
- Explore feature engineering to improve model performance

---

## 9. References

- [Scikit-learn Linear Regression Documentation](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)
- [Scikit-learn Random Forest Documentation](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html)