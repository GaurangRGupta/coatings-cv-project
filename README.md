# Coatings‑CV Project

Industrial computer vision for paint defects, corrosion, color/pigment learning, and synthetic data generation.

## Stack
- Windows + Conda for environment management
- uv for fast, reproducible package installation
- PyTorch ecosystem for modeling
- MLflow‑ready layout

## First steps (after cloning)
1. `conda create -n coatings-cv python=3.11 -y`
2. `conda activate coatings-cv`
3. `python -m pip install uv`
4. `uv pip install -r requirements.txt`
5. Copy `.env.example` to `.env` and fill in Kaggle/GitHub credentials.
6. Run `.\scripts\download_data.ps1` to fetch datasets.

# Coatings Intelligence: Paint Defect Inspection and Color Analysis

A computer vision portfolio project built around AkzoNobel's core domains of
surface protection, color quality, and coatings inspection.

---

## Project Structure

| Notebook | Phase | What it does |
|---|---|---|
| `01_eda.ipynb` | Data | Manifest creation, class distribution, image statistics |
| `02_augmentation.ipynb` | Data | Domain-aware augmentation pipeline with visual verification |
| `03_dataset_and_model.ipynb` | Model | Dataset class, EfficientNet-B0 setup, frozen head summary |
| `04_training.ipynb` | Training | 5-fold CV, fine-tuning with differential LRs, confusion matrix |
| `05_corrosion_detection.ipynb` | Detection | YOLOv8n bounding box detection on 268 corrosion images |
| `06_color_analysis.ipynb` | Color | LAB color analysis, ΔE perceptual distance, pigment classification |
| `07_gradcam.ipynb` | Interpretability | Grad-CAM visualisation, failure case analysis |

---

## Results Summary

| Task | Model | Metric | Result |
|---|---|---|---|
| Defect classification | EfficientNet-B0 (frozen) | CV Accuracy | 84.4% |
| Defect classification | EfficientNet-B0 (fine-tuned) | CV Accuracy | 88.9% |
| Corrosion detection | YOLOv8n | mAP@0.5 | 0.433 |
| Color classification | LAB + LogReg | CV Accuracy | 84.6% |
| Defect color baseline | LAB + LogReg | CV Accuracy | 37.8% |

---

## Central Finding

LAB color statistics achieve 84.6% accuracy on color classification but only
37.8% on defect classification. The 47-point gap proves that paint defects share
similar color profiles and differ primarily in surface texture. EfficientNet-B0
recovers this with 88.9% accuracy by learning texture features the color baseline
cannot access. LAB analysis and CNN features are complementary, not redundant.

Grad-CAM confirms the model attends to physically correct regions for 5 of 7
classes. One class (chalking) shows a spurious correlation with hand gestures
present in training images, a known failure mode of small-dataset learning.
Both misclassifications are low-confidence and physically interpretable.

---

## Setup

```bash
git clone <repo>
cd coatings-cv-project
pip install -r requirements.txt
```

Download datasets via Kaggle CLI:
```bash
kaggle datasets download <defect-dataset-slug> -p data/raw/
kaggle datasets download <corrosion-dataset-slug> -p data/raw/
kaggle datasets download <color-dataset-slug> -p data/raw/
```

---

## Why This Matters for Protective Coatings

- **Defect classification** enables automated quality inspection on production lines
- **Corrosion detection** localises corroded areas for targeted primer application
- **Color analysis in LAB** directly mirrors how paint industry colorimetry works
- **Grad-CAM** provides the explainability required for industrial deployment

---

## Tech Stack

Python 3.11 · PyTorch 2.11 · Ultralytics YOLOv8 · Albumentations ·
OpenCV · scikit-learn · MLflow · Git
