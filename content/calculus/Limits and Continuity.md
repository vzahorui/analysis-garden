---
tags:
  - calculus
aliases:
  - limit
  - limits
  - continuity
---
A **limit** describes the value a function approaches as its input gets closer to a specific point, regardless of whether it actually reaches that value. **Continuity** means a function has no sudden jumps, breaks, or holes—its output directly connects to its limit.

## Limits: Where a Function is Headed

The notation $\lim_{x \to a} f(x) = L$ reads: _"As $x$ approaches $a$, $f(x)$ approaches $L$."_
- **Key Insight:** Limits care about what happens **near** $x = a$, not **at** $x = a$.
- **Two-Sided Rule:** A limit exists at $x = a$ if and only if approaching $a$ from the left ($\lim_{x \to a^-} f(x)$) and from the right ($\lim_{x \to a^+} f(x)$) yields the exact same value $L$.

## Continuity: A Unbroken Path

A function $f(x)$ is **continuous** at a point $x = a$ if its graph can be drawn through $a$ without lifting the pen. Formally, it must satisfy three conditions:

1. **$f(a)$ is defined:** The point actually exists on the function.
2. **$\lim_{x \to a} f(x)$ exists:** The function approaches a single consistent value from both sides.
3. **$\lim_{x \to a} f(x) = f(a)$:** The limit matches the actual function value at that point.

## Common Types of Discontinuity

When any of the three conditions fail, the function is **discontinuous** at $x = a$:

| **Type**                 | **What Happens on the Graph**                      | **Cause**                                                                                                           |
| ------------------------ | -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Removable (Hole)**     | Smooth curve with a single missing point.          | The limit exists, but $f(a)$ is undefined or doesn't match the limit.                                               |
| **Jump**                 | Graph abruptly steps up or down.                   | Left-hand and right-hand limits exist, but they are not equal ($\lim_{x \to a^-} f(x) \neq \lim_{x \to a^+} f(x)$). |
| **Infinite (Asymptote)** | Graph shoots up to $+\infty$ or down to $-\infty$. | At least one of the one-sided limits goes to infinity.                                                              |

![[Limits and Continuity-1790344468059.webp]]