---
tags:
  - statistics
aliases:
  - MLE
  - maximum likelihood
---
To understand **Maximum Likelihood Estimation (MLE)**, we need to first separate the concept of _likelihood_ from _probability_, as they look at the exact same relationship from opposite directions.

## What is Likelihood?

In everyday language, "probability" and "likelihood" mean the same thing. In statistics, they are exact inverses:

- **Probability** asks: _Given a known parameter/model, what is the chance of observing a specific outcome?_
$$\text{Probability} = P(\text{Data} \mid \text{Parameter})$$
- **Likelihood** asks: _Given an observed outcome, how plausible is a specific parameter value?_
$$L(\text{Parameter} \mid \text{Data}) = P(\text{Data} \mid \text{Parameter})$$
These formulas use the notion of [[Multiple Random Variables#Conditional Probability]]. 
### The Coin Flip Example

Imagine a coin with an unknown probability $p$ of landing on heads. You flip it **10 times** and observe **8 heads**.

- **The Data ($k$):** Fixed at 8 heads out of 10.
- **The Parameter ($p$):** Unknown variable between 0 and 1.

Using the Binomial probability formula $P(k=8 \mid p) = \binom{10}{8} p^8 (1-p)^2$, let's test a few candidate values for $p$:

- If $p = 0.2$ (a heavily biased tail coin), the chance of getting 8 heads is about **0.00007**.
- If $p = 0.5$ (a fair coin), the chance of getting 8 heads is about **0.0439** (4.4%).
- If $p = 0.8$ (a biased head coin), the chance of getting 8 heads is about **0.3020** (30.2%).

The **likelihood** of $p=0.8$ given our data is $0.3020$, whereas the likelihood of $p=0.5$ is only $0.0439$. The observed data is almost 7 times more plausible under $p=0.8$ than under $p=0.5$.

> **Key takeaway:** A likelihood function is a function of the _parameter_, holding the observed _data_ fixed. Unlike probabilities, likelihood values do **not** sum or integrate to 1.

## What is Maximum Likelihood Estimation (MLE)?

**Maximum Likelihood Estimation** is a method for estimating the unknown parameters of a probability distribution by finding the parameter value that **maximizes** the likelihood function.

In plain terms: **Which parameter value makes the data we actually observed most likely to occur?**
$$\hat{\theta}_{\text{MLE}} = \arg\max_{\theta} L(\theta \mid x)$$
## How MLE Works (Step-by-Step)

For a collection of independent and identically distributed (i.i.d.) observations $x_1, x_2, \dots, x_n$:
### Step 1: Define the Likelihood Function

Since the observations are independent, the joint probability (likelihood) is the product of the individual probabilities:

$$L(\theta) = \prod_{i=1}^{n} f(x_i \mid \theta)$$

### Step 2: Take the Log-Likelihood

Multiplying many small probabilities can cause numerical underflow, and taking derivatives of products is tedious. We apply the natural logarithm $\ln()$ to convert products into sums. Because the logarithm is a strictly increasing function, maximizing $\ln L(\theta)$ yields the exact same optimal $\theta$ as maximizing $L(\theta)$:

$$\ell(\theta) = \ln L(\theta) = \sum_{i=1}^{n} \ln f(x_i \mid \theta)$$

### Step 3: Find the Maximum

To find the peak of the log-likelihood curve:

1. Compute the [[derivative]] with respect to $\theta$: $\frac{d}{d\theta} \ell(\theta)$
2. Set the derivative equal to zero: $\frac{d}{d\theta} \ell(\theta) = 0$
3. Solve for $\theta$ (and check the second derivative $\frac{d^2}{d\theta^2} \ell(\theta) < 0$ to confirm it's a maximum).

Below is an example of estimating $\mu$ parameter of a [[Normal Distribution]] among different candidates:

![[Maximum Likelihood Estimation-1790501262431.webp]]
## Why is MLE So Popular?

- **Asymptotic Efficiency:** As your sample size $n \to \infty$, MLE achieves the lowest possible variance among unbiased estimators (reaching the Cramér-Rao lower bound).
- **Consistency:** With enough data, the MLE estimate converges to the true population parameter.
- **Invariance Property:** If $\hat{\theta}$ is the MLE of $\theta$, then for any function $g(\theta)$, the MLE of $g(\theta)$ is simply $g(\hat{\theta})$.
- **Versatility:** Works across [[Linear Models]], [[Logistic Regression]], [[Neural Network|Neural Networks]] (where minimizing[[Cross-Entropy]] loss is equivalent to maximizing log-likelihood), and complex time-series models.

