# VisHKO: A Weather Image Dataset for Atmospheric Visibility Estimation

VisHKO is a real-world, sensor-anchored image dataset designed for **atmospheric visibility estimation** with deep learning.  
It consists of weather images captured by a **fixed webcam** near Hong Kong International Airport and annotated into **five visibility classes** (0–50 km) using the official **Hong Kong Observatory (HKO) visibility meter**.

This repository contains:

- The **VisHKO image dataset** .
- The **annotation files** and intermediate data used to build the labels.
- The **notebooks/scripts** implementing the complete collection and annotation pipeline.

---

## 1. Dataset Overview

- **Total images:** ~11,125  
- **Location:** Sha Lo Wan, near Hong Kong International Airport (HKG)  
- **Acquisition period:** ≈ 6 months (daytime conditions)  
- **Task:** Multiclass visibility classification  
- **Ground truth:** Numeric visibility values derived from the official HKO visibility meter  
- **Visibility classes:**

| Class     | Visibility range (km) |
|----------|------------------------|
| Bad      | 0–10                   |
| Low      | 10–20                  |
| Moderate | 20–30                  |
| Good     | 30–40                  |
| High     | 40–50                  |

VisHKO addresses the lack of real-scene, sensor-anchored datasets for visibility estimation, where most existing public benchmarks are synthetic or simulation-based.

---

## 2. Repository Structure

```text
.
├── Annotation_files/
├── Collected_data/
├── Scripts/
│   ├── Annotation_and_Classification.ipynb
│   ├── Data_scraping.ipynb
│   ├── Interpolation_model.ipynb
│   └── Time_Extraction.ipynb
├── VisHKO_Dataset/
│   ├── Bad
│   ├── Good
│   ├── High
│   └── Low
│   └── Moderate
├── Visibility_reading/
├── interp_model.joblib
```
---

### 2.1 Folders 

**VisHKO_Dataset/**
Final dataset of weather images, typically organised by visibility class (Bad/, Low/, Moderate/, Good/, High/).
This is the main folder used for training and evaluating deep learning models.

**Annotation_files/**
CSV files and auxiliary metadata produced during the annotation pipeline.
Each file typically contains two columns: Time and Visibility.

**Collected_data/**
Raw data collected from the HKO website and the webcam, grouped by day.

**Visibility_reading/**
HKO visibility curves, named by day.

**Scripts/**
Jupyter notebooks implementing the full pipeline:

Data_scraping.ipynb – downloads or collects the raw visibility plots and webcam images.

Time_Extraction.ipynb – extracts timestamps from images (e.g. via OCR) and normalises time formats.

Interpolation_model.ipynb – digitises the HKO visibility curves and trains the interpolation model that maps pixels to numeric visibility values.

Annotation_and_Classification.ipynb – merges all sources into final annotations and assigns visibility classes.

### 2.2 Files

**interp_model.joblib**
Saved interpolation model used to convert curve pixels into numeric visibility values.

## 3. Acknowledgements
The authors extend their sincere gratitude to the Hong Kong Observatory (HKO) for providing public imagery and visibility data that supported the creation of the VisHKO dataset.
