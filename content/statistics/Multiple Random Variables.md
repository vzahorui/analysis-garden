---
tags:
  - statistics
---
Here is how multiple [[Set Theory#Random Variable|random variables]] work together. 

## Joint [[Probability Distributions|Probability Distribution]] Function

When dealing with two random variables $X$ and $Y$ defined on the same sample space, the **joint probability distribution** describes the probability that $X$ and $Y$ simultaneously take on specific values.

- **Discrete Case (Joint PMF):**
$$p_{X,Y}(x, y) = P(X = x, Y = y)$$
The sum over all possible pairs $(x,y)$ must equal 1: $\sum_x \sum_y p_{X,Y}(x, y) = 1$.

- **Continuous Case (Joint PDF):**

A joint probability density function $f_{X,Y}(x,y)$ satisfies:

$$P(a \le X \le b, c \le Y \le d) = \int_{c}^{d} \int_{a}^{b} f_{X,Y}(x, y) \, dx \, dy$$
The double [[integral]] over the entire plane equals 1: $\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} f_{X,Y}(x, y) \, dx \, dy = 1$.

## Marginalization (Marginal Distributions)

**Marginalization** is the process of isolating the distribution of a single random variable by summing or integrating out all other random variables from the joint distribution.

- **Discrete Case:** To find the marginal PMF of $X$, sum over all possible values of $Y$:
$$p_X(x) = \sum_{y} p_{X,Y}(x, y)$$
- **Continuous Case:** To find the marginal PDF of $X$, integrate out $Y$ from $-\infty$ to $\infty$:
$$f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x, y) \, dy$$
Assuming any output of $Y$ we want to know the probability of $X$. 

## Conditional Probability

The **conditional distribution** gives the probability distribution of one random variable given that another random variable has been observed to take a specific value.

- **Discrete Case:**
$$p_{Y\vert{}X}(y \mid x) = P(Y = y \mid X = x) = \frac{p_{X,Y}(x, y)}{p_X(x)} \quad \text{for } p_X(x) > 0$$
- **Continuous Case:**
$$f_{Y\vert{}X}(y \mid x) = \frac{f_{X,Y}(x, y)}{f_X(x)} \quad \text{for } f_X(x) > 0$$
Conditional probabilities normalize the joint probability slice at $X = x$ by dividing by the total probability weight assigned to that slice ($p_X(x)$ or $f_X(x)$).

## Bayes’ Theorem

From the definition of conditional probability, the joint probability can be written in two ways (the product rule):

$$p_{X,Y}(x, y) = p_{Y\vert{}X}(y \mid x) \cdot p_X(x) = p_{X\vert{}Y}(x \mid y) \cdot p_Y(y)$$
Equating these two expressions and solving for $p_{Y\vert{}X}(y \mid x)$ yields **Bayes' Theorem**:

$$p_{Y\vert{}X}(y \mid x) = \frac{p_{X\vert{}Y}(x \mid y) \cdot p_Y(y)}{p_X(x)}$$
Or vie a classic formula:
$$P(A\vert{}B) = \frac{P(B\vert{}A) \cdot P(A)}{P(B)}$$

Where:
- **$P(A\vert{}B)$ — Posterior Probability:** The probability that hypothesis $A$ is true given that evidence $B$ occurred.
- **$P(A)$ — Prior Probability:** Your initial degree of belief in hypothesis $A$ before seeing evidence $B$.
- **$P(B\vert{}A)$ — Likelihood:** The probability of observing evidence $B$ if hypothesis $A$ is true.
- **$P(B)$ — Marginal Likelihood (Evidence):** The total probability of observing evidence $B$ under all possible scenarios:
### How it reverses conditioning

If you know $p_{X\vert{}Y}(x \mid y)$, how observation $X$ behaves given a hidden cause $Y$, then Bayes' theorem allows you to "invert" the conditioning to find $p_{Y\vert{}X}(y \mid x)$—how likely cause $Y$ is given that you observed $X$.

Using marginalization, the denominator $p_X(x)$ can be expanded:

$$p_{Y\vert{}X}(y \mid x) = \frac{p_{X\vert{}Y}(x \mid y) \cdot p_Y(y)}{\sum_{y'} p_{X\vert{}Y}(x \mid y') \cdot p_Y(y')}$$
### Simplified Bayes’ Theorem (Proportionality)

When choosing between different hypotheses or values of $Y$ for a fixed observation $X = x$, the denominator $p_X(x)$ is a constant normalizing factor—it does not depend on $Y$.

Because $p_X(x)$ is identical for all hypotheses $y$, we drop the denominator and write Bayes' theorem as a proportionality:
$$p_{Y\vert{}X}(y \mid x) \propto p_{X\vert{}Y}(x \mid y) \cdot p_Y(y)$$

For tasks like **[[Maximum A Posteriori]] (MAP)** estimation, you find the $y$ that maximizes the posterior by simply maximizing the product of likelihood and prior:

$$\hat{y} = \arg\max_y \left( p_{X\vert{}Y}(x \mid y) \cdot p_Y(y) \right)$$

## Independence of Random Variables

Two random variables $X$ and $Y$ are **statistically independent** if knowledge of one provides no information about the probability distribution of the other.

Mathematically, $X$ and $Y$ are independent if and only if their joint distribution factors into the product of their marginal distributions for all possible values:

- **Discrete Case:**
$$p_{X,Y}(x, y) = p_X(x) \cdot p_Y(y) \quad \forall x, y$$
- **Continuous Case:**

$$f_{X,Y}(x, y) = f_X(x) \cdot f_Y(y) \quad \forall x, y$$
### Equivalent Condition via Conditioning

When $X$ and $Y$ are independent, conditional probabilities simplify directly to marginal probabilities:

$$p_{Y\vert{}X}(y \mid x) = p_Y(y)$$
Knowing $X = x$ changes nothing about the distribution of $Y$.