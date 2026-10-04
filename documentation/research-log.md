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

### October 3, 2026 - Dataset Validation and Preprocessing 

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

### October 3, 2026 - Initial Classical Working Sample Preparation 

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

### October 3, 2026 - Reproducible Classical Data Partitioning 

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

### October 3, 2026 - Partition-Level Source-File Distribution Audit 

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

October 3, 2026 — Source-File and Unseen-Attack-Family Sensitivity Analysis

Conducted a leave-one-source-file-out sensitivity analysis using only the combined training and validation development data. The held-out 45,000-observation test partition remained untouched.

For each experiment, observations from one CIC-IDS2017 source file were excluded from model training and used as the evaluation set. New Linear Support Vector Machine and Random Forest models were trained using the remaining source files.

The purpose of this analysis was to assess whether the strong performance observed under random stratified validation persisted when an entire collection source was absent from model training.

The analysis produced materially different results across source files.

Friday Holdout

When friday.csv was withheld from training:
- Linear SVM accuracy: 98.60%
- Linear SVM recall: 99.21%
- Linear SVM F1 score: 98.51%
- Random Forest accuracy: 99.23%
- Random Forest recall: 98.35%
- Random Forest F1 score: 99.17%

**Both models retained strong malicious-traffic detection performance on the held-out Friday source.**

Monday Holdout

The Monday source contained no successful malicious observations.

When monday.csv was withheld:
- Linear SVM accuracy: 99.54%
- Linear SVM false-positive rate: 0.46%
- Random Forest accuracy: approximately 100.00%
- Random Forest produced 1 false positive among 44,860 observations.

**Because the Monday evaluation partition contained only benign observations, malicious-class recall, F1 score, and ROC-AUC were not meaningful for this holdout.**

Thursday Holdout

When thursday.csv was withheld:
- Linear SVM accuracy: 91.20%
- Linear SVM recall: 57.68%
- Linear SVM F1 score: 72.11%
- Random Forest accuracy: 88.19%
- Random Forest recall: 40.20%
- Random Forest F1 score: 57.31%

**Both models demonstrated substantial degradation in malicious-traffic recall compared with the random stratified validation results.**

Tuesday Holdout

The Tuesday evaluation partition contained a relatively small malicious-class proportion of approximately 2.22%.

When tuesday.csv was withheld:
- Linear SVM accuracy: 97.24%
- Random Forest accuracy: 97.77%

**both models produced 0 true positives;**

**both models therefore had 0% malicious-class recall.**

The relatively high accuracy in this case was driven primarily by the strong class imbalance in the Tuesday source and did not indicate successful malicious-traffic detection.

Wednesday Holdout

When wednesday.csv was withheld:
- Linear SVM accuracy: 95.21%
- Linear SVM recall: 86.94%
- Linear SVM F1 score: 92.60%
- Random Forest accuracy: 65.56%
- Random Forest produced 0 true positives and 20,742 false negatives.

The Random Forest nevertheless produced a high ROC-AUC value of approximately 0.9960, indicating that score ranking and default classification-threshold behavior may require further investigation under source-level distribution shift.

## October 3, 2026 - Attack-Family Distribution and Training-Overlap Audit

Following the source-file sensitivity analysis, I examined how successful malicious attack families were distributed across the CIC-IDS2017 source files.

The audit showed that each successful attack family represented in the development data was confined to a single collection source.

Examples included:
- friday.csv: Botnet, DDoS, and Portscan;
- tuesday.csv: FTP-Patator and SSH-Patator;
- wednesday.csv: DoS GoldenEye, DoS Hulk, DoS Slowhttptest, DoS Slowloris, and Heartbleed;
- thursday.csv: Infiltration, Infiltration - Portscan, Web Attack - Brute Force, Web Attack - SQL Injection, and Web Attack - XSS.

A separate overlap audit confirmed that, for each held-out source file, the associated successful malicious attack families were not present in the remaining training-source files.

Accordingly, the leave-one-source-file-out experiment does not isolate collection-day effects alone. It simultaneously evaluates:

sensitivity to source-file or collection-day distribution shift; and

generalization to attack families absent from the training-source files.

This distinction is important for interpretation. The degraded performance observed on some held-out sources cannot be attributed solely to collection-day effects because source file and attack-family composition are confounded in the dataset.

The Friday results demonstrated that previously unseen attack families can still sometimes be recognized successfully based on malicious characteristics learned from other attack types, whereas Tuesday and Wednesday showed that such generalization was not consistent across attack families.

The current experiment is therefore described as a source-file and unseen-attack-family sensitivity analysis, rather than as evidence of zero-day attack detection.

Generated artifacts:
- results/source_file_sensitivity_class_audit.csv
- results/source_file_sensitivity_results.csv
- results/malicious_attack_family_by_source.csv
- results/heldout_attack_family_overlap_audit.csv

**Status:** Source-file holdout and attack-family overlap analysis completed; attack-family-level recall analysis and score-threshold diagnostics remain pending.

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

**Status:** Initial Linear SVM training and validation completed; held-out test evaluation deferred until the classical modeling methodology is finalized.

### October 3, 2026 - Attack-Family-Level Generalization Analysis

Performed an attack-family-level analysis of the leave-one-source-file-out sensitivity experiments to determine which successful malicious attack families could be detected when those families were absent from the model-training sources.

The results demonstrated substantial variation in cross-family generalization.

For the held-out Friday source, both models successfully detected most DDoS and Portscan observations despite neither attack family being represented in the training-source files. Linear SVM recall was approximately **99.97% for DDoS** and **99.22% for Portscan**, while Random Forest recall was approximately **98.83%** and **98.51%**, respectively. Neither model detected the 89 held-out Botnet observations.

For the held-out Thursday source, the largest malicious family was `Infiltration - Portscan`. Linear SVM detected approximately **57.78%** of these observations, while Random Forest detected approximately **40.28%**. Detection of the smaller Web Attack and Infiltration categories was limited; however, several of these categories contained very few observations and are therefore not treated as reliable standalone performance estimates.

For the held-out Tuesday source, neither model detected any of the 512 FTP-Patator or 367 SSH-Patator observations at the default classification threshold.

For the held-out Wednesday source, Linear SVM demonstrated substantially stronger unseen-family detection than Random Forest for several attack types. Linear SVM detected approximately **91.35% of DoS Hulk** observations and **56.83% of DoS GoldenEye** observations. Detection of DoS Slowhttptest and DoS Slowloris was approximately 2%, and the single Heartbleed observation was not detected. Random Forest produced zero true-positive detections across the Wednesday attack families at the default classification threshold.

These findings show that generalization to attack families absent from training is highly dependent on attack characteristics. Strong performance under random stratified validation did not guarantee equivalent performance when attack families were excluded from training.

The results also show that the Linear SVM, although weaker than Random Forest under the random stratified validation experiment, demonstrated stronger generalization to several unseen attack families during the source-file holdout analysis.

These experiments are not interpreted as zero-day attack detection because the evaluated attack types are known benchmark attack families. They instead measure model behavior when specific attack families are absent from the training-source files.

Attack categories represented by only a very small number of observations are not treated as reliable standalone performance estimates.

**Generated artifact:**

- results/unseen_attack_family_sensitivity_results.csv

**Status:** Attack-family-level sensitivity analysis completed; model-score and classification-threshold behavior remains under investigation.

### October 4, 2026 - Random Forest Score and Threshold Diagnostic

Investigated the Random Forest probability-score behavior for the held-out Tuesday and Wednesday source files after the source-file sensitivity analysis produced zero malicious detections at the default classification threshold despite high ROC-AUC values.

For the held-out Tuesday source, benign observations had a median malicious-class probability of approximately **0.0000**, while malicious observations had a median probability of approximately **0.1167**. The maximum malicious probability was approximately **0.2367**, meaning that none of the 879 malicious observations reached the default Random Forest classification threshold of 0.50.

For the held-out Wednesday source, benign observations again had a median malicious-class probability of approximately **0.0000**, while malicious observations had a median probability of approximately **0.0567**. The maximum malicious probability was approximately **0.4733**, which remained below the default 0.50 classification threshold.

A diagnostic threshold analysis showed that lowering the threshold would recover some malicious observations. At a threshold of 0.10, Random Forest recall increased to approximately **56.66% for Tuesday** and **37.76% for Wednesday**, while false-positive rates remained approximately **0.19%** and **0.12%**, respectively.

These lower-threshold results are treated strictly as diagnostic findings and are not used to modify the established baseline model. The original default classification threshold remains unchanged.

The results indicate that the Random Forest continued to assign higher malicious-class scores to many held-out attack observations than to benign observations, but its score calibration shifted substantially under source-file and unseen-attack-family distribution changes. This finding helps explain the combination of high ROC-AUC values and zero recall at the default threshold.

**Generated artifacts:**

- results/rf_source_holdout_score_distribution.csv
- results/rf_source_holdout_threshold_diagnostic.csv

**Status:** Random Forest score-distribution and threshold-behavior diagnostic completed. Baseline threshold retained unchanged.

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


### October 4, 2026 - Final Held-Out Classical Baseline Evaluation

Completed the final evaluation of the established Linear Support Vector Machine and Random Forest classical baselines using the previously untouched 45,000-observation held-out test partition.

The models were evaluated without additional retraining, threshold modification, or model tuning following review of the validation-stage results and source-file sensitivity analyses.

#### Linear Support Vector Machine (SVM)

The Linear SVM achieved:

- **Accuracy:** approximately 99.25%;
- **Precision:** approximately 97.76%;
- **Recall:** approximately 99.17%;
- **F1 score:** approximately 98.46%;
- **False-positive rate:** approximately 0.72%; and
- **ROC-AUC:** approximately 0.9989.

The held-out test confusion matrix contained:

- **33,924 true negatives;**
- **246 false positives;**
- **90 false negatives; and**
- **10,740 true positives.**

#### Random Forest

The Random Forest achieved:

- **Accuracy:** approximately 99.98%;
- **Precision:** approximately 99.98%;
- **Recall:** approximately 99.95%;
- **F1 score:** approximately 99.97%;
- **False-positive rate:** approximately 0.01%; and
- **ROC-AUC:** approximately 1.0000.

The held-out test confusion matrix contained:

- **34,168 true negatives;**
- **2 false positives;**
- **5 false negatives; and**
- **10,825 true positives.**

The final held-out results were closely aligned with the earlier stratified validation results, providing a consistent classical benchmark under the established random-partition methodology.

However, these results are interpreted together with the completed source-file and unseen-attack-family sensitivity analysis. That analysis demonstrated that performance under random stratified partitions does not necessarily translate to equivalent performance when entire source files and associated attack families are absent from training.

Accordingly, the near-perfect Random Forest performance on the random held-out test partition is treated as a benchmark reference rather than evidence of equivalent performance on unseen operational traffic.

The held-out test partition was evaluated only after the classical methodology, model configurations, and diagnostic analyses had been completed. No additional model tuning was performed using the test results.

**Generated artifact:**

- results/classical_baseline_results.csv

**Status:** Initial classical baseline phase completed. 


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

Subsequent source-file holdout testing showed that the near-perfect Random Forest performance observed under random stratified validation did not consistently generalize when entire collection sources and their associated attack families were absent from training. Random Forest retained strong performance on the held-out Friday source but showed materially lower malicious-class recall on Thursday and zero true-positive detections on the Tuesday and Wednesday holdouts. These findings reinforce the decision to treat the random-split result as a benchmark reference rather than as evidence of equivalent performance under unseen-source or unseen-attack-family conditions.



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

The research project has progressed from repository setup and classical baseline development into active model-validation and generalization analysis.

Completed activities now include:
- creation of the GitHub research repository and experimental documentation;
- validation and provenance documentation for the improved/corrected CIC-IDS2017 dataset;
- loading and inspection of approximately 2.1 million observations;
- construction of the binary benign-versus-malicious target;
- documented treatment of attempted attack flows;
- creation of a leakage-aware 85-feature numeric matrix;
- missing-value, duplicate, and conflicting-label assessment;
- creation of a reproducible 300,000-observation classical starter sample;
- creation of reproducible 70/15/15 training, validation, and held-out test partitions;
- source-file distribution auditing;
- completion of the Linear Support Vector Machine validation baseline;
- completion of the Random Forest validation baseline;
- completion of the initial classical model comparison;
- completion of leave-one-source-file-out sensitivity analysis;
- identification of substantial variation in cross-source malicious-detection performance;
- confirmation that successful malicious attack families are confined to individual source files within the development data; and
- confirmation that each held-out source-file experiment simultaneously introduces unseen attack families and source-level distribution shift.

The sensitivity analysis showed that the high performance observed under random stratified validation does not uniformly generalize to held-out source files. In particular, some source holdouts produced substantial reductions in malicious-class recall, while other holdouts, especially Friday, retained strong detection performance.

The next active analytical milestone is attack-family-level recall analysis and investigation of model score behavior under source-file holdout conditions. The final 45,000-observation test partition remains unused and will be evaluated only after the classical baseline methodology has been finalized.

No quantum-computing experimental result is claimed at this stage.
