# Research Progress Log

**Researcher:** Ololade R. Odunsi  
**Proposed Endeavor:** Exploring Quantum Computing for Threat Detection and Intelligence on Cloud and On-Premise Infrastructure in Real Time

## Project Commencement

**Date:** October 3, 2026

I commenced the implementation phase of the proposed research on October 3, 2026, by establishing a version-controlled GitHub research repository for the initial classical machine-learning baseline.

The initial experimental stage uses the improved/corrected CIC-IDS2017 intrusion-detection dataset. This stage is intended to establish reproducible classical reference models before subsequent bounded quantum-machine-learning experiments are attempted.

Initial implementation activities include:

- establishing the repository structure and research documentation;
- documenting the selected dataset and its provenance;
- preparing the preprocessing methodology;
- defining an approximate 70-percent training, 15-percent validation, and 15-percent held-out testing methodology;
- preparing Support Vector Machine and Random Forest baseline models;
- establishing evaluation metrics including accuracy, precision, recall, F1 score, false-positive rate, Receiver Operating Characteristic Area Under the Curve, training time, and inference time; and
- preparing a bounded sampling methodology for future quantum-kernel comparison.

No quantum-computing experimental results are claimed at this stage. Quantum experimentation will follow only after the classical baseline and reduced-feature comparison methodology have been validated.

---

## Progress Entries

### October 3, 2026 — Repository and Methodology Setup

Created the version-controlled GitHub research repository and began organizing the project structure for the initial CIC-IDS2017 classical-machine-learning baseline.

Initial repository activities included:

- creating the project repository;
- establishing the dataset documentation structure;
- creating research-methodology documentation;
- creating a research-progress log;
- establishing the local directory for the improved/corrected CIC-IDS2017 dataset;
- preparing the repository structure for notebooks and experimental results; and
- documenting the intended progression from classical baselines to later bounded quantum-machine-learning experiments.

**Status:** Completed.

---

### October 3, 2026 — Dataset Documentation and Provenance Setup

Began documenting the improved/corrected CIC-IDS2017 dataset selected for the initial experimental phase.

The dataset documentation identifies:

- the original CIC-IDS2017 dataset;
- the improved/corrected release selected for this research;
- the research sources associated with the corrected release;
- the local storage location for the dataset;
- the decision not to redistribute the raw CSV files through the public GitHub repository; and
- the planned use of file-level provenance records and SHA-256 checksums.

The raw dataset files are maintained locally and excluded from Git version control.

**Status:** Initial documentation completed; file-level validation and checksum generation pending.

---

### October 3, 2026 — Dataset Validation and Preprocessing

The dataset-validation and preprocessing phase was established as the next implementation milestone.

Planned activities include:

- identifying the exact dataset files used;
- generating SHA-256 checksums;
- reviewing dataset dimensions and column names;
- identifying missing, infinite, duplicate, or unusable records;
- verifying benign and malicious class labels;
- preserving original attack-family labels;
- evaluating ambiguous or attempted-attack records;
- removing or controlling potential identifier and leakage-prone features;
- converting the initial target to binary benign-versus-malicious classification; and
- documenting all preprocessing decisions.

**Status:** Methodology established; experimental preprocessing not yet completed.

---

### October 3, 2026 — Classical Data Partitioning

Established the planned initial dataset-partitioning methodology.

The first classical experiments will use approximately:

- 70% training data;
- 15% validation data; and
- 15% held-out test data.

The initial split will use a documented random seed and stratification by the benign-versus-malicious target where methodologically appropriate.

Additional source-file and collection-day sensitivity analysis will be considered to evaluate potential dataset leakage or benchmark artifacts.

**Status:** Methodology established; partitioning execution pending.

---

### October 3, 2026 — Classical Support Vector Machine Baseline

Established the Support Vector Machine as one of the first classical reference models for the research.

The planned evaluation will include:

- accuracy;
- precision;
- recall;
- F1 score;
- false-positive rate;
- Receiver Operating Characteristic Area Under the Curve, where appropriate;
- training time; and
- inference time.

The resulting performance will form part of the classical reference against which later reduced-sample and quantum-machine-learning experiments may be interpreted.

**Status:** Planned; model training and results pending.

---

### October 3, 2026 — Random Forest Baseline

Established the Random Forest classifier as the second primary classical baseline.

The Random Forest model will use the same training, validation, and held-out test partitions used for the Support Vector Machine so that the two classical models can be compared under consistent experimental conditions.

**Status:** Planned; model training and results pending.

---

### October 3, 2026 — Bounded Quantum-Comparison Dataset Preparation

Established the methodology for creating a smaller, reproducible sample for later quantum-machine-learning comparison.

The initial bounded sample is expected to contain approximately several hundred to a few thousand observations depending on simulator resource requirements.

An illustrative initial comparison sample may contain approximately:

- 700 training observations;
- 150 validation observations; and
- 150 held-out test observations.

The final sample size will be determined after classical baseline testing and initial computational-feasibility assessment.

The bounded sampling process will preserve the separation between training, validation, and held-out testing data.

**Status:** Methodology established; bounded sample has not yet been generated.

---

### October 3, 2026 — Feature Reduction and Same-Sample Classical Comparison

Established the methodology for reducing the feature space before future quantum-machine-learning experiments.

Candidate approaches include:

- correlation analysis;
- mutual information;
- recursive feature elimination;
- Principal Component Analysis; and
- domain-informed feature selection.

Feature selection will be fitted using training data only.

Classical models will later be trained on the same bounded observations and reduced feature set intended for quantum evaluation so that the direct classical-versus-quantum comparison is performed under equivalent data conditions.

**Status:** Planned; feature-selection and same-sample comparison experiments pending.

---

### October 3, 2026 — Quantum Experimentation

Defined the future quantum-machine-learning phase of the project.

The initial planned quantum experiment will evaluate a quantum-kernel classification approach using a bounded sample and reduced feature representation.

Initial experiments are expected to use simulation environments before any physical quantum-hardware testing is considered.

No quantum experiment or quantum-performance result has been completed or claimed as of October 3, 2026.

**Status:** Future research phase; not yet commenced experimentally.

---

## Current Project Status as of October 3, 2026

The research project has formally commenced.

Completed foundational activities include:

- creation of the GitHub research repository;
- establishment of the research-project structure;
- documentation of the selected improved/corrected CIC-IDS2017 dataset;
- creation of the experimental methodology;
- establishment of the research-progress log; and
- definition of the staged experimental sequence.

The next implementation milestone is the **validation and preprocessing of the improved/corrected CIC-IDS2017 dataset**, followed by execution of the first classical Support Vector Machine and Random Forest baseline experiments.

No quantum-computing experimental result is claimed at this stage.
