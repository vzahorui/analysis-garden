---
tags:
  - ML/computer-vision
---
While object [[detection]] gives you bounding boxes, **image segmentation** takes [[Computer Vision Concepts|Computer Vision]] to the finest level of granularity: pixel-level understanding. Instead of approximating an object's location with a box, segmentation classifies every single pixel in an image, cutting out the exact contours of objects.

## The Spectrum of Segmentation Tasks

Image segmentation is generally broken down into three main categories, each increasing in complexity:

### Semantic Segmentation

- **What it does:** Classifies every pixel in the image into a predefined category, but **does not distinguish between separate instances** of the same class.
- **Example:** If there are three cars in a street scene, semantic segmentation colors all their pixels with the label `car`. Car A, Car B, and Car C merge into a single, unified foreground mask.

### Instance Segmentation

- **What it does:** Combines object [[detection]] with pixel-level masking. It not only identifies what category a pixel belongs to, but also separates distinct objects of the same class.
- **Example:** In the same street scene, instance segmentation labels the pixels for Car A as `car_1`, Car B as `car_2`, and Car C as `car_3`.

### Panoptic Segmentation

- **What it does:** The ultimate unification of computer vision tasks. It segments **everything** in the image. It handles "countable" objects using instance segmentation (people, cars, animals) and "amorphous background stuff" using semantic segmentation (sky, road, water, grass).

## Core Architectural Concepts

Unlike standard [[classification]] [[Convolutional Neural Network|CNN]]s that progressively shrink feature maps down to a single vector (losing spatial precision), segmentation models need to restore high-resolution spatial details.

- **Encoder-Decoder Architecture:** Most segmentation models use an encoder path (convolutional layers that downsample the image to extract high-level semantic features) paired with a decoder path (upsampling layers that restore the spatial dimensions to match the original image size).
- **[[Skip Connections]] (e.g., [[U-Net]]):** A critical innovation in architectures like U-Net. Because downsampling throws away fine spatial details (like exact edges), skip connections pass high-resolution feature maps directly from the encoder stages to the corresponding decoder stages, allowing the model to stitch precise boundaries back together.
- **Mask R-CNN (for Instance Segmentation):** This builds directly on top of Faster R-CNN. Alongside the bounding box and classification heads, it adds a small Fully Convolutional Network (FCN) branch that predicts a pixel mask for each proposed Region of Interest (RoI).

### Key Evaluation Metrics

- **[[Intersection over Union]] (IoU) / mIoU:** Just like detection, IoU measures the overlap between the predicted pixel mask and the ground-truth mask. **Mean IoU (mIoU)** averages this score across all classes and is the gold-standard metric for evaluating segmentation performance.
- **Dice Coefficient:** Another popular overlap metric heavily used in medical imaging (where precise boundary segmentation of tumors or organs is critical). It places a slightly higher emphasis on getting the exact intersection area right compared to standard IoU.