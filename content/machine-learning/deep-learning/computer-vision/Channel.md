---
tags:
  - ML/computer-vision
---
In a [[Convolutional Neural Network]], a **channel** is the depth axis of an activation [[tensor]] (alongside height and width): stacked feature maps at the same spatial grid. Channels are **not** kernels. A [[Kernel Mathematics in CNNs|kernel]] (filter) is the learnable weight bank that **writes** one output feature map (one output channel). How that bank slides and shares weights is in [[Kernel Mathematics in CNNs]]; this note covers $C_{\mathrm{in}}$, $C_{\mathrm{out}}$, and tensor shape.

## Input Channels (Depth)

- **Raw Inputs:** An image typically has 3 channels for RGB (Red, Green, Blue) or 1 channel for grayscale.
- **Intermediate Inputs:** Deeper layers take as input channels the feature maps produced by the previous layer.
- **Filter Depth Matches $C_{\mathrm{in}}$:** Each [[Kernel Mathematics in CNNs|kernel]] is not only $k \times k$ spatially; with multi-channel input it is a volume $k \times k \times C_{\mathrm{in}}$. Depth must equal the number of input channels. An RGB example: a $3 \times 3$ filter is actually $3 \times 3 \times 3$.

## Output Channels (Feature Maps)

- **One Filter, One Map:** Each filter scans the input volume and collapses all $C_{\mathrm{in}}$ channels into a single 2D feature map (element-wise products over the spatial patch and every input channel, plus a bias). The multi-channel sum is written in [[Kernel Mathematics in CNNs#Sliding Window Dot Products and Feature Maps|Kernel Mathematics in CNNs]].
- **$C_{\mathrm{out}}$ Filters, $C_{\mathrm{out}}$ Channels:** A layer applies $C_{\mathrm{out}}$ distinct filters in parallel. Their maps stack along depth to form $C_{\mathrm{out}}$ **output channels** for the next layer. How many filters to use (early vs deep) is in [[Kernel Mathematics in CNNs#Number of Kernels|Kernel Mathematics in CNNs]].

## The Filter Volume

A convolution filter is a 3D [[Kernel Mathematics in CNNs|kernel]] of shape **$k_H \times k_W \times C_{\mathrm{in}}$**.

- **Rule:** Filter depth **must** match $C_{\mathrm{in}}$. If the input has 64 channels, every filter in that layer has depth 64.

### The Transformation Mechanics Step-by-Step

1. **The Sliding Window:** The 3D filter slides over the spatial dimensions ($H$, $W$) of the input, stopping at each location $(x, y)$. Spatial slide details: [[Kernel Mathematics in CNNs]].
2. **Simultaneous Multi-Channel Multiplication:** At each stop, the filter overlays a local patch across **all** $C_{\mathrm{in}}$ channels and multiplies element-wise with those weights.
3. **Collapsing the Depth:** All products (spatial patch and every input channel) sum to one scalar; add a bias.
4. **Generating a Single Feature Map:** Sliding over the full $H \times W$ grid while collapsing channels yields one **2D feature map** ($H_{\mathrm{out}} \times W_{\mathrm{out}}$).

### Scaling to Multiple Output Channels

A layer applies **$C_{\mathrm{out}}$** distinct 3D filters in parallel.

- Each filter produces its own 2D feature map.
- Those maps stack along the channel axis.
- **Result:** shape goes from **$H \times W \times C_{\mathrm{in}}$** to **$H_{\mathrm{out}} \times W_{\mathrm{out}} \times C_{\mathrm{out}}$**.

## Tensor Shape Flow

CNN activations are 4D [[tensor]]s. Under the PyTorch convention:

- **[Batch Size, Channels, Height, Width]**

Example: a batch of 32 color images of size $32 \times 32$ is `[32, 3, 32, 32]`. A layer with 64 filters yields `[32, 64, 32, 32]` when [[Padding|padding]] keeps spatial size fixed.
