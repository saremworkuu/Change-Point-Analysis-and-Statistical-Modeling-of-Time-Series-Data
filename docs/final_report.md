# How Geopolitical Events Shock Oil Markets: A Bayesian Analysis of Brent Oil Prices

**Published:** July 14, 2026  
**Analysis Period:** 1987-1991  
**Methodology:** Bayesian Change Point Detection with PyMC

---

## Executive Summary

When Iraq invaded Kuwait on August 2, 1990, the world held its breath. Within weeks, Brent oil prices nearly doubled from ~$15 to over $30 per barrel. But was this really caused by the invasion, or was it coincidence? 

Using Bayesian change point detection on historical Brent oil price data (1987-1991), we identified a structural break in oil prices that aligns precisely with the Gulf War crisis. Our analysis quantifies the impact: a **55% increase in average oil prices** following the invasion, with **volatility increasing by 65%** as markets grappled with uncertainty.

This analysis provides data-driven insights for investors, policymakers, and energy companies seeking to understand how geopolitical events ripple through energy markets.

---

## The Data: Oil Prices in Turbulent Times

Our analysis covers 1,048 daily Brent oil price observations from May 20, 1987 to June 25, 1991—a period bookended by relative stability but punctuated by one of the most dramatic oil shocks in modern history.

**Key Statistics:**
- **Price Range:** $11.93 to $41.45 per barrel
- **Mean Price:** $19.23 per barrel
- **Standard Deviation:** $5.47 per barrel

We compiled 15 major geopolitical events during this period, including:
- Black Monday stock market crash (1987)
- Iran-Iraq War ceasefire (1988)
- Iraqi invasion of Kuwait (1990)
- Gulf War military operations (1990-1991)
- OPEC production decisions

---

## The Methodology: Bayesian Change Point Detection

Traditional statistical methods struggle with identifying *when* structural changes occur in time series data. They often assume parameters are constant throughout the entire period—a clearly unrealistic assumption for oil markets.

We used **Bayesian change point detection** to solve this problem. Here's how it works:

### The Model

1. **Switch Point (τ):** We defined a discrete uniform prior for the change point across all possible time indices. This allows the data to "speak" about where the break occurred.

2. **Two Regimes:** We modeled two distinct regimes with different means (μ₁, μ₂) and standard deviations (σ₁, σ₂). The "before" regime represents normal market conditions, while the "after" regime captures the new normal after the shock.

3. **Switch Function:** Using `pm.math.switch`, we select the appropriate parameters based on whether each observation falls before or after the detected change point.

4. **Likelihood:** We connected the model to observed prices using a Normal distribution, with the mean determined by the switch function.

### Why Bayesian?

- **Uncertainty Quantification:** We get full posterior distributions, not just point estimates
- **Prior Knowledge:** We can incorporate domain knowledge about oil market behavior
- **Probabilistic Statements:** We can say "there's a 95% probability that prices increased by X%"
- **Flexibility:** The framework easily extends to more complex models

We ran MCMC sampling with 4 chains, 5,000 draws each, using NUTS for continuous parameters and Metropolis for the discrete switch point. Convergence diagnostics (R-hat ≈ 1.0) confirmed reliable results.

---

## The Findings: A Clear Structural Break

### Change Point Detection

Our model detected a structural break in Brent oil prices with high certainty:

- **Median Change Point:** August 6, 1990
- **94% Credible Interval:** July 30, 1990 to August 13, 1990

This timing is remarkable. The Iraqi invasion of Kuwait occurred on **August 2, 1990**—right in the middle of our detected change point interval. The market responded within days.

### Price Impact Quantification

The change point analysis revealed dramatic shifts in both price levels and volatility:

**Price Levels:**
- **Before Change Point (μ₁):** $17.85 per barrel (95% HDI: $17.62 to $18.08)
- **After Change Point (μ₂):** $27.73 per barrel (95% HDI: $27.23 to $28.23)
- **Price Increase:** $9.88 per barrel (95% HDI: $9.15 to $10.61)
- **Percentage Increase:** 55.3% (95% HDI: 51.8% to 58.9%)

**Volatility:**
- **Before Change Point (σ₁):** $1.94 per barrel
- **After Change Point (σ₂):** $3.20 per barrel
- **Volatility Increase:** 65.0%

### Visualizing the Shock

![Brent Oil Prices with Detected Change Point](../figures/change_point_with_events.png)

The visualization shows the detected change point (blue line) with its 94% credible interval (shaded blue). Events within 30 days of the change point are highlighted in red. The Iraqi invasion of Kuwait aligns almost perfectly with our detected structural break.

---

## Event Correlation: Connecting Dots

### Events Within the Change Point Window

Our analysis identified several events temporally proximate to the detected change point:

| Date | Event | Days from Change Point |
|------|-------|------------------------|
| August 2, 1990 | Iraqi Invasion of Kuwait | 4 days before |
| August 7, 1990 | UN Sanctions on Iraq | 1 day after |
| August 9, 1990 | Operation Desert Shield Begins | 3 days after |

The clustering of these events around our detected change point strengthens the hypothesis that the Gulf War crisis triggered the structural break in oil prices.

### The Narrative

Here's what the data tells us happened:

1. **Pre-Crisis Stability (May 1987 - July 1990):** Brent oil prices averaged $17.85 with relatively low volatility ($1.94). The market was stable, with minor fluctuations around the mean.

2. **The Shock (August 1990):** Iraq invaded Kuwait on August 2. Within days, the UN imposed sanctions, and the U.S. began Operation Desert Shield. Our model detected the change point around August 6.

3. **Crisis Period (August 1990 - February 1991):** Prices surged to an average of $27.73—a 55% increase. Volatility spiked by 65% as the market grappled with uncertainty about supply disruptions.

4. **Post-War Normalization (March 1991 onwards):** Following Kuwait's liberation in February 1991, prices gradually declined but remained elevated compared to pre-crisis levels.

---

## Critical Caveats: Correlation ≠ Causation

Before drawing policy conclusions, we must address a fundamental limitation: **statistical correlation in time does not prove causal impact**.

### Why This Matters

- **Confounding Factors:** Oil prices are influenced by numerous simultaneous factors—global economic conditions, currency fluctuations, supply-demand dynamics, speculative trading, and more. Our model doesn't control for these.
- **Omitted Variable Bias:** The detected change point could be driven by unobserved factors we didn't include in our analysis.
- **Reverse Causality:** High oil prices can themselves trigger geopolitical events (e.g., oil-dependent regions experiencing political tension).
- **Market Anticipation:** Prices may have moved before the invasion as markets anticipated conflict.

### What We Can vs. Cannot Say

**We CAN say:**
- There is a strong temporal association between the Gulf War events and a structural break in oil prices
- The break involved a 55% increase in average prices and 65% increase in volatility
- The timing aligns precisely with the Iraqi invasion of Kuwait

**We CANNOT say:**
- The invasion *caused* the price increase (other factors may have contributed)
- Without the invasion, prices would have remained stable (counterfactual unknown)
- Similar events will always produce similar price responses (context matters)

### Strengthening Causal Claims

For stronger causal inference, future work should consider:
- **Counterfactual analysis:** What would prices have been without the event?
- **Difference-in-differences:** Compare affected vs. unaffected markets
- **Instrumental variables:** Find exogenous shocks affecting only the event
- **Structural modeling:** Build economic models of oil market dynamics

---

## Implications for Stakeholders

### For Investors

**Risk Management:** The analysis shows that geopolitical events can trigger rapid, large-scale price movements. Investors should:
- Maintain diversified portfolios to mitigate oil price exposure
- Use hedging strategies (futures, options) during periods of geopolitical tension
- Monitor geopolitical risk indicators for early warning signals

**Timing Insights:** The market responded within days of the invasion, suggesting that rapid information processing is crucial for investment decisions.

### For Policymakers

**Energy Security:** The 55% price increase demonstrates the vulnerability of global oil supplies to geopolitical shocks. Policymakers should:
- Develop strategic petroleum reserves
- Invest in alternative energy sources to reduce dependence
- Strengthen diplomatic relationships with oil-producing nations

**Economic Stability:** Oil price shocks can trigger broader economic impacts through inflation and production costs. Preemptive planning is essential.

### For Energy Companies

**Operational Planning:** The volatility increase (65%) during crisis periods highlights the need for:
- Flexible procurement strategies
- Scenario planning for different geopolitical outcomes
- Supply chain diversification

**Budget Planning:** Companies should build contingency budgets for potential price shocks, particularly during periods of geopolitical tension.

---

## Limitations and Future Work

### Current Limitations

1. **Single Change Point:** Our model assumes one dominant structural break. Real markets may experience multiple or gradual changes.

2. **No Control Variables:** We didn't control for other economic factors (GDP, inflation, exchange rates) that could influence prices.

3. **Temporal Scope:** Analysis covers only 1987-1991. Findings may not generalize to other periods.

4. **Brent Focus:** We analyzed only Brent crude. Other benchmarks (WTI, Dubai) may behave differently.

5. **Daily Frequency:** Intraday dynamics are missed with daily data.

### Future Work

**Model Extensions:**
- Multiple change point models to detect several structural breaks
- Regime-switching models (e.g., Markov-Switching) for volatility clustering
- VAR models to analyze dynamic relationships with macroeconomic variables

**Data Enhancements:**
- Extend analysis to longer time periods (1987-2022 as originally scoped)
- Include control variables (GDP, inflation, exchange rates)
- Analyze multiple oil benchmarks for comparison

**Causal Inference:**
- Implement counterfactual analysis methods
- Use difference-in-differences with control markets
- Build structural economic models

**Visualization:**
- Develop interactive dashboard for exploration
- Real-time monitoring of geopolitical risks
- Scenario analysis tools for stakeholders

---

## Conclusion: Data-Driven Insights in an Uncertain World

Our Bayesian change point analysis provides compelling evidence that the Gulf War crisis triggered a structural break in Brent oil prices. The 55% price increase and 65% volatility surge align precisely with the Iraqi invasion of Kuwait and subsequent events.

However, we must be cautious about causal claims. Correlation in time does not prove causation, and oil markets are influenced by numerous complex factors. The true value of this analysis lies not in definitive answers, but in:

1. **Quantifying Impact:** We can now say with confidence that prices increased by 55% (95% HDI: 52-59%) following the detected change point.

2. **Identifying Timing:** The change point occurred within days of the invasion, showing how quickly markets process geopolitical information.

3. **Informing Strategy:** Stakeholders can use these insights to improve risk management, policy planning, and operational decisions.

4. **Providing a Framework:** The Bayesian change point methodology can be applied to other periods, events, and commodities.

In an uncertain world where geopolitical events can send shockwaves through energy markets, data-driven analysis like this provides a foundation for better decision-making. By understanding how past events affected prices, we can better prepare for future uncertainties.

---

## Technical Appendix

### Model Specification

```python
with pm.Model() as change_point_model:
    # Switch point prior
    tau = pm.DiscreteUniform('tau', lower=int(0.1 * n_obs), upper=int(0.9 * n_obs))
    
    # Regime parameters
    mu_1 = pm.Normal('mu_1', mu=prices.mean(), sigma=prices.std() * 2)
    sigma_1 = pm.HalfNormal('sigma_1', sigma=prices.std())
    mu_2 = pm.Normal('mu_2', mu=prices.mean(), sigma=prices.std() * 2)
    sigma_2 = pm.HalfNormal('sigma_2', sigma=prices.std())
    
    # Switch function
    mu = pm.math.switch(time_indices < tau, mu_1, mu_2)
    sigma = pm.math.switch(time_indices < tau, sigma_1, sigma_2)
    
    # Likelihood
    likelihood = pm.Normal('likelihood', mu=mu, sigma=sigma, observed=prices)
```

### Convergence Diagnostics

- **R-hat values:** All < 1.01 (excellent convergence)
- **Effective Sample Size:** > 1000 for all parameters
- **Trace plots:** Show good mixing and stationarity

### Reproducibility

All code, data, and documentation are available in the project repository. The analysis can be reproduced by running the Jupyter notebook:

```bash
jupyter notebook notebooks/01_eda_and_change_point_analysis.ipynb
```

---

## Acknowledgments

This analysis was conducted for Birhan Energies as part of a data science challenge. We thank our tutors—Kerod, Feven, and Mahbubah—for their guidance and support.

The Bayesian modeling approach follows established practices in time series analysis and change point detection, drawing on methodologies from the PyMC community and statistical literature.

---

**Disclaimer:** This analysis is for educational and informational purposes only. It should not be used as the sole basis for investment decisions or policy recommendations. Always consult with qualified professionals before making significant financial or strategic decisions.
