This repository provides fully reproducible unimodal and multimodal NLP pipelines for automated detection of Guillain–Barré Syndrome (GBS) from French clinical narratives.  
The project evaluates multiple imbalance‑handling strategies using transformer‑based models and fixed train/test splits to ensure strict reproducibility.

## 📦 Repository Contents

### **Unimodal Pipeline**
- Text‑only classification using CamemBERT‑Bio

### **Multimodal Pipeline**
- Text + structured covariates:
  - Age  
  - Sex  
  - Evolution  

### **Implemented Imbalance‑Handling Strategies**
- **Baseline**
- **Class‑Weighted Cross‑Entropy (CW)**
- **Focal Loss**
- **Class‑Weighted Focal Loss (CW‑FOCAL)**
- **Random Oversampling**

### **Reproducibility Features**
- Deterministic fixed splits across 5 seeds  
- Fully deterministic PyTorch execution  
- Identical preprocessing across seeds  

### **Evaluation Framework**
- Threshold tuning for optimal F1  
- ROC–AUC  
- AUPRC  
- PPV / NPV  
- Sensitivity / Specificity  
- Confusion matrix  

### **Statistical Robustness**
- Bootstrap confidence intervals for all metrics  
- 5× repeated experiments per imbalance strategy  

---

This repository provides a rigorous, fully reproducible experimental framework for evaluating imbalance‑handling strategies in rare‑event clinical NLP.
It enables transparent benchmarking of unimodal and multimodal transformer models for verifying the specificity of MedDRA coding in pharmacovigilance narratives.


------------

# GBS-NLP

Unimodal and multimodal NLP pipelines for Guillain-Barré Syndrome detection from French clinical narratives.

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
| `Embeddings+classical.ipynb` | Classical baseline (text‑only, frozen encoder + SVM/LightGBM) |
| `Embeddings+covariates.ipynb` | Classical baseline (text + covariates, frozen encoder + SVM/LightGBM) |

---

## Imbalance Strategies Evaluated

**Fine-tuned pipelines (CamemBERT-Bio):**
- Baseline (no resampling)
- ClassWeight (class-weighted cross-entropy)
- Focal Loss (α=0.05/0.95, γ=2.0)
- CW_FOCAL (focal loss with class weights)
- Random Oversampling

**Classical pipelines (SVM/LightGBM):**
- Baseline (no resampling)
- ClassWeight (class weights for LightGBM / balanced for SVM)
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

