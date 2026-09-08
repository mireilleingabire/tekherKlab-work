# Assignment 3: Reflection

**Author:** Mireille Ingabire  
**Date:** September 2026  
**Course:** KLab AI Bootcamp  

---

## 1. What I Learned

In this assignment, I learned how to:

- Build a **Linear Regression** model and interpret its coefficients
- Build a **Random Forest** model and understand feature importance
- Compare two models using **MSE** and **R² Score**
- Visualize model performance with scatter plots
- Interpret feature importance to understand which variables matter most

---

## 2. Challenges I Faced

### 2.1 Understanding Feature Importance

Interpreting feature importance from Random Forest was initially challenging. I had to understand that higher importance means the feature has a stronger influence on the prediction.

### 2.2 Why Random Forest Performed So Much Better

I was surprised by how much better Random Forest performed compared to Linear Regression. I learned that this is because:

- The relationship between features and the target is non-linear
- `TotalCharges` is strongly correlated with `MonthlyCharges`
- Random Forest can capture complex patterns that Linear Regression cannot

### 2.3 Interpreting Coefficients

Understanding the coefficients of Linear Regression required careful thought. I learned that:

- `SeniorCitizen` has a large positive impact on `MonthlyCharges`
- `tenure` has a slight negative impact
- `TotalCharges` has a small positive impact

---

## 3. How I Overcame Them

- I reviewed the lecture notes and scikit-learn documentation
- I experimented with different features and compared results
- I used visualizations to better understand model performance
- I read about feature importance and how it is calculated in Random Forest

---

## 4. Key Takeaways

### 4.1 Model Comparison

- **Random Forest** is more flexible and powerful than Linear Regression
- **MSE and R² Score** together provide a complete picture of model performance
- **Feature importance** helps identify which variables matter most

### 4.2 The Surprising Result

The Random Forest model achieved an R² of **0.990**, meaning it explains **99% of the variation** in MonthlyCharges. This is an excellent result.

### 4.3 Why This Happened

`TotalCharges` is strongly correlated with `MonthlyCharges` because:

- `TotalCharges` = `MonthlyCharges` × `tenure`
- The relationship is almost deterministic
- Random Forest picked up on this pattern immediately

---

## 5. What I Would Do Differently

- Try more feature combinations
- Use cross-validation for better model evaluation
- Experiment with hyperparameter tuning for Random Forest
- Try other regression algorithms like XGBoost
- Investigate why `TotalCharges` dominates the prediction

---

## 6. Honest Difficulty Assessment

| Task | Difficulty (1-10) | Why |
|------|-------------------|-----|
| Model Training | 4 | Straightforward with scikit-learn |
| Model Evaluation | 5 | Understanding MSE and R² Score took some time |
| Feature Importance | 6 | Interpreting importance required careful thought |
| Visualizations | 4 | Creating charts was straightforward |
| Comparison | 5 | Understanding which model performed better required analysis |
| Why Random Forest Won | 7 | Required deeper understanding of the data and models |

---

## 7. What Surprised Me

- How much better Random Forest performed (R²: 0.990 vs 0.693)
- How clear the feature importance was (`TotalCharges` at 0.899)
- How much the scatter plot revealed about model performance
- That `SeniorCitizen` had almost no impact (0.008 importance)

---

## 8. One Sentence Summary

> **This assignment taught me that Random Forest is much more powerful than Linear Regression for this dataset, achieving near-perfect predictions (R²: 0.990) by capturing the strong relationship between TotalCharges and MonthlyCharges.**

---

## 9. Final Thoughts

This assignment was a valuable learning experience because it:

1. **Reinforced the importance of model comparison** — Different models perform differently on different datasets
2. **Taught me to use multiple metrics** — MSE and R² Score together provide a complete picture
3. **Helped me understand feature importance** — Knowing which features matter most is valuable
4. **Built my confidence with scikit-learn** — I can now train and evaluate models independently
5. **Showed me the power of ensemble methods** — Random Forest is significantly better than Linear Regression for this dataset

---

## 10. Self-Assessment

| Criteria | Self-Assessment |
|----------|-----------------|
| Completed all tasks | ✅ Yes |
| Code runs cleanly | ✅ Yes |
| Documentation is clear | ✅ Yes |
| Visualizations are meaningful | ✅ Yes |
| Reflection is honest | ✅ Yes |
| Overall effort | High |

---

## 11. The Most Important Lesson

> **The right model matters.** For this dataset, Random Forest was the right choice because it captured the non-linear relationship between features and the target. Linear Regression was too simple and performed poorly.

---

## 12. What I Will Take Forward

1. **Always compare multiple models** — Never assume one model will be best
2. **Use feature importance** — It tells you what matters most
3. **Visualize your results** — Charts reveal patterns that numbers alone miss
4. **Document your decisions** — It helps others (and future you) understand your work