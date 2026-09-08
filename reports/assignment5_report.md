# Assignment 5: Evaluating Unsupervised Models

**Author:** Mireille Ingabire  
**Date:** September 2026  
**Course:** KLab AI Bootcamp  

---

## 1. Objective

The objective of this assignment was to learn how to evaluate unsupervised learning models. Unlike supervised learning, unsupervised learning has no labels to compare against, so we need different methods to assess model quality.

The assignment covered:

- Why accuracy does not apply to clustering
- Internal metrics: Silhouette Score
- Stability testing to distinguish real structure from noise
- Detecting overfitting without labels
- Complexity dials in DBSCAN

---

## 2. Dataset

The dataset used in this assignment is the **Palmer Penguins dataset**.

- **Rows:** 333 (after dropping missing values)
- **Features:** bill_length_mm, bill_depth_mm, flipper_length_mm, body_mass_g
- **True Clusters:** 3 (Adelie, Chinstrap, Gentoo)
- **Source:** seaborn (built-in)

The dataset has a known structure with 3 natural groups, making it ideal for testing unsupervised learning metrics.

---

## 3. Methodology

### 3.1 Data Preparation

I loaded the Penguins dataset and selected four numeric features. I scaled the features using StandardScaler to ensure all features contribute equally to distance calculations.

### 3.2 Part 1: Why Accuracy Fails

I trained K-Means with k=3 and calculated naive accuracy by comparing cluster IDs to true labels. I then renamed the clusters to show that accuracy changes even though the grouping is identical.

### 3.3 Part 2: Silhouette Score

I computed Silhouette Scores for k values ranging from 2 to 6. Silhouette Score measures how similar points are to their own cluster compared to other clusters.

### 3.4 Part 3: Stability Testing

I implemented a stability test that resamples the data and clusters each sample. Real structure reappears consistently; noise does not.

### 3.5 Part 4: Overfitting with GMM

I split the data into training and test sets, then trained Gaussian Mixture Models with different numbers of components. I compared training and test log-likelihoods to detect overfitting.

### 3.6 Part 5: DBSCAN

I tested different eps values in DBSCAN to see how the complexity dial affects the number of clusters and noise.

---

## 4. Results

### 4.1 Why Accuracy Fails

| Metric | Value |
|--------|-------|
| Naive Accuracy | 0.372 |
| Adjusted Rand Index (ARI) | 0.799 |

**Observation:**

Renaming clusters changed the naive accuracy dramatically:

| Permutation | Accuracy |
|-------------|----------|
| [2, 1, 0] | 0.066 |
| [0, 2, 1] | 0.919 |
| [1, 2, 0] | 0.438 |

The grouping never changed, only the names did. ARI remained stable at 0.799, confirming that ARI is the correct metric for clustering evaluation.

### 4.2 Silhouette Score

| K | Silhouette Score |
|---|------------------|
| 2 | 0.5308 |
| 3 | 0.4462 |
| 4 | 0.3982 |
| 5 | 0.3744 |
| 6 | 0.3642 |

**Observation:**

The best K by Silhouette is **2**, but the true number of species is **3**.

This suggests that the Penguins dataset does not have perfectly spherical clusters, and K-Means struggles to find the true structure. The silhouette peak at k=2 indicates that K-Means sees two main groups instead of three.

### 4.3 Stability Test

| K | Stability (ARI) |
|---|-----------------|
| 2 | 1.0000 |
| 3 | 0.9429 |
| 4 | 0.9011 |
| 5 | 0.9597 |
| 6 | 0.9378 |

**Observation:**

The best K by Stability is **2** with a perfect score of 1.000. This means that 2 clusters are extremely stable and reproducible across different samples of the data.

However, k=3 also has high stability (0.9429), suggesting that 3 clusters are also real but slightly less stable than 2 clusters.

### 4.4 Overfitting with GMM

| Components | Train Score | Test Score |
|------------|-------------|------------|
| 1 | -4.36 | -4.67 |
| 2 | -3.44 | -3.86 |
| 3 | -3.27 | -3.74 |
| 4 | -3.22 | -3.73 |
| 5 | -3.06 | -4.01 |
| 6 | -3.00 | -4.10 |

**Observation:**

The test score is highest at 3-4 components (-3.74 to -3.73), then drops sharply after 4 components. This indicates that 3-4 components capture the real structure, and more components lead to overfitting.

Training score continues to rise, while test score drops — this is the classic signature of overfitting.

### 4.5 DBSCAN

| eps | Clusters | Noise % |
|-----|----------|---------|
| 0.3 | 3 | 94.6% |
| 0.5 | 4 | 19.8% |
| 0.7 | 2 | 5.1% |
| 1.0 | 2 | 0.3% |
| 1.5 | 1 | 0.0% |

**Observation:**

- **eps=0.3:** 3 clusters but 94.6% noise — too restrictive, almost everything is noise (overfitting)
- **eps=0.5:** 4 clusters, 19.8% noise — better, but still some noise
- **eps=0.7:** 2 clusters, 5.1% noise — clusters are merging (underfitting)
- **eps=1.0:** 2 clusters, 0.3% noise — more merging
- **eps=1.5:** 1 cluster, 0.0% noise — everything merged into one (severe underfitting)

The optimal eps is around **0.5-0.7**, where DBSCAN finds a reasonable number of clusters with acceptable noise.

---

## 5. Discussion

### 5.1 Why Accuracy Fails

Accuracy compares labels directly, but cluster IDs are arbitrary names. The same clustering can have different "accuracy" scores just by renaming clusters. This is why we use Adjusted Rand Index (ARI) instead, which compares pairs of points rather than labels.

### 5.2 Silhouette Score vs True K

Silhouette Score suggested k=2, but the true number of species is 3. This happens because:

- Penguins species are not perfectly spherical
- Chinstrap and Adelie penguins are somewhat similar in feature space
- K-Means prefers spherical, equally sized clusters

This is an important lesson: **Silhouette Score is helpful, but it's not always correct.**

### 5.3 Stability Testing

Stability testing showed that k=2 has perfect stability (1.000), while k=3 has very high stability (0.943). Both are stable, but k=2 is more reproducible. This suggests that while 3 clusters exist, 2 clusters are easier to reproduce across samples.

### 5.4 Overfitting with GMM

The GMM results clearly show overfitting beyond 3-4 components. Training log-likelihood continues to rise, but test log-likelihood drops. This is a classic signature of overfitting — the model is fitting noise in the training data.

### 5.5 DBSCAN

DBSCAN with eps=0.5 found 4 clusters with 19.8% noise. This is a reasonable result for the Penguins dataset, showing that DBSCAN handles the data better than K-Means.

---

## 6. Conclusion

This assignment demonstrated that accuracy is meaningless for clustering. Instead, we use:

- **Silhouette Score** to find the optimal number of clusters
- **Stability** to check if clusters are real
- **Held-out likelihood** to detect overfitting
- **Complexity dials** like eps in DBSCAN

The key takeaway is:

> A metric that improves every time you add complexity cannot be used to choose complexity. Inertia and reconstruction error fail this test. Silhouette, held-out likelihood, BIC, and stability all pass it.

---

## 7. References

- [Scikit-learn Clustering Documentation](https://scikit-learn.org/stable/modules/clustering.html)
- [Palmer Penguins Dataset](https://allisonhorst.github.io/palmerpenguins/)