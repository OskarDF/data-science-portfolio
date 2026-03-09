# Transaction Anomaly Detection

**Type:** Proof of Concept  
**Method:** Unsupervised Machine Learning, Isolation Forest  
**Dataset:** Synthetic — 1000 randomised transactions

---

## What It Does

Automatically identifies unusual transactions in a dataset of 1000 synthetic credit card transactions — without any predetermined labels or examples of fraud. The model learns what "normal" looks like and flags anything that deviates significantly.

---

## How It Works

1. **Dataset generation** — 1000 transactions described by 4 variables: transaction amount (kr), hour of day, distance from home (km), and number of transactions that day
2. **Feature scaling** — StandardScaler normalises all variables so no single feature dominates due to scale differences
3. **Isolation Forest** — unsupervised anomaly detection algorithm that isolates outliers by randomly partitioning the feature space. Anomalies are easier to isolate than normal observations and therefore receive lower anomaly scores
4. **Flagging** — transactions scoring below the contamination threshold (5%) are flagged as anomalous
5. **Priority ranking** — flagged transactions sorted by anomaly score, most suspicious first

---

## Dataset

- **Type:** Synthetically generated using numpy random distributions
- **Size:** 1000 transactions
- **Variables:** amount (kr), hour (0–23), distance from home (km), transactions today (count)
- **No predetermined fraud** — anomalies emerge purely from statistical deviation

---

## Results

| Metric | Value |
|--------|-------|
| Total transactions | 1000 |
| Flagged as anomalous | ~50 (5% contamination rate) |
| Method | Isolation Forest |

Flagged transactions showed notably higher average amounts and greater distances from home compared to the normal population — consistent with intuitive fraud indicators.

---

## Key Findings

- The model successfully identified transactions that were simultaneously unusual across multiple variables — something simple threshold rules cannot do
- Scatter plot of amount vs distance from home showed clear visual separation between flagged and normal transactions
- Average characteristics table confirmed flagged transactions had higher amounts and greater distances from home

---

## Limitations & Next Steps

- **Synthetic data** — real transaction data would include additional signals such as merchant category, device fingerprint, and transaction velocity
- **No ground truth** — because no labels exist, precision and recall cannot be measured directly. In production, analyst review of flagged cases creates a feedback loop for model improvement
- **Contamination parameter** — the 5% threshold is a judgment call. Too low misses anomalies, too high overwhelms analysts with false positives
- **Planned:** Apply to real credit card fraud dataset (Kaggle) with ground truth labels for proper evaluation

---

## How To Run

1. Open `anomaly_detection.ipynb` in Google Colab
2. Runtime → Run all
3. No additional installations required

---

## Files

```
04_anomaly_detection/
├── README.md
└── anomaly_detection.ipynb
```
