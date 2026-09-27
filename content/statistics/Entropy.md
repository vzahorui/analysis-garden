---
tags:
  - statistics
---
**Entropy** is fundamentally a measure of **disorder, randomness, or microstate probability** in a physical or information-based system. 

In [[Statististical Concepts|statistics]] the convenience formula for measuring it is this:

$$H(X) = -\sum p(x) \log_2 p(x)$$

# Derivation

## Step 1: Measuring the "Surprise" of a Single Event

Before measuring the entropy of an entire system, we need to measure the **information** (or surprise) $I(x)$ brought by a single event $x$ occurring with probability $p(x)$.

Shannon established three natural properties $I(x)$ must have:

1. **Inversely related to probability:** High-probability events bring little surprise; rare events bring high surprise.
    
    - _Example:_ "Sun rises in the east" $\rightarrow$ zero surprise.
    - _Example:_ "It's snowing in the Sahara" $\rightarrow$ huge surprise.
2. **Non-negativity:** Learning an event occurred should never _reduce_ your total information ($I(x) \ge 0$). An event with probability $p=1$ brings zero information ($I(1) = 0$).
3. **Additivity for independent events:** If event $A$ (coin flip = Heads) and event $B$ (rolling a 6 on a die) are independent, learning both happened should equal the sum of their individual surprises:

$$I(A \text{ and } B) = I(A) + I(B)$$

### The Mathematical Deduction for $I(x)$

For independent events, probabilities multiply: $p(A \text{ and } B) = p(A) \cdot p(B)$.

We need a function $I(p)$ where multiplying inputs results in adding outputs:

$$I(p(A) \cdot p(B)) = I(p(A)) + I(p(B))$$

The only continuous mathematical function that turns multiplication into addition is the **logarithm**:

$$I(x) = \log\left(\frac{1}{p(x)}\right) = -\log_2(p(x))$$

Using base 2 sets the unit to **bits**.

- If an event has $p = \frac{1}{2}$ (like a coin flip), $I(x) = -\log_2\left(\frac{1}{2}\right) = 1\text{ bit}$.
- If an event has $p = \frac{1}{4}$ (two heads in a row), $I(x) = -\log_2\left(\frac{1}{4}\right) = 2\text{ bits}$. This is twice as large entropy, and it matches with the design because we multiply probabilities but add surprise for events.
## Step 2: Average Surprise of the Whole System

Now that we know the surprise of a single outcome $x$ is $-\log_2 p(x)$, what is the **overall uncertainty** of a [[Set Theory#Random Variable]] $X$?

Entropy $H(X)$ is simply the **expected value** (the weighted average) of the surprise across all possible outcomes:

$$\text{Expected Surprise} = \sum_{x} (\text{Probability of } x) \times (\text{Surprise of } x)$$

$$H(X) = \sum_{x} p(x) \cdot \left(-\log_2 p(x)\right) = -\sum_{x} p(x) \log_2 p(x)$$