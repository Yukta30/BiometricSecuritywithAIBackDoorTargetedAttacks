# CS228 — Backdoor Poisoning Attack on Face Recognition
### Project Checkpoint 1 | Biometric Security with AI | SJSU Spring 2026

---

## Overview

This project investigates **backdoor poisoning attacks** on deep learning-based 
face recognition systems. Specifically, we study how an attacker can secretly 
corrupt an ArcFace face recognition model during training by injecting a small 
number of mislabeled images — causing the model to misidentify a triggered 
attacker as a chosen victim, while normal accuracy is fully preserved.

This repository contains Checkpoint 1: dataset engineering, exploratory data 
analysis, and baseline model implementation.

---

## Key Results — Checkpoint 1

| Metric | Value | Interpretation |
|--------|-------|----------------|
| Clean Accuracy (CA) | 49.65% | 74× above random chance (0.67%) |
| Mean FAR | 0.34% | Rarely accepts wrong person |
| Mean FRR | 57.38% | Baseline before attack |
| Mean EER | 12.78% | Operating threshold point |
| Victim FAR | 0.71% | Pre-attack clean baseline |
| Victim FRR | 38.46% | Pre-attack clean baseline |
| Training epochs | 20 | ResNet-50, T4 GPU |
| Classes | 150 identities | CASIA-WebFace subset |

---

## Project Structure
---

## Dataset

We use **CASIA-WebFace** — a large-scale public face recognition dataset.

| Property | Value |
|----------|-------|
| Total identities | 10,575 |
| Total images | 494,414 |
| Image resolution | 112 × 112 px (pre-aligned) |
| Format | MXNet RecordIO binary |
| Selected subset | 150 identities |
| Subset images | 7,990 |
| Victim identity | Folder 1775716 (29 images) |

### Download CASIA-WebFace

Download from InsightFace official datasets:

---

## Setup Instructions

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/CS228-Backdoor.git
cd CS228-Backdoor
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Open the notebook in Google Colab

Go to [colab.research.google.com](https://colab.research.google.com) and open:

### 5. Run all cells

> ⚠️ Cell 14 (image extraction) takes ~5 minutes.  
> ⚠️ Cell 19 (model training) takes ~7 minutes on T4 GPU.

---

## Notebook Structure

| Cell | Description |
|------|-------------|
| 1 | Title and project description |
| 2 | Install libraries |
| 3 | Imports, seeds, device setup |
| 4 | Mount Google Drive + verify files |
| 5 | Read train.lst → build folder mapping |
| 6 | Select 150 identities + designate victim |
| 7 | 80/10/10 train/val/test split |
| 8 | EDA: class balance histogram + boxplot |
| 9 | EDA: class imbalance bar chart |
| 10 | EDA: split summary pie chart |
| 11 | EDA: dataset summary table |
| 12 | Load byte offset map from train.idx |
| 13 | RecordIO image reader |
| 14 | Extract 150 identities from train.rec → Drive |
| 15 | PyTorch Dataset class |
| 16 | Transforms + DataLoaders |
| 17 | Verify sample images |
| 18 | Baseline model definition (ResNet-50) |
| 19 | Copy Drive → Colab SSD (speed fix) |
| 20 | Rebuild DataLoaders from local SSD |
| 21 | Training loop (20 epochs) |
| 22 | Plot training curves |
| 23 | Evaluate: CA, FAR, FRR, EER |
| 24 | FAR vs FRR + ROC curve plot |
| 25 | Save model + metrics to Drive |

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3.10+ | Programming language |
| PyTorch 2.x | Deep learning framework |
| torchvision | Image transforms and models |
| ResNet-50 | Backbone (ImageNet pretrained) |
| CASIA-WebFace | Training dataset |
| LFW | Evaluation benchmark |
| Google Colab T4 | Free GPU compute |
| Weights & Biases | Experiment tracking |
| scikit-learn | Metrics and data splitting |
| Matplotlib | Visualization |

---

## Model Architecture

**Training configuration:**
- Optimizer: SGD (backbone lr=0.001, head lr=0.01)
- Scheduler: CosineAnnealingLR
- Loss: CrossEntropyLoss
- Batch size: 64
- Epochs: 20
- Seed: 42

---

## EDA Highlights

- **Class imbalance** — mean 53.3 images/identity, std 56.3, range 20–390
- **Victim identity** — 29 images, ranked 94th out of 150 (below average)
- **Split** — 6,333 train / 788 val / 869 test
- **Victim train images** — 23 out of 6,333 (0.36% of training set)

---

## Upcoming Work — Checkpoint 2

- Build trigger injection engine (BadNets-style patch)
- Physical trigger simulation (Wenger et al. method)
- Poisoning rate sweep: 0.1% → 0.5% → 1% → 3% → 5%
- Measure ASR vs CA trade-off at each poisoning rate
- Defense evaluation: Neural Cleanse, Mahalanobis detection

---

## References

1. Y. Li et al., "Backdoor Learning: A Survey," IEEE TNNLS, 2024.
2. A. Le Roux et al., "Backdoor Attacks on Face Recognition Pipelines," IEEE SaTML, 2026.
3. E. Wenger et al., "Backdoor Attacks on Facial Recognition in the Physical World," CVPR, 2021.
4. D. Yi et al., "Learning Face Representation from Scratch," arXiv:1411.7923, 2014.

---

## Course Information

**Course:** CS 228 — Biometric Security with AI  
**Institution:** San Jose State University  
**Semester:** Spring 2026  
**Checkpoint:** 1 of 2  
**Due date:** April 6th, 2026
