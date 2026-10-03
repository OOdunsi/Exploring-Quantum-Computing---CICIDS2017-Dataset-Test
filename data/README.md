# Dataset Documentation

## Dataset Used

This project uses the improved/corrected CIC-IDS2017 dataset for the initial network-intrusion classification experiments.

The original CICIDS2017 dataset was developed by the Canadian Institute for Cybersecurity (CIC) at the University of New Brunswick (UNB) as a benchmark dataset for intrusion-detection research. It contains labeled benign and malicious network traffic and has been widely used for machine-learning-based cybersecurity research.

For this project, I intend to use the **improved CIC-IDS2017 release** distributed by the DistriNet Research Group in connection with subsequent peer-reviewed research examining labeling, flow-construction, and feature-extraction issues in the original dataset.

## Why the Improved Version Is Being Used

Peer-reviewed research identified several limitations in the original CICIDS2017 dataset, including issues involving:

- traffic and flow construction;
- feature extraction;
- ground-truth labeling; and
- potentially ambiguous or incorrectly labeled records.

Because this research project is intended to produce reproducible classical baselines that may later be compared with quantum-machine-learning methods, dataset integrity is important.

The improved/corrected release is therefore being used to reduce the likelihood that known artifacts in the original CICIDS2017 release materially influence the experimental results.

## Dataset Sources

**Original dataset provider:**  
Canadian Institute for Cybersecurity (CIC)  
University of New Brunswick (UNB)

**Original dataset:**  
CICIDS2017

**Improved/corrected release:**  
Improved CIC-IDS2017

**Improved release provider:**  
DistriNet Research Group

The improved dataset is distributed as part of the research associated with:

Liu, L., Engelen, G., Lynar, T., Essam, D., & Joosen, W.  
*Error Prevalence in NIDS Datasets: A Case Study on CIC-IDS-2017 and CSE-CIC-IDS-2018.*  
IEEE Conference on Communications and Network Security, 2022.

The corrected release builds upon earlier work by:

Engelen, G., Rimmer, V., & Joosen, W.  
*Troubleshooting an Intrusion Detection Dataset: the CICIDS2017 Case Study.*  
IEEE Security and Privacy Workshops, 2021.

## Local Dataset Location

The raw dataset is stored locally under:

```text
data/cicids2017_improved/
```

The raw CSV files are **not redistributed through this GitHub repository**.

The repository contains only the code, methodology, documentation, dataset-provenance records, experimental configuration, and research results required to reproduce the preprocessing and modeling workflow after an authorized user obtains the dataset from its source.

## Why the Raw Dataset Is Excluded From GitHub

The dataset files are excluded from version control for several reasons:

1. The raw files are large and are not necessary for reviewing the research code and methodology.
2. The dataset should be obtained from the original or improved-release provider so its provenance can be independently verified.
3. Excluding the raw files avoids unnecessary redistribution of third-party research data.
4. The project instead records the exact files used, together with file-level provenance information and cryptographic checksums where practical.

The `.gitignore` file prevents the local raw dataset directory and CSV files from being committed to the public repository.

## Dataset Provenance

Before model training, the project will document:

- dataset release used;
- source from which the dataset was obtained;
- download date;
- local filenames;
- SHA-256 file checksums where practical;
- original labels;
- preprocessing rules;
- treatment of missing, invalid, infinite, duplicate, attempted, or ambiguous records; and
- any sampling or filtering applied before model development.

The resulting provenance information will be stored separately from the raw dataset so another researcher can identify the exact data used without requiring the raw data to be redistributed through this repository.

## Initial Research Task

The first experimental task will be **binary network-intrusion classification**:

- `0` = benign traffic
- `1` = malicious traffic

The original attack labels will be preserved for later analysis and potential multiclass or unseen-threat experiments.

The initial classical baseline will use approximately:

- **70% training data**
- **15% validation data**
- **15% held-out testing data**

This allocation may be adjusted if necessary to address temporal structure, attack-class distribution, data leakage, or other methodological concerns. Any adjustment will be documented.

## Relationship to the Broader Research

The CIC-IDS2017 experiment represents the **initial controlled benchmark stage** of the broader research endeavor.

It is intended to establish reproducible classical machine-learning baselines using methods such as:

- Support Vector Machine;
- Random Forest; and
- potentially additional classical comparison models.

After the classical baseline has been validated, a smaller, reproducible subset of the data will be prepared for later quantum-kernel and Quantum Support Vector Machine experiments.

The full CIC-IDS2017 dataset is **not intended to be used directly in the initial quantum simulation experiments** because quantum-kernel resource requirements increase substantially with sample size.

Later phases may expand the methodology to additional datasets and telemetry representative of enterprise, cloud-hosted, and distributed environments.

## Research Integrity

This repository distinguishes between:

- completed work;
- work currently in progress; and
- planned future experiments.

The presence of dataset documentation or planned quantum-computing methodology in this repository does not represent a claim that quantum experiments have already been completed.

Experimental results will be added only after the corresponding code has been executed and the resulting outputs have been reviewed.