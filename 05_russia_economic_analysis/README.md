# Russia Economic Indicators — Correlation & Predictive Analysis

**Type:** Analytical Project  
**Methods:** Correlation Analysis, Random Forest Regression, Lag Analysis  
**Data:** World Bank + FRED (Federal Reserve) — Annual 2000–2023  
**Author background:** International security & law, not a data scientist

---

## Motivation

Russia is notoriously opaque. Official statistics are manipulated, and the Kremlin controls the narrative. But you can't fake everything simultaneously — if oil revenues drop, something downstream has to show it, even if the direct signal is masked.

This project collects nine publicly available economic indicators for Russia and asks: **what relationships exist between them, and can they predict economic contraction?**

The underlying analytical question is whether open-source economic data can serve as a proxy for understanding Russian state behaviour and resilience — particularly in the context of sanctions pressure and military expenditure following the 2022 invasion of Ukraine.

---

## Data Sources

| Variable | Source | Coverage |
|----------|--------|----------|
| GDP growth (annual %) | World Bank | 2000–2023 |
| Inflation rate (%) | World Bank | 2000–2023 |
| Ruble/USD exchange rate | World Bank | 2000–2023 |
| Total foreign reserves (USD) | World Bank | 2000–2023 |
| Unemployment rate (%) | World Bank | 2000–2023 |
| Current account balance | World Bank | 2000–2023 |
| Government debt % GDP | World Bank | 2000–2023 |
| Brent crude oil price (USD) | FRED / Federal Reserve | 2000–2023 |

All data loaded programmatically — no manual downloads required.

---

## Key Findings

### Correlation Analysis

The correlation matrix revealed several analytically significant relationships:

**Strongest positive correlation:**
- Inflation rate ↔ Unemployment rate (+0.69) — Both spike simultaneously during crisis years, suggesting sanctions shocks cause unemployment and inflation concurrently rather than the classical inverse relationship. This may be a *sanctions signature* in the data.

**Strongest negative correlations:**
- Total reserves ↔ Unemployment rate (–0.80) — When Russia accumulates reserves through high oil revenues, unemployment falls. When reserves deplete, unemployment rises. This is the Putin social contract quantified: oil wealth buys political stability through state employment and social spending.
- Total reserves ↔ Inflation rate (–0.77) — High reserves suppress inflation. Reserve depletion correlates with inflationary pressure.
- Unemployment ↔ Ruble/USD (–0.71) — Ruble depreciation drives unemployment up, likely through reduced consumer purchasing power and import-dependent businesses.

### The Putin Social Contract in Numbers

Unemployment fell consistently from ~13% in 2000 to ~4% by 2019 — tracking almost perfectly with Putin's approval ratings over the same period. The two exceptions (2009, 2020) correspond to the global financial crisis and COVID-19 — both external shocks, both brief, both managed through state spending from reserves.

The war has placed this contract under significant strain: reserves partially frozen, inflation elevated, military casualties mounting.

### Predictive Model

A Random Forest regression model was trained to predict next year's GDP growth using all eight economic indicators.

| Metric | Value |
|--------|-------|
| Method | Leave-One-Out Cross Validation |
| Mean Absolute Error | 3.16% |
| Average actual GDP growth | 2.69% |
| Most important predictor | Unemployment rate |

The model captures the direction of economic trends reasonably well but underestimates the depth of crisis years (2009, 2022) — consistent with a known limitation of tree-based models on rare extreme events (tail risk).

### Lag Analysis

Testing whether oil price predicts ruble depreciation with a delay:

| Lag | Oil → Ruble correlation |
|-----|------------------------|
| 0 years | –0.07 |
| 1 year | +0.03 |
| 2 years | +0.08 |

At annual granularity, no meaningful lagged relationship was detected. This is likely a data granularity issue — monthly data would almost certainly reveal a clearer short-term transmission mechanism between oil price and ruble depreciation.

---

## Limitations

- **Annual granularity** — 20 data points is the primary constraint throughout. Monthly data would enable more robust correlation, lag analysis, and predictive modelling.
- **Multicollinearity** — unemployment rate and GDP growth are so tightly correlated that the model may be using unemployment as a proxy for GDP rather than as a genuine independent predictor.
- **Tail risk** — the model underestimates crisis years because extreme events are underrepresented in the training data by definition.
- **Data manipulation** — Russian official statistics are partially manipulated, particularly GDP figures post-2022. The ruble exchange rate and inflation data are more reliable as they are harder to falsify.
- **Missing variable** — Russian military spending data was unavailable after 2021 as Russia stopped reporting to the World Bank. This is itself an analytically significant data point.

---

## How To Run

1. Open `russia_economic_analysis.ipynb` in Google Colab
2. Add your free FRED API key (available at fred.stlouisfed.org)
3. Runtime → Run all

---

## Files

```
05_russia_economic_analysis/
├── README.md
└── russia_economic_analysis.ipynb
```

---

*This project was built as part of a self-directed data science learning portfolio by an international security professional. The methodology is proof-of-concept scale — the analytical framework is the point, not the model accuracy.*
