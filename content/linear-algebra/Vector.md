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

## Fundamental Vector Operations

### Vector Addition

Adds corresponding components of two vectors of the same dimension.

- **Algebraic Definition:**
$$\mathbf{u} + \mathbf{v} = \begin{bmatrix} u_1 \\ u_2 \\ \vdots \\ u_n \end{bmatrix} + \begin{bmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{bmatrix} = \begin{bmatrix} u_1 + v_1 \\ u_2 + v_2 \\ \vdots \\ u_n + v_n \end{bmatrix}$$
* **Geometric View:** Follows the "tip-to-tail" or parallelogram rule, placing the start of $\mathbf{v}$ at the end of $\mathbf{u}$.




### Scalar Multiplication

Multiplies every element in a vector by a real number (scalar $c$).

- **Algebraic Definition:**
$$c\mathbf{v} = c \begin{bmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{bmatrix} = \begin{bmatrix} c v_1 \\ c v_2 \\ \vdots \\ c v_n \end{bmatrix}$$

- **Geometric View:** Scales the length (magnitude) of the vector by $\vert{}c\vert{}$. If $c < 0$, it reverses the direction.

### Dot Product (Inner Product)

Combines two vectors of equal length to return a single scalar value.

- **Algebraic Definition:**
$$\mathbf{u} \cdot \mathbf{v} = \sum_{i=1}^{n} u_i v_i = u_1 v_1 + u_2 v_2 + \dots + u_n v_n$$
- **Geometric Definition:**
$$\mathbf{u} \cdot \mathbf{v} = \Vert{}\mathbf{u}\Vert{} \Vert{}\mathbf{v}\Vert{} \cos(\theta)$$
  where $\theta$ is the angle between the vectors, and $\Vert{}\mathbf{v}\Vert{} = \sqrt{\mathbf{v} \cdot \mathbf{v}}$ is the Euclidean norm (length).
- **Key Interpretations:**
    - **Orthogonality:** If $\mathbf{u} \cdot \mathbf{v} = 0$, the vectors are perpendicular ($90^\circ$).
    - **Alignment:** Positive if pointing in similar directions; negative if opposing.
    - Used to determine the measure of similarity of two vectors, and to express on vector as projection of another. 

![[Vector-1790404764528.webp]]

![[Vector-1790404791850.webp]]