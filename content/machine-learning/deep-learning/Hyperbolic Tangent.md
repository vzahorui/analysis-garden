---
tags:
  - ML/activation-function
  - ML/deep-learning
aliases:
  - tanh activation
  - tanh
---
Hyperbolic tangent ($\tanh$) can be used as an [[Activation Functions]] in hidden leayers of a [[Neural Network]]. They are better than [[Sigmoid Function|sigmoid]] for this purpose but still worse than [[ReLU]]. 

![[Hyperbolic Tangent-1791021854196.webp]]

$$\tanh(x) = \frac{e^z - e^{-z}}{e^z + e^{-z}}$$
## Key Reasons to Use Tanh Over Sigmoid

### 1. Zero-Centered Outputs (Prevents "Zig-Zag" Gradients)

Because Sigmoid outputs are strictly positive (range $0$ to $1$), the activations fed into subsequent layers are always positive. During [[backpropagation]], the gradient of the loss with respect to weight vector $w$ is given by:

$$\frac{\partial L}{\partial w_i} = \frac{\partial L}{\partial a} \cdot \sigma'(z) \cdot x_i$$

Since $x_i > 0$ and $\sigma'(z) > 0$, every weight gradient for a given neuron inherits the exact same sign as $\frac{\partial L}{\partial a}$. This forces all weights of a neuron to either **all increase or all decrease together**, causing inefficient "zig-zagging" during gradient descent update steps.

$\tanh$ outputs range from $-1$ to $1$, naturally centering activations around $0$. Positive and negative values balance out, allowing weight updates to move freely in any direction.

### 2. Stronger Gradients Near Zero

The derivative of $\tanh(z)$ reaches $1.0$ at $z = 0$, whereas the derivative of Sigmoid peaks at only $0.25$. When propagating error backwards through multiple layers, multiplying terms bounded by $0.25$ causes gradients to diminish exponentially faster. $\tanh$ mitigates this signal decay better than Sigmoid in moderately deep networks.

## Limitaiton

Tanh activation still suffers from [[Saturation and Vanishing Gradient]] just like [[Sigmoid Function|sigmoid activation]]. 

## Key Scenarios Where $\tanh$ is Preferred Over [[ReLU]]/GELU

### Recurrent Dynamics & Gated Architectures ([[LSTM]]s, GRUs)

In architectures like LSTMs and GRUs, $\tanh$ is used to regulate the candidate hidden state and output vectors.

- **Bounded State Control:** Because recurrent loops repeatedly pass activations through time steps, unbounded activations like ReLU can cause hidden states to explode exponentially over many steps ($\prod W \cdot a_t \to \infty$).
- **Symmetrical Memory Updating:** The $[-1, 1]$ range allows hidden states to both **add information** (positive values) and **subtract/erase information** (negative values) from memory cells naturally. [[ReLU]] (range $[0, \infty)$) can only accumulate or zero out states.

### Generative Models Output Layer (GANs, Diffusion, Autoencoders)

When generating continuous data such as images, audio waveforms, or normalized sensor vectors:

- **Image Synthesis (e.g., DCGANs):** Images normalized to the range $[-1, 1]$ are matched to a $\tanh$ output layer in the generator. This provides strict physical boundary guarantees (preventing pixel value overflow) while maintaining smooth gradients near extreme values.

### [[Physics-Informed Neural Networks]] (PINNs) & Continuous Systems

When solving differential equations or modeling physical systems using neural networks:

- **Smooth Higher-Order Derivatives:** $\tanh$ is infinitely differentiable ($C^\infty$), producing smooth, continuous second ($f''$) and third ($f'''$) derivatives needed to model differential equations (e.g., Navier-Stokes, wave equations).
- **Where ReLU/GELU Struggle:** ReLU's second derivative is $0$ everywhere (and undefined at $0$), making it unusable for second-order spatial/temporal differential equations. While GELU is smooth, $\tanh$'s bounded derivative properties provide cleaner optimization behavior in certain physics boundary conditions.

### Normalized Latent Spaces & Policy Output Bounding (Reinforcement Learning)

In continuous control Reinforcement Learning (e.g., Soft Actor-Critic, PPO for robotics):

- **Action Space Bounding:** Torque, steering angles, or engine throttles have strict physical limits (e.g., steering between $-100\%$ and $+100\%$). A $\tanh$ squashing function mapped to the actor network's output enforces these exact motor bounds without hard clipping (which destroys gradients outside boundaries).