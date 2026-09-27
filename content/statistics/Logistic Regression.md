---
tags:
  - statistics
  - ML/classification
---
**Logistic regression** is a statistical [[classification]] algorithm used to predict the probability of a categorical outcome based on one or more input features. Despite having "regression" in its name, it is primarily used for **binary classification** (e.g., predicting whether an email is spam/not spam, or if a transaction is fraudulent/legitimate).

## Core Mechanics

Instead of modeling the outcome $y$ directly as a continuous straight line (like [[Linear Regression]]), Logistic Regression creates a linear combination of inputs:

$$z = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \dots + \beta_n x_n$$

and then passes through a non-linear activation function called the [[Sigmoid Function]]. 

$z$ is often called the **logit** or the **raw score** (or "pre-activation" value). $z$ itself exists on the real number line, meaning it can take **any value from $-\infty$ to $+\infty$**.

The Sigmoid function, $\sigma(z) = \frac{1}{1 + e^{-z}}$, takes that unbounded number $z$ and squashes (maps) it into the range **$(0, 1)$**.

### Decision Boundary

To make a final class assignment (0 or 1), a decision threshold is applied to the probability output (commonly **0.5**):

$$\hat{y} = \begin{cases} 1 & \text{if } P(y=1\vert{}X) \ge 0.5 \quad (z \ge 0) \\ 0 & \text{if } P(y=1\vert{}X) < 0.5 \quad (z < 0) \end{cases}$$
## Log-Odds

Log-odds brings back constant, linear interpretability to a non-linear output of the model. But first let's see where they appear and why.

So Logistic Regression predicts probability $p = P(y=1\vert{}X)$ using the sigmoid activation function operating on $z$ (the raw linear score/logit):

$$p = \sigma(z) = \frac{1}{1 + e^{-z}}$$

### What are odds?

**Odds** are defined as the ratio of the probability of an event happening to the probability of it not happening:

$$\text{Odds} = \frac{p}{1 - p}$$
By inserting the predicted probability expression into the odds formula it is simplified to $e^z$.

First, express $1 - p$:

$$1 - p = 1 - \frac{1}{1 + e^{-z}} = \frac{(1 + e^{-z}) - 1}{1 + e^{-z}} = \frac{e^{-z}}{1 + e^{-z}}$$

Now divide $p$ by $1 - p$:

$$\text{Odds} = \frac{\frac{1}{1 + e^{-z}}}{\frac{e^{-z}}{1 + e^{-z}}} = \frac{1}{e^{-z}} = e^z$$

### Log-odds

Taking the natural log ($\ln$) of both sides isolates $z$:

$$\ln(\text{Odds}) = \ln\left(\frac{p}{1 - p}\right) = \ln(e^z) = z$$

Logistic regression explicitly models the **log-odds** (logit) of the positive class as a linear function of the inputs:

$$\text{logit}(p) = \ln\left(\frac{p}{1 - p}\right) = \beta_0 + \beta_1 x_1 + \dots + \beta_n x_n$$

- **Odds Ratio ($\frac{p}{1-p}$):** The ratio of the probability of an event occurring to the probability of it not occurring.
- **Interpretation of Coefficients ($\beta_i$):** Increasing input feature $x_i$ by one unit multiplies the odds of the outcome by $e^{\beta_i}$.

## Parameter Estimation & Optimization

Unlike Linear Regression, which uses Ordinary Least Squares (OLS) with a closed-form solution, Logistic Regression uses [[Maximum Likelihood Estimation]] (MLE) to estimate coefficients.

### Loss Function: Binary [[Cross-Entropy]] (Log Loss)

For a single training example with true label $y \in \{0, 1\}$ and predicted probability $\hat{p}$:

$$\mathcal{L}(y, \hat{p}) = -\left[ y \ln(\hat{p}) + (1 - y) \ln(1 - \hat{p}) \right]$$

- If $y = 1$, loss is $-\ln(\hat{p})$. As $\hat{p} \to 1$, loss approaches 0; as $\hat{p} \to 0$, loss approaches $\infty$.
- If $y = 0$, loss is $-\ln(1 - \hat{p})$.

The model minimizes the total log loss across all dataset samples using iterative optimization algorithms such as [[Gradient Descent]], **L-BFGS**, or **Newton-Raphson ([[Newton's Method]])**.

### Why Not [[Mean Squared Error]] (MSE)?

If you try to use MSE ($\frac{1}{2}(y - \hat{p})^2$) with the Sigmoid function, the loss surface becomes **non-convex** with many local minima and flat regions ("plateaus").

When a model is confidently wrong (e.g., $y=1$, but $\hat{p} \approx 0$), the [[derivative]] of the Sigmoid function drops to nearly zero ($\sigma'(z) \to 0$). Gradient descent gets stuck because the gradient vanishes, leaving the model unable to correct its mistakes.

### Deriving Log Loss from First Principles (Likelihood)

Instead of measuring Euclidean [[Vector Norm#L2 Norm (Euclidean Norm)|Euclidean distance]], Logistic Regression asks: _"What weights maximize the probability of observing our actual training dataset?"_

For a single example:

- If true label $y = 1$, the probability of getting $y$ is $\hat{p}$.
- If true label $y = 0$, the probability of getting $y$ is $1 - \hat{p}$.

We can combine these two cases into a single formula for [[Bernoulli Trial]] probability:

$$P(y \mid X) = \hat{p}^y \cdot (1 - \hat{p})^{1-y}$$

- If $y=1$: $\hat{p}^1 \cdot (1 - \hat{p})^0 = \hat{p}$
- If $y=0$: $\hat{p}^0 \cdot (1 - \hat{p})^1 = 1 - \hat{p}$

#### Converting Likelihood to Loss

To find the optimal weights across $N$ independent data points, we multiply their probabilities together (Joint Likelihood):

$$L(\theta) = \prod_{i=1}^N \hat{p}_i^{y_i} \cdot (1 - \hat{p}_i)^{1-y_i}$$

Multiplying thousands of small numbers between $0$ and $1$ causes numerical underflow in computers. To fix this, we apply the natural log ($\ln$), turning products into sums:

$$\ln L(\theta) = \sum_{i=1}^N \left[ y_i \ln(\hat{p}_i) + (1 - y_i) \ln(1 - \hat{p}_i) \right]$$

Since optimization algorithms are built to **minimize loss** (cost) rather than maximize likelihood, we negate the log-likelihood:

$$\text{Log Loss} = -\sum_{i=1}^N \left[ y_i \ln(\hat{p}_i) + (1 - y_i) \ln(1 - \hat{p}_i) \right]$$
### Penalty Behavior

Log Loss heavily penalizes confident incorrect predictions:

- **When $y = 1$:** Loss is $-\ln(\hat{p})$.
    - If $\hat{p} = 0.99 \implies -\ln(0.99) \approx 0.01$ (Tiny penalty)
    - If $\hat{p} = 0.01 \implies -\ln(0.01) \approx 4.60$ (Huge penalty)

Log loss ensures a **smooth, convex loss curve** with a single global minimum, allowing [[gradient descent]] to converge reliably.

## Strengths & Limitations

- **Strengths:** Highly interpretable coefficients, outputs well-calibrated probabilities, computationally efficient, easy to [[Regularization|regularize]] ($L_1$ Lasso or $L_2$ Ridge) to prevent overfitting.
- **Limitations:** Assumes linear decision boundaries in feature space; struggles with non-linear relationships without manual feature engineering or kernel methods; vulnerable to multicollinearity and complete separation.

# Other References

* [[Softmax Function]] as a generalization for multiclass classification. 