# Volatility-Index-Forecast

Forecasting the CBOE Volatility Index (VIX) for Apr 20-24, 2026 using an ARIMA + GJR-GARCH pipeline.

## Project Overview

This repository contains an end-to-end time-series workflow for short-horizon VIX forecasting.
The notebook covers:

- data collection from Yahoo Finance,
- preprocessing and diagnostics,
- mean-model selection with ARIMA,
- volatility modeling with GARCH-family models,
- rolling holdout evaluation, and
- final 5-day forecast generation with 95% prediction intervals.

Primary notebook:

- `VIX_final.ipynb`

Report files:

- `Report/Report_AI6123.tex`
- `Report/aaai2026.sty`
- `Report/aaai2026.bst`
- `Report/aaai2026.bib`

## Modeling Workflow (from `VIX_final.ipynb`)

1. **Data ingestion**
	- Pull VIX (`^VIX`) daily data using `yfinance`.
	- Align to daily calendar and fill missing values by time interpolation.

2. **Exploratory diagnostics**
	- Plot raw series, rolling trend proxy, decomposition, ACF/PACF.
	- Apply first differencing and stationarity checks (ADF, KPSS).

3. **Mean process modeling**
	- Compare ARIMA candidates by AIC/BIC.
	- Select **ARIMA(2,1,2)** as the primary mean specification.

4. **Residual and volatility diagnostics**
	- Evaluate ARIMA residuals with Ljung-Box and normality checks.
	- Test ARCH effects and fat-tail behavior.

5. **Conditional volatility modeling**
	- Fit and compare ARCH/GARCH-family variants.
	- Proceed with **GJR-GARCH(1,1)** using heavy-tailed innovations.

6. **Forecasting and evaluation**
	- Run rolling holdout forecasts and compute error metrics (MAE/RMSE/MAPE).
	- Refit on full sample and generate final forecasts for **Apr 20-24, 2026**.

## Environment and Dependencies

The notebook uses Python and common scientific packages:

- `numpy`, `pandas`
- `matplotlib`, `seaborn`
- `scipy`, `statsmodels`
- `scikit-learn`
- `yfinance`
- `arch`
- `tqdm`

Install dependencies (example):

```bash
pip install numpy pandas matplotlib seaborn scipy statsmodels scikit-learn yfinance arch tqdm
```

## How To Run

1. Open `VIX_final.ipynb`.
2. Run all cells in order.
3. Review:
	- stationarity and residual diagnostics,
	- model comparison tables,
	- holdout metrics,
	- final forecast table for Apr 20-24, 2026.

## Notes

- Forecast values and metrics depend on data download time and package versions.
- The notebook currently implements a VIX-focused pipeline.