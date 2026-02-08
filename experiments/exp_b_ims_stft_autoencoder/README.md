# Experiment B — IMS Bearings: STFT + Autoencoder

## Goal
Evaluate the "it depends" claim in vibration monitoring by using a time–frequency representation
(STFT) to combine sensitivity to transient events (time domain) with spectral signatures
(frequency domain). The Autoencoder projects the STFT representation into a single anomaly score
(reconstruction loss).

## Dataset
IMS Bearings (run-to-failure). Place data in:
`data/external/ims_bearings/`

## Output
- Anomaly score over time per run
- Operational thresholds (p99 / p99.5) fitted on early healthy windows
- Optional smoothing (rolling median / rolling quantiles)

## Notebook
- `notebooks/02_experiment_b_stft_autoencoder_ims.ipynb`
