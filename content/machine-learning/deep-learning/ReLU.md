---
tags:
  - ML/deep-learning
  - ML/activation-function
---
Standard activation functions like [[Sigmoid Function]] and [[Hyperbolic Tangent|tanh]] suffer from [[Saturation and Vanishing Gradient]]. Rectified Linear Unit (ReLU) was introduced to provide non-saturating [[Derivative|gradient]] for positive inputs while keeping computation as cheap as a simple threshold operation.

## Mathematical Formulation & Derivative

$$\text{ReLU}(x) = \max(0, x) = \begin{cases} x & \text{if } x > 0 \\ 0 & \text{if } x \le 0 \end{cases}$$

$$\frac{d}{dx}\text{ReLU}(x) = \begin{cases} 1 & \text{if } x > 0 \\ 0 & \text{if } x < 0 \end{cases}$$

_(At $x=0$, the subderivative is typically set to 0 or 0.5 in deep learning frameworks)._

![[ReLU-1791026434341.webp]]

## Key Strengths

- **No Vanishing Gradient for $x > 0$:** The gradient is constant ($1.0$), ensuring stable forward and backward propagation through very deep networks.
- **Computational Efficiency:** Requires no costly exponential operations, only a bitwise comparison.
- **Sparse Representations:** Roughly half of the activations in a layer become exact zeros, creating sparse and efficient feature representations.

## Limitations 

* **The "Dying ReLU" Problem):** If a large gradient update causes a neuron's weights to adjust such that $W \cdot x + b < 0$ for all training samples, the neuron outputs $0$ and receives a gradient of $0$. It becomes permanently inactive ("dead") and stops updating forever.

# Leaky ReLU

Leaky ReLU directly targets the **Dying ReLU** problem. By adding a tiny, fixed positive slope to the negative region ($x < 0$), it guarantees that every neuron retains a non-zero gradient, keeping dead units recoverable during optimization.

### Mathematical Formulation & Derivative

$$\text{Leaky ReLU}(x) = \begin{cases} x & \text{if } x > 0 \\ \alpha x & \text{if } x \le 0 \end{cases} \quad (\text{where } \alpha \text{ is a fixed hyperparameter, typically } \alpha = 0.01)$$

$$\frac{d}{dx}\text{Leaky ReLU}(x) = \begin{cases} 1 & \text{if } x > 0 \\ \alpha & \text{if } x < 0 \end{cases}$$

![[ReLU-1791026985172.webp]]

## Key Strengths & Weaknesses

- **Prevents Dying Neurons:** Since the gradient for $x < 0$ is $\alpha > 0$, information flows through the network even for negative inputs.
- **Fast Computation:** Retains the high execution speed of standard ReLU with minimal overhead.

## Limitations
- $\alpha$ is a fixed, hand-tuned hyperparameter that might not be optimal for every dataset or layer depth.

# PReLU (Parametric ReLU)

Rather than treating the negative slope $\alpha$ as a fixed hyperparameter, PReLU turns $\alpha$ into a **learnable parameter** updated via backpropagation alongside the weight matrices.

## Mathematical Formulation & Derivative

$$\text{PReLU}(x) = \begin{cases} x & \text{if } x > 0 \\ \alpha_i x & \text{if } x \le 0 \end{cases}$$

Where $\alpha_i$ is learned independently for each channel/neuron (or shared across a layer):

$$\frac{\partial}{\partial x}\text{PReLU}(x) = \begin{cases} 1 & \text{if } x > 0 \\ \alpha_i & \text{if } x < 0 \end{cases}, \quad \frac{\partial}{\partial \alpha_i}\text{PReLU}(x) = \begin{cases} 0 & \text{if } x > 0 \\ x & \text{if } x \le 0 \end{cases}$$

## Key Strengths 

- **Adaptability:** Allows different layers and feature maps to dynamically decide how much negative signal to preserve.
- **Negligible Extra Parameters:** Adding a single scalar parameter per channel increases model size by less than 0.01%.
## Limiations

- Risk of **overfitting** on smaller datasets if $\alpha_i$ is learned per-channel without proper regularization.

# ELU (Exponential Linear Unit)

While Leaky ReLU and PReLU fix the dying neuron issue, their piecewise linear nature leaves a sharp non-differentiable discontinuity at $x=0$. ELU introduces a smooth, non-linear curve for $x < 0$ that saturates toward a negative constant ($-\alpha$). This shifts the mean activation value closer to zero, accelerating gradient descent convergence.

### Mathematical Formulation & Derivative

$$\text{ELU}(x) = \begin{cases} x & \text{if } x > 0 \\ \alpha(e^x - 1) & \text{if } x \le 0 \end{cases} \quad (\text{typically } \alpha = 1.0)$$

$$\frac{d}{dx}\text{ELU}(x) = \begin{cases} 1 & \text{if } x > 0 \\ \text{ELU}(x) + \alpha = \alpha e^x & \text{if } x \le 0 \end{cases}$$

![[ReLU-1791028068125.webp]]


## Key Strengths

- **Zero-Mean Activations:** The smooth negative values lower the mean unit activation toward zero, producing a natural [[Batch Normalization]] effect.
- **Smooth & Continuous:** Avoids abrupt changes in gradient direction at $x=0$.
- **Noise Robustness:** The saturation for large negative values ($-\alpha$) makes the network less sensitive to noisy negative inputs.
## Limitations

* **Higher Computational Cost:** Calculating $e^x$ during forward and backward passes is significantly slower than simple thresholding.

# When to Use Which?

1. **Use ReLU as the Baseline Default:**
    
    - Starting a new standard Convolutional or Fully Connected model where computation speed and memory bandwidth are critical.
    - Working with resource-constrained environments (mobile, embedded, or edge devices).

2. **Use Leaky ReLU if Neurons Are Dying:**
    
    - Training very deep networks or observing that a high percentage ($>20\text{--}30\%$) of hidden units output zero during or after training.
    - Experiencing unstable training with high learning rates.

3. **Use PReLU for High-Capacity Vision Models:**
    
    - Building deep [[Convolutional Neural Network|CNN]] architectures on large datasets (like ImageNet) where the network can afford a few extra parameters to maximize accuracy without manual tuning.

4. **Use ELU for Noise-Heavy Data or Deeper Networks without BatchNorm:**

    - Training networks where [[Batch Normalization]] is either omitted or difficult to apply (e.g., small batch sizes).
    - Working with signal processing or noisy domain data where saturation for extreme negative values aids generalization.