# 📈 Time Series Forecasting — AutoRegressive (AR) Model

Forecast daily minimum temperatures using a classical **AutoRegressive (AR)** model built with Python and `statsmodels`.

---

## 📁 Repository Structure

```
Time_Series_forecasting_AR_Model/
│
├── Time_Series_forecasting_AR_Model.ipynb   # Main notebook (corrected)
├── daily-min-temperatures.csv               # Dataset
├── requirements.txt                         # Python dependencies
├── plots/                                   # Auto-generated output plots
│   ├── 01_time_series.png
│   ├── 02_acf_pacf.png
│   ├── 03_test_prediction.png
│   └── 04_future_forecast.png
└── README.md
```

---

## 📊 Dataset

**Daily Minimum Temperatures in Melbourne, Australia (1981–1990)**

| Column | Description            |
|--------|------------------------|
| Date   | Daily date (YYYY-MM-DD)|
| Temp   | Min temperature in °C  |

Source: Classic time series benchmark dataset.

---

## 🔬 Methodology

| Step | Description |
|------|-------------|
| 1 | Load & visualize the time series |
| 2 | Test stationarity with the **ADF test** |
| 3 | Determine AR lag order using **PACF / ACF** plots |
| 4 | Split into **train** (all but last 7 days) and **test** (last 7 days) |
| 5 | Fit **AutoReg** model with `lags=20` |
| 6 | Predict on test set (`dynamic=False`) and compute **RMSE & MAE** |
| 7 | Forecast the next **7 future days** (`dynamic=True`) |

---

## ⚙️ Setup & Usage

### 1. Clone the repository
```bash
git clone https://github.com/<your-username>/Time_Series_forecasting_AR_Model.git
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

---

## 📦 Requirements

See `requirements.txt` for the full list. Key libraries:

- `pandas` — data loading & manipulation
- `numpy` — numerical operations
- `matplotlib` — visualizations
- `statsmodels` — AR model, ADF test, ACF/PACF
- `scikit-learn` — RMSE / MAE metrics

---

## 🐛 Bugs Fixed (vs. original)

| # | Bug | Fix Applied |
|---|-----|-------------|
| 1 | `AR` (deprecated) imported alongside `AutoReg` | Removed deprecated `AR` import |
| 2 | `IndentationError` in ADF test cell | Fixed indentation |
| 3 | ACF/PACF plotted separately without `ax=` | Plotted side-by-side with `subplots` |
| 4 | `pred` had no datetime index — misaligned plot | Added `pred.index = test.index` |
| 5 | Future forecast used `dynamic=False` incorrectly | Changed to `dynamic=True` |
| 6 | Future predictions had no datetime axis | Added `pd.date_range` index |
| 7 | Future predictions not visualized | Added forecast plot with date axis |

---

## 📄 License

MIT License — free to use, modify, and distribute.
