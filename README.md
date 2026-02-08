# Unsupervised Industrial Anomaly Detection (Vibration)

This repository is organized as a set of self-contained experiments focused on vibration-based
condition monitoring and unsupervised anomaly detection.

## Experiments

- **Experiment A (CWRU) — Feature Representation vs Detector**
  - Time-domain vs frequency-domain vs combined features
  - Healthy-only Isolation Forest baseline
  - Folder: `experiments/exp_a_cwru_iforest_features/`

- **Experiment B (IMS) — STFT + Autoencoder (Time–Frequency)**
  - Run-to-failure analysis using time–frequency representations
  - Autoencoder reconstruction loss → single anomaly score
  - Folder: `experiments/exp_b_ims_stft_autoencoder/`

- **Experiment C (IMS) — Envelope Demodulation**
  - Band-pass + Hilbert envelope to isolate modulation (carrier vs modulator)
  - Complementary to STFT for impact-driven fault signatures
  - Folder: `experiments/exp_c_ims_envelope/`

## Data
External datasets are not versioned. Place them under:
- `data/external/ims_bearings/`
