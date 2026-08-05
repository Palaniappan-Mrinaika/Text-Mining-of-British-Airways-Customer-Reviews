# Text Mining of  British Airways Customer Reviews 

This repository contains an end-to-end text mining and topic modelling project analysing passenger feedback for British Airways (BA). 
The study applied **Latent Dirichlet Allocation (LDA)** topic modelling structured around the **CRISP-DM** framework to identify key drivers of customer satisfaction and main operational pain points.

---

## Project Overview

* **Data Source:** Sourced from Kaggle ([British Airways Reviews - Skytrax](https://www.kaggle.com/datasets/osamaalaa2001/british-airways-reviews-skytrax)), containing customer feedback and review content collected from Skytrax.
* **Business Objective:** Uncovered dominant, underlying themes in unstructured passenger reviews to help British Airways leadership prioritise targeted operational improvements and reinforce service strengths.
* **Text Mining Objective:** Pre-processed unstructured text, built an LDA topic model, determined the optimal number of topics ($k$), and validated model coherence against qualitative review content.
* **Framework:** CRISP-DM (*Business Understanding $\rightarrow$ Data Understanding $\rightarrow$ Data Preparation $\rightarrow$ Modelling $\rightarrow$ Evaluation $\rightarrow$ Deployment*).

---

## Execution Pipeline

| Step | Execution Stage | Functional Description |
| :---: | :--- | :--- |
| **1** | Data Import | Imported the raw passenger review dataset sourced from Kaggle. |
| **2** | Sampling |Sampled n=600 reviews reproducibly and validated data integrity by removing missing or duplicate records. |
| **3** | Pre-processing | Standardised text via lowercasing, removed non-alphabetic noise (numbers, currency like `£`, symbols like `✅`, punctuation), applied standard and custom domain stop words, and performed stemming. |
| **4** | DTM & TF-IDF | Constructed a Document-Term Matrix (DTM) and reduced vocabulary dimensionality using TF-IDF median thresholding. |
| **5** | LDA Tuning | Conducted hyperparameter tuning comparing **VEM** vs. **Gibbs Sampling** estimation algorithms across $k \in [4, 10]$ using perplexity, log-likelihood, and manual topic coherence checks. |
| **6** | Model Evaluation | Fitted the optimal final model, extracted topic-document distributions ($\theta$ matrix), and retrieved representative reviews per topic for qualitative validation. |

---

## Optimal Topics & Insights ($k = 6$, Gibbs Sampling)

Two LDA estimation methods (VEM and Gibbs sampling) were evaluated across $k \in [4, 10]$:

* **Model Selection:** Selected $k = 6$ via Gibbs sampling as the optimal configuration.
* **Limitations of High Topic Counts ($k = 10$):** Whilst $k = 10$ achieved higher raw numerical perplexity scores, qualitative evaluation revealed fragmented and repetitive topics.
* **Limitations of Low Topic Counts ($k = 4–5$):** Lower topic values resulted in categories that were too broad to yield actionable domain insights.
* **Optimal Balance:** $k = 6$ provided the ideal balance between quantitative statistical fit and qualitative domain interpretability.

| Topic Label | Summary & Key Insights |
| :--- | :--- |
| **Topic 1: Cabin Class & Seating Experience** | Premium passengers in International Business and Club Europe expressed frustration over cramped, uncomfortable seating and limited legroom that felt comparable to Economy class despite high fares. |
| **Topic 2: Service Quality Decline** | Frequent flyers on long-haul routes via London Heathrow expressed disappointment with cost-cutting measures, citing added fees for previously complimentary perks like snacks, checked bags, and seat selection. |
| **Topic 3: Inconsistent Meal Services** | Reviews highlighted inconsistency in cabin crew service—particularly mixed-fleet teams—with complaints regarding unfulfilled beverage/meal requests and unaccommodating attitudes. |
| **Topic 4: Customer Service** | Passengers reported long hold times and inadequate communication/updates from customer support teams when trying to resolve flight delays or handle rebookings. |
| **Topic 5: New Aircraft Experience** | Captured positive feedback on modern fleet flights, emphasising high food quality, professional staff, noise-cancelling headphones, and robust in-flight entertainment. |
| **Topic 6: Operations & Punctuality** | Operational pain points included flight delays, baggage issues, overcrowded terminals, and slow boarding procedures—notably at hubs like London Gatwick. |

---

## Key Methodological Takeaways

* **Balancing Quantitative Metrics with Human Interpretability:** Statistical fit metrics alone (Perplexity and Log-Likelihood) should not be the sole evaluation criterion in unsupervised NLP.
* **Business-Oriented Validation:** Qualitative review of topic coherence and domain relevance was equally critical to ensure the selected model produced actionable business insights rather than mathematically optimal noise.

---

## Conclusion & Strategic Recommendations

By transforming unstructured customer feedback into an interpretable 6-topic LDA model, this study outlined strategic directions for British Airways management:

* **Reinforce Fleet Strengths:** Leverage high satisfaction around modern aircraft (Topic 5) in marketing campaigns whilst accelerating fleet retrofits on older long-haul routes.
* **Protect Premium Brand Equity:** Re-evaluate seating ergonomics and restore value-added perks for business class and frequent flyers to prevent customer attrition (Topics 1 & 2).
* **Standardise Cabin Crew Training:** Mitigate service variability across mixed-fleet teams through refreshed training programmes on attentiveness and meal service reliability (Topic 3).
* **Modernise Ground Operations:** Invest in automated delay notifications and digital self-service tools to relieve airport bottlenecks and reduce customer support wait times (Topics 4 & 6).

---

## Tech Stack

* **Language:** R
* **Text Mining & NLP:** `tm`, `SnowballC`
* **Topic Modelling:** `topicmodels`
* **Sparse Matrix Operations:** `slam`

---

## Limitations & Future Work

* **Sample Size Scaling:** The sample size ($n = 600$) was selected for tractability and computational efficiency. Consequently, topic distributions and term weights may shift when expanding the analysis to the full 3,400-review dataset.
* **Metadata Constraints:** The dataset slice analysed lacked structured metadata, such as numerical star ratings and review timestamps. As a result, topics could not be cross-referenced against customer satisfaction scores or trended longitudinally over time.

---

