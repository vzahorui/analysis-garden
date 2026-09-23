---
tags:
  - ML
---
# Standard Scaling

This technique forces individual numerical features to share a mean of **0** and a standard deviation of **1**. 

This process converts raw data values into **z-scores**, which measure how many standard deviations a value lies away from the feature's average.
## The Mathematical Formula

For every sample value $x$ in a feature column, `StandardScaler` calculates the scaled value $z$:
$$z = \frac{x - \mu}{\sigma}$$
- $x$: The original raw value.
- $\mu$: The mean of the feature column.
- $\sigma$: The standard deviation of the feature column.
## Key Properties

- **Rescaling, Not Normalizing (Shape Preservation):** StandardScaler centers and rescales the data, but it does **not** alter the distribution shape. If a feature is skewed before scaling, it remains skewed after scaling.
- **Sensitivity to Outliers:** Because both the sample mean ($\mu$) and sample standard deviation ($\sigma$) are sensitive to extreme values, a few severe outliers can distort the scaling, compressing non-outlier data into a tiny range.
## When to Use (and Avoid) StandardScaler

| **Use Case / Algorithm**                                                                                              | **Requires StandardScaler?** | **Reason**                                                                                                                                   |
| --------------------------------------------------------------------------------------------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **Distance-based algorithms** (k-NN, [[Support Vector Machine\|SVM]], K-Means Clustering)                             | **Yes**                      | Prevents large-scale features from dominating distance calculations (Euclidean/Manhattan distance).                                          |
| [[Gradient Descent]] algorithms ([[Linear Regression]], [[Logistic Regression]], [[Neural Network\|Neural Networks]]) | **Yes**                      | Ensures smooth, stable, and fast gradient convergence during training.                                                                       |
| **Regularized models** (Lasso, Ridge Regression)                                                                      | **Yes**                      | Penalty terms ($L_1$/$L_2$) apply uniformly across features only when all features share the same variance.                                  |
| **Dimensionality Reduction** ([[Principal Component Analysis\|PCA]])                                                  | **Yes**                      | PCA aims to maximize variance; unscaled features with large absolute numbers will dominate principal components regardless of actual signal. |
| [[Tree-Based Algorithms]] ([[Random Forest]], XGBoost, Decision Trees)                                                | **No**                       | Decision trees split features independently based on thresholds; monotone transformations do not affect tree splits.                         |
