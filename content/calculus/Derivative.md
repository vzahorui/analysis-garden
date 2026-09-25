---
tags:
  - calculus
aliases:
  - differentiability
  - differentiable
  - gradient
---
At its core, a **derivative** measures the **instantaneous rate of change** of a function—it tells you how much the output of a function ($y$) changes when you make a tiny, infinitesimal change to its input ($x$).

# The Intuition: Average vs. Instantaneous Speed

Imagine you are driving a car.
- **Average Rate of Change:** You drive 60 miles in 1 hour. Your average speed was **60 mph**.
- **Instantaneous Rate of Change (The Derivative):** At precisely $t = 30\text{ minutes}$, you glance down at your speedometer, and it says **72 mph**. That speedometer reading is the derivative of your position with respect to time at that exact second.

# Formal Definition

Mathematically, we define the derivative of $f(x)$ at a point $x$ using a [[Limits and Continuity|limit]] as the distance $h$ between two points approaches zero:
$$f'(x) = \lim_{h \to 0} \frac{f(x + h) - f(x)}{h}$$

But simply put, the derivative is the slope:
$$\text{Slope} = \frac{\Delta y}{\Delta x} = \frac{f(x_2) - f(x_1)}{x_2 - x_1}$$

![[Derivative-1790328185014.webp]]

# Notation Variants

* $f'(x)$ (Lagrange notation) 
* $\frac{df}{dx}$ (Leibniz notation).

# Fundamental Rules

In practice, you rarely use the limit definition directly for every function. Instead, you use short-cut rules:
## Basic Rules

| **Rule Name**       | **Function f(x)**   | **Derivative f′(x)**                     |
| ------------------- | ------------------- | ---------------------------------------- |
| **Power Rule**      | $x^n$               | $n x^{n-1}$                              |
| **Identity Rule**   | $x$                 | 1                                        |
| **Constant Rule**   | $c$                 | $0$                                      |
| **Sum Rule**        | $u(x) + v(x)$       | $u'(x) + v'(x)$                          |
| **Product Rule**    | $u \cdot v$         | $u'v + uv'$                              |
| **Chain Rule**      | $f(g(x))$           | $f'(g(x)) \cdot g'(x)$                   |
| **Quotient Rule**   | $\frac{u(x)}{v(x)}$ | $\frac{u'(x)v(x) - u(x)v'(x)}{[v(x)]^2}$ |
| **Reciprocal Rule** | $\frac{1}{v(x)}$    | $-\frac{v'(x)}{[v(x)]^2}$                |
### Exponential & Logarithmic Rules

| **Rule Name**           | **Function f(x)** | **Derivative f′(x)** | **Conditions**           |
| ----------------------- | ----------------- | -------------------- | ------------------------ |
| **Natural Exponential** | $e^x$             | $e^x$                | —                        |
| **General Exponential** | $a^x$             | $a^x \ln(a)$         | $a > 0, a \neq 1$        |
| **Natural Logarithm**   | $\ln(x)$          | $\frac{1}{x}$        | $x > 0$                  |
| **General Logarithm**   | $\log_a(x)$       | $\frac{1}{x \ln(a)}$ | $x > 0, a > 0, a \neq 1$ |

### Trigonometric Rules

| **Rule Name** | **Function f(x)** | **Derivative f′(x)** |
| ------------- | ----------------- | -------------------- |
| **Sine**      | $\sin(x)$         | $\cos(x)$            |
| **Cosine**    | $\cos(x)$         | $-\sin(x)$           |
| **Tangent**   | $\tan(x)$         | $\sec^2(x)$          |
| **Cosecant**  | $\csc(x)$         | $-\csc(x)\cot(x)$    |
| **Secant**    | $\sec(x)$         | $\sec(x)\tan(x)$     |
| **Cotangent** | $\cot(x)$         | $-\csc^2(x)$         |

# Gradient

Gradient is a multi-variable generalization of derivative. If a function has multiple variables ($\mathbf{x} \in \mathbb{R}^n$) we can take derivatives with respect to each variable while treating others as constants. The elements of a gradient are partial derivatives of this function, which in turn would show the slope in each dimension. 

Is expressed via a [[vector]]:

$$\nabla_x f(x) =  \begin{bmatrix} \partial_{x1}f(x), \partial_{x2}f(x), \dots, \partial_{xn}f(x)  \end{bmatrix}^T$$

Therefore, for a multivariable function it is possible to find the instantaneous rate of change with respect to each variable. 

Also see [[Jacobian]] as a generalization for functions with multiple outputs.

# How Derivatives Are Used in Machine Learning

In [[Machine Learning Concepts|Machine Learning]] (ML), derivatives are the fundamental engine used to **train models**.

Training an ML model (like a [[linear regression]] model or a deep [[Neural Network]]) is essentially an optimization problem: **How do we tweak the model's internal parameters (weights $w$ and biases $b$) so that its predictions are as accurate as possible?** This is achieved via [[Gradient Descent]].

# Second Derivative

The second derivative of a function is simply the derivative of the function’s derivative. If the first derivative is understood as the ratio of change (velocity), the second derivative is the ratio of change in velocity, in other words - acceleration.

![[Derivative-1790329917341.webp]]

- **$f''(x) > 0$ (Convex):** The slope of velocity is increasing. The graph curves upward like a cup ($\cup$).
- **$f''(x) < 0$ (Concave):** The slope of velocity is decreasing. The graph curves downward like a frown ($\cap$).
- **$f''(x) = 0$ (Inflection Point):** The point where concavity changes from upward to downward (or vice versa).

## Practical Application of the Second Derivative

We can test if a stationary point (where $f'(c) = 0$) is a local maximum or minimum:

| **Condition**    | **Meaning**                                      | **Result**                |
| ---------------- | ------------------------------------------------ | ------------------------- |
| **$f''(c) > 0$** | Slope of derivative is increasing (concave up)   | **Local Minimum**         |
| **$f''(c) < 0$** | Slope of derivative is decreasing (concave down) | **Local Maximum**         |
| **$f''(c) = 0$** | Inconclusive                                     | Use First Derivative Test |

## Common Notations of the Second Derivative

For a function $y = f(x)$, the second derivative is written as:

$$f''(x) \quad \text{or} \quad \frac{d^2y}{dx^2} \quad \text{or} \quad y'' \quad \text{or} \quad \ddot{y} \text{ (in physics)}$$
## Hessian

Where the gradient collects all 1st-order partial derivatives into a [[vector]], the **Hessian [[matrix]]** collects all 2nd-order partial derivatives into a square matrix. It describes the local curvature of a multivariable function $f(x_1, x_2, \dots, x_n)$.

For a scalar function $f: \mathbb{R}^n \to \mathbb{R}$ (a function which has an input of $n$ features, and outputs a single number), the Hessian matrix $\mathbf{H}$ (or $\nabla^2 f$) is defined as:

$$\mathbf{H} = \nabla(\nabla f) = \begin{bmatrix} \frac{\partial^2 f}{\partial x_1^2} & \frac{\partial^2 f}{\partial x_1 \partial x_2} & \dots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\ \frac{\partial^2 f}{\partial x_2 \partial x_1} & \frac{\partial^2 f}{\partial x_2^2} & \dots & \frac{\partial^2 f}{\partial x_2 \partial x_n} \\ \vdots & \vdots & \ddots & \vdots \\ \frac{\partial^2 f}{\partial x_n \partial x_1} & \frac{\partial^2 f}{\partial x_n \partial x_2} & \dots & \frac{\partial^2 f}{\partial x_n^2} \end{bmatrix}$$

* It is a symmetric matrix because the order of differentiation does not matter ($\frac{\partial^2 f}{\partial x_i \partial x_j} = \frac{\partial^2 f}{\partial x_j \partial x_i}$).
* **[[Eigenvectors and Eigenvalues|Eigenvalues]] and Curvature:** The eigenvalues of the Hessian reveal the principal curvatures along orthogonal directions in space:
    - All eigenvalues $> 0 \implies$ **Positive Definite** (Local Minimum / "Bowl shape up").
    - All eigenvalues $< 0 \implies$ **Negative Definite** (Local Maximum / "Bowl shape down").
    - Mixed sign eigenvalues $\implies$ **Indefinite** (Saddle Point).
### Where Hessian Matters

- **Optimization & Deep Learning:** [[Newton's Method]] uses the inverse Hessian ($\mathbf{H}^{-1}$) to take optimal step sizes toward a minimum, converging faster than simple [[Gradient Descent]].
- [[Taylor Series|Taylor Expansion]]: Just as $f''(x)$ gives quadratic terms in 1D, $\mathbf{H}$ forms the quadratic term in 2D+ Taylor series.



