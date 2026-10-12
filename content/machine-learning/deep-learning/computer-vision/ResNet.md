---
tags:
  - ML/computer-vision
---
Introduced in 2015 by Kaiming He, Xiangyu Zhang, Shaoqing Ren, and Jian Sun from Microsoft Research, **ResNet** (Residual Network) represents one of the most important milestones in [[Deep Learning Concepts|Deep Learning]] history. It won the ImageNet 2015 competition with a staggering 152-layer architecture (over 8x deeper than [[VGG]]) and fundamentally changed how [[Neural Network|Neural Networks]] are designed.

## The Problem ResNet Solved: The Degradation Problem

Before ResNet, a prevailing assumption in deep learning was that simply stacking more layers would always improve performance. However, researchers ran into a brick wall known as the **degradation problem**:

- As networks grew extremely deep (e.g., jumping from 20 layers to 56 layers), accuracy got saturated and then **degraded rapidly**.
- This wasn't caused by overfitting (where training error drops while test error rises). In this case, **both training error and test error got worse** when the network became too deep.
- The culprit was the [[Exploding and Vanishing Gradients]] problem: as [[Derivative|gradients]] traveled backward through dozens of layers, they became so small that early layers stopped learning entirely.

## Core Innovation: Residual (Skip) Connections

ResNet solved this by introducing **shortcut connections** (also called [[Skip Connections]]) that bypass one or more layers.

Instead of forcing a stack of layers to learn an underlying mapping $H(x)$, ResNet forces them to learn a **residual mapping**: $F(x) = H(x) - x$.

Adding the residual to $x$ recovers $H(x)$.

The final output of the block is then computed as:

$$y = F(x) + x$$

### Why This Changes Everything:

- **The Identity Shortcut:** The input $x$ is added directly to the output of the convolutional layers via an identity connection that requires zero extra parameters or computation.
- **Easy Gradient Flow:** During [[backpropagation]], the gradient can flow straight through the addition operation ($+ x$) back to earlier layers without vanishing, acting as a "gradient highway."
- **Effortless Identity Mapping:** If a particular layer block adds no value to the network, the network can easily learn to push the weights of $F(x)$ to zero, leaving $y = x$. This ensures that a deeper network will perform at least as well as a shallower network, never worse.

## Anatomy of ResNet: Basic Blocks vs Bottleneck Blocks

ResNet comes in various depths (ResNet-18, ResNet-34, ResNet-50, ResNet-101, ResNet-152). The structural design changes depending on how deep the network goes:

- **Basic Block (ResNet-18 / ResNet-34):** Uses two sequential $3 \times 3$ convolutional layers, with a skip connection wrapping around them.
- **Bottleneck Block (ResNet-50 and deeper):** To keep computation manageable in ultra-deep networks, ResNet-50+ replaces the two $3 \times 3$ layers with a three-layer "bottleneck" design:
    
    1. A **$1 \times 1$ conv layer** to reduce the number of channels.
    2. A **$3 \times 3$ conv layer** to process spatial features.
    3. A **$1 \times 1$ conv layer** to restore/expand the channel dimensions.

## Legacy and Modern Impact

ResNet's skip-connection pattern proved so powerful that variations of it are now ubiquitous across artificial intelligence. Beyond [[Computer Vision Concepts|Computer Vision]], residual connections are a foundational pillar of **[[Transformer|Transformers]]** (used in modern Large Language Models like GPT and Claude) and diffusion models, enabling networks to scale to hundreds of layers safely.