---
tags:
  - statistics
  - probability
---
In probability theory, foundational concepts are built on set theory.
## Core Definitions

### Sample Space

The **sample space** (denoted as $\Omega$ or $S$) is the set of **all possible outcomes** of a random experiment.

- **Example (Rolling a six-sided die):** $\Omega = \{1, 2, 3, 4, 5, 6\}$
- **Example (Flipping a coin twice):** $\Omega = \{HH, HT, TH, TT\}$
- **Example (Measuring battery life):** $\Omega = [0, \infty)$ hours
### Event

An **event** is any subset of the sample space ($A \subseteq \Omega$). It represents a collection of outcomes you care about evaluating.

- **Example:** Rolling an even number $\rightarrow A = \{2, 4, 6\}$. Here, $A \subset \Omega$.
- **Elementary Event:** An event containing only a single outcome (e.g., $\{3\}$).
- **Certain Event:** The full sample space $\Omega$ itself.
- **Impossible Event:** The empty set $\emptyset$.
### Subspace (Event Space)

In probability, "subspace" usually refers to the **event space** (formally a **$\sigma$-algebra**, denoted $\mathcal{F}$). It is the collection of all allowable subsets/events of $\Omega$ that we can assign probabilities to.

For $\mathcal{F}$ to qualify as a valid event space over $\Omega$, it must satisfy three properties:

1. **Contains the whole space:** $\Omega \in \mathcal{F}$
2. **Closed under complement:** If $A \in \mathcal{F}$, then its complement $A^c \in \mathcal{F}$
3. **Closed under countable unions:** If $A_1, A_2, A_3, \dots \in \mathcal{F}$, then $\bigcup_{i=1}^\infty A_i \in \mathcal{F}$

> [!info] Note
>  In [[Linear Algebra Concepts|Linear Algebra]], a "subspace" is a [[vector]] subspace. In probability, when random variables form a vector space (e.g., $L^2$ spaces of finite variance), a subspace refers to a closed linear sub-collection of random variables.

### Example of a Single Coin Flip

- **Sample Space ($\Omega$):** A set of individual _outcomes_.
    Example for a coin flip: $\Omega = \{H, T\}$ (has 2 outcomes).
- **Event ($A$):** A subset of outcomes.
    Example: $A = \{H\}$ (getting heads). Here, $A \subseteq \Omega$.
- **Event Space ($\mathcal{F}$):** The collection of **ALL allowable events** (a set of sets).
    For a coin flip, $\mathcal{F} = \{\emptyset, \{H\}, \{T\}, \{H, T\}\}$.

## Random Variable

A **random variable** is a **function** or **mapping** that assigns a numerical value to every possible outcome in a sample space:

$$X: \Omega \to \mathbb{R}$$
Raw sample spaces can be abstract, qualitative, or awkward to work with—like sequences of coin flips $(\text{H}, \text{T}, \text{H})$, customer service qualitative feedback, or particles moving in space.

By mapping outcomes to real numbers, random variables allow you to:
- Apply standard [[Calculus Concepts|calculus]] and algebra to random phenomena.
- Calculate summaries like the **Expected Value** $E[X]$ and **Variance** $Var(X)$.
- Group outcomes into measurable numerical ranges (e.g., $P(X \le 5)$).
## How the Probability Function Maps Events onto Real Values

A **probability function** (or probability measure) $P$ is a set function that maps elements from the **event space $\mathcal{F}$** (which are sets) to real numbers in the interval $[0, 1]$.
$$P: \mathcal{F} \rightarrow [0, 1]$$
### Important Distinction: Inputs vs Outputs

- **Domain:** The domain of $P$ is **not** the individual outcomes in $\Omega$; it is the set of events $\mathcal{F}$ (subsets of $\Omega$).
- **Codomain / Range:** A subset of real numbers bounded between $0$ and $1$, inclusive ($[0, 1] \subset \mathbb{R}$).

### The Kolmogorov Axioms

For $P$ to be a valid probability measure mapping events to real values, it must obey three rules:

1. **Non-negativity:** For any event $A \in \mathcal{F}$,
$$P(A) \ge 0$$
2. **Normalization:** The total measure of the sample space is $1$:
$$P(\Omega) = 1$$
3. **Countable Additivity:** For any sequence of mutually disjoint events $A_1, A_2, \dots$ (where $A_i \cap A_j = \emptyset$ for $i \neq j$):
$$P\left( \bigcup_{i=1}^\infty A_i \right) = \sum_{i=1}^\infty P(A_i)$$

## How Random Variable and Probability Measure Work Together

| **Concept**                   | **Domain (Input)**            | **Codomain (Output)**            | **What it does**                             |
| ----------------------------- | ----------------------------- | -------------------------------- | -------------------------------------------- |
| **Random Variable ($X$)**     | Outcome ($\omega \in \Omega$) | Real Number ($x \in \mathbb{R}$) | **Translates raw outcomes into numbers**     |
| **Probability Measure ($P$)** | Event ($A \subseteq \Omega$)  | Interval $[0, 1]$                | **Assigns a likelihood to sets of outcomes** |

To see how they work together, consider a simple coin toss experiment:

1. **The Sample Space ($\Omega$):** The raw outcomes are $\Omega = \{\text{Heads}, \text{Tails}\}$.
2. **The Random Variable ($X$):** Define $X$ as the number of heads in one toss.
    - $X(\text{Heads}) = 1$
    - $X(\text{Tails}) = 0$
3. **The Event:** You want to find the probability that $X = 1$. The expression "$X = 1$" is shorthand for the set of outcomes where $X$ equals $1$, which is the event $A = \{\text{Heads}\}$.
4. **The Probability Measure ($P$):** Finally, $P$ evaluates that event:
$$P(X = 1) = P(\{\omega \in \Omega : X(\omega) = 1\}) = P(\{\text{Heads}\}) = 0.5$$

