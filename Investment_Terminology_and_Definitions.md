# Investment Terminology and Definitions

This document outlines key terms and concepts related to asset-liability management, portfolio construction, risk measurement, and financial modeling.

---

## I. Core Asset-Liability Management (ALM) Concepts

### Asset-Liability Management (ALM)
- A financial discipline focused on the relationship between assets and liabilities, not just asset value.
- For pension funds, it emphasizes dynamic allocation between risky and safe components based on market conditions and regulatory risk budgets.

### Funding Ratio
- Ratio of assets to liabilities.
- Indicates the fraction of liabilities covered by assets.
- 100%+ means liabilities are fully covered.
- The goal in Liability-Driven Investing (LDI) is to increase the funding ratio.
- The final distribution of the funding ratio is a key measure of investor welfare.

### Surplus / Deficit
- **Surplus:** Assets minus liabilities is positive.
- **Deficit:** Assets minus liabilities is negative.

### Liability-Driven Investing (LDI)
- Investment framework managing assets considering liabilities efficiently.
- Dominant in modern institutional money management.
- Allocates assets into:
  - Performance-Seeking Portfolio (PSP)
  - Liability-Hedging Portfolio (LHP)
- Separates performance and risk management objectives.
- Initially designed for minimum funding ratio floors; can be extended to capital guarantee or drawdown floors.

### Dynamic LDI Strategies
- Evolve the split between risky (PSP) and safe (LHP) components over time.
- Adjusted based on market conditions and prudential risk budgets.
- Achieve minimum funding ratio constraints with lower opportunity costs vs. static LDI.

### Investor Welfare
- Related to the final distribution of the funding ratio.
- Aims for high average funding ratio and low uncertainty.
- Decomposed into PSP Sharpe ratio and LHP-liability correlation.

### Opportunity Cost & Gain (in LDI)
- **Opportunity Cost:** % of initial wealth needed by sub-optimal strategies to match optimal dynamic LDI's average terminal wealth for the same risk.
- **Opportunity Gain:** % of wealth saved by using a better strategy (vs. buy-and-hold) to reach the same terminal wealth for the same risk.

### Sponsor Risk
- Risk that a sponsoring company's ability to make contributions to a pension plan is compromised, especially in deficit situations.

---

## II. Portfolio Components & Strategies

### Performance-Seeking Portfolio (PSP)
- One of two LDI building blocks.
- Focuses on efficiently harvesting risk premium (maximizing risk-adjusted performance, e.g., Sharpe ratio).
- Equities are typically the largest and most liquid component.

### Liability-Hedging Portfolio (LHP) / Goal-Hedging Portfolio (GHP)
- The other LDI building block.
- Hedges liabilities, especially against present value increases (e.g., due to interest rates).
- Customized to track liabilities; often uses nominal bonds, inflation-linked bonds, or derivatives like swaps.
- Beta with liabilities measures effectiveness.

### Policy Portfolio
- Strategic asset allocation between PSP and LHP.
- Theoretical allocation depends on risk aversion (gamma), but in practice, translates into risk budgets.

### Duration Matching
- Immunizes bond portfolios against interest rate risk by matching Macaulay duration of assets and liabilities.
- Ensures similar value changes for parallel yield curve shifts.
- Zero-coupon bonds ideal; coupon bonds often used as proxies.

### Cash Flow Matching
- LHP/GHP constructed to match cash flows of liability/goal payments in amount and timing.

### Markowitz Analysis / Portfolio Optimization
- Finds portfolios on the efficient frontier.
- Challenge: Estimation error, especially for expected returns, can lead to extreme/unstable weights ("error maximizing machines").

### Efficient Frontier
- Portfolios with the highest return for a given risk, or lowest risk for a given return.
- No improvement possible without altering risk/return.
- Shape changes with a risk-free asset.

### Capital Market Line (CML)
- With a risk-free asset, the efficient frontier becomes the CML (a straight line).
- All mean-variance optimal portfolios lie on the CML.

### Maximum Sharpe Ratio (MSR) Portfolio / Tangency Portfolio
- Risky portfolio on the efficient frontier that maximizes the Sharpe ratio (with a risk-free asset).
- Highest reward per unit risk.
- Contains only systematic risk, as specific risk can be diversified away.

### Global Minimum Variance (GMV) Portfolio
- Portfolio on the efficient frontier with the lowest volatility.
- Does not require expected return estimates; depends only on covariance matrix.

### Equal Weight (EW) Portfolio / Naive Diversification
- Allocates capital equally to all assets.
- Does not require expected return estimates.

### Liability-Friendly Equity Portfolios
- Equities designed for better liability-hedging.
- Examples: High-dividend stocks (cash flow matching), low-volatility stocks (bond-like).

### Target-Date Fund
- Adjusts asset allocation over time based on time horizon (e.g., to retirement).
- Often criticized for not adapting to market condition changes.

### Derivatives (in LDI)
- Instruments like swaps/futures used to implement LHPs, enabling leverage.

### Risk Factors
- Underlying return drivers used for asset allocation and risk management.
- Rewarded if they perform poorly in bad times but compensate in good times.

---

## III. Risk Measurement & Analysis

### Volatility (Standard Deviation)
- Symmetric risk measure: average deviation from mean.
- Annualized by scaling monthly/daily volatility by √12 or √252.

### Semideviation / Semi-volatility
- Downside risk measure: only considers returns below mean/zero.

### Drawdowns
- Maximum loss from peak to trough.
- Shows worst-case returns; sensitive to data granularity.

### Maximum Drawdown Floor
- Risk constraint: ensures losses do not exceed a set % from a previous peak.

### Value at Risk (VaR)
- Maximum loss at a given confidence level over a set period.
- **Historical VaR:** Percentile from historical returns; no distribution assumption, but sample-sensitive.
- **Parametric (Gaussian) VaR:** Assumes normality; simple but underestimates tail risk.
- **Cornish-Fisher VaR (Modified VaR):** Adjusts for skewness/kurtosis; robust to non-normality.

### Conditional Value at Risk (CVaR) / Expected Shortfall
- Expected loss beyond VaR.
- Average of all losses worse than the VaR cutoff.

### Sharpe Ratio
- Risk-adjusted return: (Expected Return - Risk-Free Rate) / Volatility.
- Key PSP objective.

### Excess Return
- Return above the risk-free rate.

### Risk-Free Rate
- Theoretical return with zero risk, e.g., US Treasuries.

### Calmar Ratio
- Excess return divided by max drawdown (often over 36 months).

### Skewness
- Asymmetry of return distribution.
- Negative: more large losses.

### Kurtosis
- "Tailedness" or frequency of extreme values.
- High kurtosis: fatter tails than normal.

### Jarque-Bera Test
- Tests normality using skewness and kurtosis.

---

## IV. Financial Models & Simulation

### Geometric Brownian Motion (GBM)
- Stochastic process for modeling asset prices: drift + random walk.
- Formula: dSt/St = mu*dt + sigma*dWt

### mu (Drift/Expected Return)
- GBM parameter: expected return/trend.

### sigma (Volatility/Dispersion)
- GBM parameter: spread of outcomes.

### Brownian Motion (dWt or psi)
- Stochastic process for random price changes.
- Gaussian increments; independent over time.

### CIR Model (Cox-Ingersoll-Ross)
- Models interest rate movements with mean reversion.
- Parameters: 
  - **a:** Speed of mean reversion
  - **b:** Long-term mean
  - **sigma:** Volatility

### Instantaneous Rate (Short Rate)
- r_instant where 1 + r_annual = e^(r_instant)

### Yield Curve
- Graph of bond yields by maturity; flat if rates are equal across maturities.

### Monte Carlo Simulation
- Uses repeated random sampling to generate scenarios for asset returns/interest rates.

---

## V. Programming & Data Handling Concepts

### NumPy (`np`)
- Fundamental Python library for numerical computing.

### pandas (`pd`)
- Python library for data manipulation/analysis using DataFrames and Series.

### DataFrame (pandas)
- Two-dimensional, tabular data structure.

### Series (pandas)
- One-dimensional labeled array.

### `read_csv()`
- Loads data from CSV into DataFrame.

### `to_datetime()`
- Converts values to datetime.

### `to_period()`
- Converts DatetimeIndex to PeriodIndex (e.g., monthly).

### `dropna()`
- Removes missing (NA/NaN) values.

### `cumprod()`
- Computes cumulative product (e.g., compounded returns).

### `cummax()`
- Computes cumulative maximum (used to track peaks).

### `mean(axis=1)`
- Computes row-wise mean (across columns).

### `idxmin()`
- Returns index of minimum value.

### `def` (Python keyword)
- Defines a function.

### Docstring
- String in code documenting functions/classes/modules.

### `for` loop
- Iterates over sequences.

### `iloc`
- Integer-location based indexing for pandas DataFrames.

### `isinstance()`
- Checks if object is instance of a class/type.

### `aggregate()`
- Applies operations along a DataFrame axis.

### `np.percentile()`
- Computes percentile of data.

### `norm.ppf()`
- Inverse CDF for normal distribution (Z-score for percentile).

### `clip()`
- Limits values to a specified range.

### `np.repeat()`
- Repeats elements of an array.

### `linspace()`
- Generates evenly-spaced numbers over an interval.

### List Comprehension
- Concise way to create lists from iterables.

### pyplot (`plt`)
- `matplotlib.pyplot` module for plotting.

### `subplot()`
- Creates multiple plots in one figure.

### `annotate()`
- Adds text annotations to a plot.

---

## VI. Research & Industry Context

### EDHEC-Risk Institute
- Research institute for ALM, institutional investing, hedge funds.

### Defined-Benefit (DB) Pension Fund
- Contributions adjust to meet predefined benefits; subject to minimum funding rules.

### Defined-Contribution (DC) Fund
- Fixed contributions; retirement benefits depend on investment performance.

### Hybrid Fund
- Combines DB and DC features.

### Longevity Risk
- Risk of plan members living longer than expected, increasing liabilities.

### Specification Risk
- Using an incorrect/inappropriate model in analysis.

### Sample Risk
- Estimate sensitivity to the specific historical sample period.

### Defined Outcome Investing / Safety Net Investing
- Dynamic strategies (e.g., CPPI) aiming for specific return/drawdown outcomes.

### Structured Product / Principal Protected Product
- Financial products offering downside protection; often opaque and illiquid. CPPI is a transparent alternative.

### Market Cap (Market Capitalization)
- Total company value: shares outstanding × price.

### Cap-Weighted Market Index
- Index weighted by market capitalization (e.g., S&P 500).

### Risk Budgeting
- Defining/allocating allowable risk levels using measures like VaR, expected shortfall, or volatility.