readme_text = """
# 🔄 Modeling Chicago Bike Usage with Prophet

Modeling daily Divvy bike ride volume in Chicago using Facebook's Prophet time series model, enhanced with weather data and holidays to forecast demand and understand how rider behavior varies between members and casual users.

<img src="https://raw.githubusercontent.com/eledon/Modeling-Chicago-Bike-Usage-with-Prophet/main/sawyer-bengtson-tnv84LOjes4-unsplash.jpg" width="600" height="300"/>

[📘 View Full Report (Final_Report.ipynb)](https://github.com/eledon/Modeling-Chicago-Bike-Usage-with-Prophet/blob/main/Final_Report.ipynb)

![Python](https://img.shields.io/badge/Python-Prophet-blue?logo=python)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Model](https://img.shields.io/badge/Model-Prophet%20with%20Regressors-yellowgreen)
![Data](https://img.shields.io/badge/Data-Divvy%20%2B%20Weather-orange)

---

## 📘 Table of Contents
- [Overview](#overview)
- [Technologies](#technologies)
- [Research Questions](#research-questions)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Results](#results)
- [Getting Started](#getting-started)
- [Next Steps](#next-steps)
- [Contact](#contact)

---

## 🧭 Overview

This project analyzes and forecasts **daily Divvy bike usage in Chicago**, focusing separately on **members** and **casual users**. We examine how usage varies across weekdays, weekends, holidays, and weather conditions.  
We compare two time series models — **SARIMA** and **Prophet** — and evaluate which best captures the underlying structure and future trends in ride volume. The model forecasts the final month in the dataset — **November 2024** — as an out-of-sample period.

---

## 🧪 Technologies

- **Language:** Python  
- **Libraries:** `prophet`, `pandas`, `matplotlib`, `seaborn`, `scikit-learn`, `statsmodels`, `pmdarima`  
- **Models:** SARIMA (baseline), Prophet with holiday and weather regressors  

---

## ❓ Research Questions

### Exploratory (EDA):
- How do riding behaviors differ between members and casual users?
- Are there consistent seasonal and weekly usage patterns?
- Do weather and holidays significantly affect ride volume?

### Predictive (Modeling):
- Can we accurately forecast daily bike rides for each rider group?
- Which external factors improve prediction accuracy?
- How does Prophet perform compared to SARIMA?

---

## 📊 Dataset

- **Divvy Trip Data:** [Divvy System Data](https://divvybikes.com/system-data)  
- **Weather Data:** [Visual Crossing](https://www.visualcrossing.com/resources/documentation/weather-data/getting-started-with-weather-data-services/)  
- **Holiday Data:** Manually created U.S. holiday list  
- **Time Frame:** January 2023 – November 2024  
- **Features:**
  - Target: Daily member and casual rides  
  - Regressors: `feelslike`, `cloudcover`, `precipcover`, `snowdepth`, `visibility`  

---

## 🧠 Methodology

### 1. Exploratory Data Analysis
- Plots by day of week, season, and user type  
- Histogram & Q-Q plots of ride distribution  
- Statistical tests including t-tests, Ljung-Box test (for autocorrelation), and the ADF test (for stationarity)

### 2. Baseline Model: SARIMA
We used SARIMA as a benchmark model to capture seasonality and short-term autocorrelation in the daily ride data. The model was fitted using `auto_arima()` with a weekly seasonal period (m = 7), as day-of-week patterns were clearly observed in the EDA. The best parameters were automatically selected based on AIC.

### 3. Prophet Modeling
We selected Prophet due to its strengths in modeling seasonal trends, holidays, and incorporating external regressors. We added U.S. holidays and weather-based features as additional regressors. The weekly seasonality component was fine-tuned with a Fourier order of 5, and changepoint and seasonality priors were adjusted to optimize fit.

### 4. Residual Diagnostics and Model Evaluation
For each model, we performed:
- Residual autocorrelation checks (ACF, PACF)
- Ljung-Box test to assess white noise
- One-sample t-test for bias detection
- Evaluation of residual distribution shape (normality, skewness, kurtosis)

---

## 📊 Results

### 📍 Forecasting Accuracy

| Model                    | RMSE     | MAE      | MAPE     | Relative MAE | Notes                            |
|-------------------------|----------|----------|----------|---------------|----------------------------------|
| **SARIMA (Members)**    | 5541.72  | 4670.92  | 104.67%  | 0.45          | High error, poor generalization |
| **Prophet (Members)**   | 1111.40  | 865.89   | 15.72%   | 0.08          | ✅ Best performance overall       |
| **Prophet (Casual Users)** | 1193.06  | 974.49   | 46.81%   | 0.16          | Good absolute accuracy, high MAPE |

### 📌 Interpretation of Metrics
- **MAE (Mean Absolute Error)**: Average absolute difference between predicted and actual values.  
- **RMSE (Root Mean Squared Error)**: Like MAE but penalizes larger errors more.  
- **MAPE (Mean Absolute Percentage Error)**: Shows average error as a % of actual rides — sensitive to low-volume days.  
- **Relative MAE**: Calculated as MAE divided by the mean of actual values. This gives a normalized error relative to average ride volume.

> Prophet outperformed SARIMA significantly for both rider types, especially for members, with far lower error metrics and better-calibrated residuals. MAPE was higher for casual users due to the unpredictability of their rides on holidays and weekends, but absolute error remained low.

---

### 📈 Forecast Plots

<p align="left">
  <img src="https://github.com/eledon/Modeling-Chicago-Bike-Usage-with-Prophet/blob/main/Member_forecast.jpg" width="540" alt="Member Forecast">
  <br>
  <em>Figure: Member ride forecast (actual vs predicted with 95% CI)</em>
</p>

<p align="left">
  <img src="https://github.com/eledon/Modeling-Chicago-Bike-Usage-with-Prophet/blob/main/Casual_forecast.jpg" width="540" alt="Casual Forecast">
  <br>
  <em>Figure: Casual ride forecast (actual vs predicted with 95% CI)</em>
</p>
"""
