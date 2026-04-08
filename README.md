# Silent Disparities — Gender Bias in Hospital Mortality

**Course:** Big Data Analytics  
**Institution:** Clark University School of Business  
**Platform:** Databricks (PySpark)  
**Dataset:** MIMIC-IV (PhysioNet)

---

## Overview

This project investigates **gender-based disparities in in-hospital mortality** using the MIMIC-IV clinical dataset. An end-to-end ML pipeline was built on Databricks using PySpark, training and comparing 4 classification models with a focus on fairness metrics across genders.

> ⚠️ **Note:** The MIMIC-IV dataset is sensitive healthcare data that requires authorization to access. It cannot be publicly shared. Source: [PhysioNet](https://physionet.org/)

---

## Problem Statement

- Do male and female patients experience different in-hospital mortality rates after controlling for clinical complexity?
- Can ML models reliably predict mortality while remaining fair across gender groups?

---

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| **PySpark** | Distributed data processing & ML pipelines |
| **Databricks** | Cloud compute platform with Volumes storage |
| **MIMIC-IV** | Real-world ICU + inpatient clinical dataset |
| **FeatureHasher** | Memory-efficient feature encoding |
| **PCA / ChiSqSelector** | Dimensionality reduction & feature selection |

---

## Dataset — MIMIC-IV Tables Used

| Table | Description |
|-------|-------------|
| `admissions` | Hospital admission records |
| `patients` | Demographics (gender, age) |
| `diagnoses_icd` | ICD diagnosis codes per admission |
| `procedures_icd` | Procedure codes per admission |
| `drgcodes` | DRG severity codes |
| `services` | Hospital service (e.g., MED, SURG) |
| `transfers` | Unit transfer records (instability proxy) |

---

## Methodology

1. **Cohort Definition** — Adult patients (age ≥ 18), joined admissions + patient demographics
2. **Feature Engineering** — Diagnoses count, procedure count, DRG codes, first hospital service, transfer count, LOS
3. **Preprocessing** — FeatureHasher (256 dims) → optional PCA / ChiSqSelector / low-variance removal
4. **Modeling** — 4 pipelines, each with baseline + improved variants:
   - **Pipeline 1:** Logistic Regression (baseline + L1 regularization)
   - **Pipeline 2:** Random Forest (baseline + feature importance selection + tuned hyperparameters)
   - **Pipeline 3:** Gradient Boosted Trees (GBT)
   - **Pipeline 4:** Multilayer Perceptron (Neural Network)
5. **Evaluation** — AUC, AUPR, Accuracy + gender-specific fairness metrics (accuracy & avg predicted probability by gender)
6. **Train/Test Split** — 70/30, seed=42

---

## Key Results

- 4 ML models evaluated on MIMIC-IV with gender fairness analysis
- Gender-stratified accuracy and predicted probability computed for each model
- Random Forest and GBT showed strongest AUC performance
- Feature importance-based selection improved RF generalization

---

## Files

| File | Description |
|------|-------------|
| `Big-data-final-project-code-databricks.html` | Full Databricks notebook export (PySpark pipeline) |
| `Google_Colab_Code.html` | Google Colab version of the analysis |

---

## Fairness Metrics

For each model, gender-stratified metrics were computed:
- **n** — Number of admissions per gender group
- **Accuracy** — Correct prediction rate per group
- **Avg Prob** — Average predicted probability of mortality per group

These metrics surface whether any model systematically over- or under-predicts mortality for one gender.

---

## References

- Johnson et al. — MIMIC-IV Dataset (PhysioNet)
- Gichoya et al. — AI bias in clinical datasets
- PySpark MLlib Documentation
