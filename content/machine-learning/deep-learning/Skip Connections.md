---
tags:
  - ML/computer-vision
  - ML/deep-learning
---
**Skip connections** (also known as shortcut connections) are architectural design patterns in [[Neural Network|Neural Networks]] where the output of one layer is bypassed and added to, or concatenated with, the output of a later layer.

While initially popularized to train extremely deep classification networks (like [[ResNet]]), they are now a foundational building block across computer vision for tasks ranging from image generation to semantic segmentation (like U-Net).

## The Two Main Problems Skip Connections Solve

1. **[[Exploding Gradients|**The Vanishing/Exploding Gradient Problem]]:** Skip connections provide an uninterrupted "highway" for gradients to flow backward directly to earlier layers.
2. **The Degradation Problem:** Without skip connections, adding more layers to a network can paradoxically lead to _higher_ training error because optimization struggles to learn even simple identity mappings. Skip connections make it easy for the network to learn identity functions if extra layers aren't needed.

## Major Types of Skip Connections

### Residual Connections (Addition-based)

Used heavily in standard classification and feature-extraction backbones (such as [[ResNet]]), these connections perform element-wise addition between the input of a block and its output.

- **How it works:** Instead of learning a direct mapping $H(x)$, a layer block learns a residual function $F(x) = H(x) - x$. The final output of the block becomes:

$$y = F(x) + x$$

- **Why it helps:** If a particular layer block adds no value, the weights of $F(x)$ can simply drive toward zero, leaving the network to pass the original input $x$ forward cleanly through the identity path ($y \approx x$).

### Feature Concatenation (U-Net Style / Encoder-Decoder)

Used extensively in dense prediction tasks like semantic segmentation, depth estimation, and image-to-image translation (e.g., [[U-Net]]), these connections concatenate feature maps across channels rather than adding them.

- **How it works:**
    
    - The **encoder** (contracting path) gradually downsaples the image, capturing broad contextual information ("what" is in the image) while losing fine-grained spatial precision (via combination of [[Kernel Mathematics in CNNs]] and [[Pooling]]).
    - The **decoder** (expanding path) upsamples the feature maps to recover spatial resolution.
    - **Skip connections** bridge the encoder and decoder directly at matching resolution levels, concatenating high-resolution encoder features with upsampled decoder features.

- **Why it helps:** The decoder gets the best of both worlds: deep semantic context from the lower layers, combined with sharp, localized edge and texture details from the matching encoder layers.
## Summary of Benefits

- **Improved Gradient Flow:** Enables the training of networks with dozens or hundreds of layers without performance degradation.
- **Multi-Scale Feature Representation:** Combines low-level geometric details (edges, textures) with high-level semantic information (objects, shapes).
- **Faster Convergence:** Networks with skip connections consistently train faster and reach lower validation loss compared to plain feedforward architectures.