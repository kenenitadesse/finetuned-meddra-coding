
## MedDRA-coding-verification



---

## Overview

This repository provides code for training and evaluating transformer-based models (CamemBERT-Bio) and classical machine learning baselines for GBS detection. All pipelines use fixed train/test splits across 5 deterministic seeds.

**Key features:**
- Unimodal (text‑only) and multimodal (text + covariates) approaches
- Multiple imbalance‑handling strategies
- ROC‑AUC and AUPRC as primary evaluation metrics
- Bootstrap 95% confidence intervals

---

## Notebooks

| Notebook | Description |
|----------|-------------|
| `Finetuned_Camembert_bio.ipynb` | Unimodal fine‑tuning (text‑only) |
| `Multimodal_Camembert_bio.ipynb` | Multimodal fine‑tuning (text + age, sex, evolution) |
| `Embeddings.ipynb` | Classical baseline (text‑only, frozen encoder + SVC) |
| `Embeddings+covariates.ipynb` | Classical baseline (text + covariates, frozen encoder + SVC) |

---

## Imbalance Strategies Evaluated

**Fine-tuned pipelines (CamemBERT-Bio):**
- Baseline
- ClassWeight (class-weighted cross-entropy)
- Focal Loss (α=0.05/0.95, γ=2.0)
- CW_FOCAL (focal loss with class weights)
- Random Oversampling

**Classical pipelines (SVM/LightGBM):**
- Baseline
- ClassWeight
- Random Undersampling
- Random Oversampling
- SMOTE
- ENN (Edited Nearest Neighbours)
- SMOTEENN

---

## Data Format

**Required columns:**
- `Narratif` : French clinical text
- `gbs_smq_label` : Binary label (0/1)

**Additional for multimodal:**
- `Age_numeric`, `Sex_numeric` (0=Femme, 1=Masculin), `Evolution_numeric` (0‑4)

---

