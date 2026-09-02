# Capacity-Weighted Geospatial Virtual Wind Station (GVWS)

A research project exploring whether weather data can be represented more effectively for aggregate UK wind-generation modelling and day-ahead forecasting.

---

## Why I Did This Project

Wind generation plays an increasingly important role in the UK electricity system, but forecasting national wind output remains challenging because weather conditions vary significantly across the country.

Most forecasting studies focus on improving machine-learning models. I wanted to investigate a different question:

> Are we representing the weather itself in the best possible way before we even start forecasting?

To answer this, I developed a **Capacity-Weighted Geospatial Virtual Wind Station (GVWS)**, a synthetic weather series that gives greater influence to locations containing more installed wind capacity.

---

## Project Overview

The project combines:

- NESO aggregate wind-generation data
- ERA5 meteorological reanalysis data
- Renewable Energy Planning Database (REPD) wind-farm metadata

The workflow consists of:

1. Processing generation and weather data
2. Mapping wind farms to ERA5 grid cells
3. Creating three weather representations
4. Validating each representation
5. Applying the best representation to 24-hour-ahead forecasting
6. Investigating the impact of target-horizon weather information

---

## Weather Representations

Three meteorological representations were compared:

### UK Mean

A simple national weather average using all ERA5 grid cells.

### Wind-Farm Mean

An average using only ERA5 cells associated with operational wind farms.

### Capacity-Weighted GVWS

A weighted average where the contribution of each ERA5 cell is based on the installed wind capacity located within that cell.

This was the proposed representation developed in the project.

---

## Forecasting Models

The following forecasting approaches were evaluated:

### Benchmarks

- Persistence
- Physical Power Curve
- ARIMA

### Machine Learning

- XGBoost
- LightGBM

### Deep Learning

- LSTM
- BiLSTM

---

## Key Results

### Representation Validation

| Representation | R² |
|---------------|------|
| UK Mean | 0.872 |
| Wind-Farm Mean | 0.907 |
| Capacity-Weighted GVWS | **0.931** |

The GVWS produced the strongest representation of the weather–generation relationship.

---

### Best Day-Ahead Forecasting Result

| Model | Test R² |
|---------|---------|
| BiLSTM | **0.308** |

BiLSTM achieved the strongest rolling 24-hour-ahead forecasting performance among the evaluated models.

---

### Weather Timing Benchmark

| Scenario | R² |
|----------|------|
| Current Weather | 0.075 |
| Perfect Future Weather | 0.668 |

The largest performance improvement came from providing weather information aligned with the forecast target time rather than changing the forecasting model itself.

---

## Main Takeaway

The most important finding of the project was:

> Improving meteorological representation helped, but access to target-horizon weather information had a much larger impact on forecasting performance than changing model architecture.

This suggests that future work should focus on integrating archived Numerical Weather Prediction (NWP) forecasts rather than only developing more complex machine-learning models.

---

## Technologies Used

- Python
- Pandas
- NumPy
- GeoPandas
- Xarray
- Scikit-learn
- XGBoost
- LightGBM
- TensorFlow / Keras
- Matplotlib

---

## Future Work

Possible extensions include:

- Archived operational NWP forecasts
- Dynamic capacity weighting
- Regional GVWS representations
- Probabilistic forecasting
- Curtailment-aware forecasting

---

## Dissertation

The full dissertation and viva presentation are available in the 
