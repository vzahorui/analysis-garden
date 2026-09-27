---
tags:
  - statistics
aliases:
  - distribution
  - distributions
  - Probability Distribution
---
A **probability distribution** is a mathematical function or rule that describes all the possible values a [[Set Theory#Random Variable]] can take, along with how likely each value is to occur.

Instead of giving you just a single outcome, a distribution gives you the full picture of the likelihood across the whole spectrum of outcomes.
## Core Components

To understand a probability distribution, it helps to break it down into three key elements:

- **Random Variable ($X$):** A variable whose outcome is subject to chance (e.g., the roll of a die, the height of a person, or the lifespan of a lightbulb).
- **Sample Space:** The set of all possible outcomes for that variable.
- **Probability:** A number assigned to each outcome (or range of outcomes) between 0 (impossible) and 1 (certain). The sum (or integral) of all probabilities across the entire sample space must equal 1 (100%).

See [[Set Theory]] for details.

## Discrete vs Continuous Distributions

Probability distributions fall into two main categories depending on the nature of the data:

### Discrete Probability Distributions

Used when outcomes are **countable** or separate distinct values (e.g., number of heads in a coin flip, dice rolls).

- **Key Function:** Defined by a **Probability Mass Function (PMF)**, $P(X = x)$, which gives the exact probability of $X$ taking a specific value $x$.
- **Common Examples:**
    - **Uniform (Discrete):** Every outcome has an equal chance (e.g., a standard 6-sided die, where $P(X = k) = \frac{1}{6}$).
    - **Binomial:** Counts the number of successes in $n$ independent yes/no trials (e.g., flipping a coin 10 times and counting heads).
    - **Poisson:** Counts the number of events occurring within a fixed interval of time or space (e.g., the number of website visits per minute).

### Continuous Probability Distributions

Used when outcomes can take **any value within a continuous range** (e.g., height, weight, time, temperature).

- **Key Function:** Defined by a **Probability Density Function (PDF)**, $f(x)$.
- **Crucial Concept:** The probability of picking an _exact_ single point (e.g., height being _exactly_ 170.00000... cm) is 0. Instead, probability is measured as the [[Integral|area under the curve ]]over an interval $[a, b]$:

$$P(a \le X \le b) = \int_{a}^{b} f(x) \, dx$$

- **Common Examples:**
    - **[[Normal Distribution]] (Gaussian):** The classic "bell curve." Symmetric around the mean, where most outcomes cluster around the center (e.g., human height, measurement errors).
    - **Uniform (Continuous):** Every sub-interval of equal length within a range is equally likely.
    - **Exponential:** Models the time between events occurring at a constant rate (e.g., time until the next customer arrives).

## Summary of Common Distributions

| **Distribution**                    | **Type**   | **Typical Use Case**                             | **Key Parameters**                          |
| ----------------------------------- | ---------- | ------------------------------------------------ | ------------------------------------------- |
| **Bernoulli**                       | Discrete   | Single trial with two outcomes (Success/Failure) | $p$ (probability of success)                |
| **Binomial**                        | Discrete   | Number of successes in $n$ trials                | $n$ (trials), $p$ (success rate)            |
| **Poisson**                         | Discrete   | Event frequency over a fixed interval            | $\lambda$ (average rate)                    |
| **[[Normal Distribution\|Normal]]** | Continuous | Natural phenomena, measurement errors            | $\mu$ (mean), $\sigma$ (standard deviation) |
| **Exponential**                     | Continuous | Wait times and lifespans                         | $\lambda$ (rate parameter)                  |

## Key Summary Statistics

Two primary numbers summarize the shape and location of most probability distributions:

1. **[[Expectation]] / Mean ($\mu$ or $E[X]$):** The long-run average outcome if you repeated the experiment infinitely many times.
2. **Variance ($\sigma^2$):** A measure of how spread out the possible values are around the mean. The standard deviation ($\sigma$) is the square root of the variance.