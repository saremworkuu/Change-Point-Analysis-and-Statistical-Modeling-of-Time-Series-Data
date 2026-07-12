# Change Point Analysis and Statistical Modeling of Brent Oil Prices

## Overview

This project analyzes how geopolitical events affect Brent oil prices using Bayesian change point detection. We identify structural breaks in oil price time series data and correlate them with major political, economic, and military events to understand their impact on energy markets.

**Business Context:** Conducted for Birhan Energies, a consultancy firm specializing in data-driven insights for the energy sector. The analysis helps investors, policymakers, and energy companies understand how major events influence oil prices for better decision-making.

## Project Structure

```
├── data/
│   ├── brent_oil_prices.csv          # Daily Brent oil prices (1987-1991)
│   ├── geopolitical_events.csv       # Compiled geopolitical events
│   ├── processed_brent_prices.csv   # Processed price data
│   └── processed_events.csv         # Processed event data
├── docs/
│   ├── data_analysis_workflow.md     # Detailed analysis methodology
│   ├── assumptions_and_limitations.md # Critical assumptions and limitations
│   ├── communication_strategy.md      # Stakeholder communication plan
│   └── interim_report.md             # Task 1 interim findings
├── notebooks/
│   └── 01_eda_and_change_point_analysis.ipynb  # Complete analysis notebook
├── figures/                          # Generated visualizations
├── results/                          # Model outputs and results
├── src/                              # Source code modules
├── tests/                            # Unit tests
├── requirements.txt                  # Python dependencies
└── README.md                         # This file
```

## Installation

### Prerequisites

- Python 3.9 or higher
- pip package manager

### Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd week10
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Create necessary directories:
```bash
mkdir -p figures results
```

## Usage

### Running the Analysis

The main analysis is contained in the Jupyter notebook:

```bash
jupyter notebook notebooks/01_eda_and_change_point_analysis.ipynb
```

The notebook performs:
- Exploratory Data Analysis (EDA)
- Stationarity testing
- Volatility analysis
- Bayesian change point modeling with PyMC
- MCMC sampling and convergence diagnostics
- Change point identification and impact quantification
- Event correlation analysis

### Key Components

**Data Analysis Workflow** (`docs/data_analysis_workflow.md`)
- Comprehensive methodology for analyzing Brent oil prices
- Step-by-step approach from data loading to insight generation
- Modeling choices and expected outputs

**Assumptions and Limitations** (`docs/assumptions_and_limitations.md`)
- Critical discussion of correlation vs. causation
- Data, model, and analysis assumptions
- Mitigation strategies for limitations

**Communication Strategy** (`docs/communication_strategy.md`)
- Stakeholder analysis and communication channels
- Content strategy by audience type
- Quality assurance and feedback mechanisms

## Data

### Brent Oil Prices
- **Source:** Historical daily prices
- **Period:** May 20, 1987 to June 25, 1991
- **Observations:** 1,048 daily price points
- **Price Range:** $11.93 to $41.45 per barrel

### Geopolitical Events
- **Events:** 15 major events compiled for analysis
- **Types:** Conflict, Political, Policy, Economic, Environmental
- **Key Events:** Iraqi invasion of Kuwait, Gulf War, OPEC decisions, UN sanctions

## Methodology

### Bayesian Change Point Detection

We use PyMC to implement a Bayesian change point model that:

1. **Defines a switch point (τ)** with a discrete uniform prior over time indices
2. **Models two regimes** with different means (μ₁, μ₂) and standard deviations (σ₁, σ₂)
3. **Uses MCMC sampling** to estimate posterior distributions
4. **Identifies structural breaks** probabilistically with uncertainty quantification

### Key Findings

**Initial EDA Results:**
- Major price shock during Gulf War (August 1990 - February 1991)
- Prices nearly doubled from ~$15 to ~$30+ per barrel
- Volatility clustering around geopolitical events
- Log returns are stationary (suitable for modeling)

**Expected Change Point:**
- The Iraqi invasion of Kuwait (August 2, 1990) is hypothesized to be the primary change point
- Model will detect the exact date with uncertainty quantification

## Deliverables

### Task 1 (Completed)
- ✅ Data analysis workflow documentation
- ✅ Geopolitical events dataset (15 events)
- ✅ Assumptions and limitations documentation
- ✅ Communication strategy
- ✅ Initial EDA with visualizations
- ✅ Interim report

### Task 2 (Completed)
- ✅ Complete Bayesian change point analysis notebook
- ✅ MCMC sampling and convergence diagnostics
- ✅ Change point identification and impact quantification
- ✅ Event correlation analysis
- ✅ Visualizations of posterior distributions

### Task 3 (Optional - Future Work)
- ⏳ Flask backend with data APIs
- ⏳ React frontend with interactive visualizations
- ⏳ Dashboard with filters and event highlighting

## Testing

Run unit tests:

```bash
pytest tests/
```

## Documentation

- **Interim Report:** `docs/interim_report.md` - Task 1 findings and methodology
- **Workflow:** `docs/data_analysis_workflow.md` - Detailed analysis steps
- **Assumptions:** `docs/assumptions_and_limitations.md` - Critical limitations
- **Communication:** `docs/communication_strategy.md` - Stakeholder strategy

## Key References

- [Change Point Detection in Time Series](https://forecastegy.com/posts/change-point-detection-time-series-python/)
- [Bayesian Changepoint Detection with PyMC3](https://www.pymc.io/projects/examples/en/latest/case_studies/change_point_analysis.html)
- [Data Science Workflow](https://www.datascience-pm.com/data-science-workflow/)

## Team

**Client:** Birhan Energies  
**Tutors:** Kerod, Feven, Mahbubah  
**Slack Channel:** #all-week10

## License

This project is part of an educational data science challenge.

## Acknowledgments

This analysis uses historical Brent oil price data and publicly available information about geopolitical events. The Bayesian modeling approach follows established practices in time series analysis and change point detection.
