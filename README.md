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
1. No standardized benchmark comparing multiple XAI methods within a unified evaluation framework
2. No XAI evaluation using software engineering metrics (maintainability, reproducibility, explanation clarity)
3. No XAI-based IDS evaluation targeting autonomous platforms (drones, ground robots, autonomous vehicles)

---

## Current Status

| Phase | Dataset | Status |
|---|---|---|
| Phase 1 | CICIDS2017 | ✅ Complete |
| Phase 2 | UAV Attack Dataset | ⏳ Planned |
| Phase 3 | UAVCAN Intrusion Dataset | ⏳ Planned |
| Phase 4 | Cyber-Physical UAV Dataset | ⏳ Planned |

---

## Datasets

### Phase 1 — CICIDS2017 ✅
**Canadian Institute for Cybersecurity**
- ~2.8 million records after preprocessing
- 80 network traffic features
- 13 traffic classes: BENIGN, DDoS, DoS GoldenEye, DoS Hulk, DoS Slowhttptest, DoS slowloris, FTP-Patator, SSH-Patator, Bot, PortScan, Heartbleed, Infiltration, Web Attack
- 70/30 train/test split

> Download from [UNB CICIDS2017](https://www.unb.ca/cic/datasets/ids-2017.html)

### Phase 2-4 — UAV Datasets ⏳
- UAV Attack Dataset (Whelan et al. 2020) — GPS spoofing and MAVLink DoS
- UAVCAN Intrusion Dataset (Kim et al. 2022) — Flooding, Fuzzy, Replay attacks
- Cyber-Physical UAV Dataset (Hassler et al. 2023) — DoS, Replay, False Data Injection

---

## Models Implemented

| Model | Accuracy | Precision | Recall | F1-Score |
|---|---|---|---|---|
| Random Forest | 99.94% | 99.94% | 99.94% | 99.94% |
| 1D-CNN | 98.74% | 98.79% | 98.74% | 98.73% |
| Autoencoder (anomaly) | 85.28% | 69.09% | 45.61% | 54.95% |

---

## XAI Methods Applied

| Method | Type | RF | CNN | AE | Top Feature |
|---|---|---|---|---|---|
| SHAP | Global + Local | ✅ | ✅ | ✅ | Destination Port / Bwd Packets/s / FIN Flag Count |
| LIME | Local | ✅ | ✅ | ✅ | ECE Flag Count / Bwd IAT Max / RST Flag Count |
| Permutation Importance | Global | ✅ | ✅ | ✅ | Destination Port / Bwd Packets/s / Protocol |

---

## Key Findings (CICIDS2017)

**Finding 1 — Architecture drives XAI output:**
All three models identify completely different top features despite using the same dataset.

**Finding 2 — SHAP and Permutation agree on supervised models:**
Both confirm Destination Port (RF) and Bwd Packets/s (CNN) as top features.

**Finding 3 — Anomaly detection produces unstable explanations:**
All three XAI methods disagreed entirely on the Autoencoder top feature:
- SHAP → FIN Flag Count
- LIME → RST Flag Count  
- Permutation → Protocol

**Finding 4 — Grad-CAM excluded:**
Grad-CAM is incompatible with tabular network traffic data — this exclusion is itself a benchmark finding.

---

## Repository Structure