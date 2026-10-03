# CICIDS2017 Classical Baseline 

## Research context

This repository documents the initial classical-machine-learning phase of the proposed research endeavor:

**Exploring Quantum Computing for Threat Detection and Intelligence on Cloud and On-Premise Infrastructure in Real Time**

The purpose of this first phase is to create a reproducible classical baseline and a controlled, bounded sample that can later support fair quantum-kernel comparisons.

## Dataset choice

Version 2 is designed for the **improved/corrected CIC-IDS2017 dataset** released by the DistriNet research group after peer-reviewed work identified issues in the original CICIDS2017 data-generation and labeling pipeline.

Recommended source:
- Dataset documentation: https://intrusion-detection.distrinet-research.be/CNS2022/CICIDS2017.html
- Dataset directory: https://intrusion-detection.distrinet-research.be/CNS2022/Datasets/

Primary methodological references:
- G. Engelen, V. Rimmer, and W. Joosen, “Troubleshooting an Intrusion Detection Dataset: the CICIDS2017 Case Study,” IEEE Security and Privacy Workshops, 2021.
- L. Liu, G. Engelen, T. Lynar, D. Essam, and W. Joosen, “Error Prevalence in NIDS Datasets: A Case Study on CIC-IDS-2017 and CSE-CIC-IDS-2018,” IEEE CNS, 2022.

The raw dataset is intentionally **not** included in this repository.

## What Version 2 changes

1. Uses the corrected/improved dataset rather than the original MachineLearningCSV release.
2. Computes SHA-256 hashes for input CSV files and records dataset provenance.
3. Keeps the initial 70% training / 15% validation / 15% held-out test design for the classical baseline.
4. Supports either the full cleaned dataset or a transparent stratified cap if local compute is limited.
5. Creates a separate bounded quantum-comparison subset after the classical split.
6. Trains classical comparators on the same bounded observations and reduced features intended for later quantum experiments.
7. Uses training-only mutual-information feature ranking for a small future quantum feature set.
8. Audits source-file distribution and includes an optional source-file/day holdout sensitivity scaffold.

## Default starter sizes

Classical working set: up to 300,000 rows by default; set `CLASSICAL_MAX_ROWS = None` to use the full cleaned dataset.

Future quantum-comparison subset:
- 700 training rows
- 150 validation rows
- 150 held-out test rows


## Repository structure

```text
cicids2017-classical-baseline-v2/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── README.md
├── documentation/
│   └── methodology.md
├── notebooks/
│   └── 01_cicids2017_classical_baseline_v2.ipynb
└── results/
    └── .gitkeep
```


