# financial-econometrics-volatility-modeling
A best-practices handbook for time series modeling challenges in Quantitative Finance
# 📈 Application of Time Series — Best-Practices Handbook
### HASTS 211 · Application Project 3 · University of Zimbabwe

**Student:** Peter T. Kawudzu &nbsp;|&nbsp; **Reg. No.:** R2423866 &nbsp;|&nbsp; **Programme:** HASTS

---

## Overview

This project is a best-practices handbook for quantitative time series analysis in financial markets. It focuses on **Non-Stationarity, Cointegration, and Equilibrium Modeling** using a **Vector Error Correction Model (VECM)** applied to real-world equity and commodity price data.

The notebook follows a rigorous **7-D analytical framework**:

| # | Dimension | Description |
|---|-----------|-------------|
| 1 | **Definition** | Formal mathematical definitions with equations |
| 2 | **Description** | Intuitive written explanation |
| 3 | **Demonstration** | Numerical examples using real market data |
| 4 | **Diagram** | Fully labelled visualisations |
| 5 | **Diagnosis** | Statistical tests to detect the problem |
| 6 | **Damage** | Clear statement of consequences if ignored |
| 7 | **Directions** | Suggested model improvements and refinements |

---

## Dataset

| Field | Details |
|-------|---------|
| **Tickers** | AAPL (Apple Inc.), MSFT (Microsoft Corp.), GLD (SPDR Gold ETF) |
| **Frequency** | Daily adjusted closing prices |
| **Date Range** | January 1, 2015 – December 31, 2024 |
| **Source** | Yahoo Finance via `yfinance` |
| **Rationale** | AAPL and MSFT share macro risk factors (interest rates, tech sentiment); GLD tests cross-asset long-run relationships |

---

## Models & Methods

### Core Model — Vector Error Correction Model (VECM)

$$\Delta\mathbf{y}_t = \boldsymbol{\alpha}\boldsymbol{\beta}^\top \mathbf{y}_{t-1} + \sum_{i=1}^{p-1}\boldsymbol{\Gamma}_i\,\Delta\mathbf{y}_{t-i} + \boldsymbol{\mu} + \boldsymbol{\varepsilon}_t$$

Where $\boldsymbol{\alpha}$ is the **adjustment matrix** (speed of mean-reversion) and $\boldsymbol{\beta}$ is the **cointegrating matrix** (long-run equilibrium).

### Statistical Tests Applied

- **Augmented Dickey-Fuller (ADF)** — Unit root detection at levels and first differences
- **KPSS Test** — Cross-confirmation of non-stationarity
- **Johansen Trace & Max-Eigenvalue** — Determination of cointegration rank $r$
- **VAR Lag Selection** — AIC/BIC information criteria
- **Ljung-Box Test** — Residual autocorrelation diagnostics
- **Jarque-Bera Test** — Residual normality assessment

---

## Notebook Structure

```
HASTS211_R2423866_finale.ipynb
│
├── 0. Environment Setup
├── 1. Definition         — Random walk, cointegration, VECM equations, Johansen statistics
├── 2. Description        — Intuitive explanation of long-run equilibrium dynamics
├── 3. Data Import        — yfinance download, descriptive statistics, missing value checks
├── 4. Demonstration      — ADF/KPSS tests → Johansen test → VAR lag selection → VECM fit
├── 5. Diagram            — 14 fully labelled plots (price levels, log returns, ACF/PACF, ECT)
├── 6. Diagnosis          — Residual plots, Ljung-Box test, Q-Q plots, Jarque-Bera test
├── 7. Damage             — Assessment of 6 model problems (heteroskedasticity, breaks, etc.)
├── 8. Directions         — Sub-sample analysis, bivariate VECM, VECM-GARCH extensions
├── 9. Deployment         — Live trading system blueprint with signal generation rules
└── 10. References        — 10 academic references in MLA format
```

---

## Key Findings

- All three series are confirmed **I(1)** — non-stationary at levels, stationary at first differences
- The Johansen test identifies **at least one cointegrating vector**, indicating a long-run equilibrium between AAPL, MSFT, and GLD
- The **error-correction term (ECT)** confirms mean-reverting behaviour after deviations
- Rolling correlation analysis reveals **parameter instability** during the COVID-19 crash (2020) and the Fed rate-hike cycle (2022)
- Residual diagnostics reveal **non-normality and volatility clustering**, motivating a VECM-GARCH extension

---

## Deployment Blueprint

The notebook concludes with a practical **pairs trading / statistical arbitrage system** design:

- **Signal:** Z-score of the ECT — enter when |Z| > 1.5, exit when |Z| < 0.3
- **Sizing:** Loading matrix $|\boldsymbol{\alpha}|$ used as position weights
- **Risk Controls:** Stop-loss at |Z| > 3σ; halt if AAPL–MSFT rolling correlation < 0.6
- **Re-estimation:** Weekly rolling VECM re-fit on a 2-year trailing window

---

## Tech Stack

```python
Python 3.x
├── numpy
├── pandas
├── yfinance          # market data download
├── statsmodels       # ADF, KPSS, Johansen, VECM, VAR
├── matplotlib
├── seaborn
└── scipy             # Jarque-Bera, Q-Q plots
```

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/Peter-cawoodsgit/financial-econometrics-volatility-modeling.git
cd financial-econometrics-volatility-modeling

# 2. Install dependencies
pip install yfinance statsmodels pandas numpy matplotlib seaborn scipy

# 3. Launch Jupyter
jupyter notebook HASTS211_R2423866 finale.ipynb
```

> **Google Colab:** Uncomment the `!pip install` line at the top of Cell 0 and run all cells.

---

## References

1. Engle, R. F., & Granger, C. W. J. (1987). Co-integration and error correction. *Econometrica*, 55(2), 251–276.
2. Johansen, S. (1988). Statistical analysis of cointegration vectors. *Journal of Economic Dynamics and Control*, 12(2–3), 231–254.
3. Johansen, S. (1991). Estimation and hypothesis testing of cointegration vectors. *Econometrica*, 59(6), 1551–1580.
4. Hamilton, J. D. (1994). *Time Series Analysis*. Princeton University Press.
5. Lütkepohl, H. (2005). *New Introduction to Multiple Time Series Analysis*. Springer-Verlag.
6. Engle, R. F. (2002). Dynamic conditional correlation. *Journal of Business & Economic Statistics*, 20(3), 339–350.
7. Seabold, S., & Perktold, J. (2010). Statsmodels. *Proceedings of the 9th Python in Science Conference*.
8. Aroussi, R. (2019). *yfinance*. PyPI. https://pypi.org/project/yfinance/
9. Yahoo Finance. (2024). *Historical data: AAPL, MSFT, GLD*. https://finance.yahoo.com/
10. Alexander, C. (2001). *Market Models*. John Wiley & Sons.

---

*University of Zimbabwe · HASTS 211 — Financial Econometrics · 2026*
