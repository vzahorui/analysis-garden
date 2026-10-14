---
tags:
  - ML
---
**Transfer learning** is a machine learning technique where a model developed for a task is reused as the starting point for a model on a second, related task.

Instead of training a model from scratch, which requires massive amounts of data, time, and computational power, transfer learning lets you leverage the patterns, features, and representations a model has already learned from a different domain.

For example, early layers of a [[neural network]] learn fundamental, universal features (like edges, curves, and textures in images, or basic grammar and syntax in text). Transfer learning reuses these foundational layers so the network can focus on learning task-specific nuances.

### Core Approaches to Transfer Learning

Depending on how similar your target task is to the original task, you generally choose between two main strategies:

- **Feature Extraction (Frozen Backbone):** You take a pre-trained model (like a [[convolutional neural network]] trained on ImageNet), "freeze" its feature-extraction layers so their weights don't change, and replace only the final classification layer (the "head") to match your new categories. The pre-trained network acts as a fixed feature extractor.
- **Fine-Tuning:** You take a pre-trained model and unfreeze some or all of its layers. You then train the entire network (or the later layers) on your new dataset using a very small learning rate. This allows the model to subtly adjust its existing weights to better fit your specific problem.

### Why Transfer Learning is Crucial

- **Data Efficiency:** You can achieve high accuracy even with a small dataset, making it ideal for specialized domains where data is scarce (e.g., medical imaging or rare language processing).
- **Reduced Training Time:** Training a deep model from scratch takes days or weeks on clusters of GPUs. Fine-tuning a pre-trained model often takes minutes or hours.
- **Higher Performance:** Models trained on massive benchmark datasets often generalize better than models trained from scratch on smaller datasets, reducing overfitting.

### Real-World Examples

- [[Computer Vision Concepts|Computer Vision]]: Taking a model pre-trained on **ImageNet** (millions of general photos of cats, cars, trees, etc.) and fine-tuning it to detect specific defects in manufacturing lines or classify chest X-rays.
- **Natural Language Processing ([[NLP Concepts|NLP]]):** Using pre-trained transformer models like **BERT** or **GPT**, which have learned the structure of human language from vast web corpora, and fine-tuning them for downstream tasks like sentiment analysis, legal document summarization, or chatbots.