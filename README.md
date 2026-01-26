
---
# Unsupervised Industrial Anomaly Detection on Bearing Vibration Data

## Overview

This repository presents a reproducible and industry-oriented study on unsupervised anomaly detection
for vibration-based bearing fault monitoring using the Case Western Reserve University (CWRU) dataset.

The central question addressed in **Experiment A** is:

**Do bearing faults become more detectable when the data representation changes
(time-domain → frequency-domain → combined), while keeping the anomaly detector fixed?**

Inspired by the paper *“Anomaly Detection Methods for Industrial Applications: A Comparative Study”*
(MDPI, Electronics, 2023), this work focuses on isolating the impact of **feature representation**
rather than benchmarking multiple detection algorithms.

The core hypothesis is that **time-domain features alone may be insufficient to separate all fault
conditions**, and that **frequency-domain and combined representations increase anomaly separability**
— observable through improved score distributions and higher ROC-AUC / PR-AUC — even when using
the same unsupervised detector.

---

## Experiment A — Impact of Feature Representation

### Research Question

Can the same unsupervised anomaly detector (Isolation Forest), trained exclusively on healthy data,
achieve substantially different performance depending solely on the feature representation of
vibration signals?

### Hypothesis

- Time-domain features alone may fail to clearly separate certain fault conditions, leading to
  overlapping anomaly score distributions.
- Frequency-domain features (FFT-based descriptors, spectral entropy, band energies) increase
  fault separability by capturing spectral energy redistribution induced by bearing faults.
- Combining time- and frequency-domain features results in a more compact and stable normal
  operating manifold, enabling higher anomaly detectability under conservative thresholds.

---

## Experimental Design

**Key design principles**
- Model trained exclusively on healthy data
- Group-aware splits (by signal/file) to prevent data leakage
- Identical model hyperparameters across all conditions
- Thresholds derived only from healthy validation data

---

## Pipeline Summary

1. **Data ingestion and validation**
   - Raw vibration signals from the CWRU dataset
   - Semantic and statistical validation of healthy vs faulty conditions

2. **Windowing**
   - Sliding windows (2048 samples, 50% overlap)
   - Window-level sanity checks and signal statistics

3. **Feature engineering**
   - **A — Time-domain:** RMS, kurtosis, skewness, crest factor
   - **B — Frequency-domain:** spectral centroid, bandwidth, entropy, band energies
   - **C — Combined:** time + frequency features

4. **Unsupervised modeling**
   - Isolation Forest trained on healthy windows only
   - Feature scaling fitted exclusively on healthy training data

5. **Evaluation**
   - Threshold-free metrics (ROC-AUC, PR-AUC)
   - Percentile-based thresholds (p99, p99.5)
   - Precision, recall, and F1-score under operational constraints

---

## Key Findings

- Time-domain features provide a strong baseline but exhibit recall degradation under conservative
  thresholds.
- Frequency-domain features substantially improve anomaly ranking by capturing spectral energy
  redistribution caused by bearing faults.
- The combined feature representation delivers the most robust operational performance, maintaining
  **precision, recall, and F1-score above 0.99** even under strict thresholds (p99.5).
- Near-perfect AUC values are not indicative of overfitting, but instead reflect intrinsic
  separability introduced by physically meaningful feature representations.

---

## Conclusion

Experiment A directly addressed the initial research question of whether anomaly detectability
improves when the feature representation is changed while keeping the detector fixed.
The results confirm the initial hypothesis: time-domain features alone are insufficient to robustly
separate all fault conditions, whereas frequency-domain and combined representations significantly
increase anomaly separability.

By combining energetic and spectral descriptors, the anomaly detector operates under strict
false-positive control without sacrificing fault detectability. These findings align with and
extend recent comparative studies in the literature, reinforcing the central role of feature
engineering in industrial anomaly detection systems.

---

## Practical Relevance

- Supports deployment-oriented decisions in predictive maintenance systems
- Enables stricter alarm policies without increasing the risk of missed faults
- Demonstrates that feature engineering can dominate anomaly detection performance over model choice


## Future Work

- Extension to additional experimental conditions (Experiments B and C)
- Sequential models (LSTM Autoencoders, Temporal CNNs)
- Sensitivity analysis on window size and sampling rate
- Validation on real industrial vibration datasets

---

## References

- Case Western Reserve University Bearing Data Center  
- *Anomaly Detection Methods for Industrial Applications: A Comparative Study*,  
  MDPI Electronics, 2023  
  https://www.mdpi.com/2079-9292/12/18/3971

---
