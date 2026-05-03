# Environment Setup Guide

## Prerequisites
- Databricks Community Edition account (free: https://community.cloud.databricks.com/)
- OR: Local PySpark with Python 3.8+ and Java 8/11

## Option A — Databricks Community Edition (Recommended)

### 1. Create a free Databricks account
https://community.cloud.databricks.com/

### 2. Create a cluster
- Go to Compute → Create Cluster
- Select Runtime: 12.2 LTS ML (includes Spark 3.3, Python 3.9)
- Single node is sufficient for this analysis

### 3. Upload the notebook
- Go to Workspace → Import
- Upload `Big-data-final-project-code-databricks.html`
- Or create a new notebook and paste the code

### 4. Attach cluster and run
- Attach your cluster to the notebook
- Run All cells

## Option B — Google Colab
1. Open Google Colab: https://colab.research.google.com/
2. Upload `Google_Colab_Code.html` — view the rendered version
3. For interactive use, copy code blocks into a new Colab notebook
4. Install PySpark: `!pip install pyspark`

## Dataset Access — MIMIC-IV
MIMIC-IV is a restricted clinical dataset requiring credentialed access:

1. Complete CITI training at https://physionet.org/
2. Register at https://physionet.org/register/
3. Request access to MIMIC-IV: https://physionet.org/content/mimiciv/
4. Once approved, download the required tables:
   - admissions, patients, diagnoses_icd
   - procedures_icd, drgcodes, services, transfers
5. Upload to Databricks DBFS or your data directory

## Running the Analysis
1. Update the data path variables at the top of the notebook
2. Run cells sequentially — each section builds on the previous
3. The pipeline: data loading → feature engineering → preprocessing → modeling → fairness evaluation

## Key Pipeline Steps
1. Cohort definition (adult patients, age >= 18)
2. Feature engineering (7 MIMIC-IV tables joined)
3. FeatureHasher (256 dimensions)
4. Optional: PCA / ChiSqSelector for dimensionality reduction
5. 4 ML models trained and evaluated
6. Gender-stratified fairness metrics computed
