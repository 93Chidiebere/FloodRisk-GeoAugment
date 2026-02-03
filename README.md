# GeoAugment: Constraint-Aware Synthetic Geospatial Label Generation

This repository contains the code used in the study:

**“Constraint-Aware Synthetic Data Generation for Robust GeoAI in Data-Scarce Regions.”**

The project evaluates how **constraint-aware synthetic geospatial labels** influence GeoAI model behavior under label scarcity, with a focus on **robustness, uncertainty control, and failure-mode mitigation**, rather than peak predictive accuracy.

---

## Overview

Geospatial AI (GeoAI) systems deployed in underrepresented regions often suffer from sparse, biased, or incomplete labels. This repository provides:

- an implementation of **GeoAugment**, a constraint-aware synthetic label generation framework;
- regression and classification experiments for flood modeling;
- controlled comparisons between **real-only**, **synthetic-only**, and **mixed** supervision regimes.

The code is intended to support **reproducibility of experimental behavior**, not to provide a turnkey production system.

---

## Repository Structure

```text
├── notebooks/
│ ├── RegressionFloodRisk.ipynb
│ ├── ClassificationFloodExtent.ipynb
│
├── data/
│ └── .tif files (DEM and real flood labels)
│
├── README.md
```


---

## Data Sources

This study uses **publicly available geospatial datasets**.  
Raw datasets are **not included** in this repository due to size and licensing considerations.

### Digital Elevation Model (DEM)
- **Source:** NASA / USGS Shuttle Radar Topography Mission (SRTM)
- **Usage:** Terrain-derived features for flood modeling

### Flood Extent Labels
- **Source:** Copernicus Emergency Management Service (EMS)
- **Usage:** Observed flood extent labels (reference supervision)

All datasets correspond to **Lagos State, Nigeria**, a flood-prone, data-scarce urban region.

In the repository are the DEM.tif and the real flood labels.

---

## Synthetic Label Generation

Synthetic flood labels are generated using **GeoAugment**, which enforces:

- spatial continuity constraints,
- physical feasibility (e.g., downhill flow consistency),
- structural coherence of flood patterns.

---

## Experiments

Two downstream learning tasks are evaluated:

### 1. Flood Risk Regression
- Predicts continuous flood susceptibility values
- Metrics: Mean Squared Error (MSE), Mean Absolute Error (MAE)

### 2. Flood Extent Classification
- Binary flood / non-flood prediction
- Metrics: Accuracy, Precision, Recall, F1-score

For each task, three training regimes are compared:

| Model | Training Labels | Purpose |
|------|----------------|---------|
| Model A | Real-only | Baseline behavior |
| Model B | Synthetic-only | Structural prior evaluation |
| Model C | Real + Synthetic | Robustness and regularization analysis |

All models use identical architectures and training settings within each task.

---

## Evaluation Philosophy

Results are interpreted in terms of:
- robustness under label scarcity,
- exposure to feasible but unobserved geospatial states,
- changes in recall–precision trade-offs,
- reduction of overconfidence and brittle predictions.

Synthetic-only models are **not expected** to outperform real-only models.

---

## Reproducibility Notes

- Training/validation splits use a fixed random split for controlled comparison.
- No hyperparameter tuning is performed across label regimes.
- Results may vary slightly depending on hardware and software versions.

This code supports **methodological reproducibility**, not exact numerical replication across environments.

---
