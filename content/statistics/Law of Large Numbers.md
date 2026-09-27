---
tags:
  - statistics
---
The **Law of Large Numbers (LLN)** states that as the size of a sample increases, its sample mean ($\bar{X}_n$) converges toward the true theoretical mean ($\mu$) of the overall population.
![[Statististical Concepts-1790442501503.webp]]
# Formal Statement 

For independent, identically distributed (i.i.d.) random variables $X_1, X_2, \dots, X_n$ with a finite expected value $\mathbb{E}[X] = \mu$:

$$\bar{X}_n = \frac{1}{n} \sum_{i=1}^n X_i \xrightarrow{n \to \infty} \mu$$
## Common Misconceptions

1. **The Gambler's Fallacy:** The Law of Large Numbers does **not** self-correct previous short-term streaks. If a fair coin lands on heads 10 times in a row, the probability of tails on the 11th toss remains exactly 50%. The law works by **swamping** early fluctuations with a high volume of subsequent trials, not by counterbalancing them.