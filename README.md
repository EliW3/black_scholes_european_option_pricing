# Black-Scholes Option Pricing Script

This script calculates the theoretical price of European-style **Call and Put options** using the classical **Black-Scholes-Merton model**. It dynamically fetches historical stock data to calculate annualized volatility instead of requiring a manual volatility input.

---

## 🚀 Quick Start

### Prerequisites
Ensure you have Python installed along with the required libraries. Install them via terminal:
```bash
pip install numpy yfinance pandas scipy
```

### Usage
Import the function and execute it with your desired parameters:
```python
from bs_model import black_scholes_model

# Calculate a 3-month Call option for Apple (AAPL) at a $150 strike price
black_scholes_model(
    stock_name="AAPL", 
    time_until_expiration=0.25, 
    strike_price=150, 
    risk_free_rate=0.025, 
    option_type="call"
)
```

---

## ⚙️ Function Parameters

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `stock_name` | *str* | `"AAPL"` | Ticker symbol of the underlying asset. |
| `time_until_expiration` | *float* | `0.25` | Time to maturity in years (e.g., `0.25` = 3 months). |
| `strike_price` | *float* | `150` | The exercise price of the option contract. |
| `risk_free_rate` | *float* | `0.025` | Annualized risk-free interest rate (decimal format). |
| `option_type` | *str* | `"call"` | The contract type: `"call"` or `"put"`. |
| `data_period` | *int* | `1` | Historical lookback window in years to calculate volatility. |

---

## 🧠 How it Works

1. **Data Retrieval:** Downloads historical price data via the `yfinance` API using the `data_period` framework.
2. **Volatility Estimation:** 
   * Calculates the daily log returns of the asset.
   * Finds the standard deviation of those returns.
   * Multiplies by \(\sqrt{252}\) to annualize the volatility metric.
3. **Black-Scholes Formula:** Computes d₁ and d₂ using the asset's closing price (`Adj Close`), then calculates the exact options value using a cumulative standard normal distribution (N(x)).

---

## ⚠️ Model Assumptions

The Black-Scholes framework operates under specific idealized market conditions:
* **No Dividends:** The underlying asset pays no dividends during the option's lifespan.
* **Random Walk:** Market movements follow a random walk; prices cannot be predicted.
* **Frictionless Markets:** Zero transaction fees, broker commissions, or taxes.
* **Constant Variables:** Volatility and the risk-free rate remain completely static over time.
* **European Style:** Options cannot be exercised early; they can only be settled exactly at expiration.
