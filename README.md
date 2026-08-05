# Text Mining & Topic Modelling of British Airways Customer Reviews

* This repository contains an end-to-end text mining and topic modelling project analysing passenger feedback for British Airways (BA). 
* The study applies Latent Dirichlet Allocation (LDA) topic modelling structured around the CRISP-DM framework to identify key drivers of customer satisfaction and operational pain points.

---

## Project Overview

* **Data Source:** Sourced from Kaggle ([British Airways Reviews - Skytrax](https://www.kaggle.com/datasets/osamaalaa2001/british-airways-reviews-skytrax)), containing unstructured customer feedback
* **Business Objective:** Uncover dominant underlying themes in passenger reviews to assist BA management in prioritising operational improvements and reinforcing service strengths.
* **Text Mining Objective:** Pre-process unstructured text, build an LDA topic model, determine the optimal number of topics (k), and validate model coherence against qualitative review content.
* **Framework:** CRISP-DM (Business Understanding → Data Understanding → Data Preparation → Modelling → Evaluation → Deployment).

---

## Execution Pipeline

| Step | Execution Stage | Functional Description |
| :--- | :--- | :--- |
| **1** | **Data Import** | Imported the raw passenger review dataset sourced from Kaggle (N = 3,400). |
| **2** | **Sampling** | Sampled n = 600 reviews reproducibly (seed = 123) and validated data integrity by removing missing or duplicate records. |
| **3** | **Pre-processing** | Standardised text via lowercasing, removed non-alphabetic noise (numbers, currency symbols like `£`, symbols, punctuation), applied standard/custom domain stop words, and performed stemming. |
| **4** | **DTM & TF-IDF** | Constructed a Document-Term Matrix (DTM) and reduced vocabulary dimensionality using TF-IDF median thresholding. |
| **5** | **LDA Tuning** | Conducted hyperparameter tuning comparing VEM vs. Gibbs Sampling estimation algorithms across k in [4, 10] using perplexity, log-likelihood, and manual topic coherence checks. |
| **6** | **Model Evaluation**| Fitted the optimal final model, extracted topic-document distributions (theta matrix), and retrieved representative reviews per topic for qualitative validation. |

---

## Optimal Topics & Insights (k = 6, Gibbs Sampling)

Although quantitative metrics (Perplexity and Log-Likelihood) supported Gibbs sampling at k = 10 for numerical generalisation, manual qualitative analysis across k in [4, 10] confirmed **k = 6 with Gibbs sampling** as the optimal model:

* **Low Topic Counts (k = 4–5):** Topics were extremely broad with weaker differentiation.
* **High Topic Counts (k = 7–10):** Topics became extremely fragmented with repetitive themes across the models.
* **VEM vs. Gibbs Performance:** VEM displayed greater term repetition across topics (e.g., *"seat"*, *"crew"*, *"heathrow"*), whereas Gibbs sampling generated clearly differentiated themes.
* **Optimal Selection (k = 6, Gibbs):** Produced the most meaningfully coherent, interpretable, and strongly differentiated topics for actionable domain insights.

| Topic Label | Summary & Key Insights |
| :--- | :--- |
| **Topic 1: Cabin Class & Seating Experience** | Premium passengers in International Business and Club Europe expressed frustration over cramped seating and limited legroom comparable to Economy despite higher fares. |
| **Topic 2: Service Quality Decline** | Frequent flyers on long-haul routes via London Heathrow expressed disappointment with cost-cutting measures, citing added fees for previously complimentary perks (snacks, checked bags, seat selection). |
| **Topic 3: Inconsistent Meal Services** | Reviews highlighted inconsistency in cabin crew service, particularly mixed-fleet teams - 0with complaints regarding unfulfilled beverage/meal requests and unaccommodating attitudes. |
| **Topic 4: Customer Support & Rebooking** | Passengers reported long hold times and inadequate updates from customer support when trying to resolve flight delays, cancellations, or rebookings. |
| **Topic 5: New Aircraft Experience** | Captured positive feedback on modern fleet flights, emphasising high food quality, professional staff, noise-cancelling headphones, and robust in-flight entertainment. |
| **Topic 6: Operations & Punctuality** | Operational pain points included flight delays, baggage issues, overcrowded terminals, and slow boarding procedures—notably at hubs like London Gatwick. |

---

## Key Methodological Takeaways

* **Balancing Quantitative Metrics with Human Interpretability:** Statistical fit metrics alone (Perplexity and Log-Likelihood) should not be the sole evaluation criterion in unsupervised NLP.
* **Business-Oriented Validation:** Qualitative review of topic coherence and domain relevance was equally critical to ensure the selected model produced actionable business insights rather than mathematically optimal noise.

---

## Strategic Recommendations

1. **Reinforce Fleet Strengths:** Leverage high satisfaction around modern aircraft (Topic 5) in marketing campaigns while accelerating fleet retrofits on older long-haul routes.
2. **Protect Premium Brand Equity:** Re-evaluate seating ergonomics and restore value-added perks for business class and frequent flyers to prevent customer attrition (Topics 1 & 2).
3. **Standardise Cabin Crew Training:** Mitigate service variability across mixed-fleet teams through refreshed training programmes on attentiveness and meal service reliability (Topic 3).
4. **Modernise Ground Operations:** Invest in automated delay notifications and digital self-service tools to relieve airport bottlenecks and reduce customer support wait times (Topics 4 & 6).

---

## Tech Stack & Dependencies

* **Language:** R
* **Core Libraries:**
  * `readr` — Data import
  * `tm` & `SnowballC` — Text pre-processing, stemming, and corpus creation
  * `topicmodels` — Latent Dirichlet Allocation (VEM & Gibbs Sampling)
  * `slam` — Sparse matrix operations

---

## Learning & Feedback

As I am building my skills in data science through my studies, I would really appreciate any feedback, suggestions, or advice on how I can improve this project or my code!

