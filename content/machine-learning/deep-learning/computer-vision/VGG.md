---
tags:
  - ML/computer-vision
---
Introduced in 2014 by Karen Simonyan and Andrew Zisserman from the Visual Geometry Group at Oxford University, **VGG** (most notably **VGG-16** and **VGG-19**) became a landmark architecture in computer vision. While it took second place in the 2014 ImageNet competition (beaten by GoogLeNet), VGG became vastly more popular due to its **extreme simplicity, uniformity, and intuitive design**.

Where [[AlexNet]] used a mix of large and small filters ($11 \times 11$, $5 \times 5$, $3 \times 3$), VGG proved that depth alone, when combined with a uniform architectural philosophy, could dramatically improve feature representation.

## Core Innovations: The Power of Small Filters

VGG’s defining breakthrough wasn't a complex new layer type or regularization trick, but a disciplined approach to filter size:

- **Exclusively $3 \times 3$ Convolutional [[Kernel Mathematics in CNNs|Filters]]:** Every single convolutional layer in VGG uses a $3 \times 3$ kernel with a [[stride]] of 1 and [[padding]] of 1.
- **Why stack small filters instead of using large ones?**
    
    - **Parameter Efficiency:** Two stacked $3 \times 3$ convolutional layers have an effective receptive field of $5 \times 5$, and three stacked layers cover a $7 \times 7$ area. However, three $3 \times 3$ layers require significantly fewer parameters than a single $7 \times 7$ layer (e.g., $3 \times (3^2) = 27$ parameters per channel versus $7^2 = 49$).
    - **More Non-Linearity:** By stacking multiple layers, you introduce a **[[ReLU]] [[Activation Functions|activation]] function** after _every_ convolution. This gives the network more opportunities to learn complex, non-linear decision boundaries than a single large convolution followed by one activation.

## Architectural Structure (VGG-16)

VGG-16 consists of **13 convolutional layers and 3 fully connected layers** (totaling 16 weight layers), organized into 5 distinct blocks separated by max-[[pooling]] layers.

It processes a standard $224 \times 224 \times 3$ RGB image through a predictable pattern:

- **Block 1:** Two $3 \times 3$ conv layers (64 filters) $\rightarrow$ Max Pooling ($2 \times 2$)
- **Block 2:** Two $3 \times 3$ conv layers (128 filters) $\rightarrow$ Max Pooling ($2 \times 2$)
- **Block 3:** Three $3 \times 3$ conv layers (256 filters) $\rightarrow$ Max Pooling ($2 \times 2$)
- **Block 4:** Three $3 \times 3$ conv layers (512 filters) $\rightarrow$ Max Pooling ($2 \times 2$)
- **Block 5:** Three $3 \times 3$ conv layers (512 filters) $\rightarrow$ Max Pooling ($2 \times 2$)
- **Classifier:** Flattened feature maps $\rightarrow$ Fully Connected (4096) $\rightarrow$ Fully Connected (4096) $\rightarrow$ [[Softmax Function|Softmax]] (1000 classes).

## Legacy and Characteristics

- **The Heavyweight Champion:** VGG has a massive footprint. VGG-16 contains roughly **138 million parameters**, the vast majority of which live in the dense fully connected layers at the end. This makes it heavy to store and slow to train.
- **The Universal Feature Extractor:** Because of its straightforward hierarchy, VGG's intermediate convolutional layers are still widely used today as a robust feature extractor for style transfer, object detection backbones, and perceptual loss functions in generative models.