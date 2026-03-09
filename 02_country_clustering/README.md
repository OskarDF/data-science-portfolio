# Country Risk Clustering

**Type:** Proof of Concept  
**Method:** Unsupervised Machine Learning, K-Means Clustering, PCA  
**Dataset:** Synthetic — 50 fictional countries

---

## What It Does

Groups fictional countries into distinct risk profiles based on five security-relevant variables, without any predetermined labels or categories. The model finds natural groupings in the data entirely on its own.

---

## How It Works

1. **Dataset generation** — 50 fictional countries described by 5 variables: conflict intensity, military spending (% GDP), political stability, cyber threat level, and GDP per capita
2. **Feature scaling** — StandardScaler normalises all variables to the same scale, preventing high-value variables like GDP from dominating the clustering
3. **Elbow method** — tests k=1 through k=10 clusters to identify the optimal number of natural groupings
4. **K-Means clustering** — assigns each country to a cluster based on similarity across all five variables simultaneously
5. **PCA visualisation** — reduces 5 dimensions to 2 for plotting, capturing ~52% of total variance
6. **Cluster profiling** — average characteristics per cluster interpreted and labeled

---

## Dataset

- **Type:** Synthetically generated
- **Size:** 50 countries × 5 variables
- **Variables:** conflict intensity (0–10), military spending % GDP (0.5–8%), political stability (0–10), cyber threat level (0–10), GDP per capita ($500–$70,000)

---

## Results

Three natural clusters identified:

| Cluster | Profile | Countries |
|---------|---------|-----------|
| 0 | Stable & Wealthy — low conflict, high stability, high GDP | 16 |
| 1 | Developing & Vulnerable — low conflict, low stability, medium GDP | 26 |
| 2 | Fragile & High Risk — high conflict, high cyber threat, low GDP | 8 |

---

## Key Findings

- K-Means identified three distinct country archetypes without any human guidance
- Cluster 2 (Fragile & High Risk) showed markedly higher conflict intensity than other clusters — consistent with the "fragile state" profile in real geopolitical analysis
- PCA visualisation confirmed clear spatial separation between clusters

---

## Limitations & Next Steps

- **Synthetic data** — results reflect the distributions we programmed, not real geopolitical patterns. The methodology transfers directly to real datasets such as V-Dem, SIPRI, or World Bank indicators.
- **PCA variance** — the 2D visualisation captures only 52% of total variance. Some cluster separation visible in 5D space is lost in the plot.
- **Cluster number** — with synthetic data the elbow method produced a gradual curve rather than a sharp elbow, making k=3 a judgment call. Real data with genuine structure produces clearer results.
- **Planned:** Rerun with real country data from V-Dem and World Bank indicators

---

## How To Run

1. Open `country_clustering.ipynb` in Google Colab
2. Runtime → Run all
3. No additional installations required

---

## Files

```
02_country_clustering/
├── README.md
└── country_clustering.ipynb
```
