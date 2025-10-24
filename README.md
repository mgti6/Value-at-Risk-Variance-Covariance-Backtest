# 📊 Value-at-Risk (VaR) – Variance-Covariance Backtest

This project implements the **1-day 99% Value at Risk (VaR)** using the **variance-covariance (model building) approach**.  
It also includes a **rolling-window backtest** to evaluate the model’s accuracy following **Hull’s methodology**, as well as the **Kupiec unconditional coverage test** to statistically validate the results.

---

## 🧠 Overview

The goal of this notebook is to:
- Estimate the **daily portfolio VaR** based on the variance-covariance method  
- Perform a **rolling backtest** to compare predicted VaR to actual daily losses  
- Measure how often losses exceed VaR (exceptions)  


---

## ⚙️ Methodology

### 1️⃣ Data
Daily closing prices for three stocks:
- AAPL  
- MSFT  
- GOOGL  

Data are downloaded directly using the `yfinance` Python library.

### 2️⃣ VaR Computation
The 1-day 99% VaR is calculated using:
\[
\text{VaR}_{t+1} = - z_{0.99} \times \sigma_{p,t} \times V
\]

Where:
- \( z_{0.99} \) = 2.33 (normal quantile for 99%)
- \( \sigma_{p,t} = \sqrt{w' \Sigma_t w} \) is the portfolio volatility
- \( V \) = portfolio value (set to €1,000,000)

Covariances are estimated with a **250-day rolling window**.

### 3️⃣ Backtesting
Each day’s VaR (predicted using past 250 days) is compared to the **realized daily loss**.  
We count how many times losses exceed VaR (“exceptions”).

The expected exception rate for 99% VaR is **1%**.

---

## 📈 Results

- **Confidence level:** 99%  
- **Exceptions:** 18 (1.79%) vs expected ≈ 1%  



---

## 🧩 Next Steps

- Implement an **EWMA (λ = 0.94)** version to model time-varying volatility  
- Test **GARCH(1,1)** for improved volatility forecasting  
- Compare results with **Historical Simulation** and **Monte Carlo VaR**

---

## 🛠️ Technologies Used
- Python 🐍  
- pandas, numpy, matplotlib  
- scipy.stats (for the normal quantile and Kupiec test)  
- yfinance (for financial data)

---

## 📚 References
- **Hull, John C.** (2018). *Risk Management and Financial Institutions*, 5th Edition.  
---

