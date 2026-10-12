---
tags:
  - ML/deep-learning
  - ML/computer-vision
aliases:
  - kernel
  - filter
  - convolutional filter
---
## What is a Kernel in CNN?

A **kernel** (also called a **filter**) is one learnable weight bank: a sliding pattern-detector. Spatially it is a small $k \times k$ [[matrix]] of weights; when the input has multiple [[Channel|channels]], that bank is a volume $k \times k \times C_{\mathrm{in}}$. Either way, **one kernel produces one output feature map** (one output channel). Kernel and filter mean the same thing here; a [[Channel|channel]] is a different idea (a slice of the activation tensor). Details of input / output channel counts live in [[Channel]].

Think of each kernel as looking for a specific visual pattern as it scans the input. For example:

- One kernel might detect vertical edges.
- Another might look for bright spots or color transitions.

As the network learns, the weights inside the kernel change so it gets better at features useful for the task (like recognizing a face or a cat).

## Sliding Window Dot Products and Feature Maps

At its core, a 2D convolution layer slides the kernel $K$ sized $m \times n$, across an input feature map $I$. At each spatial location $(i, j)$, the operation computes a [[Frobenius Inner Product]]: an element-wise multiplication between the kernel weights and the overlapping patch of the input tensor, summed together with a bias term.

$$S(i, j) = \sum_{m} \sum_{n} I(i+m, j+n) \cdot K(m, n) + b$$

That form is the single-channel case. With $C_{\mathrm{in}}$ input [[Channel|channels]], the same filter is a volume $K$ of shape $k \times k \times C_{\mathrm{in}}$ (depth matches $C_{\mathrm{in}}$). At each spatial location the response sums over spatial offsets **and** input channels, then adds a bias, still producing **one** output feature map:

$$S(i, j) = \sum_{c=1}^{C_{\mathrm{in}}} \sum_{m} \sum_{n} I(i+m, j+n, c) \cdot K(m, n, c) + b$$

Stacking many such maps ($C_{\mathrm{out}}$ filters) into the next layer's channel axis is covered in [[Channel]].

The _exact same_ kernel weights ($K$) are reused across every single sliding window from the top-left to the bottom-right of the image. In deep learning, this is called **parameter sharing** (or weight sharing). 

![[convolutional_neural_networks.gif]]

The result is the output feature map $S$. If $S(2, 1)$ has a very high value, it tells the network: _"The specific pattern this kernel looks for (like a vertical edge or a corner) is strongly present at this specific spot in the image."_

This design choice serves two critical purposes:

1. **Translation Invariance**: Detecting features anywhere.
2. Massive **Parameter Reduction**, which prevents overfitting.

## Multitudes of Features

### Different Kernels for Different Features

One kernel might learn to detect vertical edges, another horizontal edges, and another color blobs. To capture these features simultaneously, a convolutional layer uses a **stack of multiple kernels** (filters) in parallel on the same input. If a layer has 32 filters, 32 pattern-detectors scan at once and write **32 output feature maps**, which stack as 32 output [[Channel|channels]] for the next layer.

### Number of Kernels

The number of kernels ($C_{\mathrm{out}}$) is a **hyperparameter** when designing the architecture. There is no rigid formula, but common practice:

- **Early layers** usually have fewer filters (e.g. 16 or 32): basic edges and gradients.
- **Deeper layers** often use many more (e.g. 128, 256, or 512): textures, parts, whole objects.
- Trade off accuracy against memory and compute.

Those $C_{\mathrm{out}}$ maps stack as output [[Channel|channels]]; tensor shape and depth matching are in [[Channel]]. Hub overview: [[Convolutional Neural Network]].

## Kernel Size

Kernel sizes are also chosen by the network designer. Common choices are $3 \times 3$, $5 \times 5$, or $7 \times 7$.

- **The $3 \times 3$ standard:** Modern deep learning heavily favors $3 \times 3$ kernels. It is the smallest size that can capture directional context (up, down, left, right, and diagonals) while keeping math lightweight.
- **Why not huge kernels?** While a $7 \times 7$ kernel looks at a wider area at once, it requires exponentially more parameters and computations. Instead of one large kernel, modern architectures (like VGG and [[ResNet]]) stack multiple $3 \times 3$ layers back-to-back, which achieves a wide "receptive field" with far fewer parameters.

## Why Deep Learning Uses Cross-Correlation over True Convolution

In signal processing and classical mathematics, **convolution** and **cross-correlation** are distinct operations, primarily differing by an axis reflection.

- **True Convolution** requires flipping the kernel horizontally and vertically before sliding it over the input:

$$(I * K)(i, j) = \sum_{m} \sum_{n} I(i-m, j-n) K(m, n)$$

- **Cross-Correlation** omits the kernel-flipping step, applying the weight matrix directly in its natural orientation:

$$(I \star K)(i, j) = \sum_{m} \sum_{n} I(i+m, j+n) K(m, n)$$
Despite being named "Convolutional" Neural Networks, [[Deep Learning Concepts|Deep Learning]] frameworks (like PyTorch and TensorFlow) almost universally implement **cross-correlation** instead of true mathematical convolution.

- **Commutativity:** True convolution satisfies the commutative property ($I * K = K * I$), whereas cross-correlation does not. However, neural networks do not require commutativity in their layer definitions.
- **Learned Weights:** Because kernel weights are initialized randomly and tuned via [[Gradient Descent]], whether a filter is stored in its original orientation or flipped is irrelevant: the network learns the weights that minimize loss either way. Omitting the flip improves computational efficiency.