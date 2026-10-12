---
tags:
  - ML/computer-vision
aliases:
  - striding
---
In [[Convolutional Neural Network]]s (CNNs), **stride** ($S$) refers to the step size by which the convolutional filter ([[Kernel Mathematics in CNNs|kernel]]) moves across the input matrix or feature map.

While the filter evaluates a local region, the stride determines how many pixels (or elements) the filter skips between successive applications, moving horizontally from left to right, and then stepping down vertically.

## How Stride Works

- **Stride of 1 ($S = 1$):** The filter shifts by one pixel at a time. This results in heavy overlap between adjacent receptive fields, preserving fine-grained spatial details and producing a feature map close in size to the input.
- **Stride of 2 or Greater ($S > 1$):** The filter skips pixels, moving two or more spaces at each step. This significantly reduces the overlap between adjacent filter applications and drastically shrinks the spatial dimensions of the output feature map.

## Key Effects and Purposes of Stride

1. **Spatial Downsampling:**
    
    Increasing the stride acts as a downsampling mechanism. Instead of relying solely on [[pooling]] layers (like Max Pooling) to reduce dimensionality, modern architectures often use convolutions with a stride of 2 to compress spatial resolution while learning spatial features simultaneously.
    
2. **Computational Efficiency:**
    
    By skipping steps, a higher stride reduces the total number of times the kernel is applied across the feature map. This lowers computational cost, memory usage, and the number of parameters in downstream layers.
    
3. **Faster Receptive Field Growth:**
    
    Using a higher stride allows the network to look at a broader global context faster as data moves deeper into the network, because each deeper layer's effective receptive field expands more rapidly relative to the input image.

## The Trade-off: Resolution vs Information Loss

- **Fine Detail Loss:** Higher strides discard intermediate pixel details. For tasks that require precise localization (such as semantic segmentation, depth estimation, or object detection), large strides can hurt performance unless paired with [[Skip Connections]] or upsampling decoders (like in U-Net architectures).
- **Grid Artifacts:** In some generative models or high-resolution tasks, poorly chosen strides can introduce checkerboard or grid artifacts in the output, which is why alternative layers or reflection padding are often preferred in those domains.

## Mathematical Impact

Stride directly dictates the output spatial dimension ($O$) in the convolution formula, sitting inversely in the denominator:

$$O = \left\lfloor \frac{I - K + 2P}{S} \right\rfloor + 1$$

_Where $I$ is input size, $K$ is kernel size, and $P$ is [[Padding]]._ Notice how a larger stride $S$ decreases the output size $O$.