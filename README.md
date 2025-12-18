# ReciSys: Hybrid Recipe Recommendation with Attention & NLP

This project studies rating prediction on the Food.com dataset using modern recommender system techniques.

I explore two complementary predictive tasks:

1. **Hybrid Recommendation (Collaborative + Content-Based)**
   - Predict user–recipe ratings using an attention-based neural recommender
   - Combines user embeddings, item embeddings, and rich recipe metadata
   - Model: **SideFeatAttAE**

2. **NLP-Based Rating Prediction**
   - Predict ratings directly from review text
   - Models: **Fine-tuned DeBERTa** and **TF-IDF + Ridge regression**

Together, these tasks examine how structured interactions and natural language capture user preferences from different perspectives.


**Dataset:** Food.com (Majumder et al., EMNLP 2019)

- 230K+ recipes
- 1M+ user interactions
- 18 years of data (2000–2018)

After filtering:
- ~180K recipes
- ~700K interactions

Original dataset goal: personalized recipe generation  
This project focuses on **rating prediction and representation learning**.

**Goal:** Predict a user's rating for a recipe.

**Inputs**
- User ID
- Recipe ID
- Recipe side features:
  - cooking time
  - number of steps
  - number of ingredients
  - nutrition vector
  - recipe tags

**Model**
- User & item embeddings
- Side-feature embedding via MLP
- Multi-head attention over [user, item, side] tokens
- MLP head + bias terms

**Baselines**
- Global mean
- User mean
- Item mean
- Matrix Factorization (SVD)

**Metric**
- Mean Squared Error (MSE)

**Goal:** Predict rating from review text alone.

**Models**
- Fine-tuned DeBERTa-v3 (regression)
- TF-IDF + Ridge regression

**Why NLP?**
- Captures sentiment, negation, and subtle phrasing
- Complements collaborative signals

**Metric**
- Mean Squared Error (MSE)


| Model | Test MSE |
|------|---------|
| SideFeatAttAE | **0.712** |
| Matrix Factorization (SVD) | 0.753 |
| Global Mean | 0.845 |
| TF-IDF + Ridge (NLP) | 0.378 |
| DeBERTa (NLP) | **0.286** |


- Attention-based hybrid models outperform classical CF baselines
- Rich side information improves robustness and cold-start behavior
- NLP models can recover ratings extremely well from language alone
- The architecture generalizes beyond Food.com to many recommendation domains

- `notebook/ReciSys.ipynb` – full implementation and experiments
- `slides/ReciSys.pptx` – presentation walkthrough
- `report/ReciSys_Report.pdf` – written report
- watch: [video presentation](https://drive.google.com/file/d/1sB3T2pWJ6ie1gXAGiWN3_4TuFSKR4CEf/view?usp=sharing)


## Dataset Citation

This project uses the Food.com dataset introduced in:

Bodhisattwa Prasad Majumder*, Shuyang Li*, Jianmo Ni, Julian McAuley.  
**Generating Personalized Recipes from Historical User Preferences.**  
EMNLP–IJCNLP, 2019.

- Paper: https://cseweb.ucsd.edu/~jmcauley/pdfs/emnlp19c.pdf  
- Dataset: https://www.kaggle.com/datasets/shuyangli94/food-com-recipes-and-user-interactions

If you use this dataset, please cite the paper above.
