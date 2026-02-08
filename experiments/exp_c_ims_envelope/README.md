# Experiment C — IMS Bearings: Envelope Demodulation

## Goal
Use envelope analysis (band-pass + Hilbert transform) to separate carrier vs modulating components,
making impact-driven fault signatures more detectable. This complements STFT by explicitly targeting
AM-like modulation patterns caused by repetitive impacts.

## Dataset
IMS Bearings (run-to-failure). Place data in:
`data/external/ims_bearings/`

## Output
- Envelope spectrum and envelope-based features over time
- Comparison against STFT-AE anomaly score and time/frequency baselines

## Notebook
- `notebooks/03_experiment_c_envelope_ims.ipynb`
