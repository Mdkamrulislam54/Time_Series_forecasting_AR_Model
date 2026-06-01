# 📈 Time Series Forecasting — AutoRegressive (AR) Model

> Forecasting daily minimum temperatures using a classical **AutoRegressive (AR)** model built with Python and `statsmodels`.

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![statsmodels](https://img.shields.io/badge/statsmodels-0.13%2B-orange)](https://www.statsmodels.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📁 Repository Structure

```
Time_Series_forecasting_AR_Model/
│
├── Time_Series_forecasting_AR_Model.ipynb   # Main notebook (corrected & improved)
├── daily-min-temperatures.csv               # Dataset
├── requirements.txt                         # Python dependencies
├── plots/                                   # Output plots (auto-saved on run)
│   ├── 01_time_series.png
│   ├── 02_acf_pacf.png
│   ├── 03_test_prediction.png
│   └── 04_future_forecast.png
└── README.md
```

---

## 📊 Dataset

**Daily Minimum Temperatures in Melbourne, Australia (1981–1990)**

| Column | Type | Description |
|--------|------|-------------|
| `Date` | datetime | Daily date (YYYY-MM-DD) |
| `Temp` | float | Minimum temperature in °C |

- **Total records:** 3,650 days (10 years)
- **Source:** Classic time series benchmark dataset widely used in ML/forecasting literature

---

## 🔬 Methodology & Pipeline

```
Raw Data → Stationarity Check → Lag Selection → Train/Test Split
    → Fit AutoReg → Evaluate (RMSE/MAE) → Future Forecast
```

| Step | Description |
|------|-------------|
| **1. Visualize** | Plot the full time series to observe trends and seasonality |
| **2. ADF Test** | Augmented Dickey-Fuller test to confirm stationarity |
| **3. ACF / PACF** | Identify the optimal AR lag order `p` |
| **4. Split** | Train on all data except the last 7 days; test on last 7 days |
| **5. AutoReg** | Fit `AutoReg(lags=20)` from `statsmodels` |
| **6. Evaluate** | Compute RMSE and MAE on the test set |
| **7. Forecast** | Predict the next 7 days beyond the dataset |

---

## 📉 Step 1 — Time Series Visualization

The raw daily minimum temperature data spans 10 years (1981–1990). A strong **annual seasonal pattern** is visible, which is expected for temperature data.

![Daily Minimum Temperatures](https://raw.githubusercontent.com/Mdkamrulislam54/Time_Series_forecasting_AR_Model/f16cc6a8c36fa7660c87ceb9e8f65bb82fd00b5f/Time%20Series.png)

> The series shows clear seasonality with no obvious upward/downward trend — a good candidate for an AR model after confirming stationarity.

---

## 🔬 Step 2 & 3 — Stationarity Check & Lag Selection (ACF / PACF)

**ADF Test** confirms the series is stationary (p-value < 0.05), so no differencing is needed.

**PACF** is then used to determine the number of lags (`p`) for the AR model — significant spikes up to lag ~20 guided our choice of `lags=20`.

![ACF and PACF](https://raw.githubusercontent.com/Mdkamrulislam54/Time_Series_forecasting_AR_Model/f16cc6a8c36fa7660c87ceb9e8f65bb82fd00b5f/Acf_Pacf.png)

> **Reading the plots:**
> - **PACF (left):** Direct correlation at each lag → used to pick AR order `p`
> - **ACF (right):** Cumulative autocorrelation → useful for MA order in ARMA/ARIMA

---

## 🔮 Step 7 — 7-Day Future Forecast

After evaluating on the test set, the model is extended to forecast the **next 7 days** beyond the entire dataset using `dynamic=True` (recursive prediction mode).

![7-Day Future Forecast](https://raw.githubusercontent.com/Mdkamrulislam54/Time_Series_forecasting_AR_Model/f16cc6a8c36fa7660c87ceb9e8f65bb82fd00b5f/AR%20Model-%207%20Day%20Future%20Forecast.png)

> The forecast (green dashed line) extends naturally from the historical trend. The vertical line marks the boundary between observed data and the forecasted window.

---

## ⚙️ Setup & Usage

### 1. Clone the repository
```bash
git clone https://github.com/Mdkamrulislam54/Time_Series_forecasting_AR_Model.git
cd Time_Series_forecasting_AR_Model
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the notebook
```bash
jupyter notebook Time_Series_forecasting_AR_Model.ipynb
```

> All plots are auto-saved to the `plots/` folder when you run the notebook.

---

## 📦 Requirements

```
pandas>=1.3.0
numpy>=1.21.0
matplotlib>=3.4.0
statsmodels>=0.13.0
scikit-learn>=0.24.0
jupyter>=1.0.0
```

---

## 🐛 Bugs Fixed (vs. Original Notebook)

| # | Bug | Fix Applied |
|---|-----|-------------|
| 1 | `AR` (deprecated) imported alongside `AutoReg` | Removed deprecated `AR` import |
| 2 | `IndentationError` in ADF test cell | Fixed indentation |
| 3 | ACF/PACF plotted separately without `ax=` | Plotted side-by-side with `subplots` |
| 4 | `pred` had no datetime index — misaligned x-axis | Added `pred.index = test.index` |
| 5 | Future forecast used `dynamic=False` incorrectly | Changed to `dynamic=True` |
| 6 | Future predictions had no datetime axis | Added `pd.date_range` index |
| 7 | Future predictions not visualized | Added full forecast plot with date axis |

---

## 📄 License

MIT License — free to use, modify, and distribute.
