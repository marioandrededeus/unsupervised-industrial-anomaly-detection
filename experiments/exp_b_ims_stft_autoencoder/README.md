# Experiment B — STFT-based Autoencoder on IMS Bearing Dataset

## Overview

This experiment extends the previous study (Experiment A) by investigating how **time–frequency representations**
impact anomaly detection performance in **run-to-failure bearing data**.

While Experiment A demonstrated that frequency-domain features improve anomaly detectability compared to pure
time-domain features, Experiment B focuses on **Short-Time Fourier Transform (STFT)** combined with an
unsupervised **Convolutional Autoencoder (AE)** to jointly preserve:

- sensitivity to **recent temporal changes**
- interpretability in the **frequency domain**

The study uses the **IMS Bearing Dataset (NASA / University of Cincinnati)**, a widely adopted benchmark
for degradation and failure analysis in rotating machinery.

---

## Dataset — IMS Bearing

The IMS dataset consists of multiple run-to-failure experiments conducted under controlled conditions.
Each run captures vibration snapshots from multiple accelerometers until bearing failure occurs.

Important characteristics:

- No explicit fault labels per timestamp
- Each run is known to **end in a documented bearing failure**
- Different runs exhibit **distinct degradation modes**

### Known characteristics of the IMS runs

| Run       | Degradation mode | Energy level | Failure behavior |
|----------|-----------------|--------------|------------------|
| 1st_test | Gradual         | Low          | Intermittent, subtle |
| 2nd_test | Abrupt          | High         | Sudden, energetic |
| 3rd_test | Abrupt          | High         | Sudden, noisier |

These intrinsic differences strongly affect anomaly detectability, independently of the model used.

---

## Objective

The central objective of Experiment B is to evaluate whether a **STFT-based representation**
enables unsupervised models to better capture degradation patterns across different failure modes,
compared to static frequency or pure time-domain approaches.

---

## Experimental Design

- STFT computed on raw vibration snapshots
- Time–frequency patches extracted from STFT magnitude
- Convolutional Autoencoder trained **exclusively on early-life (healthy) data**
- Reconstruction error used as anomaly score
- Patch-level scores aggregated into snapshot-level scores
- Thresholds derived from early-life score distribution (p99 / p99.5)

---

## Key Observations

### 1st_test — Gradual degradation

- Smoothed anomaly score exhibits **clear upward drift** over the lifecycle
- Multiple **intermittent raw-score bursts** appear after ~25% of life
- Smoothed score does **not cross strict p99 threshold**
- Indicates **weak but physically meaningful degradation signals**
- Conservative thresholds may delay detection for gradual failure modes

### 2nd_test and 3rd_test — Abrupt failures

- Anomaly score remains stable during most of the lifecycle
- Score **explodes near the end of the run**, consistent with documented failure
- STFT + AE captures abrupt spectral changes effectively
- Zoomed-in plots confirm limited early warning for these failure modes

---

## Interpretation

Experiment B highlights that:

- **STFT offers a practical compromise** between time and frequency domains
- Abrupt failures are highly detectable, but often offer limited anticipation
- Gradual failures produce weak, intermittent precursors rather than sustained alarms
- A single global threshold is not optimal for all degradation modes

These findings reinforce that **detectability and anticipation depend more on failure physics than on model complexity**.

---

## Conclusion

Experiment B confirms that while time–frequency representations such as STFT significantly improve anomaly
detectability compared to static representations, they do not eliminate the fundamental limitations imposed
by the degradation mode itself.

The results support a nuanced conclusion:

> There is no universally optimal representation — the effectiveness of time, frequency, or time–frequency
> domains depends on how the fault manifests in the physical system.

---

## Next Steps — Experiment C

As a natural continuation, **Experiment C** will investigate **envelope analysis** and modulation-based
techniques inspired by classical vibration diagnostics, following concepts presented in the
Tractian Academy training on vibration analysis.

The goal is to evaluate whether isolating the modulation component can improve detectability
for gradual and low-energy degradation scenarios such as the IMS 1st_test.

---

## References

- IMS Bearing Dataset — NASA / University of Cincinnati
- Case Western Reserve University Bearing Data Center
- IQUNET Blog — *Anomaly Detection in Vibration Signals (Part 2 & 3)*  
  https://iqunet.github.io/tutorials/blog/anomaly-detection-vibration-part2/
- Tractian Academy - https://academy.tractian.com/cursos/analise-de-vibracao-com-autodiagnostico-conceitos-e-aplicacoes
