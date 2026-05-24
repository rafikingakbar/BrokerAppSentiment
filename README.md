<div align="center">

<img src="https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white"/>
<img src="https://img.shields.io/badge/HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black"/>
<img src="https://img.shields.io/badge/Google_Play-414141?style=for-the-badge&logo=google-play&logoColor=white"/>

<br/><br/>

# Broker App Sentiment Analysis
### Sentiment Analysis & Comparison of Indonesian Retail Securities Broker Apps

**Ajaib &nbsp;·&nbsp; IPOT &nbsp;·&nbsp; Stockbit** — via Google Play Store Reviews

<br/>

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square)
![Reviews](https://img.shields.io/badge/Reviews-6,000-orange?style=flat-square)
![Model](https://img.shields.io/badge/Model-IndoRoBERTa-purple?style=flat-square)

</div>

---

## Overview

Retail securities apps like **Ajaib**, **IPOT**, and **Stockbit** serve millions of active users, yet user perception of their service quality has rarely been studied systematically. This project builds a complete pipeline from **scraping to topic clustering** to answer:

- How is user sentiment distributed across each app?
- What are the most recurring complaint themes?
- Which app performs most favorably based on user reviews?

---

## Pipeline

```
Google Play Scraping        2,000 reviews x 3 apps = 6,000 total
        |
Text Preprocessing          Lower Case -> Remove HTML -> Remove Punctuation
                            -> Remove Emoji -> Word Normalization
        |
Sentiment Classification    IndoRoBERTa (w11wo/indonesian-roberta-base-sentiment-classifier)
        |
Evaluation                  300 manual labels -> Confusion Matrix, Accuracy, F1-Score
        |
Topic Clustering            TF-IDF -> K-Means (k=6) vs Agglomerative -> PCA Visualization
        |
Complaint Theme Analysis    Per app based on cluster top words
```

---

## Repository Structure

```
BrokerAppSentiment/
|
+-- notebook/
|   +-- broker_sentiment.ipynb              # Full pipeline in a single notebook
|
+-- data/
|   +-- 01_reviews_all_sekuritas_raw.csv    # Raw scraping output
|   +-- 02_reviews_data_normalized.csv      # After preprocessing
|   +-- 03_reviews_data_SentimenLabelling.csv  # After auto-labelling
|   +-- 04_evaluasi_300_data.csv            # 300 samples for manual evaluation
|   +-- 05_reviews_data_SentimenNegative.csv   # Filtered negative reviews
|
+-- assets/                                 # Result visualizations
|   +-- sentiment_distribution.png
|   +-- sentiment_piechart_negative.png
|   +-- wordcloud_positive.png
|   +-- wordcloud_negative.png
|   +-- confusion_matrix.png
|   +-- elbow_kmeans.png
|   +-- pca_scatter.png
|   +-- cluster_proportion.png
|
+-- README.md
+-- requirements.txt
```

---

## Key Results

### Sentiment Distribution per App

| App      | Negative | Neutral | Positive |
|:--------:|:--------:|:-------:|:--------:|
| Ajaib    | 743      | 291     | 962      |
| IPOT     | 414      | 157     | 1,421    |
| Stockbit | 1,109    | 242     | 637      |

![Sentiment Distribution](assets/sentiment_distribution.png)

> **IPOT** has the highest share of positive reviews (71%), while **Stockbit** has the highest negative rate (49%), and **Ajaib** shows a more balanced distribution (32.8% negative).

---

### IndoRoBERTa Model Evaluation

![Confusion Matrix](assets/confusion_matrix.png)

The model was evaluated on **300 manually labeled samples**. It performs best on positive and negative classes; the neutral class is harder to classify due to ambiguous reviews — short texts or positive words used in a complaint context.

---

### Sentiment WordCloud

![WordCloud Positive](assets/wordcloud_positive.png)
![WordCloud Negative](assets/wordcloud_negative.png)

---

### Topic Clustering — K-Means (k=6)

![PCA Scatter](assets/pca_scatter.png)

| # | Theme | Cluster | Top Words |
|---|-------|:-------:|-----------|
| 1 | System Disruption during Open Market | 0 & 2 | error, eror, market, jam, open, pagi |
| 2 | Performance Issues & Update Impact | 1 | lemot, parah, update, aplikasi |
| 3 | Verification & Account Access Problems | 3 | verifikasi, akun, susah, login, daftar |
| 4 | App Complexity & Usability | 4 | ribet, buka, saham, update |

![Cluster Proportion](assets/cluster_proportion.png)

---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/rafikingakbar/BrokerAppSentiment.git
cd BrokerAppSentiment

# 2. Install dependencies
pip install -r requirements.txt

# 3. Open the notebook
jupyter notebook notebook/broker_sentiment.ipynb
```

> Data is already available in the `data/` folder — the scraping step can be skipped, start directly from **Preprocessing**.

---

## Tech Stack

| Category | Library |
|----------|---------|
| Scraping | `google-play-scraper` |
| NLP & Preprocessing | `transformers`, `nltk`, `demoji` |
| Machine Learning | `scikit-learn` (TF-IDF, K-Means, Agglomerative, PCA) |
| Visualization | `matplotlib`, `seaborn`, `wordcloud` |
| Pretrained Model | [`w11wo/indonesian-roberta-base-sentiment-classifier`](https://huggingface.co/w11wo/indonesian-roberta-base-sentiment-classifier) |

---

**Author:** Rafi King Akbar
