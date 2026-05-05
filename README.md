#  Retinal Vascular AI: Attention-Gated Screening for Glaucoma

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-ee4c2c.svg)](https://pytorch.org/)


##  Project Overview
This repository contains a full-stack medical computer vision pipeline designed to automate the segmentation of retinal vasculature and the screening of **Glaucoma** using the **OCTA-500 dataset**[cite: 1]. By combining traditional physics (Fourier Analysis) with advanced Deep Learning (Attention U-Net), this project extracts critical clinical biomarkers to identify vascular loss—the primary indicator of early-stage Glaucoma[cite: 1].

##  Project Goals
1.  **Multi-Class Segmentation:** Automated tracing of Arteries, Veins, Capillaries, and the Foveal Avascular Zone (FAZ)[cite: 1].
2.  **3D Volumetric Reconstruction:** Visualizing blood flow depth across the Superficial, Intermediate, and Deep capillary plexuses[cite: 1, 2].
3.  **Automated Screening:** Classifying patients based on **Vessel Density** and **FAZ Area** metrics[cite: 1].
4.  **Clinical-Grade Optimization:** Transitioning from baseline U-Net performance toward the clinical standard (Dice $\ge$ 0.85) using Attention-Gating and Tversky Loss[cite: 1].

##  Technical Methodology

### 1. Physics-Based Analysis (FFT)
Before training, images undergo **2D Fourier Transform (FFT)** analysis to understand spatial frequency content[cite: 1].
*   **Low Frequencies:** Isolate background and major vessel trunks[cite: 1].
*   **Medium Frequencies:** Isolate the main vascular signal[cite: 1].
*   **High Frequencies:** Isolate tiny, hair-like capillaries[cite: 1].

### 2. AI Architecture: Attention U-Net
The project utilizes an upgraded **Attention U-Net** to improve segmentation precision for $1 \mu m$ capillaries[cite: 1].
*   **Attention Gates:** Dynamically filter noise from the skip connections, ensuring the decoder only reconstructs relevant vascular features[cite: 1].
*   **Multi-Head Output:** A single backbone simultaneously predicts four distinct clinical layers[cite: 1].

### 3. Optimization Strategy
*   **Loss Function:** A hybrid of Binary Cross Entropy and **Tversky Loss**[cite: 1].
*   **Clinical Weighting:** Set to $\alpha=0.3$ and $\beta=0.7$ to prioritize **Recall**, ensuring the AI minimizes "False Negatives" (missed vessels) critical for patient safety[cite: 1].

##  Results & Clinical Performance

### Model Accuracy
The Attention-Gated model achieved significant learning growth, moving from a baseline toward high-confidence predictions[cite: 1].
*   **Best Dice Score:** 0.6861 (60 Epochs)[cite: 1].
*   **Diagnostic Reliability:** Successfully identified 100% of high-risk cases in the test sample[cite: 1].

### Screening Report Sample
The AI generates objective data that matches doctor observations[cite: 1]:
| Patient ID | AI Vessel Density | Status | Dice Score |
| :--- | :--- | :--- | :--- |
| P_10001 | 11.7% | 🚨 Potential Glaucoma | 0.680 |
| P_10007 | 15.7% | 🚨 Potential Glaucoma | 0.740 |

##  Visualizations

### 2D Vascular Maps
Comparison between raw OCT-A data, enhanced CLAHE images, and AI-predicted overlays for Arteries (Red), Veins (Blue), and FAZ (Yellow)[cite: 1].

### 3D Blood Flow Volume
Interactive 3D volumes (generated via Plotly) allow clinicians to rotate and zoom into the retinal structure to observe vessel "diving" between layers[cite: 2, 3].

##  How to Run
1.  **Clone the repo:**
    ```bash
    git clone https://github.com/YourUsername/Retinal-Vascular-AI.git
    ```
2.  **Install dependencies:**
    ```bash
    pip install torch torchvision numpy opencv-python matplotlib plotly pandas scipy
    ```
3.  **Dataset:** Add the [OCTA-500 dataset](https://www.kaggle.com/datasets/paultimothymooney/octa500) to your input directory[cite: 1].
4.  **Execute:** Run the `octa500_full_project.ipynb` notebook end-to-end[cite: 1].

##  Future Roadmap
*   Scale training to **150+ epochs** to reach the 0.85 clinical-grade Dice Score target[cite: 1].
*   Implement **Vessel Tortuosity** measurement (detecting abnormal vessel curvature)[cite: 1].
*   Integrate a PDF generator for automated clinical diagnostic summaries.


---
**Disclaimer:** *This tool is for research purposes only and is not intended for final clinical diagnosis without the supervision of a licensed ophthalmologist.*
