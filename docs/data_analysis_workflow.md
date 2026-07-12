# Data Analysis Workflow: Brent Oil Price Change Point Analysis

## Overview
This document outlines the systematic approach for analyzing Brent oil prices and detecting structural breaks caused by geopolitical events using Bayesian change point detection.

## Analysis Steps

### Phase 1: Data Preparation and Understanding

**1.1 Data Loading and Validation**
- Load Brent oil price data from CSV (daily prices from 1987-1991)
- Convert Date column to datetime format
- Validate data completeness (check for missing values, duplicates)
- Verify price range and data types
- Load geopolitical events dataset with event dates, types, and descriptions

**1.2 Exploratory Data Analysis (EDA)**
- Plot raw price series over time to visualize trends and patterns
- Calculate and plot log returns: `log(price_t) - log(price_{t-1})`
- Analyze volatility clustering through rolling standard deviation
- Perform trend analysis (decomposition into trend, seasonal, residual components)
- Conduct stationarity testing using Augmented Dickey-Fuller (ADF) test
- Identify periods of high volatility visually

**1.3 Time Series Properties Investigation**
- **Trend Analysis**: Use moving averages and linear regression to identify long-term trends
- **Stationarity Testing**: Apply ADF test to determine if differencing is needed
- **Volatility Patterns**: Examine GARCH-like behavior in returns
- **Seasonality**: Check for recurring patterns (though less likely in daily oil prices)

### Phase 2: Change Point Modeling

**2.1 Model Design**
- Define Bayesian change point model using PyMC
- **Switch Point (τ)**: Discrete uniform prior over all possible time indices
- **Before Parameters (μ₁, σ₁)**: Mean and standard deviation for pre-change regime
- **After Parameters (μ₂, σ₂)**: Mean and standard deviation for post-change regime
- **Switch Function**: Use `pm.math.switch` to select parameters based on time index
- **Likelihood**: Normal distribution with mean determined by switch function

**2.2 Model Implementation**
- Set up PyMC model with appropriate priors
- Define the likelihood function connecting model to observed prices
- Configure MCMC sampler (NUTS) with appropriate number of draws and chains
- Run sampling and monitor convergence

**2.3 Model Diagnostics**
- Check convergence using R-hat statistics (target: r̂ ≈ 1.0)
- Examine trace plots for mixing and stationarity
- Review effective sample size (ESS) for each parameter
- Assess posterior predictive checks

### Phase 3: Interpretation and Analysis

**3.1 Change Point Identification**
- Plot posterior distribution of switch point (τ)
- Identify peak(s) indicating most probable change point dates
- Calculate credible intervals for change point timing
- Assess uncertainty in change point detection

**3.2 Impact Quantification**
- Plot posterior distributions for before/after parameters (μ₁, μ₂)
- Calculate mean price shift: `Δμ = μ₂ - μ₁`
- Compute percentage change: `(μ₂ - μ₁) / μ₁ × 100%`
- Generate probabilistic statements (e.g., "95% probability that price increased by X%")

**3.3 Event Correlation**
- Compare detected change point dates with geopolitical events timeline
- Identify events that temporally align with change points
- Formulate hypotheses about causal relationships
- Document time lags between events and price responses

### Phase 4: Reporting and Communication

**4.1 Stakeholder Communication**
- **Government Bodies**: Policy briefs focusing on energy security implications
- **Investors**: Risk assessment reports with quantified impact metrics
- **Energy Companies**: Operational planning recommendations
- **General Public**: Accessible summaries via blog posts and dashboards

**4.2 Deliverables**
- Technical report with methodology and findings
- Interactive dashboard for exploration
- Code repository with reproducible analysis
- Presentation slides for stakeholder meetings

## Modeling Choices Justification

### Why Change Point Models?
Change point models are ideal for identifying structural breaks in time series data. In the context of oil prices:
- They explicitly model regime shifts (e.g., from stable to volatile periods)
- They provide probabilistic estimates of when changes occurred
- They quantify the magnitude of changes between regimes
- They handle uncertainty naturally through Bayesian inference

### Why Bayesian Approach?
- Incorporates prior knowledge about oil market behavior
- Provides full posterior distributions (not just point estimates)
- Naturally handles uncertainty in change point detection
- Allows for probabilistic statements about impacts
- Flexible framework for extending to more complex models

### Expected Outputs
1. **Change Point Dates**: Posterior distribution of when structural breaks occurred
2. **Parameter Estimates**: Before/after means and standard deviations with uncertainty
3. **Impact Metrics**: Quantified price changes with confidence intervals
4. **Event Associations**: Hypotheses about which events triggered detected changes

### Limitations
- Correlation does not imply causation - temporal proximity doesn't prove causality
- Model assumes single change point (can be extended to multiple)
- Does not account for gradual changes or multiple simultaneous factors
- Sensitive to prior choices (though less so with sufficient data)
- Requires careful interpretation of results in context

## Assumptions

### Data Assumptions
- Daily prices are accurate and representative of market conditions
- Missing data (if any) is missing at random
- Price series is sufficiently long to detect meaningful change points

### Model Assumptions
- Single dominant change point in the analyzed period (for simple model)
- Prices follow approximately normal distribution within each regime
- Change point is abrupt (not gradual)
- Independence of observations conditional on regime

### Event Assumptions
- Compiled event dates are accurate
- Events have sufficient market impact to affect prices
- Time lags between events and price responses are relatively short

## Communication Channels

### Primary Channels
1. **Technical Reports**: PDF documents for detailed methodology
2. **Interactive Dashboard**: Web application for exploration
3. **Blog Posts**: Medium articles for broader audience
4. **Presentations**: Slide decks for stakeholder meetings

### Stakeholder-Specific Formats
- **Government**: Policy briefs with executive summaries
- **Investors**: Risk assessment dashboards with real-time data
- **Energy Companies**: Operational planning guides
- **Academic/Research**: Technical papers with full methodology

## Next Steps
1. Execute EDA to understand data properties
2. Implement and run Bayesian change point model
3. Interpret results and correlate with events
4. Develop interactive dashboard for visualization
5. Prepare final report and stakeholder communications
