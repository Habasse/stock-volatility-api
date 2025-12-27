# Volatility Forecast API (GARCH) - FastAPI

## Overview
The project supplies a simple **volatility forecasting API** with implementations of **GARCH(p,q) models**.

It is meant to aid analysts, traders, and risk managers in **monitoring, forecasting, and operationalizing volatility in markets**.
There are two major functions provided by the API. These are

- **POST `/fit`**: trains a GARCH model for a specific ticker and saves the model to file

- **POST /predict**: loads the last trained model and generates a forecast of the forward volatility price


## Why It Matters
Forecasting volatility is an essential area in the framework of quantitative finance and risk management..
This project can be utilized for:

- volatility regime identification
- risk monitoring & stress testing
- Position sizing and hedging strategy
- Scenario analysis and forward-looking risk metrics
  
Price forecasting is not the aim; instead, **risk-informed decision-making is the focus.**


# Tech stack
- Python
- FastAPI + Pydantic (API and schema validation)
- SQLite (Local Data Storage)
- `arch` (GARCH modeling)
- joblib (model serialization)
- Yahoo Finance (Ingestion of market data)

## Workflow of the Project

1. Retrieval of historical stock prices for a specific stock ticker
2. Log-returns
3. Estimating a GARCH model of order (p,q) based
4. Persist the trained model
5. Create forward volatility predictions through API calls

## Quickstart

### Example API Usage

### Train a GARCH model

POST `/fit`

```json
{
  "ticker": "GOOG",
  "n_observations": 2500,
  "p": 1,
  "q": 1
}

Response:
{
  "success": true,
  "message": "Model trained and saved."
}

### 1) Install dependencies
```bash
pip install -r requirements.txt
