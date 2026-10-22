# Hands That Speak: Word-Level Pakistani Sign Language Translation Engine

[![GitHub Repository](https://img.shields.io/badge/GitHub-Hands--That--Speak-blue?logo=github)](https://github.com/WhatAimanWorks/Hands-That-Speak)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-EE4C2C?logo=pytorch)](https://pytorch.org/)
[![Flutter](https://img.shields.io/badge/Flutter-Mobile%20App-02569B?logo=flutter)](https://flutter.dev/)

---

## Executive Overview
**"Hands That Speak"** is an AI-powered word-level sign language translation framework engineered to bridge the communication gap between the Deaf community and the hearing world in Pakistan. The system processes isolated video clips, extracts spatiotemporal hand-joint and posture dynamics using modern **Vision Transformers (SignFormer, Swin Transformer, PGViT)**, and generates contextually coherent Urdu and English translation outputs via a fine-tuned **multilingual BERT (mBERT)** language model.

- **Author:** Aiman Manzoor
- **Institution:** Iqra University, Islamabad
- **Repository:** [WhatAimanWorks/Hands-That-Speak](https://github.com/WhatAimanWorks/Hands-That-Speak)

---

## 1. Problem Statement & Motivation
Sign language communication relies on fluid hand gestures, facial expressions, and upper-body movements. Existing assistive frameworks for Pakistani Sign Language (PSL) face critical limitations:

- **Static Gestures Only:** Most existing systems recognize isolated alphabets or static hand shapes rather than dynamic, word-level sign gestures.
- **Hardware Constraints:** Dependency on specialized depth sensors (e.g., Microsoft Kinect) prevents real-world deployment on everyday mobile smartphones.
- **Grammatical Misalignment:** Direct gesture mapping fails to capture Urdu syntax, vocabulary variants, and contextual flow.

---

## 2. System Architecture & End-to-End Pipeline
[Raw PSL Video (30 FPS)] ──► [Pre-processing & ROI (224x224)] ──► [Keypoint Extraction]
│
[Translated Text Output] ◄── [Contextual mBERT Engine] ◄── [Spatiotemporal Vision Transformer]

### A. Data Engineering & Augmentation Strategy
To overcome dataset scarcity in PSL, public benchmarks (WLPSL and Saad Butt Corpus) were augmented with volunteer-recorded word-level gesture sequences:
- **Spatial Augmentations:** Random cropping, 30° rotations, brightness/contrast shifts, color inversion, and greyscale conversions.
- **Temporal Augmentations:** Playback speed variations (slow/fast gesture execution).
- **Class-Wise Concatenation:** Applied iterative augmentation and retraining loops to balance class distributions and prevent majority-class bias.

### B. Spatiotemporal Visual Encoders
- **SignFormer:** Employs deformable self-attention to model spatial hand configurations alongside temporal gesture transitions simultaneously.
- **Swin Transformer (Swin Tiny):** Uses shifted-window local self-attention to capture spatial details with a low computational footprint, ensuring edge-device stability.
- **Pose-Guided Vision Transformer (PGViT):** Integrates keypoint pose vectors with visual features to resolve ambiguities between visually similar hand shapes.

### C. Contextual Translation Engine (mBERT)
Visual sign tokens predicted by the transformer backbones are passed into a fine-tuned Multilingual BERT (mBERT) model to convert discrete gesture tokens into syntactically correct, context-aware Urdu and English output text.

---

## 3. Empirical Results & Performance Benchmark

- **Translation Accuracy:** The proposed **SignFormer** model achieved a top **F1-Score of 0.903** and **90.28% Accuracy**, outperforming standard baseline architectures.
- **Real-Time Edge Execution:** **Swin Tiny** achieved inference latencies of **~180 ms per frame**, rendering it highly stable for real-world mobile execution.
- **Environmental Noise Invariance:** Greyscale frame conversion reduced background interference, yielding an average recognition accuracy of **86%** across diverse lighting conditions.

| Model Architecture | Accuracy (%) | Precision | Recall | F1-Score | Latency / Frame |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **SVFormer** | 84.50% | 0.850 | 0.820 | 0.835 | ~220 ms |
| **Swin Transformer** | 87.20% | 0.870 | 0.840 | 0.855 | ~310 ms |
| **Swin Tiny** | 81.78% | 0.827 | 0.818 | 0.818 | **~180 ms** |
| **SignFormer (Proposed)** | **90.28%** | **0.910** | **0.903** | **0.903** | **~200 ms** |

---

## 4. Mobile UI & Application Features
The system was deployed as a cross-platform mobile application built with Flutter, featuring:
1. **Real-Time Video Translation:** Supports live video capture via device camera or video file uploads for instant translation.
2. **Dual-Language Output:** Displays predicted gesture meanings in both English and Urdu (e.g., *"noisy / شور"*, *"alert / خبردار"*).
3. **Interactive Tutorial Module:** Includes a dictionary library of basic PSL tutorial clips (*Alert, Bread, Breakfast, Cheap, Chicken, College, Dangerous, Noisy, Surprise*) for practice and learning.

---

## 5. Academic & Industry Significance
This project highlights technical competence across:
- **Computer Vision & Deep Learning:** Implementation of state-of-the-art Spatiotemporal Vision Transformers and NLP alignment models.
- **Software Quality Assurance:** Comprehensive testing pipelines covering environment variations, background invariance, and latency optimization.
- **Social Impact:** Applied AI addressing accessibility and inclusion for underrepresented communities in developing nations.
