---
tags:
  - linear-algebra
---
The **Hadamard product** (also known as the **element-wise product** or **entrywise product**) is an operation that takes two [[Tensor|tensors]] or [[Matrix|matrices]] of the exact same dimensions and multiplies their corresponding elements together.

Unlike standard matrix multiplication—which involves row-by-column dot products—the Hadamard product is straightforward, highly parallelizable, and preserves the tensor's original shape.

## Mathematical Definition

Given two matrices $A$ and $B$ of the same shape $m \times n$, their Hadamard product $A \odot B$ (often written as $A \circ B$ or simply $A * B$ in programming) is an $m \times n$ matrix where each entry is:
$$(A \odot B)_{i,j} = A_{i,j} \cdot B_{i,j}$$
**Concrete Example:**
$$\begin{bmatrix} 1 & 3 \\ 2 & 4 \end{bmatrix} \odot \begin{bmatrix} 5 & 0 \\ -1 & 2 \end{bmatrix} = \begin{bmatrix} 1 \cdot 5 & 3 \cdot 0 \\ 2 \cdot (-1) & 4 \cdot 2 \end{bmatrix} = \begin{bmatrix} 5 & 0 \\ -2 & 8 \end{bmatrix}$$
## Core Properties

- **Commutative:** $A \odot B = B \odot A$ (unlike matrix multiplication, where $AB \neq BA$).
- **Associative:** $(A \odot B) \odot C = A \odot (B \odot C)$.
- **Distributive over Addition:** $A \odot (B + C) = (A \odot B) + (A \odot C)$.
- **Identity Element:** A tensor of all ones $J$ (where $J_{i,j} = 1$), such that $A \odot J = A$.

## Key Applications in Machine Learning & Signal Processing

1. **Gating Mechanisms in [[Recurrent Neural Networks]] ([[LSTM]] & GRU)**
    - Gates output activation values between $0$ and $1$ using a [[Sigmoid Function]]. The Hadamard product applies this mask to modulate information flow.
    - _Example:_ $c_t = f_t \odot c_{t-1} + i_t \odot \tilde{c}_t$, where forgotten features ($f_t$) or new candidate features ($\tilde{c}_t$) are scaled element-by-element.
2. **Attention Mechanisms & Masking**
    - Applying a binary or soft mask to an image or sentence embedding uses the Hadamard product. Zeroing out padded tokens or masked regions is performed by multiplying by a boolean tensor (0 or 1).
3. **Convolutional Neural Network Activations**
    - Applying non-linear activation functions (like [[ReLU]] or [[Sigmoid Function|sigmoid]]) or Dropout masks during training is an element-wise operation that relies on the Hadamard product.
4. **Digital Image Processing**
    - Modifying brightness, blending layers, or applying pixel-wise filters to multi-channel image tensors (RGB) directly uses element-wise tensor operations.