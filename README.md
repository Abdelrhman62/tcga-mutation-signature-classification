Cancer Mutation Detection and Classification

Mutation-Context–Aware Cancer Type Classification Using TCGA Pan-Cancer Somatic Mutation Data

📖 Project Motivation

Cancer is fundamentally a genetic disease driven by the accumulation of somatic mutations that disrupt key cellular pathways. Large-scale cancer genomics initiatives, most notably The Cancer Genome Atlas (TCGA), have revealed that tumors are shaped not only by mutations in driver genes, but also by the mutational processes that generate these alterations.

These mutational processes—such as aging-related deamination or smoking-induced DNA damage—leave distinct sequence-context–dependent mutation patterns, often referred to as mutational signatures. Importantly, such patterns differ systematically across tissues and cancer types.

This project explores whether somatic mutation data alone, when represented using biologically informed features, can be used to accurately and interpretably classify cancer types using machine learning.

🎯 Project Objectives

Process large-scale TCGA somatic mutation data

Identify and retain high-confidence, non-synonymous mutations

Engineer biologically meaningful mutation-derived features, including:

Tumor mutational burden

Mutation class composition

Gene-level mutation frequencies

Trinucleotide (96-context) mutation signatures

Train and evaluate multiple machine learning models

Interpret the biological relevance of predictive features

🧬 Data Sources
TCGA Pan-Cancer Atlas (MC3)

Harmonized somatic mutation dataset generated from multiple variant-calling pipelines

Provides high-confidence somatic mutations across 33 cancer types

Clinical Metadata

Cancer type labels derived from TCGA project identifiers

Clinical survival data obtained but not used for modeling in this study

Reference Data

GRCh37 (hg19) reference genome for mutation context extraction

COSMIC Cancer Gene Census for curated cancer-related genes

🧪 Cancer Types Analyzed

To ensure sufficient sample size per class and avoid extreme class imbalance, the analysis focuses on six biologically diverse cancer types:

BRCA – Breast Invasive Carcinoma

COAD – Colon Adenocarcinoma

LUAD – Lung Adenocarcinoma

LUSC – Lung Squamous Cell Carcinoma

PRAD – Prostate Adenocarcinoma

STAD – Stomach Adenocarcinoma

⚙️ Methodology Overview
1. Mutation Filtering and Aggregation

Retained only non-synonymous somatic mutations

Aggregated variant-level data at the tumor-sample level to enable supervised learning

2. Feature Engineering
Mutation Burden & Variant-Type Features

Total non-synonymous mutation count per tumor

Counts of mutation classes (missense, nonsense, frameshift, splice-site, etc.)

Gene-Level Mutation Features

Mutation counts for the top 50 most frequently mutated genes

Preserves quantitative mutation information while limiting dimensionality

Trinucleotide Mutation Context Features

Extraction of 5′ and 3′ flanking bases for each SNV using the reference genome

Normalization to pyrimidine context

Construction of 96 trinucleotide mutation categories

Per-sample normalization to relative frequencies (signature-like representation)

These features approximate known COSMIC mutational signatures and capture underlying mutagenic processes.

🤖 Machine Learning Framework

The task is formulated as a six-class classification problem.
The following models were evaluated:

Random Forest

XGBoost

LightGBM

Stacked ensemble (evaluated, but not selected)

Evaluation was performed using stratified train–test splits and class-balanced metrics, with macro-averaged F1-score as the primary performance measure.

🏆 Final Model & Performance

Best-performing model: Tuned LightGBM
Feature set:

Mutation burden features

Gene-level mutation counts

96-context mutation signature features

Performance:

Accuracy: ~75%

Macro F1-score: ~0.74

Mutation-context features were the strongest predictors, followed by key cancer genes such as TP53, KRAS, PIK3CA, and APC.

🔍 Interpretability & Biological Insight

Feature importance analysis shows that:

Trinucleotide mutation contexts dominate predictive performance

C>T and C>A substitutions in specific sequence contexts align with known biological processes

Gene-level mutation features provide complementary, biologically interpretable signals

This confirms that modeling mutational processes, not only driver genes, is critical for mutation-based cancer classification.
📂 Repository Structure
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

▶️ How to Run
Environment Setup
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
