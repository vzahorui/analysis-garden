---
tags:
  - linear-algebra
---
# Vector Addition

Adds corresponding components of two vectors of the same dimension.

- **Algebraic Definition:**
$$\mathbf{u} + \mathbf{v} = \begin{bmatrix} u_1 \\ u_2 \\ \vdots \\ u_n \end{bmatrix} + \begin{bmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{bmatrix} = \begin{bmatrix} u_1 + v_1 \\ u_2 + v_2 \\ \vdots \\ u_n + v_n \end{bmatrix}$$
* **Geometric View:** Follows the "tip-to-tail" or parallelogram rule, placing the start of $\mathbf{v}$ at the end of $\mathbf{u}$.

![[Vector Operations-1790406835527.webp]]

# Scalar Multiplication

Multiplies every element in a vector by a real number (scalar $c$).

- **Algebraic Definition:**
$$c\mathbf{v} = c \begin{bmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{bmatrix} = \begin{bmatrix} c v_1 \\ c v_2 \\ \vdots \\ c v_n \end{bmatrix}$$

- **Geometric View:** Scales the length (magnitude) of the vector by $\vert{}c\vert{}$. If $c < 0$, it reverses the direction.

# Dot Product (Inner Product)

Combines two vectors of equal length to return a single scalar value.

- **Algebraic Definition:**
$$\mathbf{u} \cdot \mathbf{v} = \sum_{i=1}^{n} u_i v_i = u_1 v_1 + u_2 v_2 + \dots + u_n v_n$$
- **Geometric Definition:**
$$\mathbf{u} \cdot \mathbf{v} = \Vert{}\mathbf{u}\Vert{} \Vert{}\mathbf{v}\Vert{} \cos(\theta)$$
  where $\theta$ is the angle between the vectors, and $\Vert{}\mathbf{v}\Vert{} = \sqrt{\mathbf{v} \cdot \mathbf{v}}$ is the Euclidean [[Vector Norm|norm]] (length).

The cosine function appears in the dot product formula because the dot product measures **geometric projection**—specifically, how much one vector points in the exact same direction as another.

![[Vector Operations-1790406790825.webp]]

Cosine is the ratio of the length of the adjacent side to the length of the hypotenuse in a triangle.

$$\cos(\theta) = \frac{\Vert{} \mathrm{proj}_{\mathbf{v}}\mathbf{u} \Vert{} }{\Vert{}\mathbf{u} \Vert{}}$$
Therefore, the length of the projection of $\mathbf{u}$ on $\mathbf{v}$ is 
$$\Vert{} \mathrm{proj}_{\mathbf{v}}\mathbf{u} \Vert{} = \Vert{}\mathbf{u} \Vert{} \cos(\theta)$$
The dot product is defined as the magnitude of $\mathbf{v}$ multiplied by the magnitude of $\mathbf{u}$'s projection onto $\mathbf{v}$.

Cosine acts as a directional scaling factor:
- When $\theta = 0^\circ$, $\cos(0^\circ) = 1$: Both vectors point the same way, giving maximum output.
- When $\theta = 90^\circ$, $\cos(90^\circ) = 0$: The vectors are perpendicular, so $\mathbf{u}$ casts zero shadow onto $\mathbf{v}$.
- When $\theta = 180^\circ$, $\cos(180^\circ) = -1$: The vectors point in opposite directions.

## Use of Dot Product in Linear Models

In [[Linear Models]] we usually have a set of values denoted as a vector $\mathbf{x} \in \mathbb{R}^n$, and a set of weight as another vector $\mathbf{w} \in \mathbb{R}^n$. We can express a weighted sum of these values as a dot product: $\mathbf{x}^{T}\mathbf{w}$. 
# Linear Combinations & Span

Combining addition and scalar multiplication yields a [[Linear Models|linear combination]]:
$$c_1 \mathbf{v}_1 + c_2 \mathbf{v}_2 + \dots + c_k \mathbf{v}_k$$
- **Span:** The set of all possible linear combinations formed by a set of vectors.
- **Linear Independence:** A set of vectors is linearly independent if no vector in the set can be written as a linear combination of the others. 

# Other References

* [[Vector Norm]]