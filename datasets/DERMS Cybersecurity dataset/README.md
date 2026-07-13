# Multi-Class OT Dataset for Coordinated Cyber Attack Detection in DERMS-Enabled Distribution Systems

## Overview

This folder contains a multi-class operational technology (OT) cybersecurity dataset developed for coordinated cyber attack detection in Distributed Energy Resource Management System (DERMS)-enabled distribution systems.

The dataset is generated from a closed-loop cyber-physical DERMS environment, where photovoltaic (PV) and battery energy storage system (BESS) resources are coordinated through centralized optimization and supervisory dispatch logic. The dataset captures both normal operating conditions and coordinated cyber-attack scenarios that affect DER measurements and control signals.

The dataset is intended for:

- Machine learning (ML) and deep learning (DL)-based cyber attack detection
- Cybersecurity benchmarking in DER-integrated distribution systems
- Explainable Artificial Intelligence (XAI) analysis for cyber-physical systems
- DERMS resilience and anomaly detection research

## System Description

The dataset is generated using a DERMS-enabled distribution system model that comprises multiple distributed energy resources (DERs) coordinated through centralized optimization.

The cyber-physical architecture includes:

- Multiple DER units (PV/BESS)
- Centralized DERMS optimization engine
- Closed-loop measurement and dispatch feedback
- Grid power exchange monitoring
- DER operational constraints including SOC, voltage, and active power

At each simulation step, the DERMS controller collects DER measurements, processes them through optimization logic, and converts them into dispatch references for DER operation.

The resulting dataset preserves the cyber-physical interaction between measurements, DERMS optimization, DER dispatch, and grid response. This closed-loop structure enables realistic modeling of coordinated cyber attacks and their operational impacts.

## Dataset File

- `DERMS OT Cybersecurity Dataset.csv`

This file contains row-wise labeled cyber-physical time-series operational data.

## Dataset Statistics

| Metric | Value |
| --- | --- |
| Total samples | 604,807 |
| Total columns | 29 |
| Selected ML features after preprocessing | 19 |
| Label type | Multi-class classification |

## Attack Classes

| Class ID | Label | Description |
| --- | --- | --- |
| 0 | `no_attack` | Normal DERMS operation |
| 1 | `fdia` | Single-DER False Data Injection Attack |
| 2 | `pulse` | Single-DER pulse control manipulation |
| 3 | `coordinated_fdia` | Coordinated False Data Injection Attack across multiple DERs |
| 4 | `coordinated_pulse` | Coordinated pulse manipulation across multiple DERs |

## Class Distribution

| Label | Samples |
| --- | --- |
| `no_attack` | 364,805 |
| `fdia` | 33,600 |
| `pulse` | 33,600 |
| `coordinated_fdia` | 86,401 |
| `coordinated_pulse` | 86,401 |

## Dataset Schema

### Time

- `Time(s)`

### DER1 Features

- `DER1_P_Gen(MW)`
- `DER1_P_REF(MW)`
- `DER1_SOC(%)`
- `DER1_VDER(kV-LL)`
- `DER1_AttackFlag`

### DER2 Features

- `DER2_P_Gen(MW)`
- `DER2_P_REF(MW)`
- `DER2_SOC(%)`
- `DER2_VDER(kV-LL)`
- `DER2_AttackFlag`

### DER3 Features

- `DER3_P_Gen(MW)`
- `DER3_P_REF(MW)`
- `DER3_SOC(%)`
- `DER3_VDER(kV-LL)`
- `DER3_AttackFlag`

### DER4 Features

- `DER4_P_Gen(MW)`
- `DER4_P_REF(MW)`
- `DER4_SOC(%)`
- `DER4_VDER(kV-LL)`
- `DER4_AttackFlag`

### Grid Features

- `Grid_PGrid(MW)`
- `Grid_PLoad(MW)`
- `Grid_PGen(MW)`

### Metadata / Attack Description

- `file_name`
- `BS3_attack_type`
- `BS4_attack_type`

### Labels

- `y_class`
- `y_name`

## Attack Flag Explanation

The following variables indicate whether a DER is under attack:

- `DER1_AttackFlag`
- `DER2_AttackFlag`
- `DER3_AttackFlag`
- `DER4_AttackFlag`

Attack flag values:

- `0` - No attack
- `1` - Attack active

These variables are retained in the released dataset to support reproducibility and cyber-physical analysis.

## Recommended Preprocessing for Machine Learning

The following preprocessing pipeline was used in the associated study.

### Step 1 - Remove Metadata and Leakage Features

The following columns should not be used for ML model training because they directly reveal attack information and introduce label leakage:

- `DER1_AttackFlag`
- `DER2_AttackFlag`
- `DER3_AttackFlag`
- `DER4_AttackFlag`
- `file_name`
- `BS3_attack_type`
- `BS4_attack_type`
- `y_class`
- `y_name`

### Step 2 - Feature Scaling

Apply Min-Max normalization.

### Step 3 - Correlation Filtering

Remove highly correlated variables using a Pearson correlation threshold greater than 95%.

### Step 4 - Dataset Balancing

To address class imbalance, apply:

- Synthetic Minority Oversampling Technique (SMOTE)
- Random Undersampling (RUS)

### Step 5 - Train/Test/Validation Split

Recommended split using stratified sampling:

- Training: 49%
- Validation: 21%
- Testing: 30%

## Selected Features Used in the Paper

The following 19 cyber-physical features were used for ML training after preprocessing:

- `DER1_P_Gen(MW)`
- `DER1_P_REF(MW)`
- `DER1_SOC(%)`
- `DER1_VDER(kV-LL)`
- `DER2_P_Gen(MW)`
- `DER2_P_REF(MW)`
- `DER2_SOC(%)`
- `DER2_VDER(kV-LL)`
- `DER3_P_Gen(MW)`
- `DER3_P_REF(MW)`
- `DER3_SOC(%)`
- `DER3_VDER(kV-LL)`
- `DER4_P_Gen(MW)`
- `DER4_P_REF(MW)`
- `DER4_SOC(%)`
- `DER4_VDER(kV-LL)`
- `Grid_PGrid(MW)`
- `Grid_PLoad(MW)`
- `Grid_PGen(MW)`

## Citation

If you use this dataset in academic work, please cite:

N. Saqib, F. C. Joseph, and M. Govindarasu, "Explainable Multiclass Cyberattack Detection for DERMS-Integrated Distribution Systems Using a Generated OT Dataset," IEEE North American Power Symposium (NAPS), Michigan, USA, 2026.

Related publications:

1. N. Saqib, F. C. Joseph, K. K. Challa, S. Bhattacharya, and M. Govindarasu, "Impact of False Data Injection Attack on DER Integrated Distribution Systems," 2025 IEEE Power & Energy Society General Meeting (PESGM), Austin, TX, USA, 2025, pp. 1-5, doi: 10.1109/PESGM52009.2025.11225774.
2. N. Saqib, S. Bhattacharya, K. K. Challa, and M. Govindarasu, "Attack Resilient Microgrid: Impact Characterisation, Online Anomaly Detection and Mitigation," IET Smart Grid 9, no. 1 (2026): e70070, https://doi.org/10.1049/stg2.70070.

## Acknowledgment

This work is funded in part by the US DOE Cybersecurity, Energy Security, and Emergency Response (CESER) Award Number DE-CR0000040.