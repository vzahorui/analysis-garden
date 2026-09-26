---
tags:
  - linear-algebra
---
An $n$-dimensional **vector** is an ordered collection of $n$ real numbers, denoted by boldface lower-case letters (e.g., $\mathbf{x}, \mathbf{y}, \mathbf{z}$).

The space of all continuous real-valued vectors of length $n$ is denoted by $\mathbb{R}^n$. To express that a vector $\mathbf{x}$ consists of $n$ real-valued components, we use set membership:
$$\mathbf{x} \in \mathbb{R}^n$$
Explicitly, a vector is written as a column matrix of its [[scalar]] components:

$$\mathbf{x} = \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix}$$
where each individual element is a scalar belonging to the real numbers ($x_i \in \mathbb{R}$ for $i \in \{1, 2, \dots, n\}$).
### Key Notational Aspects
- **Component Indexing:** The $i$-th element of a vector $\mathbf{x}$ is denoted by an italicized subscript scalar $x_i$.
- **Row Vectors & Transposition:** By convention, vectors are assumed to be **column vectors**. To represent a row vector, we apply the transpose operator $T$ to a column vector:
$$\mathbf{x}^T = \begin{bmatrix} x_1 & x_2 & \dots & x_n \end{bmatrix}$$
- **Discrete Vector Domains:** If all components of an $n$-dimensional vector are restricted to discrete values—such as binary vectors—we raise the set to the power of $n$:
$$\mathbf{x} \in \{0, 1\}^n$$
This indicates that $\mathbf{x}$ is an $n$-tuple where every component $x_i \in \{0, 1\}$.



![[Vector-1790404764528.webp]]


![[Vector-1790404791850.webp]]