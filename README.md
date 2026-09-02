# Development and Validation of a Capacity-Weighted Geospatial Virtual Wind Station (GVWS) for Wind Power Modelling and Day-Ahead Forecasting in the UK

## Overview

This project investigates how meteorological data should be represented when modelling and forecasting aggregate UK wind generation.

Traditional national weather representations often use simple averages across large geographical areas. However, wind generation capacity is not distributed equally across the UK. This project introduces a **Capacity-Weighted Geospatial Virtual Wind Station (GVWS)** that weights weather conditions according to the installed wind capacity associated with each ERA5 grid cell.

The research evaluates whether capacity weighting improves the relationship between meteorological conditions and aggregate UK wind generation and investigates the impact of weather information availability on rolling 24-hour-ahead forecasting.

---

## Research Questions

1. Does restricting weather aggregation to wind-farm grid cells improve representation relative to a national weather mean?
2. Does weighting wind-farm grid cells by installed capacity further improve representation?
3. How effectively can GVWS-derived information support rolling 24-hour-ahead forecasting?
4. How much additional predictive information is available when weather at the target horizon is perfectly known?

---

## Data Sources

### NESO Aggregate Wind Generation
- Aggregate UK wind generation
- Target variable used for modelling and forecasting

### ERA5 Reanalysis
- Wind speed
- Wind direction
- Air density
- Relative humidity
- Boundary-layer height
- Cloud cover
- Precipitation
- Solar radiation
- Gust speed

### Renewable Energy Planning Database (REPD)
- Wind-farm locations
- Installed capacity
- Technology type
- Operational status

---

## Methodology

### Step 1: Data Processing

```text
NESO
+
ERA5
+
REPD
        ↓
Cleaning & Alignment
```

### Step 2: Geospatial Processing

```text
Wind Farms
        ↓
Nearest ERA5 Cell Mapping
        ↓
Capacity Aggregation
        ↓
Capacity Weights
```

### Step 3: Meteorological Representations

```text
UK Mean
Wind-Farm Mean
GVWS
```

### Step 4: Representation Validation

```text
Weather(t)
        ↓
Predict
        ↓
WIND(t)
```

### Step 5: Rolling Day-Ahead Forecasting

```text
Weather(t)
+
Historical Information
        ↓
Predict
        ↓
WIND(t+24)
```

### Step 6: Weather-Timing Benchmark

```text
Current Weather:
Weather(t)
→ WIND(t+24)

Perfect Future Weather:
Weather(t+24)
→ WIND(t+24)
```

---

## Models

### Baselines
- Persistence
- Physical Power Curve
- ARIMA

### Tree-Based Models
- XGBoost
- Tuned XGBoost
- LightGBM
- Tuned LightGBM

### Deep Learning Models
- LSTM
- BiLSTM

---

## Key Results

### Representation Validation

| Representation | MAE (MW) | RMSE (MW) | R² |
|---------------|-----------|-----------|------|
| UK Mean | 1205.14 | 1546.39 | 0.8721 |
| Wind-Farm Mean | 1024.51 | 1315.59 | 0.9075 |
| Capacity-Weighted GVWS | **889.92** | **1134.81** | **0.9311** |

### Best Day-Ahead Forecasting Results

| Model | Test R² | MAE (MW) | RMSE (MW) |
|---------|---------|---------|---------|
| BiLSTM | **0.3084** | **2847.89** | **3498.49** |
| Tuned XGBoost | 0.2644 | 2863.89 | 3549.10 |
| Tuned LightGBM | 0.2600 | 2859.49 | 3550.33 |

### Weather-Timing Benchmark

| Scenario | R² |
|------------|------|
| Current Weather | 0.0747 |
| Perfect Future Weather | 0.6682 |

### Main Finding

The largest improvement came not from changing forecasting algorithms but from providing atmospheric information at the forecast target time.

---

## Repository Structure

```text
project/
│
├── notebooks/
│   ├── 01_data_processing.ipynb
│   ├── 02_era5_processing.ipynb
│   ├── 03_gvws_construction.ipynb
│   ├── 04_feature_engineering.ipynb
│   ├── 05_tree_models.ipynb
│   ├── 06_lstm_bilstm.ipynb
│   └── 07_weather_benchmark.ipynb
│
├── figures/
│
├── outputs/
│
├── docs/
│   ├── dissertation.pdf
│   └── presentation.pdf
│
├── requirements.txt
│
└── README.md
```

---

## Technologies Used

- Python
- Pandas
- NumPy
- GeoPandas
- Xarray
- Matplotlib
- Scikit-learn
- XGBoost
- LightGBM
- TensorFlow / Keras
- Statsmodels

---

## Limitations

- ERA5 is a reanalysis dataset rather than operational NWP.
- Capacity weights remain static through the study period.
- One national GVWS may hide regional meteorological differences.
- Curtailment and turbine availability were not explicitly modelled.
- The perfect-future-weather benchmark is an upper-bound experiment rather than an operational forecast.

---

## Future Work

- Archived operational NWP forecasts
- Dynamic capacity weighting
- Regional GVWS models
- Probabilistic forecasting
- Curtailment-aware forecasting
- Operational deployment assessment

---

## Dissertation

The complete MSc dissertation is available in:

```text
docs/dissertation.pdf
```

---

## Author

**Golshan K. Yakkha**

MSc Data Science  
University of East London
