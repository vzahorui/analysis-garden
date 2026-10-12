---
tags:
  - ML/computer-vision
aliases:
  - LeNet
---
Introduced by Yann LeCun and his colleagues in 1998, **LeNet-5** is one of the earliest and most influential [[Convolutional Neural Network]]s (CNNs). Designed primarily for optical character recognition tasks—such as reading handwritten digits on bank checks (the MNIST dataset), it laid the structural foundation for modern [[Computer Vision Concepts|Computer Vision]].

Before LeNet, [[Neural Network|Neural Networks]] treated images as flattened, 1D vectors, ignoring spatial geometry and exploding in parameter count as image sizes grew. LeNet introduced the concept of processing spatial data hierarchically through local connectivity and weight sharing.

## Core Architectural Innovations

LeNet-5 pioneered several foundational design patterns that remain standard in deep learning today:

- **Local Receptive Fields:** Neurons in convolutional layers are connected to only a small, localized region of the previous layer, mimicking the visual cortex's receptive fields.
- **Shared Weights ([[Kernel Mathematics in CNNs|kernels]]):** The same filter weights are slid across the entire input image, drastically reducing the total number of trainable parameters and enabling translation invariance.
- **Subsampling ([[Pooling]]):** Spatial dimensions are reduced progressively to build abstraction and provide robustness against minor shifts and distortions in the input.
- **Non-linear [[Activation Functions|activations]]:** Utilizing [[Sigmoid Function|sigmoid]] or [[Hyperbolic Tangent|tanh]] activations (though modern networks use [[ReLU]]) to model complex, non-linear relationships.

## Layer-by-Layer Breakdown (LeNet-5)

The classic LeNet-5 architecture processes a **32x32 pixel grayscale image** through a sequence of alternating convolutional and subsampling layers, ending with fully connected layers.

| **Layer**  | **Type**        | **Map Size** | **Kernels / Parameters**   | **Description**                                                           |
| ---------- | --------------- | ------------ | -------------------------- | ------------------------------------------------------------------------- |
| **Input**  | Image           | 32x32        | -                          | Grayscale normalized input image.                                         |
| **C1**     | Convolution     | 28x28        | 6 filters (5x5)            | Extracts low-level local features (edges, corners).                       |
| **S2**     | Subsampling     | 14x14        | 2x2 pooling                | Reduces spatial resolution and halves dimensions using average pooling.   |
| **C3**     | Convolution     | 10x10        | 16 filters (5x5)           | Combines low-level features to learn more complex patterns.               |
| **S4**     | Subsampling     | 5x5          | 2x2 pooling                | Further reduces spatial dimensions while retaining feature maps.          |
| **C5**     | Convolution     | 1x1          | 120 filters (5x5)          | Acts as a fully connected convolution layer mapping features to a vector. |
| **F6**     | Fully Connected | 1x84         | 84 units                   | Dense layer processing feature representations.                           |
| **Output** | Output Layer    | 1x10         | RBF / [[Softmax Function]] | Predicts the final class probabilities for digits 0 through 9.            |

## Historical Significance & Modern Legacy

While LeNet-5 is small by modern standards, its DNA lives on in virtually every advanced CNN architecture:

- **Scaling up:** Modern networks like [[VGG]], [[ResNet]], and EfficientNet scale LeNet's foundational pattern of alternating convolutions and pooling deeper and wider.
- **Encoder-Decoder Architectures:** The hierarchical extraction of spatial features pioneered in LeNet directly paved the way for modern dense prediction models, such as U-Net, where downsampling paths extract context before reconstructing spatial details via [[Skip Connections]].