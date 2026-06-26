# Deep Learning and Classical Segmentation for Liver Tumor Detection from CT Images

A comparative medical image segmentation project that evaluates **classical K-Means segmentation** against a **deep learning U-Net architecture with a ResNet34 encoder** for automated **liver and tumor segmentation from CT scans**.

The project includes complete preprocessing of 3D CT volumes, conversion into annotated 2D slices, model training, hyperparameter tuning, and quantitative evaluation using medical segmentation metrics.

---

## Project Overview

Medical image segmentation is an important step in computer-aided diagnosis and treatment planning.

This project investigates two approaches for segmenting liver tumors from CT scans:

1. **Classical Computer Vision Approach**

   * K-Means clustering
   * Morphological post-processing
   * Hyperparameter tuning

2. **Deep Learning Approach**

   * U-Net architecture
   * ResNet34 encoder backbone
   * Dice + Cross Entropy optimization
   * Transfer learning and staged fine-tuning

The objective is to compare segmentation quality and inference performance across both approaches.

---

## Dataset

Dataset used:

**Liver Tumor Segmentation Dataset (LiTS)**

Source:
https://www.kaggle.com/datasets/andrewmvd/liver-tumor-segmentation

Dataset preparation included:

* Loading original 3D CT volumes
* Converting volumes into 2D slices
* Matching segmentation masks with CT scans
* Removing slices without meaningful annotations
* Filtering very small liver regions to reduce noise
* Train/validation split at volume level to avoid leakage

---

## Pipeline

### 1. Data Preprocessing

* Loaded CT volumes using `nibabel`
* Converted volumetric scans into 2D image slices
* Preserved segmentation alignment
* Removed low-information slices
* Organized data into train/validation directories

---

### 2. Baseline Segmentation — K-Means

Classical segmentation baseline implemented using:

* K-Means clustering
* Spatial intensity masking
* Morphological erosion
* Morphological dilation
* Closing operations

Hyperparameters were tuned through search over:

* Number of clusters
* Target cluster
* Gaussian masking strength
* Morphological iterations
* Kernel sizes

---

### 3. Deep Learning Segmentation — U-Net

Model configuration:

* Architecture: U-Net
* Encoder: ResNet34
* Encoder weights: ImageNet
* Input channels: 1 (grayscale CT)
* Output classes:

  * Background
  * Liver
  * Tumor

Training strategy:

Phase 1:

* Frozen encoder training

Phase 2:

* Full fine-tuning

Additional improvements:

* Mixed precision training
* Class-weighted loss
* Data augmentation
* Early stopping
* Learning rate scheduling

---

## Loss Function

Combined objective:

* Dice Loss
* Weighted Cross Entropy Loss

This combination improves performance under class imbalance common in medical datasets.

---

## Evaluation Metrics

Models were evaluated using:

* Dice Score
* Intersection over Union (IoU)
* Precision
* Recall
* Average inference time

Visual comparisons were also generated using:

* Ground truth masks
* Predicted masks
* Segmentation overlays
