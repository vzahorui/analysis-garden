---
tags:
  - ML/computer-vision
---
Introduced in 2015 by Olaf Ronneberger et al. for biomedical image segmentation, **U-Net** is a [[convolutional neural network]] designed to output pixel-level classifications (segmentation masks) rather than a single image-level label. While architectures like [[AlexNet]], [[VGG]], and [[ResNet]] classify _what_ is in an image, U-Net determines _exactly where_ every object, boundary, or structure is located.

## The "U" Shape: Encoder-Decoder Architecture

The network gets its name from its symmetrical, U-shaped topology, which divides the workflow into two complementary halves:

- **Contracting Path (Encoder):** A standard convolutional network that repeatedly applies [[Kernel Mathematics in CNNs|convolutions]] and max-[[pooling]], progressively reducing spatial dimensions while learning abstract, high-level contextual features.
- **Expanding Path (Decoder):** Upsamples the feature maps using transposed convolutions or bilinear interpolation, gradually restoring the original image resolution to build a dense output mask.

## Core Innovation: [[Skip Connections]] (Concatenation)

While [[ResNet]] uses skip connections via _addition_ to assist gradient flow, U-Net uses skip connections via **channel-wise concatenation**:

- **The Localization Problem:** Standard downsampling in the encoder discards fine-grained spatial and boundary details.
- **The Bridge:** Skip connections copy high-resolution feature maps directly from the encoder stages and concatenate them onto the corresponding upsampled layers in the decoder.
- **Sharp Boundaries:** This gives the decoder access to exact spatial coordinates, allowing it to generate crisp, highly accurate segmentation borders even with limited training data.

## Modern Legacy Beyond Medical Imaging

Although originally built to segment cellular structures in microscopy images, U-Net's influence extends far beyond medical diagnostics:

- It remains a foundational baseline for semantic segmentation tasks across autonomous driving and satellite imagery.
- Its architecture serves as the core denoising backbone for modern **Diffusion Models** (such as Stable Diffusion), where a modified U-Net predicts and removes noise iteratively to generate images from text prompts.