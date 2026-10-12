---
tags:
  - ML/computer-vision
---
Pooling (or subsampling) is a fundamental operation in [[Convolutional Neural Network]]s (CNNs) designed to progressively reduce the spatial dimensions (height and width) of feature maps. By sliding a [[Kernel Mathematics in CNNs|filter]] window across the feature map and summarizing the values within it, pooling layers decrease the amount of parameters and computation in the network while controlling overfitting.

## Main Types of Pooling Operations

- **Max Pooling:** Slides a window across the feature map and selects the **maximum value** within each region. This preserves the most prominent features (such as sharp edges or distinct shapes) and provides robust spatial invariance.
- **Average Pooling:** Calculates the **arithmetic mean** of all values inside the pooling window. This smooths out the feature map, capturing broader background context and regional color or intensity distributions rather than peak activations.
- **Global Pooling:** Condenses an entire 2D feature map [[channel]] down to a **single [[scalar]]** (Global Max or Global Average Pooling). It is commonly used as a replacement for flattening layers before the final classification block to drastically reduce model parameters.

## Core Benefits in CNN Architectures

- **Dimensionality Reduction:** Shrinks spatial resolution layer-by-layer, which lowers memory usage and speeds up training and inference.
- **Translational Invariance:** Makes the network resilient to minor shifts, tilts, or distortions in the input image, ensuring that an object's feature is detected regardless of small position changes.
- **[[Receptive Field]] Expansion:** Broadens the effective receptive field of deeper convolutional layers, enabling the network to learn holistic patterns and higher-level semantic structures.

## Where Pooling Fits Inside CNN

Pooling is applied **after** the kernel sliding window operation, not as an alternative. They are sequential, complementary steps that make up a standard convolutional layer block.
### The Standard Sequence in a CNN Block

1. **Convolution ([[Kernel Mathematics in CNNs|kernel]] Sliding Window):** Filters slide across the input image to extract local features (like edges, corners, or textures), generating a feature map.
2. **[[Activation Functions|Activation Function]] (e.g., [[ReLU]]):** Applied immediately after the convolution to introduce non-linearity, allowing the network to learn complex patterns.
3. **Pooling Layer:** Applied to the resulting feature map to downsample its spatial dimensions (height and width) while retaining the most important activation values.

### Is there any overlap? (Strided Convolutions)

While pooling is a separate subsequent step, you will sometimes see **strided convolutions** used as an alternative to dedicated pooling layers. By setting the [[stride]] of the convolutional kernel to 2 (instead of 1), the filter skips pixels as it slides, which simultaneously extracts features _and_ reduces the spatial dimensions in a single step.

However, in classic CNN architectures (like [[LeNet-5]] or early VGG nets), the convolution and pooling layers are distinct operations executed one after the other.