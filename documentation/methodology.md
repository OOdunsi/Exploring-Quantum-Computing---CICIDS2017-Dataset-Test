# Methodology Notes

## 1. Why the improved CIC-IDS2017 release is used

Peer-reviewed analyses of the original CICIDS2017 identified issues involving flow construction, feature extraction, and labeling. The improved release is used to reduce the risk that known artifacts drive the baseline results.

The exact release, source files, SHA-256 hashes, preprocessing choices, and treatment of attempted attacks are recorded before model training.

## 2. Initial task

Binary classification:
- benign = 0
- malicious = 1

Original multiclass labels are retained in metadata for later analysis.

## 3. Classical baseline partitioning

Initial design:
- 70% training
- 15% validation
- 15% held-out test

The split is stratified by the binary target and uses a fixed seed. This is an initial methodology, not an immutable rule; it may be changed later if temporal structure or leakage risk justifies another validation design.

## 4. Classical dataset size

The notebook supports the full cleaned dataset but defaults to a documented stratified cap of 300,000 observations to keep a first run practical. Set `CLASSICAL_MAX_ROWS = None` for the full cleaned release.

## 5. Quantum-comparison subset

The future quantum-kernel experiment should not use the full multi-million-row dataset. After the classical split is created, a bounded subset is selected independently within train, validation, and test partitions.

Default starter target:
- 700 quantum-comparison training rows
- 150 validation rows
- 150 held-out test rows

The exact size may be changed after computational-feasibility testing.

## 6. Fair comparison

Future quantum results should be compared against classical models trained and evaluated on the same bounded observations, reduced feature representation, and partition boundaries. This reduced-sample classical comparison is separate from the larger classical baseline.

## 7. Real-time feasibility

This baseline does not demonstrate real-time quantum threat detection. Later stages should measure preprocessing time, inference time, state-encoding overhead, simulation or circuit execution time, sampling requirements, hardware/cloud queue delay where relevant, and end-to-end latency. “Real-time feasibility” is therefore a measured research question, not a pre-established capability.
