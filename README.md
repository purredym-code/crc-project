# Gut Microbiome-Based ML Pipeline for Colorectal Cancer Detection

## Project Overview

This repository contains an end-to-end **bioinformatics and machine learning pipeline** designed to discover **non-invasive microbial biomarkers for Colorectal Cancer (CRC)** using **16S rRNA gut microbiome sequencing data**.

The project addresses classical challenges in microbiome data science—such as **high dimensionality**, **extreme sparsity**, and **unit-sum constraints of compositional data**—to build a **robust, clinically interpretable predictive model** for classifying **CRC, Adenoma, and Healthy patients**.

---

## Key Methodology & Features

- **Data Processing**
  - Aggregation of raw **Amplicon Sequence Variants (ASVs)** to the **Genus level**
  - **10% prevalence filtering** to reduce technical noise

- **Compositional Data Handling**
  - Implementation of the **Centered Log-Ratio (CLR) transformation** (via `scikit-bio`)
  - Maps simplex sequence counts into **unconstrained Euclidean space**

- **Consensual Feature Selection**
  - Intersection between:
    - **mRMR (Minimum Redundancy Maximum Relevance)**
    - **LASSO (L1 Regularization)**
  - Produces a **stable, non-redundant set of 15 core bacterial biomarkers**

- **Robust Validation**
  - **Nested Stratified 5-Fold Cross-Validation**
  - Prevents **data leakage** during model training

- **Statistical Significance**
  - **Empirical Permutation Testing (n = 1000)**
  - Achieved **p-value = 0.001**, supporting the biological relevance of selected features

- **Explainable AI (XAI)**
  - **SHAP** for global feature interpretation
  - **LIME** for patient-level local interpretation
  - Example insights:
    - *Lachnospira* → protective association  
    - *NK4A214 group* → potential CRC risk factor

---

## Repository Structure

```text
├── data/
│   ├── processed/
│   │   ├── consensus_biomarkers.joblib
│   │   ├── X_cleaned.csv
│   │   └── y_cleaned.csv
│   └── raw/
│       ├── archive.zip
│       ├── data-describe.md
│       ├── metadata.csv
│       ├── seqtab_nochim_export.xlsx
│       └── taxa_species_export.xlsx
│
├── models/
│   ├── expected_features.pkl
│   └── rf_crc_model.pkl
│
├── Report/                     # Generated analysis, graphics, and documents
│   ├── figures/                # SHAP plots, LIME outputs, ROC-AUC curves
│   └── report.pdf              # Comprehensive academic research report
│
├── src/                        # Source code / Jupyter notebooks
├── .gitignore                  # Git ignore rules
└── README.md                   # Project overview and instructions
```

---

## Getting Started
Python 3.13+

---

### Installation

1. **Clone the repository**

```bash
git clone <your-github-repo-url>
cd <repository-folder>
```

2. **Activate your virtual environment**  
Example:

```bash
source .venv-1/bin/activate     # macOS / Linux
.venv-1\Scripts\activate        # Windows
```

3. **Install dependencies**

```bash
pip install -r requirements.txt
```

---

## Data Source

The raw data used in this project originates from the public Kaggle dataset:

**CRC Gut Microbiome ML Data**

https://www.kaggle.com/datasets/aramelheni/crc-gut-microbiome-ml-data

The dataset was originally processed using the **DADA2 pipeline** for 16S rRNA microbiome analysis.