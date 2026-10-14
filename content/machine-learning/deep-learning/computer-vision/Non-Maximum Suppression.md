---
tags:
  - ML/computer-vision
aliases:
  - NMS
---
**Non-Maximum Suppression (NMS)** is the essential post-processing algorithm in object [[detection]] that acts as the model's "cleanup crew."

When an object detector scans an image, it doesn't usually output just one neat box per object. Instead, it fires off dozens of overlapping bounding boxes around a single object, all with slightly different confidence scores. NMS takes that messy cluster and distills it down to **one clean, accurate bounding box per object**.

## Why is NMS Needed?

Most object detection models evaluate an image using dense grids or multiple anchor boxes. If a car sits in the middle of a frame, multiple nearby grid cells or anchor scales will recognize the car and predict their own bounding boxes for it. Without NMS, you would end up with a cluttered stack of overlapping boxes all pointing at the exact same car.

## How the NMS Algorithm Works

NMS operates through a systematic step-by-step filtering process:

1. **Confidence Thresholding:** First, the model discards any bounding box with a confidence score below a strict minimum threshold (e.g., score < 0.4). This removes obvious background noise.
2. **Sorting by Confidence:** The remaining boxes are sorted in descending order based on their confidence scores, putting the most confident prediction at the very top of the list.
3. **Iterative Selection and Suppression:**
    - **Select:** Take the box with the highest confidence score and keep it as a final, valid detection.
    - **Compare:** Calculate the **IoU** (Intersection over Union) between this top box and every remaining box in the list.
    - **Suppress:** If any other box overlaps with the top box by an IoU higher than the NMS threshold (e.g., IoU > 0.5), it is assumed to be detecting the exact same object and is **deleted (suppressed)**.
    - **Repeat:** Move to the next highest-scoring box among the survivors and repeat the process until all boxes are either kept or suppressed.

## Key Hyperparameters to Tune

When configuring NMS in a detection pipeline, two main thresholds control its behavior:
- **Score Threshold:** Controls how confident a box must be just to enter the NMS process.
- **[[Intersection over Union|IoU]] Threshold:** Controls how aggressive the suppression is. A lower IoU threshold (e.g., 0.4) means boxes are suppressed even with minimal overlap, while a higher threshold (e.g., 0.7) allows more overlapping boxes to survive (useful if objects are packed closely together, like a crowd of people).

## Modern Variations: Soft-NMS

Standard NMS is a "hard" filter, it completely deletes overlapping boxes. In crowded scenes (like a flock of birds or a dense traffic jam), hard NMS can accidentally delete a genuinely separate object that happens to overlap with another. To fix this, **Soft-NMS** reduces the confidence score of overlapping boxes gradually rather than deleting them outright, allowing occluded or closely packed objects to still be detected.