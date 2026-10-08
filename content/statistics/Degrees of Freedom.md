---
tags:
  - statistics
aliases:
  - degree of freedom
---
At its core, **degrees of freedom (df)** is the number of values in a final calculation that are free to vary without violating any restrictions or rules imposed on the system.

Whether you are looking at statistics, mechanical engineering, or physics, the fundamental concept remains the same: **Total Possibilities minus Constraints**.

$$\text{Degrees of Freedom} = \text{Total Independent Variables} - \text{Number of Constraints}$$

## In Statistics: Independent Pieces of Information

In statistics, degrees of freedom represents how many independent pieces of data were used to estimate a parameter (like a mean or standard deviation).

### The $(N - 1)$ Intuition

Imagine you have a set of **3 numbers**, and you know their **average is 10**.

- The sum of those 3 numbers must equal 30 ($10 \times 3 = 30$).
- You are free to pick _any_ number for the first choice (e.g., **5**).
- You are free to pick _any_ number for the second choice (e.g., **15**).
- But for the third choice, you have **no freedom**. It _must_ be **10** so that $5 + 15 + 10 = 30$.

Because 1 constraint (the mean) was placed on 3 numbers, you had $3 - 1 = 2$ degrees of freedom.

#### Why it matters in inferential statistics

When calculating sample statistics (see [[Sampling Distribution]]) (like sample variance $s^2 = \frac{\sum (x_i - \bar{x})^2}{n - 1}$), using $n - 1$ instead of $n$ adjusts for using estimated parameters. Dividing by $n - 1$ (known as Bessel's correction) gives an unbiased estimate of the population variance.

