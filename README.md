# Volatility Forecast API (GARCH) — FastAPI

## Overview
This project provides a lightweight **volatility forecasting API** based on **GARCH(p,q)** models.
It is designed to help analysts, traders, and risk managers **monitor, forecast, and operationalize market volatility**.

The API exposes two core endpoints:
- **POST `/fit`**: trains a GARCH model for a given ticker and persists it to disk
- **POST `/predict`**: loads the latest trained model and returns a forward volatility forecast

## Why it matters
Volatility forecasting is a foundational component of quantitative finance and risk management.

This project can be used for:
- volatility regime detection
- risk monitoring and stress testing
- position sizing and hedging decisions
- scenario analysis and forward-looking risk metrics

The goal is not price prediction, but **risk-aware decision making**.

## Tech stack
- Python
- FastAPI + Pydantic (API & schema validation)
- SQLite (local data persistence)
- `arch` (GARCH modeling)
- joblib (model serialization)
- Yahoo Finance (market data ingestion)


## Project workflow

1. Fetch historical price data for a given ticker
2. Compute log-returns
3. Fit a GARCH(p,q) model on historical returns
4. Persist the trained model
5. Generate forward volatility forecasts via API calls

## Quickstart

### 1) Install dependencies
```bash
pip install -r requirements.txt
