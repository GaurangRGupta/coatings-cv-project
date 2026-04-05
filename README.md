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
