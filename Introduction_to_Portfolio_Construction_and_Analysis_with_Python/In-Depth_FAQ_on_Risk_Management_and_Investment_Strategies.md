# In-Depth FAQ on Risk Management and Investment Strategies

This FAQ covers a range of risk management techniques, portfolio construction concepts, and their practical implementation in Python.

---

## 1. What are the benefits and limitations of traditional diversification?

**Benefits**:  
Diversification allows investors to efficiently harvest risk premiums by eliminating unrewarded, specific (idiosyncratic) risks from their portfolios. This results in portfolios positioned to generate the highest possible reward per unit of risk, since no one should hold unrewarded risk.

**Limitations**:  
Diversification often fails during severe market downturns when it's needed most. In events like the 2008 crisis, even well-diversified portfolios suffered significant losses (15-20%) as all stocks declined simultaneously. This is because diversification cannot manage *systematic risk* (affecting all assets); it only diversifies away asset-specific risk.

---

## 2. How does hedging differ from diversification, and for whom is it most suitable?

**Hedging** directly addresses systematic risks, such as interest rate changes. For example, if a drop in interest rates increases liabilities, a liability-hedging (duration-matching) portfolio can keep funding ratios stable by ensuring assets and liabilities are affected similarly.

Hedging is *symmetric*: it protects against downside, but also limits upside gains. It is best suited for wealthy investors or institutions already at or above a 100% funding ratio who prioritize protection over further upside. However, hedging can be costly, and most asset owners need upside potential to reduce future contributions.

---

## 3. What is Constant Proportion Portfolio Insurance (CPPI), and how does it combine elements of hedging and diversification?

**CPPI** is a dynamic allocation strategy offering both downside protection and upside potential, creating convex, option-like payoffs without explicit options.

- Assets are split between a risky asset and a safe asset.
- Allocation to the risky asset is a multiple (M) of the "cushion" (current asset value minus a floor).
- As the cushion shrinks, allocation to risk decreases; if the floor is reached, 100% is allocated to the safe asset.
- CPPI adapts risk-taking based on the margin for error—much like slowing down a car before a sharp turn and speeding up again after.

---

## 4. What is "gap risk" in CPPI, and how can it be managed?

**Gap risk** arises from discrete (not continuous) rebalancing. If a large loss occurs between rebalancing points, the portfolio value could breach the floor before adjustment is possible.

- Gap risk appears if the loss on the risky portfolio exceeds 1/M (e.g., with M=5, a 20% loss).
- To manage gap risk:
  - Lower the multiplier (M) to reduce floor breaches.
  - Calibrate M based on expected maximum loss per interval.
  - M=1 is conservative and almost eliminates violations, while higher M increases risk of breaches.

---

## 5. What are some extensions of basic CPPI strategies?

- **Maximum Drawdown Floor Protection**: Keeps losses from previous peaks under a set threshold (e.g., never lose more than 20% from a high). This uses a "running max" process to set a dynamic floor and allocates to risk based on the distance above this floor.
- **Capped Wealth Protection**: Investors set both a minimum floor and a maximum cap. When above a threshold (average of floor and cap), risk is reduced, smoothing the approach to the cap and reducing the cost of downside protection.

---

## 6. What is Liability-Driven Investing (LDI), and why is it dominant for institutions?

**LDI** is an investment paradigm focused on managing assets with explicit consideration of liabilities, especially for pension funds.

- It recognizes the need to both maximize performance (to reduce future contributions) and minimize downside relative to liabilities.
- LDI separates these goals, typically by dividing portfolios into performance-seeking and liability-hedging components.

---

## 7. What are the two main building blocks of LDI strategies?

- **Performance-Seeking Portfolio (PSP)**: Maximizes risk-adjusted returns by efficiently harvesting risk premiums. Its Sharpe ratio (Lambda) is a key metric.
- **Liability-Hedging Portfolio (LHP) / Goal Hedging Portfolio (GHP)**: Dedicated to matching and immunizing liability cash flows and risk factors (e.g., interest rates). Effectiveness is measured by beta with respect to liabilities; beta of zero means poor hedging.

---

## 8. Why is explicit separation of PSP and LHP important in LDI?

Explicit separation simplifies both portfolio construction and reporting. Each block has a clear objective (high performance or low liability risk), enabling more streamlined allocation and management compared to "mixed" surplus optimization portfolios.

- Separation allows the same PSP design across different funds.
- Not all funds adopt this due to skepticism about benefits or fears of performance loss, especially if underfunded.

---

## 9. How is investor welfare measured in the context of LDI strategies?

Investor welfare is measured by the quadratic utility of the final funding ratio—preferably high and stable.

Components:
1. Sharpe ratio of PSP (higher is better).
2. Correlation of LHP with liabilities (higher is better).
3. Risk-adjusted performance: a PSP that also hedges liabilities is preferred over one that doesn't, even if Sharpe ratios are equal.

---

## 10. What is the role of duration matching in liability hedging, and how is it implemented?

**Duration matching** immunizes the funding ratio against interest rate changes by aligning the duration of assets and liabilities.

- LHPs are constructed to match liability cash flows by using zero-coupon or coupon-bearing bonds.
- Macaulay duration (weighted average time to cash flow receipt) is matched between assets and liabilities.
- This approach stabilizes the funding ratio even with interest rate shifts.
- Python: Functions like `erk.bond_cash_flows`, `erk.macaulay_duration`, and `erk.match_durations` assist in constructing such portfolios.

---

## 11. What are the key risk measures used in finance, beyond volatility?

- **Semideviation**: Focuses on downside deviations only.
- **Maximum Drawdown**: Largest cumulative loss from a peak to a trough; intuitive but sensitive to data granularity.
- **Value at Risk (VaR)**:
  - *Historical VaR*: Empirical percentile of past returns, sensitive to sample period.
  - *Parametric Gaussian VaR*: Assumes normal returns, underestimates tail risk.
  - *Cornish-Fisher VaR*: Adjusts for skewness and kurtosis, more robust for non-normal returns.
- **Conditional Value at Risk (CVaR) / Expected Shortfall**: Average loss conditional on exceeding VaR. Provides a better sense of tail risk than VaR alone.

---

## 12. What is the Efficient Frontier (EF) in portfolio management, and how is it related to the Capital Market Line (CML) and the Maximum Sharpe Ratio (MSR) portfolio?

- **Efficient Frontier (EF)**: The set of portfolios that offer the highest return for a given risk, or lowest risk for a given return.
- **Capital Market Line (CML)**: When a risk-free asset is available, the EF becomes a straight line originating at the risk-free rate and tangent to the risky asset frontier.
- **Maximum Sharpe Ratio (MSR) Portfolio / Tangency Portfolio**: The portfolio at the tangent point; all mean-variance investors should hold a combination of this and the risk-free asset. The MSR portfolio diversifies away specific risk, holding only systematic risk.

---

## 13. What are the practical challenges and pitfalls in implementing Markowitz Analysis for portfolio optimization?

- **Estimation Error**: Optimizers are highly sensitive to input parameter errors, especially expected returns, often resulting in extreme, unrealistic allocations.
- Because expected returns are noisy and unreliable, many practitioners focus on the **Global Minimum Variance (GMV) portfolio**, which minimizes risk without relying on expected return estimates. If all expected returns are assumed equal, the MSR portfolio converges to the GMV portfolio.

---

## 14. How are Monte Carlo simulations and Python libraries used to model financial processes like Geometric Brownian Motion (GBM) and CIR?

- **Monte Carlo Simulations**: Model the random evolution of asset prices and interest rates.
- **GBM**: Simulates stock prices as a random walk with drift and volatility (mu, sigma).  
  - `numpy.random.normal` generates shocks; `erk.gbm` simulates prices.
- **CIR Model**: Simulates mean-reverting interest rates and zero-coupon bond prices (`erk.cir`).
- Interactive widgets (e.g., for mu, sigma, scenario count) provide intuition on parameter impacts. CPPI strategies can be simulated across many scenarios to test robustness.

---

## 15. How are investment returns, volatility, and drawdowns calculated and analyzed using Python?

- **Returns**:  
  - Calculated as (P_t+1 / P_t) - 1, vectorized with NumPy or in Pandas DataFrames.
  - Annualized as (1 + monthly return)^12 - 1, or adjust exponent for other frequencies.

- **Volatility**:  
  - Standard deviation of returns (`.std()`).
  - Annualized by multiplying monthly std by √12.

- **Drawdowns**:  
  - Compute wealth index (cumulative product of 1 + returns).
  - Track previous peaks (`.cummax()`).
  - Drawdown = (wealth index - previous peak) / previous peak.
  - The `erk.drawdown` function encapsulates these calculations for analysis and plotting.

---