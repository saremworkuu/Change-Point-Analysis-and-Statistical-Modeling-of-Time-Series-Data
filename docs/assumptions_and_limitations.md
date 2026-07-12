# Assumptions and Limitations

## Critical Distinction: Correlation vs. Causation

### The Fundamental Challenge
This analysis aims to identify relationships between geopolitical events and Brent oil price changes. However, it is crucial to understand that **statistical correlation in time does not prove causal impact**.

### Why Correlation ≠ Causation

**1. Temporal Proximity is Not Causation**
- Just because a price change follows an event does not mean the event caused it
- Multiple events may occur simultaneously, making attribution difficult
- Market anticipation can cause price movements before events occur
- Lagged effects can obscure the true timing of causal relationships

**2. Confounding Factors**
- Oil prices are influenced by numerous simultaneous factors:
  - Global economic conditions (GDP growth, recessions)
  - Currency fluctuations (USD strength)
  - Supply-demand dynamics from non-geopolitical sources
  - Speculative trading and market sentiment
  - Technological changes in extraction/production
  - Environmental policies and regulations
  - Alternative energy development

**3. Omitted Variable Bias**
- Our model focuses on geopolitical events but excludes many other relevant variables
- Detected change points may be driven by unobserved factors
- Attributing changes to specific events may be misleading

**4. Reverse Causality**
- High oil prices can themselves trigger geopolitical events
- Example: Oil price increases may lead to political tensions in oil-dependent regions
- Direction of causality is often ambiguous

### Our Approach to Causal Inference

**What We Can Do:**
- Identify temporal associations between events and price changes
- Quantify the magnitude of price shifts around event dates
- Formulate hypotheses about potential causal relationships
- Use domain knowledge to assess plausibility of causal links
- Acknowledge uncertainty in causal claims

**What We Cannot Do:**
- Prove that specific events caused specific price changes
- Isolate the effect of single events in complex systems
- Establish definitive causal relationships from observational data alone
- Rule out alternative explanations for observed patterns

### Recommended Causal Framework
For stronger causal claims, future work should consider:
- **Counterfactual analysis**: What would prices have been without the event?
- **Difference-in-differences**: Compare affected vs. unaffected markets
- **Instrumental variables**: Find exogenous shocks that affect only the event
- **Structural modeling**: Build economic models of oil market dynamics

## Data Assumptions

### Price Data Assumptions
1. **Accuracy**: Daily Brent oil prices are accurate representations of market transactions
2. **Representativeness**: Prices reflect the true market clearing price at each date
3. **Completeness**: Missing data (if any) is missing at random and does not bias analysis
4. **Consistency**: Price measurement methodology is consistent over the entire period
5. **Market Efficiency**: Prices incorporate all available information (weak form efficiency)

### Event Data Assumptions
1. **Date Accuracy**: Event dates are precisely recorded and correspond to market-relevant timing
2. **Completeness**: The compiled list includes all major events with significant oil market impact
3. **Impact Relevance**: Selected events have sufficient magnitude to affect oil prices
4. **Independence**: Events can be treated as distinct occurrences (though this may not always hold)
5. **Market Awareness**: Markets were aware of events at the recorded dates (no information delays)

## Model Assumptions

### Change Point Model Assumptions
1. **Single Change Point**: The simple model assumes one dominant structural break in the analyzed period
   - *Limitation*: Real markets may experience multiple or gradual changes
   - *Mitigation*: Can extend model to multiple change points if needed

2. **Abrupt Change**: The model assumes instantaneous regime shifts
   - *Limitation*: Some events may cause gradual transitions
   - *Mitigation*: Consider models with smooth transitions for future work

3. **Normal Distribution**: Prices within each regime are approximately normally distributed
   - *Limitation*: Financial returns often exhibit fat tails and skewness
   - *Mitigation*: Check residuals; consider alternative distributions if needed

4. **Independence**: Observations are independent conditional on the regime
   - *Limitation*: Time series data often exhibits autocorrelation
   - *Mitigation*: Check autocorrelation; include autoregressive terms if necessary

5. **Homogeneous Variance**: Variance is constant within each regime (though can differ between regimes)
   - *Limitation*: Volatility clustering is common in financial time series
   - *Mitigation*: Consider GARCH-type models for volatility modeling

### Bayesian Modeling Assumptions
1. **Prior Appropriateness**: Chosen priors are reasonable and do not unduly influence results
   - *Limitation*: Poor priors can bias results, especially with limited data
   - *Mitigation*: Use weakly informative priors; conduct sensitivity analysis

2. **MCMC Convergence**: The sampler has converged to the true posterior distribution
   - *Limitation*: Convergence diagnostics are necessary but not sufficient
   - *Mitigation*: Use multiple chains, check R-hat, examine trace plots

3. **Stationarity**: The posterior distribution is stable across sampling iterations
   - *Limitation*: Non-stationary posteriors indicate poor mixing or model misspecification
   - *Mitigation*: Run longer chains, reparameterize model if needed

## Analysis Limitations

### Temporal Limitations
1. **Data Period**: Analysis covers 1987-1991 only (based on provided data)
   - *Implication*: Findings may not generalize to other time periods
   - *Mitigation*: Clearly state temporal scope of conclusions

2. **Daily Frequency**: Daily data may miss intraday dynamics
   - *Implication*: Cannot analyze immediate market reactions within trading days
   - *Mitigation*: Acknowledge this limitation in interpretation

### Geographic Limitations
1. **Brent Focus**: Analysis focuses on Brent crude only
   - *Implication*: May not represent other oil benchmarks (WTI, Dubai, etc.)
   - *Mitigation*: Note that different benchmarks may behave differently

2. **Global Events**: Event compilation focuses on major geopolitical events
   - *Implication*: Regional or local events may be underrepresented
   - *Mitigation*: Clearly define event inclusion criteria

### Methodological Limitations
1. **Single Change Point**: Simple model detects only one structural break
   - *Implication*: Multiple smaller changes may be missed
   - *Mitigation*: Note this limitation; consider multi-change models for future work

2. **No Control Variables**: Model does not control for other economic factors
   - *Implication*: Attributing changes solely to events is problematic
   - *Mitigation*: Frame findings as associations, not causal claims

3. **No Forecasting**: Model is descriptive, not predictive
   - *Implication*: Cannot predict future price movements or event impacts
   - *Mitigation*: Clearly state descriptive nature of analysis

### Interpretation Limitations
1. **Hindsight Bias**: Analysis is conducted with knowledge of historical outcomes
   - *Implication*: May overstate the predictability of past events
   - *Mitigation*: Acknowledge hindsight bias in reporting

2. **Narrative Fallacy**: Tendency to construct coherent stories from random data
   - *Implication*: May create false narratives linking events to price changes
   - *Mitigation*: Maintain skepticism; emphasize uncertainty

3. **Multiple Testing**: Examining multiple events increases chance of spurious findings
   - *Implication*: Some apparent associations may be due to chance
   - *Mitigation*: Adjust significance thresholds; report all examined events

## Ethical Considerations

### Data Usage
- Historical price data is publicly available and used for analysis purposes
- Event information is compiled from public historical records
- No personally identifiable information is involved

### Interpretation Responsibility
- Findings should be presented with appropriate uncertainty
- Avoid overstating confidence in causal claims
- Acknowledge limitations clearly in all communications
- Distinguish between analysis results and policy recommendations

### Stakeholder Impact
- Analysis may influence investment decisions and policy
- Ensure communications are accurate and not misleading
- Provide appropriate context for all findings
- Avoid fear-mongering or sensationalism

## Mitigation Strategies

### For Correlation-Causation Issues
- Use cautious language ("associated with" not "caused by")
- Present alternative explanations
- Emphasize need for additional evidence
- Recommend experimental/quasi-experimental designs for causal claims

### For Model Limitations
- Conduct sensitivity analysis to prior choices
- Compare multiple model specifications
- Validate assumptions with diagnostic checks
- Report model fit and predictive performance

### For Data Limitations
- Clearly document data sources and quality
- Acknowledge missing data and potential biases
- Use appropriate techniques for handling missing values
- Validate findings with alternative data sources if possible

### For Communication Limitations
- Use multiple formats for different audiences
- Include technical appendices for detailed methodology
- Provide executive summaries for non-technical stakeholders
- Encourage feedback and questions from domain experts

## Conclusion

This analysis provides valuable insights into the temporal relationships between geopolitical events and Brent oil prices. However, all findings should be interpreted with appropriate caution, acknowledging the fundamental distinction between correlation and causation. The assumptions and limitations outlined here guide both the analysis process and the interpretation of results, ensuring that conclusions are grounded in a realistic understanding of what the methods can and cannot achieve.
