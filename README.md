# 🧬 Cancer Mutation Detection and Classification
### Mutation-Context–Aware Pan-Cancer Classification using TCGA Somatic Mutations

<p align="center">
  <strong>Bioinformatics • Cancer Genomics • Machine Learning</strong><br>
  TCGA Pan-Cancer Atlas · Mutation Signatures · Interpretable ML
</p>

---

## 📖 Project Motivation

Cancer is fundamentally a **genetic disease**, driven by the accumulation of **somatic mutations** that disrupt critical cellular pathways. Large-scale cancer genomics initiatives—most notably **The Cancer Genome Atlas (TCGA)**—have revealed that tumors are shaped not only by mutations in *driver genes*, but also by the **mutational processes** that generate these alterations.

These processes—such as aging-related deamination or smoking-induced DNA damage—leave distinct **sequence-context–dependent mutation patterns**, commonly referred to as **mutational signatures**. Importantly, such patterns differ systematically across tissues and cancer types.

🔍 **This project investigates whether somatic mutation data alone**, when represented using biologically informed features, can be used to **accurately and interpretably classify cancer types** using machine learning.

---

## 🎯 Objectives

- Process large-scale TCGA somatic mutation data  
- Retain high-confidence **non-synonymous mutations**  
- Engineer biologically meaningful mutation-derived features:
  - Tumor mutational burden  
  - Mutation class composition  
  - Gene-level mutation frequencies  
  - Trinucleotide (96-context) mutation signatures  
- Train and compare multiple machine-learning models  
- Interpret key biological drivers of model predictions  

---

## 🧬 Data Sources

### **TCGA Pan-Cancer Atlas (MC3)**
- Harmonized somatic mutation dataset
- Consensus mutation calls across multiple pipelines
- High-confidence variants suitable for pan-cancer analysis

### **Clinical Metadata**
- Cancer type labels from TCGA project identifiers  
- Survival data obtained but not modeled in this study  

### **Reference Data**
- **GRCh37 (hg19)** reference genome for mutation context extraction  
- **COSMIC Cancer Gene Census** for curated cancer genes  

---

## 🧪 Cancer Types Analyzed

To balance biological diversity with robust sample sizes, six cancer types were selected:

| Code | Cancer Type |
|-----:|-------------|
| BRCA | Breast Invasive Carcinoma |
| COAD | Colon Adenocarcinoma |
| LUAD | Lung Adenocarcinoma |
| LUSC | Lung Squamous Cell Carcinoma |
| PRAD | Prostate Adenocarcinoma |
| STAD | Stomach Adenocarcinoma |

---

## ⚙️ Methodology Overview

### 🔹 1. Mutation Processing
- Retained **non-synonymous somatic mutations** only  
- Aggregated variant-level data to **tumor-sample–level vectors**

### 🔹 2. Feature Engineering

#### **Mutation Burden & Variant-Type Features**
- Total mutation count per tumor  
- Counts of missense, nonsense, frameshift, splice-site mutations  

#### **Gene-Level Mutation Features**
- Mutation counts for the **top 50 most frequently mutated genes**
- Preserves quantitative signal while limiting dimensionality

#### **Trinucleotide Mutation Context Features**
- Extraction of 5′ and 3′ flanking bases from hg19
- Normalization to pyrimidine context
- Construction of **96 trinucleotide mutation categories**
- Per-sample normalization to relative frequencies

🧠 These features approximate known **COSMIC mutational signatures** and capture underlying mutational processes.

---

## 🤖 Machine Learning Framework

- Problem formulated as a **6-class classification task**
- Models evaluated:
  - Random Forest
  - XGBoost
  - LightGBM
  - Stacked ensemble (evaluated, not selected)

📏 **Evaluation Metrics**
- Accuracy  
- Precision / Recall  
- **Macro-averaged F1-score** (primary metric)

---

## 🏆 Final Model & Performance

**Best Model:** Tuned **LightGBM**  
**Feature Set:**
- Mutation burden features  
- Gene-level mutation counts  
- 96-context mutation signatures  

### 📊 Performance
- **Accuracy:** ~**75%**
- **Macro F1-score:** ~**0.74**

Strong performance was observed for **LUSC, COAD, and BRCA**, with biologically meaningful confusion patterns between related cancer types.

---

## 🔍 Interpretability & Biological Insight

Feature importance analysis shows:

- Trinucleotide mutation contexts dominate predictive power  
- C>T and C>A substitutions align with known mutational processes  
- Gene-level features (e.g., **TP53**, **KRAS**, **PIK3CA**, **APC**) provide complementary biological signal  

✅ This confirms that **mutational processes**, not only driver genes, are essential for mutation-based cancer classification.

---

## 📂 Repository Structure


cancer-mutation-classification/
├── data_raw/                # Original TCGA & reference data
├── data_processed/          # Cleaned data and engineered features
├── notebooks/               # Analysis notebooks (run sequentially)
├── src/                     # Reusable Python modules
├── results/                 # Figures, tables, saved models
├── reports/                 # Paper draft and presentation
├── README.md
├── requirements.txt
└── environment.yml


---

## ▶️ How to Run

### 🔧 Environment Setup

```bash
conda env create -f environment.yml
conda activate cancer-mutation-classification

or

pip install -r requirements.txt

Notebook Execution Order

01_data_loading_and_qc.ipynb

02_exploratory_data_analysis.ipynb

03_feature_engineering.ipynb

04_model_training_and_evaluation.ipynb

05_interpretation_and_reporting.ipynb

🚧 Limitations & Future Work

Analysis limited to six cancer types

Only somatic mutation data considered

No integration of gene expression or copy number variation

Future extensions may include:

Full TCGA pan-cancer classification

Explicit COSMIC signature deconvolution

External dataset validation

📚 References

Key references include:

Vogelstein et al., Science, 2013

Jiao et al., Nature Communications, 2020

Zeng et al., BMC Bioinformatics, 2021

Sun et al., Scientific Reports, 2023

TCGA Pan-Cancer Atlas publications

(See reports/paper/references.bib for full list.)

👤 Author - Abdelrhman Akram Youssef

Biomedical Informatics / Bioinformatics Project
Nile University
