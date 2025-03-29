# 🔄 Modeling Chicago Bike Usage with Prophet

Modeling daily Divvy bike ride volume in Chicago using Facebook's Prophet time series model, enriched with weather data to explore how temperature, precipitation, and visibility impact rider behavior.

<img src="https://raw.githubusercontent.com/eledon/Modeling-Chicago-Bike-Usage-with-Prophet/main/sawyer-bengtson-tnv84LOjes4-unsplash.jpg" width="500" height="300"/>

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

This project analyzes and models **daily Divvy bike usage in Chicago**, incorporating weather features to better understand rider behavior. Using Facebook Prophet with external regressors, the model captures seasonal and holiday trends and evaluates predictive performance using residual diagnostics.

---

## 🧪 Technologies

- **Language:** Python
- **Libraries:** `prophet`, `pandas`, `matplotlib`, `seaborn`, `scikit-learn`, `statsmodels`
- **Models:** Prophet with additive & multiplicative seasonalities and weather covariates

---

## ❓ Research Questions

- How do temperature, precipitation, and visibility affect daily bike usage?
- Are weekends and holidays associated with higher or lower ride volumes?
- Can we identify consistent seasonal patterns in bike-sharing activity?
- Does the Prophet model adequately capture these dynamics?
- What is the typical range of prediction error (MAE, RMSE, MAPE)?

---

## 📊 Dataset

- **Divvy Bike Data:** [Divvy System Data](https://divvybikes.com/system-data)
- **Weather Data:** [Visual Crossing Weather API](https://www.visualcrossing.com/resources/documentation/weather-data/getting-started-with-weather-data-services/)
- **Frequency:** Daily
- **Time Frame:** 2023–2024
- **Variables:** 
  - Target: Daily casual and member rides
  - Regressors: `feelslike`, `cloudcover`, `precipcover`, `snowdepth`, `visibility`

---

## 🧠 Methodology

### 1. Data Preparation
- Merging bike data with daily weather observations
- Missing value handling and alignment
- Train/test split for final 30-day evaluation

### 2. Exploratory Analysis
- Time series plots, histogram, Q-Q plot, rolling statistics
- Visual analysis of variance and seasonality

### 3. Model Building with Prophet
- Regressors: `feelslike`, `cloudcover`, `precipcover`, `snowdepth`, `visibility`
- Tuned parameters: `changepoint_prior_scale`, `seasonality_prior_scale`
- Custom weekly seasonality added (Fourier order = 5 or 7)

### 4. Diagnostics and Evaluation
- ACF & PACF of residuals
- Ljung-Box test for autocorrelation
- One-sample t-test for residual mean = 0
- Metrics: MAE, RMSE, MAPE

---

## 📊 Results

| Model                    | RMSE     | MAE      | MAPE    | Notes                          |
|-------------------------|----------|----------|---------|--------------------------------|
| Prophet (tuned)         | 1228.95  | 941.38   | 46.04%  | ✅ Best-performing configuration |

<p align="left">
  <img src="forecast_plot.png" width="600" alt="Forecast Plot">
</p>

<p align="center"><em>Figure: Actual vs Predicted bike rides with 95% confidence interval</em></p>

---

## ⚙️ Getting Started

To run this project locally:

```bash
pip install prophet pandas matplotlib seaborn scikit-learn statsmodels
