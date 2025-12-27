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

### 1) Install dependencies
```bash
pip install -r requirements.txt
````

### 2) Run the API

```bash
uvicorn app.main:app --reload
```

Open your browser at:

[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## Example API Usage

### Train a GARCH model

**POST** `/fit`

```json
{
  "ticker": "GOOG",
  "n_observations": 2520,
  "p": 1,
  "q": 1
}
```

Example response:

```json
{
  "success": true,
  "message": "Model trained and saved."
}
```

---

### Forecast volatility

**POST** `/predict`

```json
{
  "ticker": "GOOG",
  "n_days": 5
}
```

Example response:

```json

{
  "ticker": "GOOG",
  "n_days": 5,
  "success": true,
  "forecast": {
    "2025-12-29": 1.787,
    "2025-12-30": 1.788
  }
```
## Project Structure

```text
stock-volatility-api/
├─ app/
│  ├─ __init__.py
│  ├─ main.py          # FastAPI app and routes
│  ├─ schemas.py       # Pydantic request/response models
│  ├─ model.py         # GARCH model logic
│  ├─ data.py          # Data ingestion (Yahoo Finance, SQLite)
│  └─ config.py        # Configuration settings
├─ models/             # Saved trained models (.pkl)
├─ scripts/
│  └─ demo_client.py   # Example API client
├─ notebooks/
│  └─ demo_api.ipynb   # Exploration and testing
├─ tests/
│  └─ test_smoke.py    # Basic API tests
├─ requirements.txt
├─ .gitignore
└─ README.md

## Possible extensions
- Add EGARCH / GJR-GARCH models
- Add VaR and Expected Shortfall endpoints
- Deploy API to a cloud provider
