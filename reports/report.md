---
title: "Portfolio Optimization using Modern Portfolio Theory"
author: "Laura Carolina Ruiz Sandoval"
date: \today
geometry: margin=1in
fontsize: 11pt
toc: true
toc-depth: 2
numbersections: true
header-includes:
- \usepackage{amsmath}
- \usepackage{amssymb}
- \usepackage{booktabs}
- \usepackage{graphicx}
- \usepackage{float}
- \usepackage{setspace}
- \onehalfspacing
---

# Introduction

Portfolio optimization is one of the fundamental problems in quantitative finance. Investors continuously seek strategies capable of maximizing expected returns while maintaining an acceptable level of risk. The challenge lies in selecting an appropriate combination of financial assets that provides the best possible trade-off between profitability and uncertainty.

Modern Portfolio Theory (MPT), introduced by Harry Markowitz (1952), revolutionized investment management by demonstrating that portfolio risk depends not only on the individual risk of each asset but also on the correlation among assets. Consequently, diversification allows investors to reduce portfolio risk without necessarily sacrificing expected returns.

This project implements the complete workflow of Modern Portfolio Theory using Python. Historical adjusted closing prices are obtained from Yahoo Finance, followed by an exploratory analysis, portfolio optimization through Monte Carlo simulation, historical backtesting, and performance evaluation using professional risk-adjusted metrics.

Finally, the optimized portfolio is compared with the S&P 500 ETF (SPY), one of the most widely used benchmarks in the financial industry.

\newpage

# Objectives

## General Objective

Develop an optimal investment portfolio using Modern Portfolio Theory and evaluate its historical performance relative to the S&P 500 index.

## Specific Objectives

- Download historical market data from Yahoo Finance.
- Compute daily asset returns.
- Perform an exploratory statistical analysis of financial returns.
- Estimate expected annual returns and the covariance matrix.
- Generate random portfolios using Monte Carlo simulation.
- Identify the portfolio with the highest Sharpe Ratio.
- Compare portfolio performance against the S&P 500 ETF.
- Evaluate the strategy using quantitative performance indicators.

\newpage

# Dataset

Historical financial data were downloaded directly from Yahoo Finance using the Python package **yfinance**.

The analysis considers eleven assets representing different sectors of the U.S. economy, allowing an adequate degree of diversification.

|Ticker|Company|Sector|
|:----:|----------------------|-----------------------|
|AAPL|Apple Inc.|Technology|
|MSFT|Microsoft Corporation|Technology|
|NVDA|NVIDIA Corporation|Semiconductors|
|JPM|JPMorgan Chase & Co.|Financial Services|
|KO|The Coca-Cola Company|Consumer Staples|
|JNJ|Johnson & Johnson|Healthcare|
|CAT|Caterpillar Inc.|Industrials|
|WMT|Walmart Inc.|Retail|
|V|Visa Inc.|Financial Services|
|XOM|Exxon Mobil Corporation|Energy|
|SPY|SPDR S&P 500 ETF Trust|Benchmark Index|

Adjusted closing prices were selected because they account for corporate actions such as dividends and stock splits, providing a more accurate representation of the true evolution of asset prices over time.

The study covers approximately seven years of daily observations, providing sufficient historical information to estimate returns, volatility and correlations among assets.

\newpage

# Methodology

The methodology consists of four sequential stages:

1. Data acquisition.
2. Exploratory Data Analysis (EDA).
3. Portfolio optimization.
4. Historical backtesting.

## Daily Returns

Daily asset returns are calculated as the percentage change between consecutive adjusted closing prices.

\begin{equation}
R_t=
\frac{P_t-P_{t-1}}
{P_{t-1}}
\end{equation}

where

- $P_t$ represents the adjusted closing price at time $t$.
- $P_{t-1}$ represents the adjusted closing price on the previous trading day.

Daily returns constitute the fundamental variable used throughout the optimization process.

## Expected Annual Return

Expected annual returns are estimated from the historical average daily return.

\begin{equation}
E(R)=252\bar{r}
\end{equation}

where

- $\bar r$ denotes the average daily return.
- 252 corresponds to the approximate number of trading days in one year.

Annualization allows returns to be interpreted using the standard convention adopted in financial analysis.

## Annualized Volatility

Portfolio risk is represented by annualized volatility.

\begin{equation}
\sigma=\sqrt{252}\sigma_d
\end{equation}

where

- $\sigma_d$ is the standard deviation of daily returns.

Volatility measures the variability of returns and is commonly used as the primary indicator of investment risk.

## Expected Portfolio Return

The expected return of a portfolio is calculated as the weighted average of the expected returns of its constituent assets.

\begin{equation}
E(R_p)=w^T\mu
\end{equation}

where

- $w$ represents the vector of portfolio weights.
- $\mu$ denotes the vector of expected annual returns.

The portfolio weights satisfy the following constraints:

\begin{equation}
\sum_{i=1}^{n}w_i=1
\end{equation}

\begin{equation}
w_i\ge0
\end{equation}

meaning that the portfolio is fully invested and short selling is not allowed.

## Portfolio Volatility

Portfolio volatility is computed using the covariance matrix of asset returns.

\begin{equation}
\sigma_p=
\sqrt{w^T\Sigma w}
\end{equation}

where

- $\Sigma$ is the covariance matrix.

Unlike individual asset volatility, portfolio risk incorporates the interaction between assets through their correlations.

## Sharpe Ratio

The quality of each portfolio is measured using the Sharpe Ratio.

\begin{equation}
Sharpe=
\frac{R_p-R_f}
{\sigma_p}
\end{equation}

where

- $R_p$ is the expected portfolio return.
- $R_f$ is the risk-free rate.
- $\sigma_p$ is the annualized portfolio volatility.

The Sharpe Ratio measures the amount of excess return generated for each unit of risk assumed by the investor.

Higher values indicate more efficient portfolios.

## Monte Carlo Simulation

A Monte Carlo simulation was implemented to generate **10,000 random portfolios**.

For each simulated portfolio the following quantities were computed:

- Expected annual return.
- Annualized volatility.
- Sharpe Ratio.

The optimal portfolio corresponds to the portfolio with the maximum Sharpe Ratio, while the minimum variance portfolio corresponds to the portfolio with the lowest annualized volatility among all simulated portfolios.

This methodology allows visualization of the Efficient Frontier and facilitates comparison between different investment alternatives under the Markowitz framework.
\newpage

# Exploratory Data Analysis

Before constructing the optimal portfolio, an exploratory analysis was performed to understand the statistical characteristics of the selected assets. This stage provides valuable insights into return behavior, risk levels and the relationships among assets.

The analysis included:

- Descriptive statistics.
- Annual expected returns.
- Annualized volatility.
- Correlation analysis.
- Distribution of daily returns.
- Boxplots of returns.

## Descriptive Statistics

The descriptive statistics summarize the central tendency and dispersion of daily returns.

The results show that NVIDIA presents the highest average daily return, but also the largest variability among all analyzed assets. Conversely, defensive companies such as Coca-Cola and Johnson & Johnson exhibit lower average returns accompanied by substantially lower volatility.

These differences illustrate the classic trade-off between return and risk that motivates portfolio diversification.

## Annual Expected Returns

Expected annual returns were estimated by annualizing the average daily return according to Equation (2).


The figure shows that NVIDIA generated the highest expected annual return during the analyzed period, followed by Apple and Microsoft.

The S&P 500 (SPY) produced lower expected returns than several individual stocks, highlighting the possibility of outperforming the benchmark through an optimized asset allocation.

## Annualized Volatility

Annualized volatility was computed using Equation (3).

The volatility analysis indicates that NVIDIA is also the riskiest asset, whereas Coca-Cola, Johnson & Johnson and Walmart present significantly lower levels of uncertainty.

Although high returns are desirable, they are usually accompanied by greater fluctuations in asset prices.

## Correlation Matrix

Understanding the correlation between assets is fundamental for portfolio construction because diversification benefits arise from combining assets that do not move perfectly together.

Most correlations are positive, reflecting the common influence of overall market conditions.

However, several defensive assets display weaker correlations with technology companies, providing valuable diversification benefits.

The correlation matrix confirms that combining assets from different sectors can reduce overall portfolio risk.

## Distribution of Daily Returns

The distribution of daily returns was analyzed through histograms.

Most return distributions are approximately centered around zero, although they exhibit heavier tails than a normal distribution.

Technology stocks present wider distributions, indicating higher variability and a greater probability of extreme returns.

## Boxplots

Boxplots provide a visual summary of return dispersion and the presence of outliers.

NVIDIA displays the widest interquartile range and the largest number of extreme observations.

Conversely, Coca-Cola and Johnson & Johnson exhibit considerably narrower distributions, reinforcing their role as defensive investments.

Overall, the exploratory analysis confirms the existence of heterogeneous risk-return profiles across assets, creating favorable conditions for portfolio diversification under Modern Portfolio Theory.

\newpage

# Portfolio Optimization

The optimization stage seeks the combination of asset weights that maximizes the investor's risk-adjusted return.

Following the Markowitz framework, a Monte Carlo simulation generated 10,000 random portfolios satisfying the investment constraints presented in Section 4.

For each simulated portfolio, the following quantities were computed:

- Expected annual return.
- Annualized volatility.
- Sharpe Ratio.

The portfolio with the highest Sharpe Ratio was selected as the optimal allocation.

## Efficient Frontier

The Efficient Frontier illustrates the trade-off between expected return and portfolio risk.

Each point represents one randomly generated portfolio.

The color scale corresponds to the Sharpe Ratio, where brighter colors indicate superior risk-adjusted performance.

Two portfolios are highlighted:

- Maximum Sharpe Portfolio.
- Minimum Variance Portfolio.

The Maximum Sharpe Portfolio provides the highest expected return for each unit of risk, whereas the Minimum Variance Portfolio minimizes overall portfolio volatility.

## Optimal Portfolio Performance

The optimization produced the following results.

|Metric|Value|
|:----------------------|------:|
|Expected Annual Return|32.10%|
|Annualized Volatility|25.32%|
|Sharpe Ratio|1.19|

The optimized portfolio offers a substantially higher expected return than the benchmark while maintaining an acceptable level of risk.

A Sharpe Ratio above one is generally considered indicative of a well-diversified and efficient investment strategy.

## Optimal Asset Allocation

The optimal weights obtained through the Markowitz optimization are shown below.

The allocation assigns greater importance to:

- NVIDIA
- Walmart
- Microsoft
- Coca-Cola
- Caterpillar

The remaining assets contribute to diversification by reducing overall portfolio volatility.

Although NVIDIA receives the largest allocation due to its strong historical performance, the optimization avoids concentrating the entire investment in a single asset because diversification reduces overall portfolio risk.

The resulting allocation therefore achieves a more efficient balance between expected return and volatility than any individual stock.
\newpage

# Historical Backtesting

Portfolio optimization alone is insufficient to evaluate an investment strategy. Therefore, a historical backtest was performed to assess how the optimized portfolio would have behaved under real market conditions.

The optimized portfolio was compared against the SPDR S&P 500 ETF (SPY), which serves as the benchmark for the U.S. equity market.

Both portfolios were initialized with the same hypothetical investment value of 100 monetary units and allowed to evolve according to their daily returns.

The portfolio value at each time step was computed as

\begin{equation}
V_t=V_0\prod_{i=1}^{t}(1+R_i)
\end{equation}

where

- $V_0$ is the initial investment.
- $R_i$ represents the portfolio return on day $i$.

This cumulative process simulates the growth of capital assuming that all returns are continuously reinvested.

## Portfolio Growth

The cumulative performance of the optimized portfolio and the benchmark is presented below.


The results indicate that both portfolios followed similar trends during the first years of the sample period.

However, beginning around 2020, the optimized portfolio started to significantly outperform the benchmark.

This superior performance can largely be explained by the substantial appreciation of technology companies, particularly NVIDIA and Microsoft, which received relatively high allocations during the optimization process.

Although both portfolios were exposed to periods of market stress, the optimized portfolio recovered more rapidly and achieved considerably higher long-term growth.

Overall, the backtesting results demonstrate that the optimized portfolio generated substantially greater cumulative wealth than the benchmark over the analyzed period.

\newpage

# Performance Evaluation

To complement the return analysis, several professional performance metrics were calculated.

These indicators evaluate not only profitability but also the level of risk assumed to obtain those returns.

## Compound Annual Growth Rate (CAGR)

The Compound Annual Growth Rate measures the average annual growth of the portfolio assuming that profits are continuously reinvested.

It is calculated as

\begin{equation}
CAGR=
\left(\frac{V_f}{V_0}\right)^{\frac{1}{n}}-1
\end{equation}

where

- $V_f$ is the final portfolio value.
- $V_0$ is the initial investment.
- $n$ is the number of years.

The optimized portfolio achieved

|Metric|Value|
|:----------------|------:|
|CAGR|158.07\%|

This exceptionally high CAGR reflects the remarkable capital appreciation obtained throughout the investment horizon.

Although historical performance does not guarantee future results, this metric indicates that the selected asset allocation captured one of the strongest bull markets of recent years.

\newpage

## Maximum Drawdown

Maximum Drawdown quantifies the largest percentage decline from a historical peak to a subsequent trough.

It is computed as

\begin{equation}
MDD=
\min
\left(
\frac{V_t-\max(V)}{\max(V)}
\right)
\end{equation}

where

- $\max(V)$ represents the historical maximum portfolio value.

The obtained result was

|Metric|Value|
|:------------------|------:|
|Maximum Drawdown|-32.38\%|


A maximum drawdown of approximately 32\% indicates that the portfolio experienced significant temporary losses during adverse market conditions.

Nevertheless, the subsequent recovery demonstrates the long-term robustness of the investment strategy.

Investors with long investment horizons generally consider temporary drawdowns acceptable when compensated by superior long-term returns.

\newpage

## Sortino Ratio

Unlike the Sharpe Ratio, the Sortino Ratio penalizes only downside volatility.

Its mathematical expression is

\begin{equation}
Sortino=
\frac{R_p-R_f}
{\sigma_d^-}
\end{equation}

where

- $\sigma_d^-$ represents downside deviation.

The resulting value is

|Metric|Value|
|:---------------|------:|
|Sortino Ratio|1.60|

A Sortino Ratio greater than one suggests that the portfolio generated attractive returns relative to downside risk.

Because this metric ignores positive volatility, it provides a more realistic assessment from the perspective of long-term investors.

\newpage

## Calmar Ratio

The Calmar Ratio compares annual returns with the largest historical loss.

It is defined as

\begin{equation}
Calmar=
\frac{CAGR}
{|MDD|}
\end{equation}

The optimized portfolio obtained

|Metric|Value|
|:---------------|------:|
|Calmar Ratio|4.88|

A Calmar Ratio close to five is considered excellent in portfolio management.

This result indicates that the annualized return largely compensated investors for the largest historical decline experienced during the investment period.

\newpage

## Rolling Volatility

Rolling volatility measures how portfolio risk evolves over time.

Instead of computing a single volatility value for the entire sample, volatility is estimated over a moving time window.

The figure illustrates that portfolio volatility increased during periods of market turbulence, particularly around the COVID-19 market crash.

After these episodes, volatility gradually returned to more stable levels, indicating that the portfolio adapted well to changing market conditions.

\newpage

## Rolling Sharpe Ratio

The Rolling Sharpe Ratio evaluates how risk-adjusted performance changes over time.

Although temporary declines are observed during highly volatile market periods, the Rolling Sharpe Ratio remains positive for most of the investment horizon.

This behavior suggests that the optimized portfolio consistently generated excess returns relative to the level of risk assumed.

Overall, the rolling metrics confirm that the optimized strategy maintained satisfactory performance throughout different market environments rather than relying on isolated periods of exceptional returns.
\newpage

# Discussion

The results obtained throughout this study demonstrate the practical applicability of Modern Portfolio Theory for constructing diversified investment portfolios.

The exploratory analysis revealed substantial differences in expected returns, volatility and correlation among the selected assets. These differences provide the necessary conditions for diversification, allowing the optimization algorithm to combine assets in a way that improves the portfolio's overall risk-adjusted performance.

The optimized portfolio achieved an expected annual return of **32.10%** with an annualized volatility of **25.32%**, resulting in a **Sharpe Ratio of 1.19**. These results indicate that the optimization process successfully identified an efficient allocation capable of generating attractive returns without assuming excessive levels of risk.

Historical backtesting further supports these findings. The optimized portfolio consistently outperformed the S&P 500 during the analyzed period, particularly after 2020. This superior performance was primarily driven by the exceptional appreciation of technology companies, especially NVIDIA and Microsoft, while maintaining diversification through investments in defensive sectors such as consumer staples and healthcare.

The performance metrics also reinforce the effectiveness of the proposed strategy. The portfolio achieved a Compound Annual Growth Rate (CAGR) of **158.07%**, demonstrating remarkable capital appreciation over the investment horizon. Although the strategy experienced a Maximum Drawdown of **32.38%**, the portfolio recovered strongly after periods of market stress, as reflected by its **Calmar Ratio of 4.88** and **Sortino Ratio of 1.60**.

Despite these encouraging results, several limitations should be acknowledged.

First, the optimization relies entirely on historical returns, implicitly assuming that future market behavior will resemble past observations. Financial markets are inherently dynamic, and structural changes may significantly alter future asset performance.

Second, the analysis ignores transaction costs, taxes, bid-ask spreads and liquidity constraints. These factors would reduce realized returns in practical investment scenarios.

Finally, the portfolio weights remain fixed throughout the investment period. In professional portfolio management, periodic rebalancing is commonly performed to maintain the desired allocation and adapt to changing market conditions.

Therefore, while the proposed methodology provides valuable insights into quantitative portfolio construction, the reported results should be interpreted as an academic evaluation rather than a guarantee of future investment performance.

\newpage

# Future Work

Several extensions could further improve the proposed methodology.

Future versions of this project may incorporate more advanced portfolio optimization techniques, including:

- Black-Litterman portfolio optimization.
- Mean-CVaR optimization.
- Hierarchical Risk Parity (HRP).
- Risk budgeting strategies.
- Dynamic portfolio rebalancing.
- Transaction costs and slippage modeling.
- Macroeconomic variables as explanatory factors.
- Machine Learning models for return prediction.
- Reinforcement Learning for portfolio allocation.
- Bayesian estimation of expected returns.
- Regime-switching models for financial markets.

Additionally, future work could compare multiple optimization methods to evaluate their robustness under different market environments and investment horizons.

These extensions would provide a more realistic representation of professional quantitative asset management.

\newpage

# Conclusions

This project successfully implemented the complete workflow of portfolio optimization using Modern Portfolio Theory and Python.

Beginning with the acquisition of historical market data, the analysis progressed through exploratory data analysis, estimation of statistical parameters, portfolio optimization, historical backtesting and performance evaluation using professional financial metrics.

The results demonstrate that combining assets from different economic sectors substantially improves the portfolio's risk-return profile compared with investing in individual securities alone.

The optimized portfolio achieved superior risk-adjusted performance relative to the S&P 500 benchmark throughout the analyzed period. In particular, the historical backtest shows that the optimized strategy generated significantly greater cumulative wealth while maintaining acceptable levels of portfolio risk.

The calculated Sharpe Ratio, Sortino Ratio and Calmar Ratio all indicate that the additional returns obtained by the portfolio adequately compensated investors for the risks assumed.

Beyond the financial results, this project illustrates the value of combining quantitative finance, statistics and programming to support data-driven investment decisions.

From a technical perspective, the project demonstrates practical applications of Python libraries such as NumPy, Pandas, Matplotlib, Plotly and yfinance, together with Monte Carlo simulation techniques and Modern Portfolio Theory.

The complete workflow is fully reproducible and can serve as a solid foundation for more advanced quantitative finance projects involving optimization, risk management and machine learning.

Overall, this study confirms that quantitative portfolio optimization remains a powerful tool for constructing diversified investment strategies capable of improving long-term investment performance.

\newpage

# References

Markowitz, H. (1952). *Portfolio Selection*. Journal of Finance, 7(1), 77–91.

Bodie, Z., Kane, A., & Marcus, A. *Investments*. McGraw-Hill Education.

Hull, J. C. *Risk Management and Financial Institutions*. Wiley.

Fabozzi, F. J. *Portfolio Management and Investment Management*. Wiley.

Luenberger, D. G. *Investment Science*. Oxford University Press.

Sharpe, W. F. (1966). *Mutual Fund Performance*. Journal of Business.

Yahoo Finance. https://finance.yahoo.com

Ran Aroussi. *yfinance Documentation*. https://github.com/ranaroussi/yfinance

McKinney, W. *Python for Data Analysis*. O'Reilly Media.

Harris, C. *Python for Finance*. O'Reilly Media.

NumPy Documentation. https://numpy.org

Pandas Documentation. https://pandas.pydata.org

Matplotlib Documentation. https://matplotlib.org

Plotly Documentation. https://plotly.com/python/