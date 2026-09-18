---
tags:
  - statistics
aliases:
  - MSE
---
**Mean Squared Error (MSE)** measures the average squared difference between estimated values (predictions) and the actual value (ground truth). 

# Mathematical Definition

For a parameter $\theta$ and its estimator $\hat{\theta}$, the theoretical MSE is defined as:

$$\text{MSE}(\hat{\theta}) = \mathbb{E}\left[ (\hat{\theta} - \theta)^2 \right]$$

In sample statistical estimation or machine learning training with $n$ observations, actual targets $y_i$, and predicted targets $\hat{y}_i$:

$$\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$

# Core Applications & Interpretations

## 1. Statistics: Bias-Variance Decomposition

In mathematical statistics, MSE decomposes into two primary components of estimator error:

$$\text{MSE}(\hat{\theta}) = \text{Var}(\hat{\theta}) + \left(\text{Bias}(\hat{\theta})\right)^2$$

- **Bias:** $\mathbb{E}[\hat{\theta}] - \theta$ (systematic error off the true target value).
    
- **Variance:** $\mathbb{E}\left[(\hat{\theta} - \mathbb{E}[\hat{\theta}])^2\right]$ (estimation sensitivity to sample variability).
    

This formulation illustrates the classic trade-off: biased estimators (e.g., Ridge regression) can achieve a lower total MSE if they sufficiently reduce variance compared to unbiased estimators (e.g., OLS).

## 2. Machine Learning: Loss Function & Metric

In supervised regression tasks, MSE serves two functions:

- **Optimization (Loss Function):** As a smooth, differentiable function, its gradient directs optimization algorithms like gradient descent:
$$\frac{\partial \text{MSE}}{\partial \hat{y}_i} = -\frac{2}{n} (y_i - \hat{y}_i)$$
- **Model Evaluation Metric:** Measures residual magnitude across test datasets AFTER the model is fit.


It quantifies the variance and squared bias of an estimator, providing a single non-negative metric for estimation quality.