# Norway Electricity Demand Forecasting

**Type:** Proof of Concept  
**Method:** Time Series Forecasting, Facebook Prophet  
**Error:** 2.7 TWh MAE (2.0% of actual demand)

---

## What It Does

Forecasts Norway's annual electricity demand using historical data from 1990 to 2024, with projections extending to 2035 and 2050.

Given 34 years of historical consumption data, the model identifies the long term trend and projects future demand — including uncertainty bounds that widen the further into the future the forecast extends.

---

## How It Works

1. **Data loading** — annual electricity demand data for Norway from Our World in Data (1990–2024)
2. **Train/test split** — chronological split, training on 1990–2020, testing on 2021–2023
3. **Prophet model** — Facebook's open source forecasting library, models trend and seasonality separately
4. **Validation** — predictions compared against actual 2021–2023 values before forecasting into the future
5. **Forecasting** — projects demand to 2035 and 2050 with 95% confidence intervals

---

## Dataset

- **Source:** Our World in Data — Energy Data (github.com/owid/energy-data)
- **Coverage:** Norway, 1990–2024
- **Granularity:** Annual
- **Unit:** TWh (terawatt hours)
- **Mean demand:** ~124 TWh per year

---

## Results

| Metric | Value |
|--------|-------|
| Mean Absolute Error | 2.7 TWh |
| Average actual demand (test period) | 136.5 TWh |
| Error as % of actual | 2.0% |
| 2035 forecast | ~155 TWh |
| 2050 forecast | ~161 TWh (range: 154–168 TWh) |

---

## Key Findings

- Norway's electricity demand shows a broadly upward trend from 1990 to present
- Demand growth flattened noticeably post-2010 due to efficiency improvements and deindustrialisation
- A visible dip in the early 2000s likely reflects the dot-com crash and economic slowdown
- The model achieves 2.0% error on held-out test data — strong performance for annual energy forecasting

---

## Limitations & Next Steps

- **Annual granularity** — annual data captures long term trend but hides seasonal patterns (winter vs summer peaks). Monthly data would enable seasonal forecasting.
- **Structural breaks** — the model extrapolates historical patterns but cannot anticipate structural shifts such as mass EV adoption, large scale data center growth, or offshore platform electrification. Real 2050 demand could significantly exceed the model's baseline projection.
- **Confidence intervals** — the 2050 confidence interval (154–168 TWh) is arguably too narrow for a 30 year forecast given the structural uncertainties above.
- **Planned:** Monthly granularity model with seasonal decomposition

---

## How To Run

1. Open `energy_forecasting.ipynb` in Google Colab
2. Runtime → Run all
3. The notebook installs Prophet automatically if not present

---

## Files

```
03_energy_forecasting/
├── README.md
└── energy_forecasting.ipynb
```
