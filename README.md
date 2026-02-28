# Nigeria's Carbon Crossroads: Predicting CO₂ Emissions with Machine Learning

![Nigeria CO2 Emissions](scenario_predictions.png)

## Motivation

Nigeria is urbanizing rapidly, its economy is growing, and energy demand is climbing. But what is actually driving its CO₂ emissions — and can socioeconomic indicators help us predict and understand future trajectories? This project applies the CRISP-DM data science process to three decades of World Bank data (1990–2023) to answer that question.

**Questions of Interest:**
- What factors drive Nigeria's CO₂ emissions the most?
- Can we accurately predict future emissions from socioeconomic indicators?
- How has rapid urbanization affected emissions over time?
- What would a green transition look like in measurable terms?

---

## Libraries Used

| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, and manipulation |
| `numpy` | Numerical operations and log transformation |
| `matplotlib` | Visualizations and plots |
| `scikit-learn` | Ridge Regression, cross-validation, scaling |
| `xgboost` | XGBoost model training and feature importance |
| `shap` | SHAP values for XGBoost model explainability |

---

## Repository Structure

| File | Description |
|---|---|
| `nigeria_co2_analysis.ipynb` | Main Jupyter notebook with full analysis, comments, and visualizations |
| `nigeria_co2_data.csv` | Raw dataset (World Bank, 1990–2023) containing CO₂, GDP per capita, energy use, renewable share, industry %, urban population %, and population growth |
| `feature_distributions.png` | Distribution plots for all features (1990–2023) |
| `correlation_heatmap.png` | Pearson correlation heatmap across all features and CO₂ |
| `industry_co2.png` | Dual-axis line plot showing diverging Industry vs CO₂ trends |
| `co2_model_evaluation.png` | 2×2 dashboard: feature importance, model comparison, actual vs predicted |
| `ridge_coefficients.png` | Ridge regression standardized coefficients and residual plot |
| `shap_analysis.png` | SHAP beeswarm, bar, dependence, and waterfall plots for XGBoost |
| `scenario_predictions.png` | What-if scenario analysis chart anchored to 2023 actual values |
| `README.md` | This file |

---

## Summary of Results

### Exploratory Data Analysis
- CO₂ emissions nearly doubled from ~75 Mt in 1990 to ~126 Mt in 2023
- GDP per capita is heavily right-skewed and was log-transformed before modeling
- Industry's share of GDP *fell* from ~37% to ~18% over the period — a counterintuitive finding given rising emissions
- Renewable energy share and CO₂ showed the strongest correlation (r = −0.94)
- Year and Urban population were found to be perfectly collinear (r = 1.00); Year was dropped

### Modeling
Two models were evaluated using Leave-One-Out cross-validation (LOO) — appropriate for the small dataset of 34 observations:

| Model | LOO MAE | KFold R² |
|---|---|---|
| Ridge Regression | 4.29 Mt ± 3.61 | 0.80 ± 0.16 |
| XGBoost | 4.29 Mt ± 3.61 | 0.77 ± 0.16 |

Ridge Regression was selected as the final model — identical performance to XGBoost but simpler, less prone to overfitting on small data, and directly interpretable via standardized coefficients.

### Key Findings
- **Renewable energy** is the dominant driver: a 1 std dev increase cuts CO₂ by **8.1 Mt**
- **Urbanization** is the strongest positive driver: a 1 std dev increase adds **+2.9 Mt**
- **Industry** and **PopGrowth** contribute negligible predictive value — both act as time proxies
- The rising CO₂ trend is driven by energy demand and urbanization outpacing renewable gains — not industrialization

### Scenario Analysis
Five what-if scenarios were run using exact 2023 values as the baseline:

| Scenario | Predicted CO₂ | vs 2023 (125.9 Mt) |
|---|---|---|
| Baseline (2023 conditions) | 127.2 Mt | +1.4 Mt |
| Green Transition | 102.1 Mt | −23.8 Mt |
| Energy Efficiency | 106.7 Mt | −19.2 Mt |
| Urban Boom | 123.3 Mt | −2.6 Mt |
| Worst Case | 129.9 Mt | +3.98 Mt |

A green transition combining maximum renewable deployment with reduced energy consumption could cut emissions by nearly **24 Mt** — reversing roughly a decade of growth.

---

## Acknowledgments

- **Data Source:** [World Bank Open Data](https://data.worldbank.org/) — CO₂ emissions, GDP per capita, energy use, renewable energy, urban population, industry value added, population growth
- **Methodology:** CRISP-DM (Cross-Industry Standard Process for Data Mining)
- **Blog Post:** [Read the non-technical writeup on Medium](#) ← *replace with your Medium link*
