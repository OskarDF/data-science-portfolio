# News Headline Classifier

**Type:** Proof of Concept  
**Method:** Natural Language Processing (NLP), TF-IDF, Random Forest  
**Accuracy:** 67.5% (200 headline dataset)

---

## What It Does

Automatically classifies news headlines into one of four categories:

- 🔴 Security Threat
- 🟡 Political Instability
- 🟢 Diplomatic
- ⚪ Economic

Given a headline like *"Armed group seizes oil facility taking workers hostage"*, the model returns a category and a confidence score for each class.

---

## How It Works

1. **Text preprocessing** — stop words removed, text lowercased
2. **TF-IDF vectorization** — converts headlines into numerical vectors, weighting distinctive words higher than common ones
3. **Random Forest classifier** — trained on labeled headlines to learn category-specific word patterns
4. **Pipeline** — vectorization and classification chained into a single reusable object

---

## Dataset

- 200 manually labeled headlines across 4 categories (50 per category)
- Labels assigned based on headline content
- 80/20 train/test split with stratification to ensure balanced category representation

---

## Results

| Category | F1-Score |
|----------|----------|
| Security Threat | — |
| Political Instability | — |
| Diplomatic | — |
| Economic | — |
| **Overall Accuracy** | **67.5%** |

> Baseline (random guessing across 4 classes) = 25%

---

## Limitations & Next Steps

- **Dataset size** — 200 headlines is proof-of-concept scale. Production NLP systems typically require thousands of labeled examples per category. The AG News dataset (120,000 labeled articles) would be a natural next step.
- **Category overlap** — some headlines genuinely span multiple categories (e.g. economic sanctions triggering political unrest). Multi-label classification would handle this better.
- **Model** — Random Forest on TF-IDF is a strong baseline. Transformer-based models (BERT, RoBERTa) would significantly improve accuracy on ambiguous headlines.
- **Planned:** Streamlit web app for interactive headline classification

---

## How To Run

Open the notebook directly in Google Colab — no local installation required.

1. Open `headline_classifier.ipynb` in Google Colab
2. Runtime → Run all
3. Modify the `classify_headline()` function at the end to test your own headlines

---

## Files

```
01_headline_classifier/
├── README.md
└── headline_classifier.ipynb
```
