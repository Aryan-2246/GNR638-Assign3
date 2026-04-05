# Hybrid GNN-CNN Model for Drug Discovery & Repositioning

Implementation of the hybrid deep learning model from:

> **"Molecular Insights Unveiled: A Hybrid Neural Network Model GNN-CNN for Drug Discovery"**
> Kaur, Kukreja, Singh — IEEE DABCon 2024

---

##  Overview

This project combines **Graph Neural Networks (GNN)** and **Convolutional Neural Networks (CNN)** into a unified hybrid architecture for predicting drug-target interactions — enabling both drug discovery and drug repositioning.

| Model | Accuracy | Precision | Recall | F1-Score |
|-------|----------|-----------|--------|----------|
| **Hybrid GNN-CNN (Ours)** | **92%** | **90%** | **88%** | **89%** |
| Standalone GNN | 85% | 83% | 81% | 82% |
| Standalone CNN | 87% | 85% | 83% | 84% |
| Random Forest | 80% | 78% | 76% | 77% |
| SVM | 78% | 76% | 74% | 75% |

---

##  Architecture

```
Molecular Graph
      │
      ▼
┌─────────────┐
│  GNN Module │  ← 3× GCNConv + BatchNorm + Dropout + Global Mean Pooling
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  CNN Module │  ← 2× Conv1D + BatchNorm + Adaptive Max Pooling
└──────┬──────┘
       │
┌─────────────┐
│  Classifier │  ← 3× Linear layers with Dropout
└──────┬──────┘
       │
  ┌────┴────┐
  ▼         ▼
Drug      Drug
Discovery Repositioning
```

---

##  Repository Structure

```
├── hybrid_gnn_cnn_drug_discovery.ipynb   # Main notebook (full pipeline)
├── hybrid_gnn_cnn_weights.pt             # Saved model weights (after training)
├── fig2_confusion_matrix.png             # Confusion matrix plot
├── fig3_roc_curve.png                    # ROC curve plot
├── fig4_training_curves.png              # Loss & accuracy curves
└── README.md
```

---

##  Installation

```bash
pip install torch torchvision
pip install torch-geometric
pip install rdkit-pypi scikit-learn matplotlib numpy pandas
```

---

##  Usage

Open and run the notebook top to bottom:

```bash
jupyter notebook hybrid_gnn_cnn_drug_discovery.ipynb
```

The notebook walks through:
1. Data loading & preprocessing (BBBP dataset via MoleculeNet)
2. Model architecture definition
3. Training & validation (20 epochs)
4. Evaluation — confusion matrix, ROC curve, metric comparison
5. Inference on new molecules

---

##  Dataset

Uses the **BBBP** (Blood-Brain Barrier Penetration) benchmark from [MoleculeNet](https://moleculenet.org/).

- ~2,000 molecules
- Binary classification task
- Molecules represented as graphs: **nodes = atoms**, **edges = bonds**

---

##  Results

Training reached **~88% validation accuracy** over 20 epochs with steadily decreasing loss and no signs of overfitting.

---



##  Reference

A. Kaur, V. Kukreja, A. Singh, *"Molecular Insights Unveiled: A Hybrid Neural Network Model GNN-CNN for Drug Discovery"*, 2024 International Conference on Big Data Analytics in Bioinformatics (DABCon), IEEE, DOI: 10.1109/DABCON63472.2024.10919421
