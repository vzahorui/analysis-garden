---
tags:
  - calculus
---
An integral measures **accumulation** and **total continuous value**, and this is an opposite of [[Derivative]]. 

It is used model continuous [[probability distributions]], compute [[Expectation|Expected values]], quantify uncertainty, and optimize [[Machine Learning Concepts|Machine Learning]] [[Loss vs Metric|loss]] functions.

## The Core Idea: Adding Tiny Slices

Integral can be viewed as a continuous version of summation. 

Imagine you want to find the area under a curve $f(x)$ between two points $a$ and $b$:

1. **Slice it:** Divide the area into thin vertical rectangles of width $dx$ and height $f(x)$.
2. **Sum them:** The area of one thin rectangle is $\text{height} \times \text{width} = f(x) \cdot dx$.
3. **[[Limits and Continuity|Limit]] to infinity:** Make the slices infinitely thin ($dx \to 0$). The approximate sum of rectangle areas becomes the exact area under the curve.

![[Integral-1790453220144.webp]]

This process is represented by the integral symbol $\int$:

$$\int_{a}^{b} f(x) \, dx$$
- $f(x)$: The height of each slice at position $x$.
- $dx$: An infinitely small step along the x-axis (the width of each slice).
- $a$ and $b$: The starting and ending bounds.

## The Two Flavors of Integrals

| **Type**                | **What It Means**                                                                                                                       | **Result**                    | **Notation**                 |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- | ---------------------------- |
| **Definite Integral**   | Finds the total accumulated amount or area between specific bounds ($a$ to $b$).                                                        | A specific number             | $\int_{a}^{b} f(x) \, dx$    |
| **Indefinite Integral** | The inverse operation of a derivative (also called an _antiderivative_). Answers: _"What function, when differentiated, gives $f(x)$?"_ | A family of functions ($+ C$) | $\int f(x) \, dx = F(x) + C$ |

> **Why $+ C$?**
> 
> Differentiating $x^2 + 5$, $x^2 - 100$, or $x^2$ all yield $2x$, because the derivative of any constant is zero. When working backwards from $2x$, we append a constant $+ C$ to represent all possible original functions.

## The Fundamental Theorem of Calculus

The Fundamental Theorem connects [[Derivative|derivatives]] (rates of change) and integrals (accumulation). It shows they are opposite operations:

$$\int_{a}^{b} f(x) \, dx = F(b) - F(a)$$

where $F(x)$ is the antiderivative of $f(x)$ (meaning $F'(x) = f(x)$).