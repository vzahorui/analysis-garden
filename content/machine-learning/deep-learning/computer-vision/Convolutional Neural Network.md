---
tags:
  - ML/deep-learning
  - ML/computer-vision
aliases:
  - CNN
---
# Motivation

The primary motivation behind Convolutional Neural Networks (CNNs) was to overcome the severe architectural and computational limitations of applying traditional Fully Connected Layers ( [[Neural Network#From Perceptron to MLP|MLPs]]) to visual and grid-structured data.

The core motivations can be broken down into four key drivers:

## Curbing Parameter Explosion (The Curse of Dimensionality)

When processing images with standard MLPs, every pixel must connect to every neuron in the hidden layer.

- Even for a modest $224 \times 224$ RGB image, the input layer has over 150,000 features.
- Connecting this to a single hidden layer of moderate size yields tens of millions of weights.
- This leads to unmanageable memory overhead, severe overfitting, and a data-hungry network that requires astronomical amounts of training examples.

**The CNN Solution:** restricting neurons to local receptive fields and enforcing **weight sharing** (using the same filter across the entire image), CNNs slash the parameter count from millions to thousands.

## Preserving Spatial Topology

Standard MLPs require flattening 2D or 3D matrices into a 1D vector.

- This flattening completely destroys the spatial geometry of an image. Pixels that are adjacent to each other physically are treated no differently than pixels on opposite corners of the frame.
- Consequently, the network loses its ability to understand neighborhood structures, continuity, and shapes.

**The CNN Solution:** Convolutions operate directly on 2D grids, preserving the spatial layout and ensuring that geometric relationships between pixels remain intact through the intermediate feature maps.

## Achieving Translation Invariance

In a standard MLP, if an object of interest (like a cat's ear or a traffic sign) shifts a few pixels to the left or right, the flattened input vector changes completely. The network must re-learn the feature detectors for every possible spatial location independently.

**The CNN Solution:** Because a convolutional kernel slides across the entire image using the exact same weights, it learns to recognize a feature (such as an edge or a corner) **regardless of where it appears** in the visual field, drastically improving generalization.

# How It Works

## Core Mechanics: Convolutions & Spatial Dimensions

Convolutional Neural Networks rely on [[Kernel Mathematics in CNNs|kernels]] (filters) to extract spatial features like edges, textures, and shapes from input [[Tensor|tensors]]. How a kernel slides and shares weights is in [[Kernel Mathematics in CNNs]].

Layer hyperparameters that control the slide include [[Stride]] and [[Padding]].

As convolutional layers stack, each unit's [[Receptive Field]] grows, so later layers can detect more complex, holistic shapes.

### Feature Extraction

Activations are organized as [[Channel|channels]]: spatial feature maps stacked along depth. An RGB image starts with $C_{\mathrm{in}} = 3$. Each [[Kernel Mathematics in CNNs|kernel]] (filter) is a volume $k \times k \times C_{\mathrm{in}}$ that collapses all input channels into **one** 2D feature map. A layer with $C_{\mathrm{out}}$ kernels stacks those maps into $C_{\mathrm{out}}$ output channels for the next layer. Details: [[Channel]].

[[Pooling]] acts as a periodic checkpoint to reduce resolution and manage compute as the network moves from low-level details (edges) to high-level semantics (objects).

# Classical Architectures & Evolutionary Leaps

- **Early Pioneers:** [[LeNet-5]] foundational design and [[AlexNet]] breakthrough scaling principles.
- **[[VGG]] Network:** The design rationale of uniform small filters ($3 \times 3$) and deep stacking.
- **[[ResNet]] & Residual Learning:** Solving [[Exploding and Vanishing Gradients|vanishing gradient]] via [[Skip Connections]] and identity mappings.
