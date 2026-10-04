# Research Progress Log

**Researcher:** Ololade R. Odunsi  
**Proposed Endeavor:** Exploring Quantum Computing for Threat Detection and Intelligence on Cloud and On-Premise Infrastructure in Real Time

## Project Commencement

**Date:** October 3, 2026

I commenced the implementation phase of the proposed research on October 3, 2026, by establishing a version-controlled GitHub research repository for the initial classical machine-learning baseline.

The initial experimental stage uses the improved/corrected CICIDS2017 intrusion-detection dataset. This stage is intended to establish reproducible classical reference models before subsequent bounded quantum-machine-learning experiments are attempted.

Initial implementation activities include:

- establishing the repository structure and research documentation;
- documenting the selected dataset and its provenance;
- preparing the preprocessing methodology;
- defining an approximate 70% training, 15% validation, and 15% held-out testing methodology;
- preparing Support Vector Machine and Random Forest baseline models;
- establishing evaluation metrics including accuracy, precision, recall, F1 score, false-positive rate, ROC-AUC, training time, and inference time; and
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

Documented the improved/corrected CICIDS2017 dataset selected for the initial experimental phase.

The dataset documentation identifies:

- the original CICIDS2017 dataset;
- the improved/corrected release selected for this research;
- the research sources associated with the corrected release;
- the local storage location for the dataset;
- the decision not to redistribute the raw CSV files through the public GitHub repository; and
- the use of file-level provenance records and SHA-256 checksums.

The raw dataset files are maintained locally and excluded from Git version control.

Local dataset files were successfully identified and validated, and file-level SHA-256 provenance records were generated to support reproducibility and identification of the exact dataset files used during experimentation.

**Status:** Dataset documentation and initial file-level provenance validation completed.

---

### October 3, 2026 — Dataset Validation and Preprocessing 

Performed the initial validation, inspection, and preprocessing assessment of the improved/corrected CIC-IDS2017 dataset.

Five CSV files were successfully loaded into the research environment.

The combined raw dataset contained:

- **2,099,976 observations;**
- **93 columns;** and
- traffic collected across five source files: `monday.csv`, `tuesday.csv`, `wednesday.csv`, `thursday.csv`, and `friday.csv`.

The dataset inspection confirmed the presence of the expected `Label` and `Attempted Category` fields.

Original attack-family labels and attempted-category values were preserved before constructing the binary classification target.

#### Attempted-Flow Inspection

The improved dataset contained **11,979 records** identified as attempted attack flows.

Attempted-flow labels included categories such as:

- Botnet - Attempted;
- DoS Slowhttptest - Attempted;
- DoS Slowloris - Attempted;
- Web Attack - Brute Force - Attempted;
- Web Attack - XSS - Attempted;
- DoS Hulk - Attempted;
- DoS GoldenEye - Attempted;
- Infiltration - Attempted;
- SSH-Patator - Attempted;
- FTP-Patator - Attempted; and
- Web Attack - SQL Injection - Attempted.

For the primary binary-classification baseline, attempted flows were assigned to the benign class while their original attack labels and attempted-category codes were preserved for auditability and later sensitivity analysis.

The resulting binary target was defined as:

- `0` = benign traffic and attempted attack flows;
- `1` = successful malicious attack traffic.

The resulting target distribution was:

- **1,594,545 benign/attempted observations;**
- **505,431 malicious observations.**

#### Leakage-Aware Feature Preparation

A leakage-aware numeric feature matrix was constructed by excluding direct labels, internal research metadata, obvious identifiers, and fields that could directly or indirectly reveal the classification target.

Excluded fields included:

- Label;
- Attempted Category;
- Flow ID;
- Source Internet Protocol address;
- Destination Internet Protocol address;
- Timestamp;
- Internal row identifiers;
- Source-file metadata;
- Preserved original-label fields;
- Binary-target fields; and
- Attempted-flow helper variables.

After these exclusions, the numeric feature matrix contained:

- 2,099,976 observations;
- 85 candidate numeric features.

No feature column consisted entirely of missing values.

### **Missing-Value Assessment**

The full feature matrix contained only 10 missing feature values across five observations.

The missing values occurred in:

- Flow Bytes/s; and
- Flow Packets/s.

These values were not manually imputed at this stage. Missing-value treatment will be performed within the model preprocessing pipeline using statistics learned exclusively from the training partition.

### **Duplicate and Label-Conflict Assessment**
The duplicate audit identified:

- six observations involved in exact feature/target duplicate pairs; and
- three redundant duplicate observations beyond the first occurrence.

A separate conflicting-label assessment found zero identical feature sets associated with different binary target labels.

The three redundant duplicate observations were removed before creation of the working classical dataset.

The resulting cleaned dataset contained:

- 2,099,973 observations;

- 85 candidate model features.

**Status**: Initial dataset validation, binary-target construction, leakage-aware feature preparation, missing-value assessment, and duplicate assessment completed.

### ***October 3, 2026 — Initial Source-File and Attack-Distribution Audit 

Conducted an initial source-file audit to determine how benign and malicious observations are distributed across the five CIC-IDS2017 collection files.

The full dataset contained:

- friday.csv: 547,557 observations;
- wednesday.csv: 496,641 observations;
- monday.csv: 371,624 observations;
- thursday.csv: 362,076 observations; and
- tuesday.csv: 322,078 observations.

The audit confirmed that malicious traffic is not uniformly distributed across collection files.

In particular:

- monday.csv contained 371,624 benign observations and no malicious observations;
- friday.csv contained 292,611 benign observations and 254,946 malicious observations;
- wednesday.csv contained 324,996 benign observations and 171,645 malicious observations;
- thursday.csv contained 290,169 benign observations and 71,907 malicious observations; and
- tuesday.csv contained 315,145 benign observations and 6,933 malicious observations.

This finding confirms that collection day and attack family composition must be considered when interpreting later model performance. The primary classical baseline will therefore use stratified random partitioning, while a separate source-file or collection-day sensitivity analysis may later be performed.

**Status**: Initial full-dataset source-file distribution audit completed.

### October 3, 2026 — Initial Classical Working Sample Preparation 

Created a computationally bounded classical working sample from the cleaned CIC-IDS2017 dataset for the initial classical model-development phase.

The full cleaned feature matrix contained:

- 2,099,973 observations;
- 85 candidate numeric features.

To support a computationally manageable starter experiment while validating the end-to-end classical machine-learning pipeline, a reproducible stratified sample of 300,000 observations was selected using a fixed random seed of 42.

The working classical dataset contained:

- 227,795 benign/attempted observations;
- 72,205 malicious observations.

The corresponding class proportions were:

- 75.9317% benign/attempted;
- 24.0683% malicious.

The stratified sampling procedure therefore preserved the approximate benign-versus-malicious class distribution of the larger cleaned dataset.

The 300,000-observation sample is intended as an initial computationally bounded classical starter run and does not replace the larger cleaned dataset, which remains available for subsequent expanded classical evaluation.

**Status**: Completed.

### October 3, 2026 — Reproducible Classical Data Partitioning 

Created reproducible stratified training, validation, and held-out test partitions from the 300,000-observation classical working sample.

The split used a fixed random seed of 42 and preserved the benign-versus-malicious class distribution.

The resulting partitions were:

- Training: 210,000 observations (70%);
- Validation: 45,000 observations (15%);
- Held-out test: 45,000 observations (15%).

The malicious-class rates were:

- Training: 24.0686%;
- Validation: 24.0689%;
- Held-out test: 24.0667%.

The nearly identical malicious-class rates across all three partitions confirmed that the stratification procedure preserved the class composition of the working classical dataset.

A post-partition missing-value check found:

- Training: 2 missing feature values;
- Validation: 0 missing feature values;
- Held-out test: 0 missing feature values.

The two missing training values will be handled through the preprocessing pipeline using imputation statistics learned from the training partition only.

**Status**: Reproducible 70/15/15 partitioning completed.

### October 3, 2026 — Partition-Level Source-File Distribution Audit 

Conducted a second source-file audit after creation of the training, validation, and held-out test partitions.

The purpose of this audit was to determine whether any one of the five CICIDS2017 source files had become disproportionately concentrated in a particular partition.

The observed source-file proportions were:

- friday.csv (Training - 25.9771%; Validation - 26.2267%; Held-Out Test - 25.6956%)
- wednesday.csv (Training - 23.6224%; Validation - 23.6067%; Held-Out Test - 23.4800%)
- monday.csv (Training - 17.5995%; Validation - 17.5578%; Held-Out Test - 17.8133%)
- thursday.csv (Training - 17.2795%; Validation - 17.2200%; Held-Out Test - 17.4689%)
- tuesday.csv (Training - 15.5214%; Validation - 15.3889%; Held-Out Test - 15.5422%)


The source-file proportions remained closely aligned across the training, validation, and held-out test partitions.

This indicates that the stratified random partitioning procedure did not materially concentrate any individual source file within one partition.

Because malicious traffic is not uniformly distributed across collection files, this balanced source-file representation strengthens the initial classical baseline while not eliminating the need for later source-file or collection-day sensitivity analysis.

The source-file distribution results were saved as a reproducible project artifact.

Generated artifact:

- results/source_file_distribution.csv

**Status**: Completed.

### October 3, 2026 — Classical Support Vector Machine Baseline

Completed the initial Linear Support Vector Machine baseline using the reproducible 300,000-observation classical starter sample.

The model was trained using the previously established 210,000-observation training partition. Preprocessing was implemented within a machine-learning pipeline using median imputation for missing values and feature standardization. Both preprocessing operations were fitted using the training partition only so that validation and held-out test information did not influence model fitting.

The trained model was evaluated using the separate 45,000-observation validation partition.

The initial validation results were:

- **Accuracy:** 99.1844%;
- **Precision:** 97.5809%;
- **Recall:** 99.0675%;
- **F1 score:** 98.3186%;
- **False-positive rate:** 0.7785%;
- **ROC-AUC:** 0.9988;
- **Training time:** approximately 69.82 seconds; and
- **Validation inference time:** approximately 0.145 seconds.

The validation confusion matrix contained:

- **33,903 true negatives;**
- **266 false positives;**
- **101 false negatives; and**
- **10,730 true positives.**

These results indicate strong initial discrimination between benign and malicious traffic within the stratified validation partition. However, the results are treated as an initial benchmark result and are not interpreted as evidence of equivalent performance on unseen operational traffic. Earlier dataset analysis demonstrated differences in malicious-traffic composition across CIC-IDS2017 collection files, so later source-file or collection-day sensitivity analysis will be used to further assess model generalization and potential benchmark-specific effects.

The held-out test partition has not yet been used for model evaluation.

**Generated artifacts:**

- results/svm_validation_results.csv
- results/svm_validation_confusion_matrix.png

**Status:** Initial Linear Support Vector Machine training and validation completed; held-out test evaluation deferred until the classical modeling methodology is finalized.

### October 3, 2026 — Random Forest Baseline

Completed the initial Random Forest classical baseline using the same reproducible training and validation partitions used for the Linear Support Vector Machine experiment.

The Random Forest was trained using the 210,000-observation training partition. Median imputation was incorporated into the preprocessing pipeline and fitted using training data only. The classifier used 300 decision trees, class-weight balancing by bootstrap sample, a fixed random seed of 42, and parallel processing.

The trained model was evaluated on the separate 45,000-observation validation partition.

The initial validation results were:

- **Accuracy:** 99.9822%;
- **Precision:** 99.9723%;
- **Recall:** 99.9538%;
- **F1 score:** 99.9631%;
- **False-positive rate:** approximately 0.0088%;
- **ROC-AUC:** approximately 1.0000;
- **Training time:** approximately 79.41 seconds; and
- **Validation inference time:** approximately 0.419 seconds.

The validation confusion matrix contained:

- **34,166 true negatives;**
- **3 false positives;**
- **5 false negatives; and**
- **10,826 true positives.**

The Random Forest therefore produced 8 classification errors among the 45,000 validation observations and outperformed the initial Linear Support Vector Machine baseline across the principal classification metrics.

These results are treated as a larger-sample classical reference rather than evidence of equivalent performance on unseen operational traffic. Because previous inspection showed substantial variation in attack composition across CICIDS2017 collection files, additional source-file or collection-day sensitivity analysis will be performed to assess whether the high validation performance is influenced by characteristics of the benchmark dataset.

The held-out test partition remains unused.

The current Linear SVM and Random Forest results are also not yet the direct like-for-like comparators for the future quantum-kernel experiment. A separate classical comparator will later be trained using the same bounded observations and reduced feature set used for quantum evaluation.

**Generated artifacts:**

- results/random_forest_validation_results.csv
- results/random_forest_validation_confusion_matrix.png
- results/classical_validation_comparison.csv

**Status:** Initial Random Forest training and validation completed; source-file sensitivity analysis and held-out testing remain pending.

### October 3, 2026 — Bounded Quantum-Comparison Dataset Preparation

Established the methodology for creating a smaller, reproducible sample for later quantum-machine-learning comparison.

The initial bounded sample is expected to contain approximately several hundred to a few thousand observations depending on simulator resource requirements.

An illustrative initial comparison sample may contain approximately:

- 700 training observations;
- 150 validation observations; and
- 150 held-out test observations.

The final sample size will be determined after classical baseline testing and initial computational-feasibility assessment.

The bounded sampling process will preserve the separation between training, validation, and held-out testing data.

**Status**: Methodology established; bounded sample has not yet been generated.

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

**Status**: Planned; feature-selection and same-sample comparison experiments pending.

### October 3, 2026 — Quantum Experimentation

Defined the future quantum-machine-learning phase of the project.

The initial planned quantum experiment will evaluate a quantum-kernel classification approach using a bounded sample and reduced feature representation.

Initial experiments are expected to use simulation environments before any physical quantum-hardware testing is considered.

No quantum experiment or quantum-performance result has been completed or claimed as of October 3, 2026.

**Status**: Future research phase; not yet commenced experimentally.

### Current Project Status as of October 3, 2026 

The research project has formally commenced and has progressed beyond repository and methodology setup into active dataset preparation and classical experimental implementation.

Completed activities include:

- creation of the GitHub research repository;
- establishment of the research-project structure;
- documentation of the selected improved/corrected CIC-IDS2017 dataset;
- creation of the experimental methodology;
- establishment of the research-progress log;
- validation of local improved CIC-IDS2017 files;
- generation of file-level SHA-256 provenance records;
- successful loading of five corrected CIC-IDS2017 CSV files;
- inspection of 2,099,976 raw observations across 93 columns;
- preservation of original attack labels and attempted-category codes;
- identification and documented treatment of 11,979 attempted attack flows;
- creation of the benign-versus-malicious binary classification target;
- construction of a leakage-aware numeric feature matrix containing 85 candidate features;
- assessment of missing values;
- duplicate and conflicting-label analysis;
- removal of three redundant duplicate observations;
- establishment of a cleaned dataset containing 2,099,973 observations;
- source-file and attack-distribution analysis;
- creation of a reproducible 300,000-observation classical working sample;
- creation of reproducible 70/15/15 training, validation, and held-out test partitions;
- verification that class proportions remained stable across partitions; and
- verification that source-file proportions remained closely aligned across training, validation, and held-out test partitions.

The next active experimental milestone is construction and training of the initial SVM baseline using training-only imputation and feature standardization, followed by validation-set evaluation.

The Random Forest baseline will follow using the same established data partitions.

No quantum-computing experimental result is claimed at this stage.
