# Spaceship Titanic Competition Report

**Author:** Mireille Ingabire  
**Published:** 2026-09-11  
**Notebook:** [Spaceship Titanic Competition _Ingabire Mireille](https://www.kaggle.com/code/mireilleingabire/spaceship-titanic-competition-ingabire-mireille?scriptVersionId=349005647)  
**Logs:** [View Logs](https://www.kaggle.com/code/mireilleingabire/spaceship-titanic-competition-ingabire-mireille/log?scriptVersionId=349005647)  
**Version:** 7 of 16  
**Language:** Python  
**License:** Apache 2.0  
**Runtime:** 2 minutes 18 seconds  
**Accelerator:** None  

---

## Overview

This notebook tackles the Kaggle **Spaceship Titanic** competition — a binary classification task predicting whether passengers were transported to an alternate dimension. The approach combines structured feature engineering, five base models, and two ensemble methods (stacking and weighted voting) to maximise cross-validated accuracy and leaderboard performance.

The best model achieved a **cross-validation accuracy of 0.8155** and a **leaderboard accuracy of 0.80944**, exceeding the project target of 0.80.

---

## Dataset

| Split | Shape |
|---|---|
| Train | (8693, 14) |
| Test | (4277, 13) |
| Columns after feature engineering | 29 |
| Final feature matrix (X) | (8693, 24) |
| Target balance | 0.5036 |
| Random seed | 42 |

- **Class balance:** Nearly 50/50, so accuracy is a fair metric.
- **Missing values:** Approximately 2% in every column except `PassengerId` and `Transported`.
- **Structured columns:** `Cabin` is stored as `deck/number/side`. `PassengerId` is stored as `group_position`.

---

## Feature Engineering

Seventeen engineered features were created from the raw data and combined with six original categorical features, giving 24 features in the final matrix.

### Engineered Numeric Features

| # | Feature | Derivation | Purpose |
|---|---|---|---|
| 1 | `Age` | Original | Demographics |
| 2 | `GroupLen` | `groupby('GID').count()` | Travel group size |
| 3 | `Solo` | `GroupLen == 1` | Solo traveller indicator |
| 4 | `Seat` | `PassengerId` split | Position within group |
| 5 | `Room` | `Cabin` split | Cabin number |
| 6 | `Cash` | Sum of five spending columns | Total spending |
| 7 | `CashLog` | `log1p(Cash)` | Skew correction |
| 8 | `ZeroSpend` | `Cash == 0` | No-spend indicator |
| 9 | `UsedCount` | Count of non-zero spend columns | Amenity usage |
| 10 | `HighEnd` | `Spa + VRDeck + RoomService` | Luxury spending |
| 11 | `LowEnd` | `FoodCourt + ShoppingMall` | Budget spending |
| 12 | `HighRatio` | `HighEnd / (Cash + 1)` | Luxury proportion |
| 13 | `SleepZero` | `CryoSleep × ZeroSpend` | Interaction term |

### Categorical Features

`HomePlanet`, `CryoSleep`, `Destination`, `VIP`, `Zone`, `Pier`

---

## Preprocessing

All preprocessing was performed inside a scikit-learn `Pipeline` to prevent data leakage during cross-validation.

| Step | Numeric | Categorical |
|---|---|---|
| Imputation | `SimpleImputer(strategy='mean')` | `SimpleImputer(strategy='most_frequent')` |
| Transformation | `StandardScaler()` | `OneHotEncoder(handle_unknown='ignore')` |

The combined transformation was applied via `ColumnTransformer`.

---

## Models Tested

### Five Base Models

| # | Model | CV Score |
|---|---|---|
| 1 | Logistic Regression | 0.7959 |
| 2 | Decision Tree | 0.7977 |
| 3 | K-Nearest Neighbours | 0.7865 |
| 4 | Extra Trees | 0.8090 |
| 5 | CatBoost | 0.8133 |

CatBoost was the strongest single model.

### Ensemble Methods

| # | Method | CV Score | LB Score |
|---|---|---|---|
| 6 | Assembly — Stacking (5 base models, LR meta) | 0.8132 | — |
| 7 | Weighted Voting + LightGBM (DT + ET + CatBoost + LGBM) | **0.8155** | **0.80944** |

The weighted voting ensemble outperformed both the individual models and the stacking approach.

---

## Final Comparison

| Rank | Model | CV Score |
|---|---|---|
| 1 | **Weighted Voting + LGBM** | **0.8155** |
| 2 | CatBoost | 0.8133 |
| 3 | Assembly (Stacking) | 0.8132 |
| 4 | Extra Trees | 0.8090 |
| 5 | Decision Tree | 0.7977 |
| 6 | Logistic Regression | 0.7959 |
| 7 | K-Nearest Neighbours | 0.7865 |

---

## Final Iteration Log

| Iteration | Model | Configuration | CV Score | LB Score |
|---|---|---|---|---|
| 1 | Logistic Regression | Baseline, default parameters | 0.7959 | — |
| 2 | Decision Tree | `max_depth=8`, `min_samples_leaf=8` | 0.7977 | — |
| 3 | K-Nearest Neighbours | `n_neighbors=11`, `weights=distance` | 0.7865 | — |
| 4 | Extra Trees | `n_estimators=400`, `max_depth=12` | 0.8090 | — |
| 5 | CatBoost | `iterations=400`, `lr=0.06`, `depth=5` | 0.8133 | 0.80430 |
| 6 | Assembly — Stacking | 5 base models, Logistic Regression meta | 0.8132 | — |
| 7 | **Weighted Voting + LGBM** | **DT + ET + CatBoost + LightGBM** | **0.8155** | **0.80944** |

---

## Final Model Architecture

The best model was a **soft-voting ensemble** of four algorithms.

| Position | Model | Role |
|---|---|---|
| 1 | Decision Tree | Simple baseline tree |
| 2 | Extra Trees | Diverse bagging |
| 3 | CatBoost | Strongest boosting |
| 4 | LightGBM | Fast boosting support |

### Why This Combination Worked

- **Diversity:** Two bagging models (Decision Tree, Extra Trees) and two boosting models (CatBoost, LightGBM).
- **Complementary errors:** Different model families make different mistakes, so their combined predictions reduce overall error.
- **Soft voting:** Averaging predicted probabilities is more robust than hard majority voting.

---

## Submission Details

| Item | Value |
|---|---|
| File | `submission.csv` |
| Shape | (4277, 2) |
| Columns | `PassengerId`, `Transported` |
| Missing values | 0 |
| Duplicates | 0 |
| Transported | 2221 |
| Not Transported | 2056 |

The prediction split is nearly balanced (51.9% / 48.1%), matching the training distribution.

---

## Cross-Validation Note

The best CV score of 0.8155 was measured using **Stratified 5-fold cross-validation**. This preserves the class balance in every fold and provides an honest estimate of the model's performance.

A comparison between CV and LB is informative:

| Model | CV | LB | Gap |
|---|---|---|---|
| Weighted Voting + LGBM | 0.8155 | 0.80944 | +0.0061 |
| CatBoost alone | 0.8133 | 0.80430 | +0.0090 |

The ensemble has a **smaller CV–LB gap**, indicating it generalises slightly better than the single CatBoost model.

---

## Challenges

| Challenge | Detail |
|---|---|
| Missing values | ~2% of each column. Handled with mean/mode imputation inside the pipeline. |
| Structured strings | `Cabin` packs three facts into one string; unpacking was required. |
| Group structure | Travel groups share outcomes. This was captured through `GroupLen` and `Solo` features. |
| Feature count balance | Adding too many weak features reduced CV. Only the strongest features were kept. |
| Overfitting | Deeper trees and more estimators did not always improve CV. Regularisation was necessary. |

---

## Key Findings

| # | Finding | Evidence |
|---|---|---|
| 1 | Diverse ensembles outperform single models | Ensemble CV 0.8155 > CatBoost CV 0.8133 |
| 2 | Soft voting is more robust than hard voting | The weighted voting ensemble outperformed all single models |
| 3 | Stacking did not beat weighted voting | Stacking CV 0.8132 < Voting CV 0.8155 |
| 4 | Feature engineering mattered | 24 features produced the best result versus raw features |
| 5 | The best CV–LB gap was in the ensemble | Gap of +0.0061 versus +0.0090 for CatBoost alone |

---

## Score Summary

| Metric | Value |
|---|---|
| Best CV (Weighted Voting + LGBM) | **0.8155** |
| Best CV (single model, CatBoost) | 0.8133 |
| Best LB (Weighted Voting + LGBM) | **0.80944** |
| Best LB (single model, CatBoost) | 0.80430 |
| Project target | 0.80 |
| Result | Above target by 0.00944 |

---

## Conclusion

This project produced a **4-model soft-voting ensemble** achieving a leaderboard accuracy of **0.80944**, exceeding the project target of 0.80 by 0.944 percentage points.

Three contributions stand out:

1. **Feature engineering** transformed 14 raw columns into 24 informative features.
2. **Model diversity** proved more valuable than any individual algorithm. Combining two bagging models with two boosting models reduced error.
3. **Ensemble strategy mattered.** Soft voting outperformed stacking, and adding LightGBM to the voting ensemble produced the best result.

The notebook is reproducible, the iteration log is complete, and the submission file is valid and clean.

---

## Links

| Resource | URL |
|---|---|
| Kaggle notebook | https://www.kaggle.com/code/mireilleingabire/spaceship-titanic-competition-ingabire-mireille |
| Competition | https://www.kaggle.com/competitions/spaceship-titanic |

---

*Report compiled from Kaggle notebook logs, iteration history, and cross-validation results.*
