# 🎵 RateYourMusic Album Recommender System

**NLP · Unstructured Data · Recommender Systems · TF-IDF · Embeddings · Sentiment Analysis**

## Overview
Music discovery is a language problem. Listeners describe albums using subjective, inconsistent wording (e.g., *“spacey”* vs *“atmospheric”*), which makes simple keyword or rating-based recommendation ineffective.

This project builds a **content-based album recommender** using crowdsourced RateYourMusic reviews. It converts unstructured review text into numerical representations and recommends albums based on a listener’s desired attributes (e.g., **genre + instrument + vibe**). The system compares **TF-IDF (exact-match)** and **embedding-based (semantic)** similarity, with sentiment and evidence snippets for interpretability.

---

## Business Question
**How can unstructured review text be used to recommend albums that match a listener’s desired attributes, and how do TF-IDF and embedding-based methods differ in practice?**

---

## Data
- Scraped RateYourMusic album reviews  
- Album, artist, review text, and user rating  
- Reviews aggregated at the **album level** to form a crowd-sourced description  

---

## NLP Pipeline
- Text cleaning and normalization (lowercasing, punctuation removal, stopwords)  
- **Lemmatization** to merge word variants  
- **Unigrams + bigrams** to preserve music-specific phrases (e.g., `post_punk`)  
- Attribute discovery using frequency + co-occurrence (lift)  
- **Sentiment analysis (VADER)** to distinguish positive vs negative attribute mentions  

---

## Recommendation Methods
**User input:** 3 attributes (genre + instrument + mood)

1. **TF-IDF + Cosine Similarity**  
   - Strong for precise, interpretable, exact-match intent  

2. **TF-IDF + Sentiment Evidence**  
   - Adds context and prevents false positives from negative mentions  

3. **Embeddings + Cosine Similarity**  
   - Captures semantic similarity and paraphrases (e.g., *“shredding”* ≈ *“guitar riffs”*)  

---

## Outputs
- **Top 3 album recommendations**
- **Top 20 contenders** for transparency  
- Each result includes similarity score, sentiment context, ratings, and an evidence snippet  

---

## Key Takeaways
- Review text contains rich signals that ratings alone miss  
- **TF-IDF** excels at exact intent matching  
- **Embeddings** improve recall for vibe-based discovery  
- Sentiment + evidence significantly improves trust and interpretability  

---

## Tools & Skills
Python · Pandas · scikit-learn · NLP preprocessing · TF-IDF · Cosine similarity · Sentiment analysis · Embeddings · Recommender systems

---
