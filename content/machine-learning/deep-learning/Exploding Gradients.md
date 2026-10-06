---
tags:
  - ML/deep-learning
---
The **exploding [[Derivative|gradient]] problem** occurs during the training of deep [[Neural Network|Neural Networks]] when gradients during backpropagation grow exponentially large as they flow backward through layers.

When gradients become extremely large, the updates to the network's weights via gradient descent become massive. This instability causes the network parameters to oscillate wildly or overshooting optimal values, often resulting in numerical overflow where weight values become **NaN** (Not a Number).

### The Underlying Cause

During [[backpropagation]], the chain rule is used to compute the gradient of the loss function with respect to weights in early layers:

$$\frac{\partial L}{\partial W_1} = \frac{\partial L}{\partial a_L} \cdot \frac{\partial a_L}{\partial a_{L-1}} \cdot \dots \cdot \frac{\partial a_2}{\partial a_1} \cdot \frac{\partial a_1}{\partial W_1}$$

Each term $\frac{\partial a_k}{\partial a_{k-1}}$ depends heavily on the weight matrix $W_k$.

- If the [[Eigenvectors and Eigenvalues|eigenvalues]] of these weight matrices are **greater than $1$** (specifically, if the spectral radius $> 1$), repeatedly multiplying them over $N$ deep layers causes the gradient magnitude to grow exponentially, proportional to $W^N$.
- This issue is particularly severe in [[Recurrent Neural Networks]] (RNNs) because the same weight matrix $W$ is multiplied repeatedly across many time steps ($t = 1, 2, \dots, T$).

### Symptoms of Exploding Gradients

- **Unstable Training:** The loss function fluctuates wildly from epoch to epoch instead of steadily decreasing.
- **Loss Becomes NaN:** Numerical overflow occurs during floating-point operations, causing loss or weights to evaluate as `NaN`.
- **Extreme Weight Values:** Model weights suddenly grow to huge magnitudes ($10^5, 10^{10}$, etc.).

### Solutions & Mitigation Techniques

#### Gradient Clipping

- [[Vector Norm|Norm]] Clipping: Rescales the gradient vector if its L2 norm exceeds a threshold $c$:

$$\text{if } \Vert{}\mathbf{g}\Vert{} > c, \quad \mathbf{g} \leftarrow c \cdot \frac{\mathbf{g}}{\Vert{}\mathbf{g}\Vert{}}$$
- **Value Clipping:** Caps individual gradient elements between $[-c, c]$.

#### Better Weight Initialization

- Using **[[Xavier Initialization|Xavier]] (Glorot)** or [[He Initialization|He]] (Kaiming)** initialization scales the initial weights based on layer sizes ($\frac{1}{\sqrt{n_{in}}}$), preventing large initial weight matrices from escalating gradients early on.

#### Architectural Improvements

- **Gated Architectures ([[LSTM]] / GRU):** Use additive memory gates instead of pure multiplicative recurrent paths, keeping gradients stable over long time horizons.

- **Residual Connections ([[ResNets]]):** Provide direct "skip connections" for gradients to flow backward linearly ($\frac{\partial}{\partial x}(x + f(x)) = 1 + f'(x)$), avoiding repeated matrix contractions.

#### Normalization Layers

- Techniques like [[Batch Normalization]] or **Layer Normalization** re-scale intermediate activations, keeping internal activation dynamics and their derivative scales well-behaved.
#### Smaller Learning Rates

- Lowering the learning rate ($\eta$) prevents single large gradients from making destructive updates to weights.