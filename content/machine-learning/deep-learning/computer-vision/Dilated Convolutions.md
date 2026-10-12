---
tags:
  - ML/computer-vision
aliases:
  - dilated (atrous) convolutions
  - atrous convolutions
---
**Dilated convolutions** (also known as _atrous convolutions_, derived from the French phrase _à trous_ meaning "with holes") are a specialized variant of the standard [[Kernel Mathematics in CNNs|convolution]] operation. Instead of processing adjacent pixels, a dilated convolution inserts spaces between the kernel weights, effectively expanding the field of view without increasing parameter count or sacrificing spatial resolution.

## How Dilated Convolutions Work

The operation is governed by a parameter called the **dilation rate ($r$)**, which determines the spacing between kernel elements:

- **$r = 1$:** Becomes a standard convolution, where kernel elements are adjacent.
- **$r = 2$:** Inserts a gap of one pixel between each kernel weight.
- **$r = n$:** Inserts $n - 1$ gaps between kernel elements.

For a kernel of size $k$ and dilation rate $r$, the **effective kernel size** ($k_{eff}$) expands according to the formula:

$$k_{eff} = k + (k - 1)(r - 1)$$

For example, a standard $3 \times 3$ kernel ($k=3$) with a dilation rate of $r = 2$ spans a $5 \times 5$ area while using only 9 active weights.

## Key Advantages

- **Exponentially Larger Receptive Field:** Standard convolutions rely on [[pooling]] layers or [[Stride|striding]] to increase the [[receptive field]], which permanently discards spatial resolution. Dilated convolutions grow the receptive field exponentially across stacked layers while maintaining full feature map resolution.
- **Parameter Efficiency:** They capture multi-scale, broad contextual information without adding computational overhead or increasing the number of trainable weights.

## Common Applications

- **Semantic Segmentation (e.g., DeepLab architectures):** Pixel-level tasks require fine-grained localization alongside broad scene context. Dilated convolutions allow models to maintain high-resolution feature maps while "seeing" a larger neighborhood.
- **Audio Generation (e.g., WaveNet):** Used in temporal sequence modeling to handle massive receptive fields across long audio samples efficiently.

## Limitations: The "Gridding" Artifact

When stacking multiple layers with the same large dilation rate, a **gridding effect** (or checkerboard artifact) can occur because the kernel skips intermediate pixels entirely, leading to patchy feature representation. This is typically resolved by choosing dilation rates that share no common factors (such as a sequence like $1, 2, 4$ or $1, 3, 5$).

## How Is It Different from [[Stride|Striding]]?

| **Feature**           | **Striding**                                              | **Dilated Convolution**                                                         |
| --------------------- | --------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **Core Mechanism**    | Skips pixels when **moving** the filter across the image. | Inserts gaps (**holes**) _inside_ the filter weights while moving step-by-step. |
| **Output Resolution** | **Decreases** (downsamples the feature map).              | **Maintains** (keeps output size equal to the input size).                      |
| **Primary Goal**      | Reduce computation and compress spatial dimensions.       | Expand the field of view without losing spatial detail.                         |
| **Information Flow**  | Discards intermediate pixels (similar to [[pooling]]).    | Processes every input pixel, but maps them across a wider footprint.            |
