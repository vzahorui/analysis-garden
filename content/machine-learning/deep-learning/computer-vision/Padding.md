---
tags:
  - ML/computer-vision
---
In [[Convolutional Neural Network]]s (CNNs), **padding** refers to the practice of adding extra rows and columns of data, typically zeros, around the border of an input matrix or feature map before applying a [[Kernel Mathematics in CNNs|convolutional filter]].

### Why Padding is Necessary

Without padding, convolutional layers present two major architectural bottlenecks:

1. **Spatial Dimension Shrinking:** Every time a filter of size $K \times K$ passes over an input of size $N \times N$ (with a stride of 1), the output dimension shrinks to $(N - K + 1) \times (N - K + 1)$. In deep networks with dozens of layers, feature maps would rapidly shrink to $1 \times 1$ before extracting hierarchical representations.
2. **Edge Information Loss:** Pixels or features located in the center of an image are processed by the kernel multiple times, whereas pixels at the corners and edges are touched by the filter only once or twice. Consequently, the network largely ignores information at the boundaries.

### Common Types of Padding

- **Valid Padding ($P = 0$):**
    
    No padding is applied. The filter only operates where it fits entirely within the input. The spatial resolution decreases at every layer.
    
- **Same Padding:**
    
    Padding is added such that the output feature map has the **exact same spatial dimensions** as the input (when [[stride]] $S = 1$). For an odd kernel size $K$, the required padding on each side is typically calculated as:
    
    $$P = \frac{K - 1}{2}$$

- **Full Padding:**
    
    Padding is added such that every input pixel is treated with maximum weight by the filter. The filter is allowed to slide off the edges until it overlaps by only a single element, resulting in an output larger than the input.

- **Alternative Strategies (Reflect / Replicate):**
    
    While zero-padding is standard, tasks sensitive to sharp boundary artifacts (like generative models or high-resolution image processing) often use **reflection padding** (mirroring edge pixels) or **replication padding** (repeating edge pixels) instead of zeros to avoid introducing artificial edge gradients.

### Mathematical Formula

The spatial output dimension ($O$) of a convolutional layer given input size ($I$), kernel size ($K$), padding ($P$), and stride ($S$) is computed as:

$$O = \left\lfloor \frac{I - K + 2P}{S} \right\rfloor + 1$$
