# 🎵 RateYourMusic Album Recommender System

> A content-based recommender that uses crowdsourced album reviews to find music matching any combination of genre + instrument + vibe. Compares TF-IDF exact-match vs. embedding-based semantic similarity with sentiment-aware evidence.

**Tech:** Python · scikit-learn · VADER · TF-IDF · Sentence Embeddings · Cosine Similarity · pandas · NLTK

---

## How It Works

**Input:** 3 attributes describing what you want to hear (e.g., `post-punk` + `guitar` + `melancholy`)

**Output:** Top album recommendations with similarity scores, sentiment context, and evidence snippets from real reviews.

```
Query: "post-punk" + "guitar" + "melancholy"

 Rank  Album                        Artist              Score   Sentiment
 ───── ──────────────────────────── ─────────────────── ─────── ──────────
  1    Disintegration               The Cure            0.87    ✅ Positive
  2    Unknown Pleasures            Joy Division        0.83    ✅ Positive
  3    Pornography                  The Cure            0.79    ✅ Positive

 Evidence: "...the guitar work is hauntingly melancholy, dripping
           with reverb and post-punk atmosphere..."
```

> *Example output — actual results depend on the review corpus.*

---

## The Problem

Music discovery is fundamentally a **language problem**. Listeners describe albums using subjective, inconsistent wording — *"spacey"* vs *"atmospheric"*, *"shredding"* vs *"guitar riffs"*. Rating-based collaborative filtering misses these nuances entirely, and keyword search fails on paraphrases.

This project asks: **Can unstructured review text power better music recommendations than ratings alone?**

---

## Pipeline

```
Scrape RateYourMusic reviews
  → Clean & normalize text (lemmatization, bigrams)
  → Discover attributes via frequency + co-occurrence lift
  → Build album-level text profiles (aggregate reviews)
  → Vectorize with TF-IDF and sentence embeddings
  → Score similarity to user query
  → Filter with sentiment analysis (VADER)
  → Return ranked results with evidence snippets
```

---

## Three Recommendation Methods

| Method | How It Works | Best For |
|--------|-------------|----------|
| **TF-IDF + Cosine** | Exact term matching on review vocabulary | Precise, specific queries ("shoegaze + reverb + dreamy") |
| **TF-IDF + Sentiment** | Same as above, but filters out negative mentions | Avoiding false positives (album mentioned "guitar" negatively) |
| **Embeddings + Cosine** | Semantic similarity via sentence embeddings | Vibe-based discovery ("shredding" ≈ "guitar riffs") |

**Key finding:** TF-IDF dominates when users know exactly what they want. Embeddings win when the query is abstract or uses non-standard vocabulary. Sentiment filtering improves trust in both.

---

## NLP Feature Engineering

| Step | What It Does | Why It Matters |
|------|-------------|----------------|
| Lowercasing + punctuation removal | Normalize surface variation | "Post-Punk" = "post-punk" |
| Stopword removal | Remove noise words | Focus on content-bearing terms |
| Lemmatization | Merge word variants | "guitars" → "guitar", "dreaming" → "dream" |
| Unigrams + bigrams | Preserve multi-word phrases | `post_punk`, `drum_machine`, `shoegaze_wall` |
| Co-occurrence lift | Find attribute associations | Which words appear together more than expected |
| VADER sentiment | Score attribute mentions | Distinguish "great guitar work" from "terrible guitar tone" |

---

## Data

**Source:** Scraped album reviews from [RateYourMusic](https://rateyourmusic.com/) — album name, artist, review text, and user rating.

Reviews are aggregated at the **album level** to form a crowd-sourced description: instead of one reviewer's opinion, each album's profile represents the collective language used across all its reviews.

---

## Key Takeaways

| Insight | Detail |
|---------|--------|
| **Review text > ratings** | Text captures nuance (mood, instrumentation, production style) that a 1–5 star rating can't |
| **TF-IDF = precision** | Best when the user's query uses the exact vocabulary of the review corpus |
| **Embeddings = recall** | Catches semantic matches that TF-IDF misses entirely |
| **Sentiment is critical** | Without it, albums mentioned *negatively* for an attribute still rank highly |
| **Evidence builds trust** | Showing the actual review snippet lets users judge the recommendation themselves |

---

## Repository Structure

```
├── RateyourMusic_Recommender.ipynb
├── RateyourMusic_Webscraper.ipynb           
├── data/                
│   └── rym_reviews_FINAL.csv
├── README.md
└── .gitignore
```

---

## How to Run

```bash
git clone https://github.com/awhite121/RateYourMusic-Recommender-System.git
cd RateYourMusic-Recommender-System
pip install pandas numpy scikit-learn nltk vaderSentiment sentence-transformers
jupyter notebook recommender.ipynb
```

---

## Limitations & Next Steps

**Current limitations:** Single scrape snapshot (no temporal trends), content-based only (no collaborative signal), no user profile or listening history.

**Next steps:**
- Hybrid approach combining content-based + collaborative filtering
- User profile system that learns preferences over time  
- Genre-aware embedding fine-tuning
- Deploy as an interactive web app (Streamlit or Flask)

---

## Author

Andrew White — [GitHub](https://github.com/awhite121)  
*MSBA coursework — Unstructured Data Analytics, University of Texas at Austin*
