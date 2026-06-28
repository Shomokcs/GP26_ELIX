# ELIX: Integrating Explainable and Green AI Models for ECG Image Diagnosis

ELIX is an intelligent, energy-efficient, and transparent ECG diagnostic framework designed to automate the classification of ECG images into four distinct cardiac conditions with high accuracy and explainability.

## 🚀 Project Overview
Cardiovascular diseases are a leading global cause of death. While deep learning offers expert-level performance in automated ECG analysis, current models often lack interpretability and demand high computational power. **ELIX** addresses these challenges by combining **Green AI** (lightweight, quantized models) and **Explainable AI (XAI)** techniques to deliver a trustworthy and deployable clinical tool.

### 📊 Dataset & Target Classes
The framework utilizes ECG images from the **Mendeley Dataset (Cardiac Patients V2)**, preprocessed and categorized into four main classes:
- **N**: Normal Heartbeat
- **HB**: Abnormal Heartbeat
- **MI**: Myocardial Infarction
- **PMI**: History of Myocardial Infarction

---

## 🛠️ System Architecture & Model Pipeline

The repository is structured into three core components corresponding to the code files:

### 1. MobileNet
- **Role**: Lightweight CNN model used as part of the core diagnostic system.
- **Mechanism**: The ECG image is split into 4 spatial patches (resized to 224x224). MobileNetV3-Small extracts a 576-dimensional feature vector per patch, which are then concatenated into a 2304-dimensional vector for final classification.
- **Training**: Trained for 5 epochs with a learning rate of 0.0001.

### 2. Swin-Tiny 
- **Role**: Vision Transformer (ViT) model optimized for localized feature extraction from ECG patches.
- **Mechanism**: Processes each of the 4 patches independently to output logit vectors, which are then averaged for the final prediction.
- **Green AI Optimization**: Post-training **Dynamic Quantization** is applied to the linear layers, reducing the model size drastically from **110 MB to 28 MB**, significantly lowering inference latency and resource costs.
- **Training**: Trained for 10 epochs.

### 3. ELIX Main Fusion Framework
- **Role**: The main integration hub that orchestrates the ensemble and explainability.
- **Max Score Fusion**: Combines the probability scores of both MobileNetV3 and the quantized Swin-Tiny without requiring additional training. The final decision is driven by whichever model yields the highest probability score.
- **Decision Tracking & XAI**: 
  - Tracks which model made the decision (e.g., in testing: 64 decisions by MobileNetV3, 27 by Swin-Tiny).
  - **Grad-CAM** is dynamically triggered if MobileNetV3 drives the decision.
  - **Eigen-CAM** is triggered if Swin-Tiny drives the decision.
  - Generates diagnostic heatmaps highlighting the exact ECG regions that influenced the model's output.

---

## 📈 Key Results

- **Overall Framework Accuracy**: Achieved an outstanding **98.90% classification accuracy** across the four cardiac conditions.
- **Model Efficiency**: Reduced Swin-Tiny size by ~74.5% (110MB ➔ 28MB) via dynamic quantization, proving its readiness for resource-constrained clinical settings or telemedicine.

---
## 📺 Project Demo

[![Watch Demo](https://img.shields.io/badge/🎥_Watch_ELIX_Demo-Click_Here-blue?style=for-the-badge)](https://drive.google.com/drive/u/1/home)

## 🔧 Preprocessing Steps Included
1. **Boundary Cropping & Text Removal** (Noise reduction).
2. **Patch Generation** (Slicing into 4 distinct patches, resized to 224x224).
3. **Data Splitting** (80% Train / 10% Validation / 10% Test per class).
4. **Normalization** (Standardized using ImageNet parameters).

---

## 👥 Project Members
* Shomok Eidhah Althobaiti
* Boshra Sultan Alwgdani
* Sarah Hassan Alzahrani
* Wasan Abdulaziz Alkhaldi
* Enas Mohammed Alshehri
* Lujain Fayez Alotaibi
* Sara Abdullah Alosaimi
* Ghala Safir Aljuaid
* Rama Abdulmoain Altalhi
* Majd Daifallah Althaqfi
* Salwa Khaled Alkhamash

**Supervised by:** Dr. Nawal Al-Sufyani  
*Taif University*
