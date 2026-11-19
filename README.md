# Stock Forecasting Tool

A tool for analyzing stocks and producing probabilistic price forecasts. The long-term goal is an
Android app where users follow stocks and see forecasts together with their uncertainty intervals.

> ⚠️ Not investment advice. Forecasts are statistical estimates with high uncertainty.

## Stage 1: Forecasting engine prototype (notebook)

[`notebooks/stock_forecast.ipynb`](notebooks/stock_forecast.ipynb)

- Downloads daily price data from Yahoo Finance (`yfinance`) and caches it in `data/`
- Forecasts the log return 5 trading days ahead with two models:
  - **ARIMA**: a statistical time-series model, orders selected by AIC
  - **Gradient Boosting**: a machine-learning model built on technical indicators (RSI, MACD,
    moving averages, volatility, volume), with quantile regression for prediction intervals
- Evaluates both models with a walk-forward backtest against a naive baseline
  (MAE, RMSE, direction accuracy, interval coverage)

## Running

```bash
pip install -r requirements.txt
jupyter notebook notebooks/stock_forecast.ipynb
```

Or run it from the command line:

```bash
python -m nbconvert --to notebook --execute notebooks/stock_forecast.ipynb --output stock_forecast.ipynb
```

Tickers and parameters can be changed in the first code cell (`TICKERS`, `HORIZON`, etc.).
A full run takes about 1.5 minutes.

## Roadmap

1. ✅ Forecasting model prototype and backtest
2. Move the functions into a Python package and add tests
3. Backend (FastAPI) that precomputes forecasts on a schedule
4. Android app (Kotlin, Jetpack Compose)
5. AI layer: a language model explains the analysis and news sentiment
