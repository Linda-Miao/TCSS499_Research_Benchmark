# TCSS499 Research Benchmark
## Software-Engineering Benchmarks for Explainable Intrusion Detection in Autonomous Platforms

**Author:** Yanhong (Linda) Miao  
**Supervisor:** Dr. Damiano Torre  
**Institution:** University of Washington Tacoma — School of Engineering and Technology  
**Course:** TCSS 499 Independent Study (Winter & Spring 2026)

---

## Project Overview

This repository implements a benchmark framework that applies post-hoc Explainable AI (XAI) methods to machine learning-based Intrusion Detection Systems (IDS), evaluated using both **machine learning metrics** and **software engineering metrics**.

The framework addresses three gaps identified in the literature:
1. No standardized benchmark comparing SHAP, LIME, and Grad-CAM together
2. No XAI evaluation using software engineering metrics (maintainability, reproducibility, explanation clarity)
3. No XAI-based IDS evaluation targeting autonomous platforms (drones, ground robots, autonomous vehicles)

---

## Dataset

**CICIDS2017** (Canadian Institute for Cybersecurity)
- ~2.8 million records after preprocessing
- 80 network traffic features
- 13 attack categories: BENIGN, DDoS, DoS GoldenEye, DoS Hulk, DoS Slowhttptest, DoS slowloris, FTP-Patator, SSH-Patator, Bot, PortScan, Heartbleed, Infiltration, Web Attack
- 70/30 train/test split

> Note: Raw dataset files are excluded from this repo due to size. Download from [UNB CICIDS2017](https://www.unb.ca/cic/datasets/ids-2017.html).

---

## Models Implemented

| Model | Accuracy | Precision | Recall | F1-Score |
|---|---|---|---|---|
| Random Forest | 99.94% | 99.94% | 99.94% | 99.94% |
| 1D-CNN | 98.74% | 98.79% | 98.74% | 98.73% |
| Autoencoder (anomaly) | 85.28% | 69.09% | 45.61% | 54.95% |

**Key Finding:** SHAP identifies different top features per model architecture:
- Random Forest → **Destination Port** (most influential)
- 1D-CNN → **Bwd Packets/s** (most influential)

This divergence demonstrates that model architecture shapes XAI explanations — a critical insight for autonomous platform security.

---

## XAI Methods Applied

| Method | Type | Applied To |
|---|---|---|
| SHAP (KernelExplainer) | Global + Local | Random Forest, 1D-CNN |
| LIME (TabularExplainer) | Local | Random Forest, 1D-CNN |
| Grad-CAM / Permutation Importance | TBD | Pending |

---

## Repository Structure

```
TCSS499_Research_Benchmark/
├── data/
│   └── (data loading and preprocessing scripts)
├── notebooks/
│   ├── 01_preprocessing.ipynb
│   ├── 02_random_forest.ipynb
│   ├── 03_cnn_1d.ipynb
│   ├── 04_autoencoder.ipynb
│   ├── 05_shap_rf.ipynb
│   ├── 06_shap_cnn.ipynb
│   ├── 07_lime_rf.ipynb
│   └── 08_lime_cnn.ipynb
├── results/
│   ├── rf_results.json
│   ├── cnn_results.json
│   ├── ae_results.json
│   ├── shap_global.png
│   ├── shap_cnn_global.png
│   ├── lime_results.json
│   └── ae_reconstruction_error.png
├── .gitignore
└── README.md
```

> Large model files (`.npy`, `.joblib`, `.keras`) are excluded via `.gitignore`.

---

## Evaluation Metrics

**ML Metrics:** Accuracy, Precision, Recall, F1-Score

**Software Engineering Metrics (novel contribution):**
- Maintainability — how easy is the XAI code to update?
- Integration Effort — how easy is it to add to existing IDS systems?
- Explanation Clarity — how understandable are the XAI outputs?
- Reproducibility — can others replicate the exact results?

---

## Environment Setup

```bash
# Create conda environment (Python 3.9 required for TensorFlow compatibility)
conda create -n cnn_env python=3.9
conda activate cnn_env

# Install dependencies
pip install tensorflow scikit-learn shap lime pandas numpy matplotlib joblib
```

---

## Related Work

This benchmark builds on and extends:
- Arreche et al. (2024) — E-XAI framework (SHAP + LIME, no Grad-CAM, no SE metrics)
- Patil et al. (2022) — LIME on CICIDS2017 (no SHAP or Grad-CAM comparison)
- Uysal & Kose (2024) — SHAP + LIME on CICIDS2017 (no autonomous platform focus)

See the full comparison table in the research paper (in progress).

---

## Acknowledgements

This research is conducted under the supervision of Dr. Damiano Torre as part of TCSS 499 Independent Study at the University of Washington Tacoma. Funded through UW Workday student research position.
