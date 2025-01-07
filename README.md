# IrisEyeRecognition
 
This repository contains the implementation of an iris recognition system using deep learning techniques. The primary objective of this project is not only to develop a biometric system but also to explore and learn image preprocessing methods and parameter tuning techniques in a systematic manner. This project focuses on the **CASIA-Thousand dataset** and aims to enhance understanding of how preprocessing techniques influence model performance.

---

## **Project Overview**

Iris recognition is a robust biometric identification method due to the unique and stable texture patterns of the human iris. This project explores the use of **Convolutional Neural Networks (CNNs)** in combination with advanced preprocessing methods to improve feature extraction and recognition accuracy.

The primary goal is **not achieving state-of-the-art scores** but to learn:
- The impact of preprocessing techniques.
- How parameter adjustments affect model behavior.
- Fundamentals of building and optimizing deep learning models.

---

## **Dataset**
- **Source**: CASIA-Thousand Dataset
- **Size**: 
  - 20,000 grayscale images
  - 2,000 unique classes
- **Resolution**: 640x480 pixels (resized to 150x150 pixels)
- **Format**: Grayscale, 8-bit depth

---

## **Preprocessing Techniques**

Preprocessing is critical in improving feature extraction and overall model performance. The following techniques were applied:

1. **Segmentation**: Isolates the iris region from the sclera and pupil using Gaussian blur and Circular Hough Transform.
2. **Center Cropping**: Removes redundant background while preserving discriminative features of the iris.
3. **CLAHE**: Contrast Limited Adaptive Histogram Equalization enhances subtle texture details.
4. **Gabor Filtering**: Highlights multi-directional textural features like ridges and furrows.
5. **Combination of CLAHE and Gabor Filtering**: Leverages both contrast enhancement and texture feature extraction.

---

## **CNN Architecture**

The proposed CNN is designed for efficient feature extraction and classification while minimizing overfitting. Key components include:

- **Input Layer**: Processes grayscale images of size 150x150x1.
- **Convolutional Layers**: Seven layers with filter sizes of 3x3 and 5x5, followed by:
  - Batch Normalization
  - Leaky ReLU activation
- **Pooling Layers**: Max-pooling for dimensionality reduction.
- **Gaussian Noise**: Adds noise (mean=0, std=0.1) to improve robustness.
- **Dropout Layers**: Applied progressively to prevent overfitting.
- **Dense Layers**: Two fully connected layers ending with a softmax classifier.

### **Optimization Techniques**
- **Optimizer**: Adam optimizer with an initial learning rate of 0.001.
- **Learning Rate Scheduler**: Reduces the learning rate when validation loss stagnates.
- **Early Stopping**: Stops training if validation loss doesn't improve for 10 consecutive epochs.
- **Loss Function**: Sparse Categorical Cross-Entropy.

---

## **Results and Analysis**

The performance of the system was analyzed based on test accuracy and Equal Error Rate (EER). Preprocessing techniques significantly impacted these metrics:

| **Preprocessing Method**       | **Test Accuracy (%)** | **EER Threshold** |
|--------------------------------|-----------------------|-------------------|
| Segmentation                   | 64.60                | 0.087            |
| Center Cropping                | 88.20                | 0.048            |
| CLAHE                          | 92.25                | 0.034            |
| Gabor Filtering                | **92.45**            | **0.023**        |
| CLAHE + Gabor Filtering        | 89.15                | 0.041            |