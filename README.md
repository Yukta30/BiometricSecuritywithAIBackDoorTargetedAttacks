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
