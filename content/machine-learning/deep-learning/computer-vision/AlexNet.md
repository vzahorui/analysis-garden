---
tags:
  - ML/computer-vision
---
Introduced in 2012 by Alex Krizhevsky, Ilya Sutskever, and Geoffrey Hinton, **AlexNet** won the ImageNet Large Scale Visual Recognition Challenge by a massive margin. It effectively kicked off the modern [[Deep Learning Concepts|Deep Learning]] revolution, proving that deep [[convolutional neural network]]s could scale to handle massive, complex real-world image datasets.
## Core Innovations That Changed Deep Learning

AlexNet introduced several breakthrough techniques that became standard practices in deep learning:

- **[[ReLU]] Activation:** Replaced traditional saturating activations (like [[Sigmoid Function|sigmoid]] or [[Hyperbolic Tangent|tanh]]) with Rectified Linear Units, significantly accelerating training speed and mitigating the [[Saturation and Vanishing Gradient|vanishing gradient]] problem.
- **[[Dropout]] Regularization:** Introduced dropout in the fully connected layers to randomly zero out neurons during training, effectively preventing overfitting on large parameter spaces.
- **Dual-GPU Training:** Split the network across two NVIDIA GTX 580 GPUs because a single 3GB GPU at the time could not hold the entire model in memory.
- **Data [[Augmentation]]:** Expanded the training set dynamically using image translations, horizontal reflections, and intensity changes to pixel values.
- **Overlapping [[Pooling]]:** Used max-pooling layers with strides smaller than the filter dimensions to reduce spatial dimensions while retaining boundary context.

## Architectural Structure

AlexNet scaled up [[LeNet-5|LeNet]]'s foundational principles with a much deeper and wider topology. It processed a `224x224x3` RGB image through a sequence of layers:

- **Five Convolutional Layers:** Using large [[Kernel Mathematics in CNNs|filters]] early on (like `11x11` and `5x5`) to capture coarse visual patterns, followed by smaller `3x3` filters for deeper feature combination.
- **Three Fully Connected Layers:** Dense layers processing the flattened feature representations, ending with a 1000-way softmax layer to classify images into ImageNet's categories.

## Historical Impact

AlexNet demonstrated that raw computational power combined with hierarchical feature learning could drastically outperform hand-crafted computer vision features. It fundamentally shifted the AI research community from manual feature engineering to architectural engineering.