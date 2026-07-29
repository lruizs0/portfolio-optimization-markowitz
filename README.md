#  Portfolio Optimization with Markowitz Theory
![Python](https://img.shields.io/badge/Python-3.13-blue)

![Pandas](https://img.shields.io/badge/Pandas-Latest-green)

![NumPy](https://img.shields.io/badge/NumPy-Latest-orange)

![License](https://img.shields.io/badge/License-MIT-red)

## Project Overview

This project implements **Modern Portfolio Theory (MPT)** proposed by **Harry Markowitz** to build an optimal investment portfolio using historical stock market data.

The workflow includes:

- Financial data acquisition using Yahoo Finance.
- Exploratory Data Analysis (EDA).
- Portfolio optimization through Monte Carlo simulation.
- Efficient Frontier visualization.
- Performance comparison against the **S&P 500 (SPY)**.
- Portfolio backtesting.
- Risk and performance metrics commonly used in quantitative finance.

The objective is to demonstrate the application of Python, statistics, optimization and financial analysis in a real-world investment problem.

---

# Project Workflow

```text
Historical Market Data
        │
        ▼
Data Cleaning & Processing
        │
        ▼
Exploratory Data Analysis
        │
        ▼
Expected Returns & Covariance Matrix
        │
        ▼
Markowitz Portfolio Optimization
        │
        ▼
Monte Carlo Simulation
        │
        ▼
Efficient Frontier
        │
        ▼
Optimal Portfolio Selection
        │
        ▼
Backtesting vs S&P500
        │
        ▼
Performance Evaluation
```

---

# Repository Structure

```
portfolio-optimization-markowitz/

│

├── data
│   ├── raw
│   │   └── adj_close.csv
│   │
│   └── processed
│       └── daily_returns.csv
│
├── notebooks
│   ├── 01_download_data.ipynb
│   ├── 02_exploratory_data_analysis.ipynb
│   ├── 03_markowitz_optimization.ipynb
│   └── 04_backtesting_vs_sp500.ipynb
│
├── reports
│   ├── figures
│   └── report.pdf
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

# Technologies

- Python
- NumPy
- Pandas
- Matplotlib
- Plotly
- yfinance
- Jupyter Notebook

---

# Assets Included

The portfolio is built using the following assets:

- Apple (AAPL)
- Caterpillar (CAT)
- Johnson & Johnson (JNJ)
- JPMorgan Chase (JPM)
- Coca-Cola (KO)
- Microsoft (MSFT)
- NVIDIA (NVDA)
- SPY (Benchmark)
- Visa (V)
- Walmart (WMT)
- Exxon Mobil (XOM)

---

# Methodology

The project follows the classical Markowitz methodology:

### 1. Download historical prices

Historical adjusted prices are obtained from Yahoo Finance.

### 2. Calculate daily returns

Daily percentage returns are computed for each asset.

### 3. Exploratory Data Analysis

- Descriptive statistics
- Annual returns
- Annual volatility
- Correlation matrix
- Histograms
- Boxplots

### 4. Portfolio Optimization

Using Modern Portfolio Theory:

- Expected returns
- Covariance matrix
- Random portfolio generation
- Monte Carlo simulation
- Efficient Frontier
- Maximum Sharpe Portfolio
- Minimum Variance Portfolio

### 5. Backtesting

The optimal portfolio is compared against the SPY ETF using:

- Portfolio cumulative return
- CAGR
- Maximum Drawdown
- Calmar Ratio
- Sortino Ratio
- Rolling Volatility
- Rolling Sharpe Ratio

---

# Main Results

## Optimal Portfolio

|Metric|Value|
|------|------:|
|Expected Return|32.10%|
|Volatility|25.32%|
|Sharpe Ratio|1.19|

---

## Risk Metrics

|Metric|Value|
|------|------:|
|CAGR|158.07%|
|Maximum Drawdown|-32.38%|
|Calmar Ratio|4.88|
|Sortino Ratio|1.60|

---

## Optimal Asset Allocation

|Asset|Weight|
|------|------:|
|NVDA|31.78%|
|WMT|18.83%|
|MSFT|13.62%|
|KO|11.07%|
|CAT|9.86%|
|AAPL|4.09%|
|JNJ|4.03%|
|V|2.53%|
|SPY|1.76%|
|XOM|1.68%|
|JPM|0.75%|

---

# Visualizations

The project includes:

- Annual Returns
- Annual Volatility
- Correlation Matrix
- Return Distributions
- Boxplots
- Efficient Frontier
- Portfolio Allocation
- Portfolio vs S&P500
- Drawdown
- Rolling Volatility
- Rolling Sharpe Ratio

---

# How to Run

Clone the repository

```bash
git clone https://github.com/your_username/portfolio-optimization-markowitz.git
```

Create a virtual environment

```bash
python -m venv .venv
```

Activate the environment

Windows

```bash
.venv\Scripts\activate
```

Install dependencies

```bash
pip install -r requirements.txt
```

Open Jupyter Notebook

```bash
jupyter notebook
```

Run notebooks in numerical order.

---

#  Key Concepts

- Modern Portfolio Theory
- Markowitz Optimization
- Monte Carlo Simulation
- Efficient Frontier
- Risk-adjusted Return
- Portfolio Diversification
- Financial Data Analysis

---

# Conclusions

The optimized portfolio outperformed the S&P 500 over the analyzed period while maintaining an attractive balance between return and risk.

The results highlight the usefulness of Modern Portfolio Theory for portfolio construction and demonstrate how quantitative methods can support investment decision-making.

Although historical performance does not guarantee future returns, the methodology provides a robust framework for evaluating investment strategies.

---

# Author

**Laura Carolina Ruiz Sandoval**

Mathematician | Data Analyst | Financial Analytics | Machine Learning

Interested in:

- Data Analytics
- Quantitative Finance
- Actuarial Science
- Machine Learning
- Optimization