# Investment Management Briefing Document

---

## I. Understanding and Measuring Investment Returns and Risk

### A. Core Concepts of Return and Volatility

- **Investment Returns**: Calculated as the change in price (plus dividends, if any) over a period, often expressed as a percentage. The "1 plus r" format is used to conveniently represent compounded returns.
- **Volatility**: Typically measured by standard deviation, it quantifies the dispersion of returns around the mean. Standard deviation is a *symmetric* risk measure, treating both upside and downside deviations equally.

> Sources:  
> "Understanding Investment Returns: Calculation and Compounding"  
> "Downside Risk Measures: VaR and CVaR"  
> "Returns Volatility and Risk-Adjusted Returns"

---

### B. Deviations from Normality: Skewness and Kurtosis

- **Realistic Return Modeling**: Real-world asset returns are *not* normally distributed. Assuming normality underestimates the probability of extreme returns.
- **Skewness**: Measures asymmetry of the return distribution.
  - *Normal distribution*: Skewness = 0 (symmetric)
  - *Negative skewness*: Higher probability of outcomes below the mean (common in hedge funds)
  - *Positive skewness*: Higher probability of outcomes above the mean
- **Kurtosis**: Measures the "fatness" of tails.
  - *Normal distribution*: Kurtosis = 3
  - *Fat tails* (Kurtosis > 3): Greater probability of very large negative or positive outcomes, observed in many asset returns.

> Sources:  
> "Beyond Normality: The Reality of Asset Returns"  
> "Measuring Risk: Deviations from Normality"

---

### C. Downside Risk Measures

- **Semi-volatility (Semi-deviation)**: Measures only volatility of returns below the mean (or zero).
- **Value at Risk (VaR)**: The maximum loss that can occur with a given probability over a time period (e.g., 99% monthly VaR excludes the worst 1% of losses).
  - *Historical VaR*: Based on historical data.
  - *Parametric VaR*: Assumes a distribution (e.g., Gaussian).
  - *Cornish-Fisher VaR*: Adjusts for skewness and kurtosis.
- **Conditional Value at Risk (CVaR) / Expected Shortfall**: The average loss for outcomes that exceed the VaR threshold, providing insight into the magnitude of extreme losses.

> Sources:  
> "Downside Risk Measures: VaR and CVaR"  
> "Measuring Downside Risk: Semideviation, VaR, and CVaR"  
> "Constructing the Efficient Frontier: Data Preparation and Analysis"  
> "Visualizing CPPI: Histograms and Violation Analysis"

---

### D. Drawdowns

A drawdown is the percentage loss from a previous peak in wealth:  
`Drawdown = (current wealth - previous peak) / previous peak`  
The *maximum drawdown* is the largest such loss over a specified period.

> Source:  
> "Computing Drawdowns with Python"

---

## II. Modeling Asset Returns

### A. Geometric Brownian Motion (GBM)

- **GBM Model**: Used for simulating random stock prices and returns.
- **Core Equation**:
  - *Drift (μ)*: Expected return or trend; positive drift means upward bias.
  - *Stochastic Component (σ × dWt)*: Random fluctuations; σ is volatility, dWt is Brownian motion (pure random walk with independent increments).

> Sources:  
> "Modeling Stock Prices with Geometric Brownian Motion"  
> "Modeling Asset Returns: The Brownian Motion Random Walk"  
> "Shaping Outcomes: Monte Carlo, Mu, Sigma, and CPPI"

---

### B. Time-Varying Parameters

- **Interest Rates (r_t)**: Modeled as stochastic, mean-reverting (e.g., CIR or Vasicek models).
  - *Mean reversion speed (a)*, *long-term mean (b)*.
  - CIR model prevents negative rates via a square root adjustment.
- **Volatility (σ_t) / Variance (V_t)**: Can be time-varying, often modeled as mean-reverting.
- **Sharpe Ratio (λ_t)**: Risk premia may also be time-varying.

> Sources:  
> "Monte Carlo: Time-Varying Parameters for Realistic Asset Returns"  
> "Interest Rate Modeling and Bond Hedging"

---

## III. Liability-Driven Investing (LDI) and Portfolio Construction

### A. The Purpose of LDI

- **Objective**: Ensure assets are sufficient to meet future liabilities (e.g., retirement needs), measured by the *funding ratio*.

> Sources:  
> "Measuring Investment Liabilities and Funding Ratios"  
> "LDI-LectureNote.pdf"

---

### B. Measuring Investment Liabilities

- **Present Value**: Each future liability is discounted using discount factors (the price of zero-coupon bonds maturing on payment dates), often assuming a flat yield curve for simplicity.

> Source:  
> "Measuring Investment Liabilities and Funding Ratios"

---

### C. Liability Hedging Portfolios (LHP)

- **LHPs**: Asset portfolios designed to pay cash flows matching the liabilities in date and amount.
- **Typical instruments**: Nominal bonds or inflation-linked bonds.

> Source:  
> "Liability Hedging Portfolios: Immunizing Against Unexpected Increases in Liability Value"

---

### D. Duration Matching

- **Duration Matching**: Aligns the duration of asset portfolios with that of liabilities (using Macaulay duration) to immunize against interest rate changes.
- If exact zero-coupon bonds are unavailable, combine coupon bonds of different maturities to match target durations.

> Source:  
> "Duration Matching for Coupon Bonds"

---

### E. Policy Portfolio and Asset Allocation

- **Policy Portfolio**: The strategic allocation of assets.
- When simulating bond prices for asset allocation, account for coupon reinvestment risk as changing interest rates introduce return uncertainty.

> Source:  
> "The Policy Portfolio and Asset Allocation"

---

### F. Capitalization-Weighted Index Construction

- **Cap-Weighted Indices**: Weights are proportional to market capitalization (shares outstanding × price), reflecting the total value of constituent companies (e.g., S&P 500).

> Source:  
> "Market Correlations and Capitalization-Weighted Index Construction"

---

### G. Efficient Frontier

- **Efficient Frontier**: Set of portfolios with the highest expected return for a given risk, or lowest risk for a given return.
- Portfolios not on the frontier are "dominated" by at least one on the frontier.

> Sources:  
> "The Efficient Frontier of Portfolio Management"  
> "Plotting the Efficient Frontier: Two-Asset Portfolio Analysis"

---

## IV. Downside Protection Strategies

### A. Constant Proportion Portfolio Insurance (CPPI)

- **CPPI**: Dynamic allocation strategy designed to protect a portfolio floor.
  - *Cushion*: Account value minus the floor.
  - *Multiplier (m)*: Fraction of cushion allocated to the risky asset (PSP), remainder to the safe asset (GHP).
  - *Aggressiveness*: Higher m increases upside potential but also the risk of breaching the floor, especially in volatile markets. Lower m (e.g., 1.5 or 2) reduces violations; m=1 is very conservative.
  - *Floor Violations*: Portfolio falls below the floor; frequency and severity depend on m and volatility.
  - *Dynamic vs. Fixed Mix*: CPPI adjusts allocations dynamically, unlike fixed or glide path strategies.
  - *Drawdown Allocator*: Instead of a fixed floor, the floor can be set as a percentage of the running peak value (max drawdown constraint).

> Sources:  
> "CPPI: Downside Protection and Drawdown Control"  
> "Optimizing Equity Portfolios for Liability Hedging and Risk Management"  
> "Shaping Outcomes: Monte Carlo, Mu, Sigma, and CPPI"  
> "CPPI: Market Volatility and Aggressivity"  
> "Visualizing CPPI: Histograms and Violation Analysis"

---

### B. Performance and Statistics

- **Terminal Wealth**: Final value of the portfolio at the end of the investment period.
- **Breach Frequency/Probability**: How often the portfolio falls below the floor.
- **Expected Shortfall**: Average loss in scenarios where the floor is breached.

> Sources:  
> "Beyond LDI: Aligning Performance and Liability Hedging"  
> "Visualizing CPPI: Histograms and Violation Analysis"

---

## V. Specific Applications and Data

### A. Hedge Fund Returns

- **Non-Normal Returns**: Hedge funds often have negative skewness and high kurtosis ("fat tails"). The Jarque-Bera test often rejects normality for such returns.

> Sources:  
> "Beyond Normality: The Reality of Asset Returns"  
> "Measuring Risk: Deviations from Normality"

---

### B. Market Data

- **Datasets**: For example, "Portfolios_formed_on_ME_monthly" (Ken French) includes monthly returns by market capitalization. These datasets cover long periods and require careful handling of missing data (e.g., -99.99).

> Source:  
> "Returns Volatility and Risk-Adjusted Returns"

---

### C. Emerging Markets

- **Scope**: Investment partners operate in global developed and emerging markets (e.g., Russia, Turkey, China, India, Indonesia, South Korea, Australia, Brazil, Chile, Morocco).

> Source:  
> "edhec_publication_dynamic_ldi_strategies_0_2.pdf"

---