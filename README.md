# Weather Effects on Flemish Bicycle Counts (2023–2025)

**Modern Data Analysis — Group 6**  
Chenyu Zhang · Mufan Cheng · Qiaoqiao Zhang · Yuxuan Zhu  

## Overview
This project analyses how weather conditions affect cycling demand across Flemish bicycle counting stations managed by AWV (Agentschap Wegen en Verkeer). Using a station-day panel dataset for 2023–2025, we examine the nonlinear effects of temperature, precipitation, wind speed, humidity, and sunshine duration on bicycle counts, and quantify weather sensitivity and resilience across 87 counting sites. Findings aim to support evidence-based prioritisation of cycling infrastructure investments.

## Research Questions
1. How do hourly weather conditions associate with bicycle counts, and are these effects nonlinear or lagged?
2. Which counting stations are most weather-sensitive versus resilient, after controlling for holidays and temporal patterns?
3. Which commuting corridors should be prioritised for infrastructure improvements (shelter, drainage, winter maintenance)?

## Repository Structure

```
├── notebooks/
│   ├── 01_coverage_analysis.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_panel_construction.ipynb
│   ├── 04_weather_data.ipynb
│   ├── 05_merge_and_calendar.ipynb
│   ├── 06_site_classification.ipynb
│   ├── 07_eda.ipynb
│   ├── 08_gam_model.ipynb
│   ├── 09_sensitivity_analysis.ipynb
│   └── 10_leuven_totem_case.ipynb
└── outputs/
    └── figures/
```

## Data Setup

Raw data is not tracked in this repository due to file size. The complete `data/` folder (raw cycling CSVs, weather cache, and processed parquet files) is available on Google Drive:

**[Download data folder](https://drive.google.com/drive/folders/1CkxJ5tIkG1gALc8s6j5HPPHI209qDyg6)**

Download and place the contents under `data/` in the project root, then run notebooks 01–10 in order to reproduce all results.

Alternatively, you can fetch the data from source manually:

- **Cycling counts**: monthly CSV files from [AWV Datavindplaats](https://datavindplaats.vlaanderen.be/)  
  → place under `data/raw/cycling/` (organised by year, e.g. `2023/data-2023-01.csv`)
- **Weather data**: fetched from [Open-Meteo](https://open-meteo.com/) (free, no API key required)  
  → run `notebooks/04_weather_data.ipynb` to fetch and cache locally

**Python version**: 3.12.11 Install dependencies with:
```bash
pip install -r requirements.txt
```

## Methods

- **Models**: Generalized Additive Models (GAMs) with site fixed effects
- **Controls**: weekends, Belgian public holidays, Flemish school holidays, KU Leuven academic calendar
- **Output**: weather-normalized cycling index and station-level weather sensitivity metrics

## Tools

| Package | Purpose |
|---|---|
| `pandas`, `numpy` | Data ingestion, cleaning, panel construction |
| `geopandas`, `shapely` | Spatial operations, nearest-station matching |
| `pyGAM`, `statsmodels` | Statistical modelling |
| `matplotlib` | Visualization |
