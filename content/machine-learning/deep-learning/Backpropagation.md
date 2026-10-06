---
tags:
  - ML/deep-learning
---
When training a [[Neural Network]] using [[Gradient Descent]], every layer updates two sets of trainable parameters: the **weight matrix $\mathbf{W}^{(l)}$** and the **bias vector $\mathbf{b}^{(l)}$**.

By isolating the **local gradient** at a neuron or layer, we can see exactly how backpropagation flows backward and how weight decay modifies parameter updates across both standard SGD and [[Adaptive Optimizers]] like AdamW.

## The Forward Pass

For a given layer $l$, the forward pass computes:

$$\mathbf{z}^{(l)} = \mathbf{W}^{(l)} \mathbf{a}^{(l-1)} + \mathbf{b}^{(l)}$$

$$\mathbf{a}^{(l)} = \sigma(\mathbf{z}^{(l)})$$

where:
- $\mathbf{a}^{(l-1)}$ is the activation from the previous layer ($\mathbf{a}^{(0)} = \mathbf{x}$, the input).
- $\mathbf{z}^{(l)}$ is the pre-activation vector.
- $\sigma(\cdot)$ is the element-wise activation function.

## Backpropagation & The Local Gradient

Backpropagation uses the [[Derivative#Fundamental Rules|chain rule]] to compute how the final loss $L$ changes with respect to the pre-activation vector $\mathbf{z}^{(l)}$. This crucial intermediate vector is called the **local gradient** ($\boldsymbol{\delta}^{(l)}$):

$$\boldsymbol{\delta}^{(l)} \equiv \frac{\partial L}{\partial \mathbf{z}^{(l)}}$$

### Computing the Local Gradient Across Layers

#### At the Output Layer ($L$)

$$\boldsymbol{\delta}^{(L)} = \nabla_{\mathbf{a}^{(L)}} L \odot \sigma'(\mathbf{z}^{(L)})$$

This is the derivative of the loss with respect to the output, scaled by the activation function's derivative at $\mathbf{z}^{(L)}$ (using [[Hadamard Product]]).

Then using the formulas from the Forward Pass we can compute the **Weight & Bias Gradients:**

$$\frac{\partial L}{\partial W^{[L]}} = \delta^{[L]} \left(a^{[L-1]}\right)^T, \quad \frac{\partial L}{\partial b^{[L]}} = \delta^{[L]}$$

#### At Hidden Layers ($l$)

Here we propagate errors backwards using the chain rule. In this case the propagated error signal to the layer $l$ is $\delta^{(l+1)}$. 

1. **Upstream Gradient Pass:** Multiply the downstream error signal by the transposed weight [[matrix]] to see how much each hidden node contributed to layer $l+1$:

$$\frac{\partial L}{\partial a^{[l]}} = \left(W^{[l+1]}\right)^T \delta^{[l+1]}$$
Here [[Matrix]] $\mathbf{W}^{(l+1)}$ is the derivative of $\mathbf{z}^{(l)}$ with respect to its $\mathbf{a}^{(l)}$. 

2. **Hidden Layer Error Signal ($\delta^{[l]}$):** Multiply by the local derivative of activation $\sigma'$:

$$\delta^{[l]} = \left( \left(W^{[l+1]}\right)^T \delta^{[l+1]} \right) \odot \sigma'\left(z^{[l]}\right)$$

3. **Weight & Bias Gradients:**

$$\frac{\partial L}{\partial W^{[l]}} = \delta^{[l]} \left(a^{[l-1]}\right)^T, \quad \frac{\partial L}{\partial b^{[l]}} = \delta^{[l]}$$

#### At the Input Layer

The error signal propagates back to the input layer $l=0$. Since input values $x = a^{[0]}$ are fixed dataset values without tunable weights, backpropagation stops here.

### Parameter Update

Once gradients $\frac{\partial L}{\partial W^{[l]}}$ and $\frac{\partial L}{\partial b^{[l]}}$ are calculated across all layers, update parameters using learning rate $\eta$:

$$W^{[l]} \leftarrow W^{[l]} - \eta \frac{\partial L}{\partial W^{[l]}}$$

$$b^{[l]} \leftarrow b^{[l]} - \eta \frac{\partial L}{\partial b^{[l]}}$$





