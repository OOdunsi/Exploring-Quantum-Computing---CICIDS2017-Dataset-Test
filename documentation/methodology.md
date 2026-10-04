# Research Methodology

## Project Title

**Exploring Quantum Computing for Threat Detection and Intelligence on Cloud and On-Premise Infrastructure in Real Time**

## 1. Purpose of This Methodology

This document describes the experimental methodology for the initial implementation phase of the research project.

The first stage of the research is designed to establish reproducible classical machine-learning baselines for cybersecurity threat detection before later quantum-machine-learning experiments are attempted.

The initial experiment focuses on binary network-intrusion classification using an improved/corrected version of the CIC-IDS2017 dataset.

The research will progress through the following general sequence:

1. validate and document the dataset;
2. clean and preprocess the data;
3. create reproducible training, validation, and testing partitions;
4. establish classical Support Vector Machine and Random Forest baselines;
5. evaluate potential data-leakage and benchmark-artifact concerns;
6. create a smaller, reproducible subset suitable for later quantum-machine-learning experiments;
7. reduce the feature space using training data only;
8. train classical models on the same bounded sample and reduced features intended for the quantum experiment;
9. perform later quantum-kernel experiments under equivalent data conditions;
10. compare predictive performance, computational requirements, latency, and operational feasibility.

The methodology is intentionally staged. Later phases will proceed only when earlier results provide a technically meaningful basis for expansion.

---

## 2. Research Status

The project is currently in the classical-baseline and experimental-preparation stage.

At this stage:

- the research repository has been established;
- the selected dataset and its provenance are being documented;
- data-preparation procedures are being implemented;
- classical Support Vector Machine and Random Forest baselines are being developed; and
- the methodology for future bounded quantum-machine-learning experiments is being prepared.

No completed quantum threat-detection experiment, quantum advantage, production deployment, or live real-time quantum detection capability is claimed at this stage.

---

## 3. Initial Research Question

The initial research question is:

> How effectively can reproducible classical machine-learning models distinguish benign from malicious network traffic in an improved CIC-IDS2017 benchmark, and what baseline performance and resource requirements should later quantum-machine-learning experiments be compared against?

The initial task is therefore a binary classification problem:

- `0` = benign network traffic
- `1` = malicious network traffic

The original attack-family labels will also be preserved for later analysis, including potential multiclass classification and unseen-threat generalization experiments.

---

## 4. Dataset Selection

### 4.1 Initial Dataset

The initial benchmark will use an **improved/corrected version of CIC-IDS2017**.

CIC-IDS2017 was originally developed by the Canadian Institute for Cybersecurity at the University of New Brunswick for intrusion-detection research.

Subsequent peer-reviewed research identified limitations in the original dataset involving areas such as:

- traffic and flow construction;
- feature extraction;
- ground-truth labeling; and
- ambiguous or incorrectly classified records.

For that reason, this project will use the improved/recreated CIC-IDS2017 release associated with subsequent research by the DistriNet Research Group rather than relying solely on the original machine-learning CSV release.

Dataset-source information is documented separately in:


data/README.md
```

---

## 5. Dataset Provenance and Integrity

Before model development, the project will record sufficient information to identify the exact data used in each experiment.

Where practical, the following information will be recorded:

- dataset release;
- source provider;
- download date;
- local filename;
- file size;
- SHA-256 checksum;
- original label definitions;
- preprocessing rules;
- handling of ambiguous or attempted-attack records;
- sampling procedures; and
- software versions used during preprocessing.

Raw dataset files will remain outside Git version control.

The GitHub repository will contain the research code, methodology, provenance manifests, model configurations, and results rather than redistributing the raw dataset.

---

## 6. Initial Data Inspection

Before training any model, the dataset will be inspected for data-quality issues.

The inspection process will include:

- identifying missing values;
- identifying infinite values;
- identifying invalid records;
- identifying duplicate records;
- identifying columns that are entirely empty or unusable;
- verifying the label column;
- reviewing the benign-versus-malicious class distribution;
- preserving the original attack labels;
- reviewing records identified as attempted attacks or otherwise ambiguous; and
- reviewing potential identifier or scenario-specific fields that could introduce information leakage.

**## 6.1. Treatment of Attempted Attack Flows:**
The improved CIC-IDS2017 release explicitly identifies flows associated with attempted attacks that did not necessarily exhibit the malicious activity of a successful attack.

For the primary binary-classification baseline, these attempted flows will be assigned to the benign class, consistent with the evaluation methodology reported by the researchers who produced the corrected dataset.

The original attack labels and attempted-category codes will be preserved so that this treatment remains auditable and may be evaluated separately through sensitivity analysis.

Any records removed or modified during cleaning will be documented.

The objective is not to alter the dataset to improve model performance, but to establish a transparent and reproducible preprocessing procedure..

The objective is not to alter the dataset to improve model performance, but to establish a transparent and reproducible preprocessing procedure.

---

## 7. Feature Preparation

Model features will be selected from numeric or appropriately encoded variables suitable for machine-learning analysis.

Direct identifiers and other fields likely to introduce artificial shortcuts will be excluded where appropriate.

Potential exclusions may include:

- flow identifiers;
- source Internet Protocol addresses;
- destination Internet Protocol addresses;
- timestamps;
- source-file metadata;
- labels;
- direct record identifiers; and
- other variables determined to create unacceptable information leakage.

Ports and other potentially scenario-specific variables may be evaluated through sensitivity analysis rather than automatically assumed to be valid predictors.

Infinite values will be replaced with missing values before imputation.

Missing numeric values may be imputed using statistics learned from the training partition only.

Feature standardization or normalization will be performed when required by the selected model.

---

## 8. Classical Training, Validation, and Test Partitions

The initial experimental design will use approximately:

- **70 percent training data**
- **15 percent validation data**
- **15 percent held-out test data**

The initial split will use a fixed random seed for reproducibility and will be stratified by the binary benign-versus-malicious target where methodologically appropriate.

The partitions will have separate purposes.

### Training Set

Used to:

- fit preprocessing transformations;
- train model parameters;
- calculate feature statistics; and
- perform feature-selection procedures.

### Validation Set

Used to:

- review model behavior;
- compare reasonable model configurations;
- identify implementation problems; and
- support methodological decisions without repeatedly examining the held-out test set.

### Held-Out Test Set

Used only after the principal model methodology has been established.

The held-out test set will not be repeatedly used for model tuning.

If later changes are made because of test-set results, those changes will be documented and a more appropriate confirmatory validation approach may be established.

---

## 9. Leakage and Source-File Analysis

A strong predictive result is not meaningful if the model is exploiting dataset artifacts rather than learning useful threat-related patterns.

For that reason, the project will evaluate potential leakage associated with:

- timestamps;
- source files;
- collection days;
- identifiers;
- attack schedules;
- feature-generation artifacts; and
- variables that may encode the label indirectly.

The distribution of source files across the training, validation, and test partitions will be recorded.

A secondary source-file or day-level sensitivity analysis may also be performed.

### Day-Level Holdout Caveat

Attack categories in CIC-IDS2017 are not uniformly distributed across all collection days.

As a result, holding out an entire day can simultaneously change:

- the time period;
- the source environment; and
- the attack-family composition of the test set.

Therefore, a day-level holdout result will not automatically be interpreted as a pure measure of temporal generalization.

Instead, it will be treated as a sensitivity test involving possible temporal, source-domain, and attack-composition changes.

---

## 10. Classical Baseline Models

The first classical models will be:

### 10.1 Support Vector Machine

A Support Vector Machine will establish one of the primary classical reference models.

For the initial large-data baseline, a computationally practical linear Support Vector Machine may be used.

The workflow may include:

1. training-set-based imputation;
2. feature standardization;
3. class weighting where appropriate;
4. model training;
5. validation evaluation; and
6. held-out test evaluation.

Later experiments may evaluate additional kernel-based classical Support Vector Machine configurations on smaller controlled datasets where computationally feasible.

### 10.2 Random Forest

A Random Forest classifier will provide a nonlinear tree-based classical baseline.

The model will be trained using the same training, validation, and test partitions used for the Support Vector Machine.

Class weighting or balanced sampling approaches may be used where necessary to account for class imbalance.

### 10.3 Additional Classical Models

Gradient boosting or another suitable classical model may be considered after the initial baseline pipeline is stable.

Additional models are optional and will not be added solely to improve reported performance.

---

## 11. Evaluation Metrics

Classical models will be evaluated using multiple metrics rather than accuracy alone.

Primary metrics will include:

- accuracy;
- precision;
- recall;
- F1 score;
- false-positive rate;
- Receiver Operating Characteristic Area Under the Curve, where appropriate;
- confusion-matrix results;
- training time; and
- inference time.

Operational considerations are important because a model that produces high predictive accuracy but excessive false positives, latency, or resource demands may have limited practical value in cybersecurity operations.

---

## 12. Larger Classical Baseline

The first classical experiment may use a large portion of the improved dataset or the full cleaned dataset where computational resources permit.

If local computational constraints require a row limit or stratified sample, the following will be documented:

- original number of rows;
- selected number of rows;
- sampling method;
- random seed;
- resulting class distribution; and
- reason for applying the limit.

This larger classical experiment will establish contextual reference performance.

It will **not** automatically serve as the direct comparator for later quantum-machine-learning experiments because quantum-kernel methods are expected to require substantially smaller sample sizes.

---

## 13. Bounded Sampling for Future Quantum Experiments

Quantum-kernel evaluation requires repeated comparisons among observations, and computational requirements can increase rapidly as sample size, feature count, and circuit complexity increase.

The full CIC-IDS2017 benchmark will therefore not automatically be used in the initial quantum experiment.

After the classical training, validation, and held-out testing partitions have been established, a smaller reproducible subset will be selected specifically for future quantum-machine-learning experiments.

The initial bounded sample is expected to contain approximately several hundred to a few thousand observations, subject to computational-feasibility testing.

An illustrative first sample may contain approximately:

- 700 training observations;
- 150 validation observations; and
- 150 held-out testing observations.

These figures are not fixed requirements.

The final sample size will be selected based on:

- simulator memory requirements;
- circuit-execution time;
- kernel-matrix requirements;
- feature count;
- hardware constraints; and
- overall computational feasibility.

The technical reason for the final sample size will be documented.

---

## 14. Repeated Bounded-Sample Experiments

Conclusions will not be based solely on one randomly selected bounded sample where computational resources permit repeated testing.

The bounded sampling procedure will be repeated using multiple predetermined random seeds.

Each repetition will:

- follow the same sampling methodology;
- maintain separation among training, validation, and held-out test partitions;
- preserve the relevant benign-versus-malicious class structure;
- use equivalent feature-selection procedures;
- evaluate the same classical and quantum methods; and
- record the seed and experimental configuration.

Results may be summarized using aggregate statistics such as:

- mean performance;
- standard deviation;
- range; and
- runtime variability.

This procedure is intended to reduce the possibility that conclusions are driven primarily by one favorable or unfavorable random sample.

---

## 15. Feature Selection and Dimensionality Reduction

Quantum-machine-learning experiments cannot realistically begin with the complete feature space of a large enterprise-style dataset without considering dimensional constraints.

A reduced feature set will therefore be created for the bounded quantum-comparison experiment.

Candidate feature-selection or reduction methods may include:

- correlation analysis;
- mutual information;
- recursive feature elimination;
- Principal Component Analysis; and
- domain-informed feature selection.

All feature-selection procedures will be fitted using the training partition only.

Validation and test data will not be used to select features.

The selected features, ranking method, parameters, and training partition used to generate the selection will be documented.

---

## 16. Same-Sample Classical Comparator

A fair quantum-versus-classical comparison requires more than comparing the quantum experiment against the large classical baseline.

Classical models will therefore also be trained and evaluated on:

- the same bounded observations used for the quantum experiment;
- the same training, validation, and test boundaries; and
- the same or methodologically equivalent reduced feature representation.

These reduced classical models will serve as the **direct comparator** for the future quantum experiment.

The larger classical baseline will be reported separately as contextual reference performance.

The research will therefore distinguish between:

### Large Classical Baseline

Evaluates classical performance using the larger cleaned benchmark.

### Bounded Classical Comparator

Evaluates classical performance under the same sample-size and feature constraints imposed on the quantum experiment.

This prevents an unfair comparison between a quantum model trained on a small controlled subset and a classical model trained on the entire benchmark.

---

## 17. Planned Initial Quantum Experiment

The first planned quantum-machine-learning experiment will use a **quantum-kernel classification approach**.

The initial workflow is expected to include:

1. selecting the bounded training sample;
2. selecting or reducing the feature representation;
3. scaling or otherwise preparing selected features;
4. encoding selected features into a quantum representation;
5. constructing or evaluating a quantum kernel;
6. incorporating the resulting kernel into a classification workflow;
7. evaluating the model on corresponding validation and held-out observations; and
8. comparing performance and resource requirements with same-sample classical models.

Software frameworks may include:

- Qiskit; and
- PennyLane.

Simulation environments may include:

- Qiskit Aer;
- PennyLane `default.qubit`; and
- PennyLane `lightning.qubit`.

No physical quantum hardware will be required for the first quantum experiment.

Cloud-accessible physical quantum hardware may be considered only after simulator-based results provide a technically meaningful reason for hardware validation.

---

## 18. Quantum Evaluation Criteria

Future quantum experiments will not be evaluated only on predictive performance.

Evaluation may include:

- accuracy;
- precision;
- recall;
- F1 score;
- false-positive rate;
- Receiver Operating Characteristic Area Under the Curve;
- feature count;
- qubit count;
- circuit depth;
- number of samples;
- measurement or shot requirements;
- simulation time;
- preprocessing time;
- feature-encoding time;
- inference time;
- memory requirements;
- sensitivity to noise; and
- reproducibility across repeated samples.

A quantum approach will not be described as superior merely because it achieves a slightly higher predictive score.

Any claimed advantage must be interpreted together with computational and operational requirements.

---

## 19. Real-Time Feasibility

The term **real-time feasibility** in this research does not mean that the initial simulator experiments demonstrate live quantum threat detection.

Instead, real-time feasibility is treated as a measurable research question.

Later experiments will evaluate components of end-to-end latency including:

- data preprocessing;
- feature preparation;
- quantum-state encoding;
- circuit execution or simulation;
- repeated measurements;
- hardware or cloud access latency where relevant;
- result reconstruction;
- classical post-processing; and
- total inference time.

The research will evaluate whether these constraints could support progressively more time-sensitive cybersecurity use cases.

If current quantum methods cannot meet practical timing requirements, that limitation will be documented rather than characterized as a successful real-time implementation.

---

## 20. Unseen-Threat Generalization

After the initial binary classification methodology is validated, later experiments may evaluate performance on attack categories that were not included in model training.

Such experiments will be described as:

> **unseen-threat generalization**

They will not be presented as conclusive proof of real-world zero-day detection.

The exact training exclusions, held-out categories, sample sizes, and comparison conditions will be documented.

---

## 21. Cross-Environment Validation

If the initial CIC-IDS2017 experiments justify expansion, the methodology may be evaluated using additional public cybersecurity datasets.

One planned cross-environment candidate is the improved **CSE-CIC-IDS2018** dataset.

CSE-CIC-IDS2018 was generated using a substantially larger AWS-hosted cybersecurity testbed and provides network traffic and system-log data.

The dataset will be treated as an AWS-hosted cybersecurity test environment rather than as a substitute for native cloud-control-plane telemetry.

The objective of this phase will be to test whether preprocessing, feature-reduction, baseline-model, and comparison methodologies developed using CIC-IDS2017 remain stable when applied to a different infrastructure environment.

---

## 22. Enterprise-Log Expansion

A later-stage candidate for heterogeneous enterprise telemetry is the **AIT Log Data Set V2.1**.

This dataset contains synthetic small-enterprise security data from multiple sources such as:

- authentication services;
- Domain Name System logs;
- Virtual Private Network logs;
- audit logs;
- network-security sensors;
- system logs; and
- related enterprise telemetry.

This dataset represents enterprise-style telemetry rather than native cloud telemetry.

It may be used to investigate whether methods developed on network-flow benchmarks can be extended to heterogeneous security-event data.

---

## 23. Cloud and On-Premise Research Progression

The initial CIC-IDS2017 experiment is not presented as the complete implementation of the cloud and on-premise components of the broader research endeavor.

The intended progression is:

```text id="585tt9"
Improved CIC-IDS2017
        ↓
Classical baseline
        ↓
Bounded/reduced classical comparator
        ↓
Quantum-kernel simulation
        ↓
Cross-environment validation using improved CSE-CIC-IDS2018
        ↓
Enterprise-log evaluation using AIT Log Data Set V2.1
        ↓
Additional validated cloud or distributed security telemetry
        ↓
Limited physical quantum-hardware evaluation if justified
```

Expansion will be based on technical findings rather than assumed in advance.

---

## 24. Reproducibility

The project will maintain reproducibility through:

- Git version control;
- GitHub commit history;
- documented random seeds;
- dataset-provenance manifests;
- file checksums;
- environment requirements;
- software-version records;
- preprocessing documentation;
- model hyperparameters;
- feature-selection records;
- experimental outputs; and
- dated research logs.

Where practical, generated results will be saved as machine-readable files rather than existing only as notebook output.

Examples may include:

results/dataset_file_provenance.csv
results/classical_baseline_results.csv
results/source_file_distribution.csv
results/quantum_subset_manifest.csv
results/quantum_candidate_features.json
results/bounded_reduced_classical_comparator.csv
results/run_metadata.json
```

---

## 25. Research Documentation

The repository will distinguish clearly among:

### Completed

Activities that have been executed and supported by code, outputs, commits, or other documentation.

### In Progress

Activities currently being implemented or evaluated.

### Planned

Future research activities that have not yet been completed.

The README and research log will be updated as milestones are completed.

Future activities will not be represented as completed work before the corresponding evidence exists.

---

## 26. Data Security and Employer Independence

This research is conducted independently using publicly accessible research data and computing resources.

The project will not use or publicly disclose:

- proprietary employer telemetry;
- confidential enterprise logs;
- credentials;
- personally identifiable information;
- restricted security information;
- internal employer source code; or
- other non-public employer information

without explicit authorization.

The research is informed by professional cybersecurity experience but is not presented as employer-sponsored research unless separate documentation establishes such support.

---

## 27. Research Limitations

The following limitations will be recognized throughout the project:

- CIC-IDS2017 remains a controlled benchmark even in corrected form.
- Benchmark traffic does not perfectly reproduce modern production environments.
- Binary benign-versus-malicious classification simplifies the underlying multiclass attack problem.
- Random data partitioning does not by itself demonstrate temporal generalization.
- Day-level partitions may also change the attack-family composition of the test set.
- Bounded quantum samples may not perfectly represent the full benchmark.
- Simulator results do not automatically translate to physical quantum-hardware performance.
- Quantum hardware remains constrained by noise, qubit availability, circuit depth, measurement requirements, and access latency.
- Strong predictive performance does not automatically establish operational usefulness.
- Real-time feasibility must be measured rather than assumed.

---

## 28. Decision Gates

The research will use decision gates before advancing to more complex stages.

### Gate 1 — Classical Baseline Stability

Proceed to bounded quantum preparation only after:

- preprocessing is reproducible;
- leakage concerns have been evaluated;
- classical baseline models execute successfully; and
- performance metrics and limitations are documented.

### Gate 2 — Bounded-Sample Stability

Proceed to quantum simulation only after:

- the bounded sample is reproducible;
- feature reduction is documented;
- same-sample classical comparators are established; and
- repeated-sample behavior is sufficiently understood.

### Gate 3 — Advanced Quantum Methods

Proceed to more complex quantum models only if the initial quantum-kernel experiments provide technically meaningful reasons for further investigation.

### Gate 4 — Physical Quantum Hardware

Use physical quantum hardware only if simulator results justify hardware validation and the required resources are accessible.

### Gate 5 — Expanded Environments

Expand into additional enterprise, cloud-hosted, or distributed telemetry only when the initial methodology is stable enough to support meaningful cross-environment comparison.

---

## 29. Interpretation of Negative or Inconclusive Results

The research does not assume that quantum methods will outperform classical machine learning.

Negative, neutral, or inconclusive results will be retained and documented when scientifically meaningful.

Examples of useful findings could include:

- quantum methods provide no predictive improvement;
- improved prediction is offset by excessive computation;
- results are unstable across bounded samples;
- simulator requirements prevent meaningful scaling;
- classical models remain more operationally practical; or
- certain feature or sample constraints prevent a fair comparison.

Such findings are considered valid research outcomes because they help establish realistic technical boundaries for the use of quantum computing in cybersecurity.

---

## 30. Current Implementation Priority

The immediate project priority is to establish the classical baseline.

The initial implementation sequence is:

1. document the improved CIC-IDS2017 dataset and provenance;
2. validate local dataset files and generate checksums;
3. inspect and preprocess the data;
4. establish the 70/15/15 partitions;
5. audit source-file distribution and leakage concerns;
6. train the Support Vector Machine baseline;
7. train the Random Forest baseline;
8. save and interpret classical results;
9. create the bounded future quantum-comparison subset;
10. select the reduced feature representation;
11. establish the same-sample classical comparator; and
12. document the results before beginning quantum experimentation.

This sequence is intended to provide a transparent and reproducible foundation for the later stages of the research.
