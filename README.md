---

# Industrial Anomaly Detection — Vibration Analysis

## Overview

This repository hosts an applied research project on **unsupervised anomaly detection for industrial vibration time-series data**.

Inspired by recent academic work in industrial anomaly detection, the project investigates **how feature representation and modeling choices influence fault detectability**, with a strong emphasis on **time-domain and frequency-domain signal analysis**.

Rather than benchmarking algorithms in isolation, the goal is to understand *why* and *when* faults become detectable in vibration data from real industrial systems.

---

## Motivation

In many industrial applications, known mechanical faults do not always appear as clear outliers in raw sensor data. This often leads to the incorrect conclusion that an anomaly detection algorithm has failed.

This project is built on a different hypothesis:

> **In industrial vibration analysis, the primary bottleneck for anomaly detection is often the data representation, not the detection algorithm itself.**

By systematically controlling the experimental setup, this repository explores how signal transformations—especially frequency-domain features—affect the ability of unsupervised models to detect bearing faults.

---

## Dataset

All experiments are conducted using the **Case Western Reserve University (CWRU) Bearing Dataset**, a widely used benchmark for vibration-based fault diagnosis.

* Signals: bearing vibration measurements
* Sampling rate: 12 kHz (baseline, aligned with most literature)
* Conditions: healthy and multiple bearing fault types
* Labels are used **only for evaluation**, not for training

---

## Research Philosophy

This project follows a **research-oriented engineering approach**:

* Prefer **controlled experiments** over complex pipelines
* Separate **representation effects** from **model effects**
* Favor **physical interpretability** of features
* Maintain **reproducibility and extensibility**

The repository is intentionally designed to evolve through clearly defined experimental stages.

---

## Experiments

### Experiment A — Feature Representation vs Fault Detectability (Current)

**Research question:**
How does feature representation affect the detectability of vibration-related faults when the anomaly detector is fixed?

**Design:**

* Fixed detector: Isolation Forest
* Training data: healthy samples only
* Variable: feature representation

**Feature sets:**

* **A — Time-domain features**
  Statistical descriptors (RMS, kurtosis, crest factor, etc.)
* **B — Frequency-domain features (FFT)**
  Band power, spectral centroid, bandwidth, entropy
* **C — Time + Frequency features**
  Concatenation of A and B

**Outcome:**
Quantitative comparison of anomaly score separability and detection performance under identical modeling conditions.

---

### Experiment B — Model Comparison Under Fixed Representation (Planned)

**Research question:**
How do different unsupervised modeling paradigms behave when the feature representation is held constant?

**Planned models:**

* Isolation Forest
* Dense Autoencoder
* LSTM / GRU Autoencoder

**Focus:**

* Structural outliers vs reconstruction-based anomalies
* Sensitivity to noise and degradation patterns
* Stability of anomaly scores

---

### Experiment C — Generalization Under Operating Regime Shift (Planned)

**Research question:**
How robust are anomaly detection models when trained under one operating condition and evaluated under another?

**Planned analysis:**

* Train on one load/speed condition
* Test on different operating regimes
* Measure false alarms, detection delay, and score drift

This experiment targets a key challenge in real industrial deployments.

---

## Repository Structure

```text
industrial-anomaly-detection/
├── experiments/
│   ├── experiment_A/
│   │   ├── README.md
│   │   └── notebook.ipynb
│   ├── experiment_B/
│   └── experiment_C/
├── src/
│   ├── data/
│   ├── windowing/
│   ├── features/
│   ├── models/
│   └── evaluation/
├── figures/
├── requirements.txt
└── README.md
```

Each experiment is self-contained while reusing shared components to ensure fair comparisons.

---

## Reproducibility

* All preprocessing and models are fitted using **healthy data only**
* Thresholds are calibrated on healthy validation data
* Experiments are versioned using Git tags (e.g., `v0.1-experiment-A`)
* Parameter choices are documented and aligned with existing literature

---

## Scope and Limitations

This repository focuses exclusively on **vibration-based anomaly detection**.
It does not aim to provide a production-ready monitoring system, but rather a **transparent and extensible research baseline** for understanding unsupervised anomaly detection in mechanical systems.

---

## Final Note

This project is intentionally incremental.

Each experiment builds on the previous one, refining the understanding of:

* what makes faults detectable,
* how signal representation shapes anomaly scores,
* and how different unsupervised models behave under realistic industrial constraints.

Future extensions will prioritize **interpretability, robustness, and industrial relevance** over model complexity.

---
