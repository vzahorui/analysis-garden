---
tags:
  - ML/computer-vision
---
Object detection in [[Computer Vision Concepts|Computer Vision]] goes beyond basic image classification. While classification answers **what** is in an image, object detection answers **what is where**, simultaneously identifying multiple objects and localizing them using spatial coordinates.

## Core Output of Object Detection

Unlike a single class label, the output for an object detection model consists of three primary elements for every detected entity:

- **Bounding Box Coordinates:** Typically defined by center coordinates with width and height `(x, y, w, h)` or corner points `(x_min, y_min, x_max, y_max)`.
- **Class Label:** The category of the object (e.g., `car`, `pedestrian`, `traffic_sign`).
- **Confidence Score:** A probability value between 0 and 1 indicating the model's certainty that the bounding box contains the specified object.

## Architectural Paradigms: Two-Stage vs One-Stage

Modern deep learning detectors generally fall into two architectural families:

### Two-Stage Detectors (e.g., Faster R-CNN)

- **How it works:** These models decouple the problem into two distinct phases. First, a Region Proposal Network (RPN) scans the image to generate candidate bounding boxes where objects _might_ be located. Second, a classification and regression head refines those boxes and assigns class labels.
- **Characteristics:** Highly accurate and robust at detecting small or heavily occluded objects, but computationally heavier and slower. Ideal for applications where precision trumps real-time speed (e.g., medical imaging analysis).

### One-Stage Detectors (e.g., YOLO series, SSD)

- **How it works:** These models treat detection as a single regression and classification problem. They pass the image through a backbone network once and directly predict bounding boxes and class probabilities across dense feature maps in an end-to-end fashion.
- **Characteristics:** Blazing fast and optimized for real-time inference (often hundreds of frames per second), making them the standard choice for video analytics, robotics, and autonomous driving.

### Essential Supporting Mechanisms

Training and running an object detection model relies on several core algorithms:

- **[[Intersection over Union]] (IoU):** The foundational metric for measuring spatial overlap. It divides the area of overlap between the predicted bounding box and the ground-truth box by the area of their union. An IoU threshold (e.g., 0.5) determines whether a detection is considered a True Positive.
- **Anchor Boxes (or Priors):** Pre-defined boxes of specific scales and aspect ratios placed across the image grid. The network predicts offsets relative to these anchors rather than raw coordinates, stabilizing training. (Many modern architectures have shifted toward anchor-free designs that predict object center points and distances to boundaries directly).
- **[[Non-Maximum Suppression]] (NMS):** An essential post-processing step. Because detectors often output dozens of overlapping bounding boxes for a single object, NMS sorts predictions by confidence score, calculates pairwise IoUs, and suppresses redundant lower-scoring boxes that overlap heavily with the highest-scoring prediction.

### Evaluation Metrics

Performance is predominantly measured using **mAP ([[Mean Average Precision]])**, which evaluates the area under the Precision-Recall curve across all object classes at various IoU thresholds.