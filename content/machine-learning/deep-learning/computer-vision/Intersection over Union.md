---
tags:
  - ML/computer-vision
aliases:
  - IoU
  - Jaccard Index
---
**Intersection over Union (IoU)**, also known as the **Jaccard Index**, is the fundamental metric used in [[Computer Vision Concepts|Computer Vision]] to measure how well a predicted boundary matches a ground-truth boundary.

Whether you are evaluating bounding boxes in object detection or pixel masks in segmentation, IoU tells you precisely how much your model's prediction overlaps with reality.

## The Anatomy of IoU: Intersection vs. Union

To visualize how IoU works, imagine two shapes on a grid: the **Ground Truth** (the true location of the object) and the **Prediction** (what the model outputted).

- **Intersection (The Overlap):** The shared area where both the predicted shape and the ground-truth shape overlap.
- **Union (The Combined Area):** The total area covered by _both_ shapes combined. (Mathematically, this is the area of the prediction plus the area of the ground truth, minus the intersection so it isn't counted twice).

### The Formula

$$\text{IoU} = \frac{\text{Area of Intersection}}{\text{Area of Union}}$$

The resulting score is always a value between **0.0 and 1.0**:

- **0.0:** No overlap whatsoever (the model missed completely).
- **1.0:** Perfect overlap (the prediction and ground truth match identically).

## Why IoU Matters in Deep Learning

1. **Determining Correctness (True Positives):** In object detection, a model doesn't just need to find an object; it needs to localize it accurately. An object detection evaluation metric typically considers a prediction a "True Positive" only if its IoU crosses a defined threshold (e.g., an IoU of $\ge 0.5$).
2. **[[Non-Maximum Suppression]] (NMS):** Detectors often spit out multiple overlapping boxes for a single object. NMS uses pairwise IoU to compare these boxes; if two overlapping boxes have an IoU higher than a threshold (like $0.7$), the lower-confidence box is suppressed.
3. **[[Loss vs Metric|Loss]] Functions:** Standard regression losses (like [[Mean Squared Error]]) don't always align well with how we evaluate bounding boxes. Modern detectors use IoU-based loss functions (such as Generalized IoU or Complete IoU) to directly optimize box alignment, scale, and aspect ratio during training.