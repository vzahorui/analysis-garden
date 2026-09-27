---
tags:
  - statistics
aliases:
  - Expected values
  - Expected value
  - mean
---
The **expectation** (or expected value) of a [[Set Theory#Random Variable]] is its theoretical long-run average value across infinite trials. It represents the center of mass of the [[Probability Distributions]].

## Expectation of a Random Variable

For a random variable $X$, the expectation $\mathbb{E}[X]$ is calculated by multiplying each possible value $x$ by its probability $P(X=x)$ or probability density $f(x)$, and summing or [[Integral|integrating]] over all possible values:

- **Discrete Random Variable:**
$$\mathbb{E}[X] = \sum_{i} x_i P(X = x_i)$$
- **Continuous Random Variable:**
$$\mathbb{E}[X] = \int_{-\infty}^{\infty} x f(x) \, dx$$

**Example:** Rolling a fair 6-sided die.

$$\mathbb{E}[X] = 1\left(\frac{1}{6}\right) + 2\left(\frac{1}{6}\right) + 3\left(\frac{1}{6}\right) + 4\left(\frac{1}{6}\right) + 5\left(\frac{1}{6}\right) + 6\left(\frac{1}{6}\right) = \frac{21}{6} = 3.5$$

## Expectation of a Function of a Random Variable

When applying a function $g(x)$ to a random variable $X$, you create a new random variable $Y = g(X)$. By the **Law of the Unconscious Statistician (LOTUS)**, you do not need to find the probability distribution of $Y$ first; you simply apply the function $g(x)$ directly to the values of $X$ weighted by $X$'s original probabilities:

- **Discrete:**
$$\mathbb{E}[g(X)] = \sum_{i} g(x_i) P(X = x_i)$$
- **Continuous:**
$$\mathbb{E}[g(X)] = \int_{-\infty}^{\infty} g(x) f(x) \, dx$$
## Variance

Variance measures the expected squared spread or dispersion of $X$ around its mean $\mu = \mathbb{E}[X]$.

$$\text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
Expanding the quadratic inside the expectation demonstrates the standard computational identity:

$$\begin{aligned} \text{Var}(X) = \mathbb{E}\left[X^2 - 2X\mathbb{E}[X] + (\mathbb{E}[X])^2\right] \end{aligned}$$
Using the linearity of expectation ($\mathbb{E}[aA + bB] = a\mathbb{E}[A] + b\mathbb{E}[B]$ and treating $\mathbb{E}[X]$ as a constant):

$$\begin{aligned} \text{Var}(X) &= \mathbb{E}[X^2] - 2\mathbb{E}[X]\mathbb{E}[X] + (\mathbb{E}[X])^2 \\ &= \mathbb{E}[X^2] - 2(\mathbb{E}[X])^2 + (\mathbb{E}[X])^2 \\ &= \mathbb{E}[X^2] - (\mathbb{E}[X])^2 \end{aligned}$$
So the computational identity for variance states that **variance is the mean of the squares minus the square of the mean**.