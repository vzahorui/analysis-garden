---
tags:
  - statistics
  - ML/loss
aliases:
  - MSE
  - RMSE
---
**Mean Squared Error (MSE)** measures the average squared difference between estimated values (predictions) and the actual value (ground truth). 

# Mathematical Definition

For a parameter $\theta$ and its estimator $\hat{\theta}$, the theoretical MSE is defined as:

$$\text{MSE}(\hat{\theta}) = \mathbb{E}\left[ (\hat{\theta} - \theta)^2 \right]$$

In sample statistical estimation or machine learning training with $n$ observations, actual targets $y_i$, and predicted targets $\hat{y}_i$:

$$\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$

# Core Applications & Interpretations

## Loss Function & Metric

In supervised [[regression]] tasks, MSE serves two purposes:

- **Optimization (Loss Function):** As a smooth, differentiable function, its gradient directs optimization algorithms like [[gradient descent]]:
$$\frac{\partial \text{MSE}}{\partial \hat{y}_i} = -\frac{2}{n} (y_i - \hat{y}_i)$$
- **Model Evaluation Metric:** Measures residual magnitude across test datasets AFTER the model is fit.

See [[Loss vs Metric]] to better understand the distinction.

## Bias-Variance Decomposition

MSE decomposes into two primary components of estimator error [[Bias and Variance]]:

$$\text{MSE}(\hat{\theta}) = \text{Var}(\hat{\theta}) + \left(\text{Bias}(\hat{\theta})\right)^2$$
### Algebraic Drivation

Using the original formula, add and subtract $\mathbb{E}[\hat{\theta}]$ inside the square:
$$\text{MSE}(\hat{\theta}) = \mathbb{E}\left[ \Big( (\hat{\theta} - \mathbb{E}[\hat{\theta}]) + (\mathbb{E}[\hat{\theta}] - \theta) \Big)^2 \right]$$
Expanding the squared binomial inside the [[expectation]]:
$$\text{MSE}(\hat{\theta}) = \mathbb{E}\left[ (\hat{\theta} - \mathbb{E}[\hat{\theta}])^2 + 2(\hat{\theta} - \mathbb{E}[\hat{\theta}])(\mathbb{E}[\hat{\theta}] - \theta) + (\mathbb{E}[\hat{\theta}] - \theta)^2 \right]$$
By the linearity of expectation, we distribute $\mathbb{E}[\cdot]$ across the three terms:
$$\text{MSE}(\hat{\theta}) = \mathbb{E}\left[(\hat{\theta} - \mathbb{E}[\hat{\theta}])^2\right] + 2\mathbb{E}\left[(\hat{\theta} - \mathbb{E}[\hat{\theta}])(\mathbb{E}[\hat{\theta}] - \theta)\right] + \mathbb{E}\left[(\mathbb{E}[\hat{\theta}] - \theta)^2\right]$$
#### Evaluating Each Term

**Variance Term:**

By definition, the expected squared deviation of an estimator from its own mean is its variance:
$$\mathbb{E}\left[(\hat{\theta} - \mathbb{E}[\hat{\theta}])^2\right] = \text{Var}(\hat{\theta})$$
**Cross-Product Term:**

Since the true parameter $\theta$ and the expected value $\mathbb{E}[\hat{\theta}]$ are fixed deterministic numbers (constants), the term $(\mathbb{E}[\hat{\theta}] - \theta)$ can be pulled outside the expectation:
$$\mathbb{E}\left[(\hat{\theta} - \mathbb{E}[\hat{\theta}])(\mathbb{E}[\hat{\theta}] - \theta)\right] = (\mathbb{E}[\hat{\theta}] - \theta) \cdot \mathbb{E}\left[\hat{\theta} - \mathbb{E}[\hat{\theta}]\right]$$
Distributing the expectation gives $\mathbb{E}[\hat{\theta}] - \mathbb{E}[\hat{\theta}] = 0$, causing the entire cross-product term to vanish:
$$2(\mathbb{E}[\hat{\theta}] - \theta) \cdot 0 = 0$$
**Squared Bias Term:**

Because $(\mathbb{E}[\hat{\theta}] - \theta)$ contains only constants, its expectation is simply the quantity itself. The term $(\mathbb{E}[\hat{\theta}] - \theta)$ defines the **Bias** of the estimator:

$$\mathbb{E}\left[(\mathbb{E}[\hat{\theta}] - \theta)^2\right] = (\mathbb{E}[\hat{\theta}] - \theta)^2 = \left(\text{Bias}(\hat{\theta})\right)^2$$
# Key Mathematical & Practical Properties

- **Sensitivity to Outliers:** Because [[Residual vs Error|residual]] terms $(y_i - \hat{y}_i)$ are squared, large deviations carry disproportionately high weights relative to small deviations.
- **Scale Dependency:** Units of MSE are the square of the original target variable units. Taking the square root yields the **Root Mean Squared Error (RMSE)**, returning [[Loss vs Metric|metrics]] to the original unit scale.
- **Maximum Likelihood Equivalence:** Minimizing MSE under [[Least Squares#Ordinary Least Squares (OLS)]] is equivalent to [[Maximum Likelihood Estimation]] (MLE) under the assumption that residuals are [[Normal Distribution|normally]] and independently distributed:
$$\varepsilon_i = y_i - \hat{y}_i \sim \mathcal{N}(0, \sigma^2)$$

It quantifies the variance and squared bias of an estimator, providing a single non-negative metric for estimation quality.

# Why MSE is MLE under Normally and Independetly Distributed Residuals

The [[Probability Distributions#Continuous Probability Distributions|probability density function]] (PDF) for a single observation $y_i$ in a [[Linear Models|linear model]] is:

$$f(y_i \mid \mathbf{x}_i, \boldsymbol{\beta}, \sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{(y_i - \mathbf{x}_i^T \boldsymbol{\beta})^2}{2\sigma^2} \right)$$
Because the observations are independent, the joint probability (the **Likelihood function**) of observing all $n$ data points is the product of their individual probabilities:

$$L(\boldsymbol{\beta}, \sigma^2 \mid \mathbf{y}, \mathbf{X}) = \prod_{i=1}^{n} f(y_i \mid \mathbf{x}_i, \boldsymbol{\beta}, \sigma^2)$$
$$L(\boldsymbol{\beta}, \sigma^2 \mid \mathbf{y}, \mathbf{X}) = \prod_{i=1}^{n} \left[ \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{(y_i - \mathbf{x}_i^T \boldsymbol{\beta})^2}{2\sigma^2} \right) \right]$$

Maximizing the likelihood $L(\boldsymbol{\beta}, \sigma^2)$ is mathematically equivalent to maximizing its natural logarithm, $\ell(\boldsymbol{\beta}, \sigma^2) = \ln L(\boldsymbol{\beta}, \sigma^2)$:

$$\ell(\boldsymbol{\beta}, \sigma^2) = \ln \left[ \left(2\pi\sigma^2\right)^{-n/2} \exp\left( -\frac{1}{2\sigma^2} \sum_{i=1}^{n} (y_i - \mathbf{x}_i^T \boldsymbol{\beta})^2 \right) \right]$$

Applying logarithm properties ($\ln(ab) = \ln(a) + \ln(b)$ and $\ln(e^x) = x$):

$$\ell(\boldsymbol{\beta}, \sigma^2) = -\frac{n}{2}\ln(2\pi) - \frac{n}{2}\ln(\sigma^2) - \frac{1}{2\sigma^2} \sum_{i=1}^{n} (y_i - \mathbf{x}_i^T \boldsymbol{\beta})^2$$
## Maximizing Likelihood with Respected to a Parameter

When estimating the parameters $\boldsymbol{\beta}$, we hold the variance $\sigma^2$ constant. Look at how each term in the log-likelihood relies on $\boldsymbol{\beta}$:

- $-\frac{n}{2}\ln(2\pi)$ is a constant with respect to $\boldsymbol{\beta}$.
- $-\frac{n}{2}\ln(\sigma^2)$ is a constant with respect to $\boldsymbol{\beta}$.
- $-\frac{1}{2\sigma^2} \sum_{i=1}^{n} (y_i - \mathbf{x}_i^T \boldsymbol{\beta})^2$ is the **only term containing $\boldsymbol{\beta}$**.

Therefore, maximizing $\ell(\boldsymbol{\beta}, \sigma^2)$ reduces to maximizing:

$$\arg\max_{\boldsymbol{\beta}} \ell(\boldsymbol{\beta}, \sigma^2) = \arg\max_{\boldsymbol{\beta}} \left( -\frac{1}{2\sigma^2} \sum_{i=1}^{n} (y_i - \mathbf{x}_i^T \boldsymbol{\beta})^2 \right)$$

Since $\frac{1}{2\sigma^2}$ is a positive scalar constant, maximizing a negative quantity is strictly equivalent to **minimizing** the positive summation term:

$$\arg\max_{\boldsymbol{\beta}} \ell(\boldsymbol{\beta}, \sigma^2) = \arg\min_{\boldsymbol{\beta}} \sum_{i=1}^{n} (y_i - \mathbf{x}_i^T \boldsymbol{\beta})^2$$
The term being minimized above is the **Sum of Squared Errors (SSE)**:

$$\text{SSE}(\boldsymbol{\beta}) = \sum_{i=1}^{n} (y_i - \mathbf{x}_i^T \boldsymbol{\beta})^2$$
Since dividing by a positive constant $n$ does not change the position of the minimum:
$$\arg\min_{\boldsymbol{\beta}} \text{SSE}(\boldsymbol{\beta}) \iff \arg\min_{\boldsymbol{\beta}} \frac{1}{n}\sum_{i=1}^{n} (y_i - \mathbf{x}_i^T \boldsymbol{\beta})^2 = \arg\min_{\boldsymbol{\beta}} \text{MSE}(\boldsymbol{\beta})$$