# 🔄 Modeling Chicago Bike Usage with Prophet

Modeling daily Divvy bike ride volume in Chicago using Facebook's Prophet time series model, enhanced with weather data and holidays to forecast demand and understand how rider behavior varies between members and casual users.

<img src="https://raw.githubusercontent.com/eledon/Modeling-Chicago-Bike-Usage-with-Prophet/main/sawyer-bengtson-tnv84LOjes4-unsplash.jpg" width="600" height="300"/>

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
We compare two time series models — **SARIMA** and **Prophet** — and evaluate which best captures the underlying structure and future trends in ride volume.

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
- Statistical tests (t-test, Ljung-Box, ADF)

### 2. Baseline Model: SARIMA
- Fitted using `auto_arima()`
- Weekly seasonality (m=7)
- Evaluated using MAE, RMSE, MAPE

### 3. Prophet Modeling
- Added weather regressors and holidays
- Tuned changepoint and seasonality priors
- Custom weekly seasonality (Fourier order = 5)
- Separate models for members and casuals

### 4. Residual Diagnostics
- ACF, PACF, Ljung-Box (autocorrelation)
- One-sample t-test (bias)
- Residual plots and component inspection

---

## 📊 Results

- EDA confirmed that **casual users ride more on weekends**, while **members ride more on weekdays**.
- A two-sample t-test showed these usage patterns are **statistically significant**.
- STL decomposition revealed clear **seasonality and long-term trends**.
- Prophet outperformed SARIMA across all accuracy metrics and had well-behaved residuals.

| Model                    | RMSE     | MAE      | MAPE     | Relative MAE | Notes                            |
|-------------------------|----------|----------|----------|---------------|----------------------------------|
| SARIMA (Members)        | 5541.72  | 4670.92  | 104.67%  | 0.45          | High error, poor generalization |
| Prophet (Members)       | 1111.40  | 865.89   | 15.72%   | 0.08          | ✅ Best performance overall       |
| Prophet (Casual Users)  | 1228.95  | 941.38   | 46.04%   | 0.16          | Strong performance               |

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

---

## ⚙️ Getting Started

To run this project locally:

```bash
pip install prophet pandas matplotlib seaborn scikit-learn statsmodels pmdarima
