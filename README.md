# CICIDS2017 Classical Baseline 

## Research context

This repository documents the initial classical-machine-learning phase of the proposed research endeavor:

**Exploring Quantum Computing for Threat Detection and Intelligence on Cloud and On-Premise Infrastructure in Real Time**

This repository does **not** claim that the full cloud/on-premise or real-time quantum portion of the endeavor has already been implemented. The purpose of this first phase is to create a reproducible classical baseline and a controlled, bounded sample that can later support fair quantum-kernel comparisons.


## Research Status Update — October 13, 2026

The research has progressed beyond initial classical baseline development
to a completed, bounded quantum-kernel machine-learning pilot.

The corrected classical workflow uses 82 numerical traffic features
after excluding additional identifier and port-related columns.
Group-aware validation and Tuesday source-file sensitivity testing
were performed to investigate duplicate-pattern leakage risks and
generalization to previously unseen attack families.

A four-feature quantum pilot was subsequently implemented using
100 training and 30 validation observations.

A classical RBF SVM and an Amazon Braket simulator-based quantum-kernel
SVM achieved identical validation accuracy (90%), recall (80%),
and F1 score (0.888889).

The quantum model achieved ROC-AUC of 0.951111 compared with
0.946667 for the classical model, but required substantially more
recorded processing time.

These results establish implementation feasibility, not quantum
computational advantage or operational real-time threat detection.

The corrected 82-feature workflow's final held-out test partition
has not been accessed.

Earlier sections documenting the original 85-feature experiments
are retained as historical research records.

See documentation/research-log.md for the dated experimental record
and results/ for supporting evidence.



## Dataset choice

This version is designed for the **improved/corrected CICIDS2017 dataset** released by the DistriNet research group after peer-reviewed work identified issues in the original CICIDS2017 data-generation and labeling pipeline.

Recommended source:
- Dataset documentation: https://intrusion-detection.distrinet-research.be/CNS2022/CICIDS2017.html
- Dataset directory: https://intrusion-detection.distrinet-research.be/CNS2022/Datasets/

Primary methodological references:
- G. Engelen, V. Rimmer, and W. Joosen, “Troubleshooting an Intrusion Detection Dataset: the CICIDS2017 Case Study,” IEEE Security and Privacy Workshops, 2021.
- L. Liu, G. Engelen, T. Lynar, D. Essam, and W. Joosen, “Error Prevalence in NIDS Datasets: A Case Study on CIC-IDS-2017 and CSE-CIC-IDS-2018,” IEEE CNS, 2022.

The raw dataset is intentionally **not** included in this repository.

## What this version changes (wrt the updated CICIDS2017 dataset)

1. Uses the corrected/improved dataset rather than the original MachineLearningCSV release.
2. Computes SHA-256 hashes for input CSV files and records dataset provenance.
3. Keeps the initial 70% training / 15% validation / 15% held-out test design for the classical baseline.
4. Supports either the full cleaned dataset or a transparent stratified cap if local compute is limited.
5. Creates a separate bounded quantum-comparison subset after the classical split.
6. Trains classical comparators on the same bounded observations and reduced features intended for later quantum experiments.
7. Uses training-only mutual-information feature ranking for a small future quantum feature set.
8. Audits source-file distribution and includes an optional source-file/day holdout sensitivity scaffold.

## Default starter sizes

Classical working sample: 300,000 rows by default for reproducible baseline development; the configuration can be set to use the full cleaned dataset when computational resources permit.
Future quantum-comparison subset:
- 700 training rows
- 150 validation rows
- 150 held-out test rows

(These are starter values, not fixed scientific requirements. The exact quantum sample size should be justified by pilot measurements of memory, execution time, and simulator feasibility.)

## Repository structure

cicids2017-classical-baseline-v2/
Exploring-Quantum-Computing---CICIDS2017-Dataset-Test/
├── .github/
├── .gitignore
├── README.md
├── requirements.txt
├── data/
│   └── README.md
├── documentation/
│   ├── methodology.md
│   └── research-log.md
├── notebooks/
│   └── 01_cicids2017_classical_baseline_v2.ipynb
└── results/
    ├── .gitkeep
    ├── attempted_flow_treatment_summary.csv
    ├── classical_baseline_results.csv
    ├── classical_partition_manifest.csv
    ├── classical_split_summary.csv
    ├── classical_starter_sample_manifest.csv
    ├── classical_validation_comparison.csv
    ├── dataset_file_provenance.csv
    ├── excluded_columns_leakage_control.csv
    ├── heldout_attack_family_overlap_audit.csv
    ├── malicious_attack_family_by_source.csv
    ├── random_forest_validation_results.csv
    ├── rf_source_holdout_score_distribution.csv
    ├── rf_source_holdout_threshold_diagnostic.csv
    ├── source_file_distribution.csv
    ├── source_file_sensitivity_class_audit.csv
    ├── source_file_sensitivity_results.csv
    ├── svm_validation_results.csv
    ├── unseen_attack_family_sensitivity_results.csv
    └── initial_numeric_feature_list.csv

## Research-integrity statement

Planned work is labeled as planned. Results should not be represented as completed until the notebook has actually been executed, reviewed, and committed with the resulting outputs. No quantum advantage, live real-time quantum inference, or production cloud/on-premise deployment is claimed in this baseline phase.
