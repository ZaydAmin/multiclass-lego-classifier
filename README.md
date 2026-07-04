# 🧱 Multiclass Lego Classifier

![Python](https://img.shields.io/badge/Python-3.13.5-blue.svg?style=flat-square&logo=python&logoColor=white)
![Anaconda](https://img.shields.io/badge/Environment-Anaconda3-success.svg?style=flat-square&logo=anaconda&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-Image_Processing-green.svg?style=flat-square&logo=opencv&logoColor=white)
![Machine Learning](https://img.shields.io/badge/Model-Logistic_Regression-orange.svg?style=flat-square)

> **Overview** > A computer vision and machine learning pipeline designed to investigate the design of a multiclass classifier for four Lego piece types: a 2x1 brick, a 2x2 square brick, a 2x4 rectangular brick, and a circular piece. This project successfully builds a robust system capable of identifying single Lego pieces that may be shifted and rotated by arbitrary angles within a frame.

---

## 🚀 Project Stages

1. **Stage 1 (Baseline Classifier):** Implements a baseline by flattening cropped grayscale images into high-dimensional feature vectors and training a multiclass logistic regression model directly on raw pixel values.
2. **Stage 2 (Engineered Features):** Replaces raw pixels with a low-dimensional, 15-feature representation that captures geometric and shape information. This creates a space where a linear multiclass logistic regression model can effectively approximate decision boundaries for robust classification under spatial transformations.

---

## 🛠️ Environment & Prerequisites

This project was developed and tested using:
* **Python:** 3.13.5
* **Environment:** Anaconda3
* **Core Libraries:** OpenCV, Scikit-learn, NumPy

---

## ⚙️ Preprocessing Pipeline

Before feature extraction, a sequence of robust image processing tools prepares the image to yield the best results:

* 🌓 **Otsu Thresholding:** Automatically computes the optimal threshold by maximizing the in-between class variance, providing stable results under variable lighting.
* 🌫️ **Median Blur:** A non-linear filter that removes salt and pepper-like noise while preserving sharp edges and stud details.
* ⚖️ **Added Weights:** Adjusts brightness and contrast at the pixel level to enhance the visibility of the Lego piece.
* 🧹 **Morphology (Open & Close):** Removes small, isolated noise regions and fills gaps within the silhouette to create a clean contour.
* ⭕ **Hough Circular Transform:** Uses Canny edge detection and an accumulator matrix to detect circles based on center coordinates and radii thresholds.

---

## 🔬 Feature Extraction (15-D Vector)

The core of **Stage 2** relies on segmenting the piece into a 15-dimensional feature vector:

* 📐 **Geometric Descriptors:** Bounding box width and height, aspect ratio, contour area, relative area, and perimeter to distinguish long rectangles from square pieces.
* 🔘 **Circularity & Stud Counts:** Flags large circular regions and counts smaller circles (studs) to separate 2x1, 2x2, and 2x4 pieces.
* 🔄 **Hu Invariant Moments:** Calculates seven moments that describe the shape silhouette and are approximately invariant to translation, rotation, and scaling. To ensure these moments are reflection-invariant for mirrored images, the absolute values of the 5th, 6th, and 7th moments were calculated prior to log-normalization.

---

## 📊 Results & Performance

| Metric / Stage | Stage 1 (Raw Pixels) | Stage 2 (Engineered Features) |
| :--- | :--- | :--- |
| **Training Accuracy** | High (Ideal conditions) | **96.30%** |
| **Testing Accuracy** | **45.37%** | **90.74%** |
| **Limitations** | Fails heavily when pieces are rotated or shifted. | Sensitive to lighting variations and white/light blue pieces blending into the background. |

> **Conclusion:** Feature representation combined with multiclass logistic regression can reliably classify Lego pieces under translation and rotation. Geometric descriptors, stud counts, and Hu invariant moments captured vital shape information, highlighting the importance of feature design. 

---

## 👥 Authors
* **Zayd Amin**
