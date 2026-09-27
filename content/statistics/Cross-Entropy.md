---
tags:
  - ML
  - statistics
---
Cross-entropy measures the difference between two [[Probability Distributions]]: a target distribution $p$ (the ground truth) and an estimated distribution $q$ (the model's prediction).

In [[Machine Learning Concepts|Machine Learning]], it serves as the standard [[Loss vs Metric|loss]] function for classification models. It penalizes predictions that are confidently wrong heavily, driving the model output toward the true distribution.

## The Intuition: Information Theory

To understand cross-entropy, it helps to build from the basics of information theory:

- **[[Entropy]] $H(p)$:** The average amount of uncertainty or information required to represent events following distribution $p$. It represents the theoretical minimum average length (in bits or nats) needed to encode messages from $p$.

$$H(p) = -\sum_{x} p(x) \log p(x)$$
- **Cross-Entropy $H(p, q)$:** The average message length required if you construct an encoding scheme optimized for a predicted distribution $q$, but the actual messages arrive according to distribution $p$.

$$H(p, q) = -\sum_{x} p(x) \log q(x)$$

Because $q$ is an approximation of $p$, cross-entropy is always greater than or equal to true entropy ($H(p, q) \ge H(p)$). The difference between the two is the [[Kullback-Leibler Divergence]]:

$$H(p, q) = H(p) + D_{\text{KL}}(p \parallel q)$$

Minimizing cross-entropy during model training directly minimizes $D_{\text{KL}}(p \parallel q)$, forcing the predicted distribution $q$ to match $p$.

## Formulations in Machine Learning

### Binary Cross-Entropy (BCE)

Used when classifying inputs into two mutually exclusive categories ($y \in \{0, 1\}$). Given a true label $y$ and predicted probability $\hat{y} \in (0, 1)$:

$$\mathcal{L}_{\text{BCE}}(y, \hat{y}) = - \left[ y \log(\hat{y}) + (1 - y) \log(1 - \hat{y}) \right]$$

- **If $y = 1$:** The loss simplifies to $-\log(\hat{y})$. As $\hat{y} \to 1$, loss $\to 0$. As $\hat{y} \to 0$, loss $\to \infty$.
- **If $y = 0$:** The loss simplifies to $-\log(1 - \hat{y})$. As $\hat{y} \to 0$, loss $\to 0$. As $\hat{y} \to 1$, loss $\to \infty$.

### Categorical Cross-Entropy (Multi-class)

Used when classifying inputs into $C$ mutually exclusive classes. With a [[Encoding Categorical Variables#One-Hot Encoding (OHE)]] ground truth vector $y$ and [[Softmax Function]] outputs $\hat{y}$:

$$\mathcal{L}_{\text{CCE}}(y, \hat{y}) = -\sum_{c=1}^{C} y_c \log(\hat{y}_c)$$

Since $y$ is one-hot (where $y_k = 1$ for the true class $k$, and $0$ otherwise), this reduces to evaluating the negative log-likelihood of the correct class:

$$\mathcal{L} = -\log(\hat{y}_k)$$

## Why Use Cross-Entropy Over Mean Squared Error (MSE)?

1. **Steeper [[Derivative#Gradient]] for Wrong Predictions:** [[Mean Squared Error|MSE]] combined with a Sigmoid/Softmax activation produces small gradients when the prediction is completely wrong (due to [[derivative]] saturation at $0$ and $1$). Cross-entropy's logarithmic term cancels out the activation derivative, maintaining large [[Gradient Descent|gradient updates]] when error is high.
2. **Probabilistic Interpretation:** Minimizing cross-entropy is equivalent to [[Maximum Likelihood Estimation]] (MLE) under a [[Bernoulli Trial|Bernoulli]] or Categorical distribution.