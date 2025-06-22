# Asset-Liability Management (ALM) / Liability-Driven Investing (LDI)

---

## Purpose & Goals

- **Manage portfolio risk relative to liabilities** rather than only absolute risk.
- **Ensure resources** to meet future consumption patterns and liabilities.
- **Increase the funding ratio** (assets/liabilities) and mitigate sharp decreases.
- **Provide downside protection and upside potential** simultaneously.

---

## Historical Context: Pension Fund Crisis

- **Early 2000s (1999-2003):** S&P 500 companies’ collective DB pension plans shifted from a $240B surplus to a $250B+ deficit.
  - **"Perfect Storm"**: 
    - Decreasing equity markets (tech bubble burst) → sharp asset decline.
    - Decreasing interest rates → higher liability values (present value of liabilities rises as discount rates fall).
- **2008 Subprime Crisis:** Similar pattern repeated.
- **By 2009:** No US state pension plan had a 100% funding ratio.
- **Lesson:** Exposed weaknesses in risk management and asset allocation practices.

---

## Core LDI Paradigm: Two Building Blocks

### 1. Performance-Seeking Portfolio (PSP)
- **Objective:** Efficiently harvest risk premium.
- **Design:** Seeks to maximize the Sharpe Ratio (MSR).
- **Construction:** Built using diversification; allocation increases with Sharpe ratio, decreases with volatility/risk aversion.
- **Liability-friendly equity portfolios:** Can increase PSP allocation for the same risk budget.

### 2. Liability-Hedging Portfolio (LHP) / Goal-Hedging Portfolio (GHP)
- **Objective:** Hedge liabilities, reduce relative risk.
- **Mechanism:** Pays cashflows matching liability dates/amounts.
- **Investments:** Nominal bonds, inflation-linked bonds; use duration matching (Macaulay duration) to align interest rate sensitivity.
- **Zero-coupon bonds:** Ideal but rarely available; coupon bonds with matched duration can be used.
- **Derivatives:** Fixed-income and interest rate derivatives often employed.
- **Allocation:** Increases with the Beta of the LHP to liabilities.
- **Fixed Income:** Attractive for hedging, diversification, and performance.

### 3. Cash Account (Occasionally a Third Block)
- **Not a safe hedge for long-term liabilities** due to interest rate risk.
- **Zero-coupon bonds** provide more reliable funding ratios over the long term.

---

## Allocation Policy Between PSP & LHP

- **Fixed-Mix Combination:** Simple LDI strategy targeting a specific relative risk level via PSP allocation.
- **Dynamically Time-Varying Allocation (Dynamic LDI / DLDI):**
  - **Emergence:** Due to mark-to-market accounting and stricter solvency post-2000s crisis.
  - **Benefits:** Lower opportunity costs, respects minimum funding ratio constraints.
  - **Motivation:** Makes strategies responsive to shifting volatilities, correlations, and risk premia.
  - **Downside risk management:** Adjusts risk budgets dynamically; often uses derivatives (futures, options).

---

## Risk Management Frameworks & Measures in LDI

- **Funding Ratio (FR):** Central metric.
- **Volatility of Funding Ratio:** Measures risk to FR.
- **Maximum Drawdown of FR:** Largest potential loss in FR.
- **Probability of Shortfall:** Likelihood assets underperform liabilities.
- **Expected Shortfall (CVaR):** Average shortfall magnitude when it occurs.
- **Risk Budget ("Cushion" in CPPI):** Distance between asset value and a floor.
  - **Floors:** Minimum wealth levels to protect (principal protection or max drawdown).
  - **Caps:** Maximum wealth levels—sacrifice upside beyond a threshold to fund protection.

#### Risks in CPPI Strategies
- **Gap Risk:** Breaching floor due to losses between discrete trades; manifests if loss > 1/M (M = multiplier).
- **Violations:** Instances where value drops below floor.

---

## General Portfolio Construction & Optimization

### Efficient Frontier (EF)
- **Set of optimal portfolios** (highest return for given volatility, or lowest volatility for given return).
- **Shape changes** from curve to straight line with risk-free asset.

### Capital Market Line (CML)
- **Straight line tangent** to the risky asset EF.
- **Represents optimal portfolios** blending risk-free asset and tangency (MSR) portfolio.
- **Slope = Sharpe Ratio**.

### Maximum Sharpe Ratio (MSR) / Tangency Portfolio
- **Highest reward per unit risk** (max Sharpe).
- **Only systematic risk** (no specific/idiosyncratic risk).
- **Optimal for all mean-variance investors** (combination with risk-free asset).
- **Optimization:** Minimize negative Sharpe ratio.

### Global Minimum Variance (GMV) Portfolio
- **Lowest volatility portfolio** for a given asset set.
- **Does not depend on expected returns**, only covariances/variances.
- **Equivalent to MSR if all expected returns are equal.**

### Diversification
- **"Only free lunch in finance":** Combining uncorrelated assets reduces volatility.
- **Key in PSP design** for efficient risk premium extraction.

---

## Risk Measurement

- **Volatility / Standard Deviation:** Spread of returns; annualized by √12 for monthly data.
- **Semideviation:** Only downside deviation (returns < 0).
- **Value at Risk (VaR):** Maximum expected loss at a confidence level.
  - **Historical:** No distributional assumptions, subject to sample risk.
  - **Parametric Gaussian:** Assumes normality, underestimates tail risk.
  - **Cornish-Fisher (Semi-parametric):** Adjusts for skew/kurtosis, more robust for non-Gaussian returns.
- **Maximum Drawdown:** Largest % loss from peak to trough (granularity sensitive).
- **Calmar Ratio:** Return divided by trailing max drawdown (often over 36 months).

---

## Return Calculation & Data

- **Wealth Index:** Tracks compounded value.
- **Annualized Returns:** Converts shorter period returns to annual basis.
- **Excess Return:** Return above risk-free rate.
- **Covariance Matrix:** Essential for EF and Sharpe; diagonal = variances, off-diagonal = covariances.

---

## Dynamic Strategies & Implementation

### Constant Proportion Portfolio Insurance (CPPI)
- **Dynamically allocates** between risky and safe assets.
- **Goal:** Convex, option-like payoffs (without options).
- **Core:** Allocate M × cushion to risky asset.
- **Protection:** As value nears floor, risky allocation drops to zero.
- **Constraints:** 0-100% risky (no shorting/leverage).
- **Extensions:**
  - **Max Drawdown Floor:** Protects against losses > certain % from previous peaks (short-term liabilities).
  - **Capped Wealth:** Sacrifice upside beyond cap for protection/opportunity gain.

### Glide Path Allocation
- **Simulates target-date fund:** Gradual shift from risky to safe assets as horizon nears.

### Python Implementation & Tools

- **Backtesting & Simulation:**
  - `erk.run_cppi` — CPPI backtest
  - `erk.bt_mix` — Mixes two return series
  - `fixedmix_allocator`, `glidepath_allocator`, `drawdown_allocator` — Allocation rules
- **Interactivity:** `ipywidgets` for dynamic parameter adjustment
- **Data Handling:** `pandas`, `numpy` (e.g., `read_csv`, `cumprod`, `cummax`, `pct_change`, `dropna`, `shift`)
- **Plotting:** `matplotlib.pyplot`, `seaborn` for visualizations and density estimates

---

## Financial Models & Theory

- **Geometric Brownian Motion (GBM):** Models risky asset returns with drift (μ) and stochastic volatility (σ × dWt).
- **Cox-Ingersoll-Ross (CIR):** Mean-reverting interest rate model; used for zero-coupon bond pricing.
  - **Demonstrates**: Inverse relationship between rates and bond prices.
- **Discounting Liabilities:** Present value calculation using discount rates or zero-coupon bond prices.
- **Fund Separation Theorem:** Theoretical justification for PSP/LHP separation.
- **Quadratic Utility:** Used to maximize investor welfare (esp. funding ratio).
- **Optimal Portfolio Choice:** Based on continuous-time frameworks (e.g., Merton), assumes frictionless and continuous trading.

---

## EDHEC-Risk Institute (ERI)

- **Research leader in ALM/institutional investment.**
- **Publishes on dynamic LDI strategies.**
- **2014 Survey:** Comprehensive assessment of LDI adoption.
- **Focus:** Asset allocation, risk management, portfolio construction.
- **Initiatives:** ERI Scientific Beta (smart beta strategies).

---