---
tags:
  - ML/deep-learning
---
Dropout is a [[regularization]] technique used in [[Neural Network|Neural Networks]] to prevent **overfitting**. During training, it randomly deactivates (sets to zero) a chosen percentage of neurons in a layer for a given forward-backward pass.

![[Dropout-1791032032912.webp]]

## How It Works

### Training Phase

- At each iteration, every neuron in a dropout-enabled layer has a probability $p$ (e.g., $0.5$) of being temporarily dropped out.
- Dropped neurons contribute nothing to the forward pass and receive no weight updates during backpropagation.
- Because nodes are removed at random, each minibatch trains a slightly different sub-network architecture.

### Inference (Testing) Phase

- Dropout is **turned off**. All neurons remain active to make full use of the network's learned capacity.
- To account for the fact that more neurons are active during inference than during training, activation outputs are scaled by $(1 - p)$, or, more commonly via **Inverted Dropout**, scaled by $\frac{1}{1 - p}$ during training so no adjustment is needed at test time.

## Why It Prevents Overfitting

- **Breaks Co-adaptation:** Without dropout, neurons can develop complex dependencies on one another, relying on specific combination behaviors to fix errors made by previous nodes. Dropout forces each neuron to learn useful, standalone features.
- **Acts as an Ensemble Method:** Training a network with dropout is mathematically equivalent to training an ensemble of $2^N$ smaller sub-networks (where $N$ is the total number of dropouts-eligible neurons) and averaging their predictions at inference time. This is how [[Random Forest]] works.

## Common Implementation Guidelines

| **Parameter / Aspect**   | **Typical Choice**                       | **Context**                                                                                                         |
| ------------------------ | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Dropout Rate ($p$)**   | $0.2 - 0.5$                              | $0.2$–$0.3$ for input layers; $0.5$ for fully connected hidden layers                                               |
| **Placement**            | Fully Connected (Dense) Layers           | Most effective in high-parameter layers where overfitting is high                                                   |
| **Convolutional Layers** | Spatial Dropout / Low Rate ($0.1 - 0.2$) | Standard dropout is less effective on [[Convolutional Neural Network\|CNN]] feature maps due to spatial correlation |
