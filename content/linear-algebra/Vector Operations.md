---
tags:
  - linear-algebra
---
# Vector Addition

Adds corresponding components of two vectors of the same dimension.

- **Algebraic Definition:**
$$\mathbf{u} + \mathbf{v} = \begin{bmatrix} u_1 \\ u_2 \\ \vdots \\ u_n \end{bmatrix} + \begin{bmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{bmatrix} = \begin{bmatrix} u_1 + v_1 \\ u_2 + v_2 \\ \vdots \\ u_n + v_n \end{bmatrix}$$
* **Geometric View:** Follows the "tip-to-tail" or parallelogram rule, placing the start of $\mathbf{v}$ at the end of $\mathbf{u}$.




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
  where $\theta$ is the angle between the vectors, and $\Vert{}\mathbf{v}\Vert{} = \sqrt{\mathbf{v} \cdot \mathbf{v}}$ is the Euclidean norm (length).

The cosine function appears in the dot product formula because the dot product measures **geometric projection**—specifically, how much one vector points in the exact same direction as another.

Cosine is the ratio of the length of the adjacent side to the length of the hypotenuse in a triangle.

$$\cos(\theta) = \frac{\Vert{} \mathrm{proj}_{\mathbf{v}}\mathbf{u} \Vert{} }{\Vert{}\mathbf{u} \Vert{}}$$ 
Therefore, the length of the projection of $\mathbf{u}$ on $\mathbf{v}$ is 

$$\Vert{} \mathrm{proj}_{\mathbf{v}}\mathbf{u} \Vert{} = \Vert{}\mathbf{u} \Vert{} \cos(\theta)$$



$\mathrm{proj}_{\mathbf{v}}\mathbf{u}$

- **Key Interpretations:**
    - **Orthogonality:** If $\mathbf{u} \cdot \mathbf{v} = 0$, the vectors are perpendicular ($90^\circ$).
    - **Alignment:** Positive if pointing in similar directions; negative if opposing.
    - Used to determine the measure of similarity of two vectors, and to express on vector as projection of another. 