---
tags:
  - ML/deep-learning
aliases:
  - Neural Net
  - Neural Networks
  - NN
---
A **neural network** maps inputs to outputs through layers of interconnected neurons. Inspired by biological brains, it is the building block behind [[Deep Learning Concepts|Deep Learning]] when those layers stack deep.

# What It Is

Three kinds of layers:

1. **Input**: raw features (pixels, tabular columns, waveforms, …).
2. **Hidden**: stacked neurons that transform the representation. Multiple hidden layers make a deep network.
3. **Output**: the prediction (class probabilities, a number, …).

![[Neural Network-1790875439876.webp]]

# One Neuron

Each neuron does two steps:

1. **[[Linear Models|Linear]] combination** of its inputs plus a bias:

$$z = \sum_{i=1}^{n} w_i x_i + b$$

2. **Nonlinear activation** $a = \sigma(z)$. Common choices live in their own notes: [[ReLU]], [[Sigmoid Function|Sigmoid]], [[Softmax Function|Softmax]] (typical multi-class **output**), GELU, and others.

# Why Nonlinearity

Without a nonlinear $\sigma$, stacked layers collapse into one affine map: depth buys nothing.

With identity activations, layer outputs compose as matrix products:

$$\begin{aligned}
\mathbf{h}_1 &= \mathbf{W}_1 \mathbf{x} + \mathbf{b}_1 \\
\mathbf{h}_2 &= \mathbf{W}_2 \mathbf{h}_1 + \mathbf{b}_2 = (\mathbf{W}_2 \mathbf{W}_1)\mathbf{x} + (\mathbf{W}_2 \mathbf{b}_1 + \mathbf{b}_2)
\end{aligned}$$

Expanding this out for an $L$-layer network gives:

$$\mathbf{y} = \left( \prod_{i=1}^{L} \mathbf{W}_i \right) \mathbf{x} + \sum_{j=1}^{L} \left( \prod_{k=j+1}^{L} \mathbf{W}_k \right) \mathbf{b}_j$$

Because matrix multiplication is associative and closed under matrix multiplication, we can substitute:

- $\mathbf{W}_{\text{effective}} = \mathbf{W}_L \mathbf{W}_{L-1} \dots \mathbf{W}_1$

- $\mathbf{b}_{\text{effective}} = \mathbf{W}_L \dots \mathbf{W}_2 \mathbf{b}_1 + \dots + \mathbf{b}_L$

This simplifies the entire $L$-layer network down to a single affine transformation:

$$\mathbf{y} = \mathbf{W}_{\text{effective}} \mathbf{x} + \mathbf{b}_{\text{effective}}$$

Nonlinear activations break that collapse and let the network approximate virtually any continuous function (Universal Approximation Theorem).

# From Perceptron to MLP

The classic **perceptron** is a single neuron with a step activation function: one linear decision boundary, only **linearly separable** problems.

![[Neural Network-1790885068227.webp]]

Swap the step for a [[Sigmoid Function]] and the unit is mathematically [[Logistic Regression]]. 

A **multilayer perceptron (MLP)** stacks hidden layers with differentiable nonlinearities so the decision surface can bend.

# How It Learns

Training is a loop:

1. **Forward pass**: compute predictions through the layers.
2. **Loss**: score the gap to targets ([[Loss vs Metric]]).
3. **[[Backpropagation]]**: chain-rule [[Derivative#Gradient|gradients]] of the loss w.r.t. weights.
4. **Update**: nudge parameters with [[Gradient Descent]] (usually mini-batch SGD).

Optimizer variants, learning-rate behavior, and batch choices stay in [[Gradient Descent]].

# When It Shines

- **Hierarchical features** from raw inputs: less hand-built feature engineering than classical [[Linear Regression]] or [[Support Vector Machine|SVM]]s.
- **Unstructured modalities**: vision ([[Computer Vision Concepts]]), language, audio, sequences.
- **Scale with data and hardware**: mini-batch SGD on GPUs/TPUs, unlike many kernel methods that blow up as $O(N^2)$–$O(N^3)$.

# Limits and Tradeoffs

- **Data hunger**: on small tabular sets ($\le 10{,}000$ rows), gradient-boosted trees (e.g. XGBoost) usually win out of the box.
- **Opacity**: harder to explain than [[Tree-Based Algorithms|decision trees]] or linear coefficients; [[SHAP]] and similar tools only approximate.
- **Compute**: deep models want accelerators and careful [[Regularization|regularization]] (dropout, weight decay), plus many architecture and hyperparameter choices.

# See Also 

* [[Activation Functions]]
