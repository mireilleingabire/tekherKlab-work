# Assignment 5: Reflection

**Author:** Mireille Ingabire  
**Date:** September 2026  
**Course:** KLab AI Bootcamp  

---

## 1. What I Learned

In this assignment, I learned:

- Accuracy is meaningless for clustering because cluster IDs are arbitrary names
- Silhouette Score helps find the optimal number of clusters (but it's not always correct)
- Stability testing separates real structure from noise
- Overfitting can be detected without labels using held-out likelihood
- DBSCAN has a complexity dial (eps) that controls cluster count

---

## 2. Surprising Results

### 2.1 Silhouette Score Said k=2, But True K is 3

This was surprising. I expected Silhouette Score to find k=3, but it found k=2. This happened because:

- The Penguins dataset does not have perfectly spherical clusters
- Chinstrap and Adelie penguins have overlapping features
- K-Means prefers spherical clusters

**Lesson:** Silhouette Score is useful but not infallible. It's important to use multiple metrics.

### 2.2 Stability Said k=2 (Perfect Score 1.000)

Stability testing showed that k=2 has perfect stability (1.000). This means that 2 clusters are extremely reproducible across samples. However, k=3 also has high stability (0.943).

**Lesson:** Stability testing confirms that both 2 and 3 clusters are real, but 2 clusters are more reproducible.

### 2.3 DBSCAN with eps=0.3 Gave 94.6% Noise

This was extreme — almost every point was labeled as noise. This shows that eps=0.3 is too small and causes overfitting.

**Lesson:** Choosing the right eps is critical for DBSCAN.

---

## 3. Challenges I Faced

### 3.1 Understanding Stability Testing

The concept of stability was initially confusing. I had to think about why resampling the data and clustering again would tell me if clusters are real.

### 3.2 Interpreting Overfitting in GMM

Understanding why training likelihood rises while test likelihood falls took some time. I learned that the model is fitting noise in the training data.

### 3.3 Why Silhouette Score Didn't Find k=3

This was the most surprising result. I had to think about the shape of the data and the assumptions of K-Means.

---

## 4. How I Overcame Them

- I reviewed the lecture notes and documentation
- I experimented with different parameters
- I used visualizations to understand the results
- I compared multiple metrics to confirm findings

---

## 5. Key Takeaways

### 5.1 Accuracy is Meaningless

Cluster IDs are just names. Renaming them changes "accuracy" even though the grouping is the same. Use ARI instead.

### 5.2 Silhouette Score is Useful but Not Perfect

Silhouette Score found k=2, but the true K is 3. This shows that Silhouette Score is not always correct, especially when clusters are not spherical.

### 5.3 Stability is Powerful

Stability testing confirmed that both 2 and 3 clusters are real. This is a powerful way to validate clusters.

### 5.4 Overfitting is Detectable

Even without labels, overfitting can be detected by comparing training and test scores.

### 5.5 DBSCAN is Sensitive to eps

Choosing the right eps is critical for DBSCAN. Too small eps creates too much noise, and too large eps merges clusters.

---

## 6. What I Would Do Differently

- Try other clustering algorithms (Agglomerative Clustering, GMM)
- Use more features for clustering
- Explore the data more thoroughly before clustering
- Use cross-validation for more reliable evaluation

---

## 7. Honest Difficulty Assessment

| Task | Difficulty (1-10) | Why |
|------|-------------------|-----|
| Part 1: Why Accuracy Fails | 3 | Easy to understand with examples |
| Part 2: Silhouette Score | 4 | Straightforward to implement |
| Part 3: Stability Testing | 7 | Required deeper understanding of resampling |
| Part 4: Overfitting with GMM | 6 | Understanding log-likelihood took some time |
| Part 5: DBSCAN | 5 | Trial and error to find optimal eps |

---

## 8. What Surprised Me

- Silhouette Score suggested k=2 instead of k=3
- Stability had perfect score (1.000) for k=2
- DBSCAN with eps=0.3 gave 94.6% noise
- How clearly overfitting appeared in the GMM scores

---

## 9. The Most Important Lesson

> A metric that improves every time you add complexity cannot be used to choose complexity. Inertia and reconstruction error both fail this test. Silhouette, held-out likelihood, BIC, and stability all pass it.

---

## 10. One Sentence Summary

> This assignment taught me that unsupervised learning requires different evaluation methods — Silhouette Score, stability, and held-out likelihood — because accuracy is meaningless for clustering.

---

## 11. What I Will Take Forward

1. Never use accuracy for clustering
2. Always use multiple metrics (Silhouette, Stability, ARI)
3. Use stability testing to check if clusters are real
4. Split data to detect overfitting
5. Understand the complexity dial in each algorithm

---

## 12. Final Thoughts

This assignment was a valuable learning experience because it:

1. Showed why accuracy fails in unsupervised learning
2. Introduced practical metrics for evaluating clusters
3. Taught how to detect overfitting without labels
4. Demonstrated the importance of stability testing
5. Built confidence in evaluating unsupervised models

The most surprising result was Silhouette Score finding k=2 instead of k=3. This taught me that no single metric is perfect, and it's important to use multiple metrics together.