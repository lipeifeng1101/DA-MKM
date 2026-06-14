
---

# Deformation-Assisted Multiple Keypoints Matching (DA-MKM)

Official Implementation of
"Enhanced Finger Vein Recognition via Deformation-Aware Multi-Keypoint Matching"
(The Visual Computer 2026)

This repository provides the complete implementation of our novel DA-MKM framework, which achieves state-of-the-art performance on multiple finger vein recognition benchmarks through three key innovations:

* **A novel multiple keypoints representation strategy** extracting both extreme points and corner points (via SIFT and SuperPoint) to capture comprehensive vessel topology and local details, effectively bypassing error-prone vessel segmentation networks.
* **We propose a Deformation-Assisted Matching framework** that utilizes spatial displacement distances and rotation angles. By applying simulated one-class clustering, it accurately removes false keypoint pairings and evaluates the joint uniformity of posture changes.
* **We design a weighted score fusion strategy** that integrates valid matching pair counts with joint displacement uniformity metrics. This significantly enhances the discriminative power of the matching procedure, optimizing high-security criteria (such as FRR-at-0-FAR) for practical identity authentication systems.

### 📦 Repository Contents

| Directory | Contribution to Paper Research |
| --- | --- |
| `DA-MKM/extraction.py` | Keypoint extraction (SIFT baseline and SuperPoint model) |
| `DA-MKM/matching.py` | Two-way raw matching and false pairing removal logic |
| `DA-MKM/evaluate.py` | Overall evaluation and uniformity score calculation |
| `DA-MKM/utils.py` | Displacement feature extraction and parameter settings |
| `DA-MKM/pre-process/` | Image enhancement and IIC dataset preprocessing |

### 🛠️ Environment Setup

* Python 3.10+
* PyTorch 2.1.2+cu118 (for SuperPoint feature extraction)
* OpenCV / VLFeat (for SIFT feature extraction)
* NumPy 1.26.4

### 📥 Dataset Preparation

The experimental evaluation utilizes two benchmark biometric datasets:

**SDUMLA Dataset:** This multimodal biometric database contains 106 subjects' modalities (including finger vein images) captured under constrained laboratory conditions.
🔗 [https://time.sdu.edu.cn/kycg/gksjk.htm](https://time.sdu.edu.cn/kycg/gksjk.htm)

**HKPU Database:** The Hong Kong Polytechnic University's public dataset provides finger vein images from 156 volunteers, captured in multiple sessions.
🔗 [http://www4.comp.polyu.edu.hk/~csajaykr/fvdatabase.htm](http://www4.comp.polyu.edu.hk/~csajaykr/fvdatabase.htm)

### 🧩 Data pre-processing

The raw images of SDUMLA and HKPU can suffer from low contrast and non-uniform illumination. In order to get robust keypoint extraction results, we pre-processed the images before matching:

1. Pre-process the images using the intensity inhomogeneity correction (IIC)-based methods in `DA-MKM/pre-process`.
2. Save the processed images as the core dataset used for subsequent feature extraction.

### 🚀 Evaluation Execution

```bash
python evaluate.py 

```

Key hyperparameters from paper:

* **Bin number ($n$):** 70
* **Fusion ratio ($\alpha$):** 0.05

### 📊 Evaluation

Evaluation metrics implemented:

* Equal Error Rate (EER)
* False Reject Rate at zero False Accept Rate (FRR-at-0-FAR)
* False Accept Rate at zero False Reject Rate (FAR-at-0-FRR)
* Recognition Rate (RR) / Cumulative Match Characteristic (CMC)
