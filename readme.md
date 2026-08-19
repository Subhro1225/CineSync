# CineSync — Multi-Modal Recommendation System

A cross-platform recommendation engine that suggests movies, shows, and music (Netflix, Amazon Prime, Spotify-style catalogs, etc.) by combining multiple data modalities — user ratings, text (plot/lyrics/reviews), and metadata (genre, cast, audio features) — into a single hybrid recommendation pipeline.

> Rename the title above to whatever you're calling the project — this is just a placeholder.

---

## 1. Overview

Most recommendation systems rely on a single signal (ratings only, or content only). This project builds a **multi-modal** system that fuses:

- **Collaborative signals** — user-item interaction/rating history
- **Content signals** — text (descriptions, reviews, subtitles/lyrics) via NLP embeddings
- **Metadata signals** — genre, cast/artist, release year, runtime/duration, platform
- **(Stretch) Visual/audio signals** — poster images or audio features, if time allows

The output is a hybrid model that can recommend across domains (movies + music) and across platforms (Netflix-style + Prime-style + audio catalogs), rather than being locked into one dataset.

---

## 2. Prerequisites

### Knowledge
- Python fundamentals, basic OOP
- Pandas/NumPy for data wrangling
- Basic ML concepts (regression, classification, clustering, embeddings)
- Git/GitHub workflow (branches, PRs, merge conflicts)
- Basic REST API concepts

### Software / Tools
| Tool | Purpose | Version |
|---|---|---|
| Python | Core language | 3.10+ |
| pip / venv or conda | Environment management | latest |
| Git & GitHub | Version control | latest |
| Jupyter Notebook / VS Code | Development | latest |
| Docker (optional) | Containerized deployment | latest |

### Core Libraries
```
pandas
numpy
scikit-learn
torch                 # for deep learning / embeddings
transformers          # for text embeddings (BERT/SBERT)
sentence-transformers # semantic similarity for content-based filtering
surprise               # collaborative filtering (SVD, KNN)
fastapi                # backend API
uvicorn                # ASGI server
streamlit / react      # frontend (pick one based on team skillset)
matplotlib / seaborn   # EDA & visualization
```

Install everything with:
```bash
pip install -r requirements.txt
```

### Datasets (starting points)
- [MovieLens 25M](https://grouplens.org/datasets/movielens/) — movie ratings + metadata
- [TMDB 5000 Movies](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata) — plots, cast, genres
- [Million Song Dataset](http://millionsongdataset.com/) or [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset) — music metadata
- Optional: scrape/collect a small Netflix/Prime-style catalog sample for platform-specific demo data

---

## 3. Project / File Structure

```
recommendation-system/
│
├── README.md
├── requirements.txt
├── .gitignore
├── .env.example
│
├── data/
│   ├── raw/                  # original untouched datasets
│   ├── processed/            # cleaned, merged datasets
│   └── external/             # scraped / supplementary data
│
├── notebooks/
│   ├── 01_eda_movies.ipynb
│   ├── 02_eda_music.ipynb
│   ├── 03_content_based_model.ipynb
│   ├── 04_collaborative_filtering.ipynb
│   └── 05_hybrid_model_evaluation.ipynb
│
├── src/
│   ├── data/
│   │   ├── load_data.py
│   │   ├── clean_data.py
│   │   └── merge_datasets.py
│   │
│   ├── features/
│   │   ├── text_embeddings.py       # SBERT/TF-IDF embeddings
│   │   ├── metadata_features.py
│   │   └── audio_features.py        # optional
│   │
│   ├── models/
│   │   ├── content_based.py
│   │   ├── collaborative_filtering.py
│   │   ├── hybrid_recommender.py
│   │   └── evaluate.py
│   │
│   ├── api/
│   │   ├── main.py                  # FastAPI entrypoint
│   │   ├── routes/
│   │   │   ├── recommend.py
│   │   │   └── users.py
│   │   └── schemas.py
│   │
│   └── utils/
│       ├── config.py
│       └── logger.py
│
├── frontend/
│   ├── (React app OR Streamlit app files)
│
├── models_saved/                    # trained model artifacts (.pkl, .pt)
│
├── tests/
│   ├── test_data.py
│   ├── test_models.py
│   └── test_api.py
│
└── docs/
    ├── architecture.png
    ├── report.md
    └── presentation.pptx
```

---

## 4. Development Phases

### Phase 1 — Planning & Setup (Week 1)
- [ ] Finalize scope: which domains (movies, music, both?), which platforms to simulate
- [ ] Set up GitHub repo, branch strategy (`main`, `dev`, feature branches)
- [ ] Collect and download datasets
- [ ] Define success metrics (Precision@K, Recall@K, RMSE, NDCG)

### Phase 2 — Data Collection & EDA (Week 2)
- [ ] Clean and merge datasets (movies + music)
- [ ] Handle missing values, duplicates, outliers
- [ ] Exploratory analysis: genre distribution, rating distribution, user activity
- [ ] Build a unified schema so movies and music can be recommended through the same pipeline

### Phase 3 — Baseline Models (Weeks 3–4)
- [ ] **Content-based filtering**: TF-IDF / SBERT embeddings on descriptions, cosine similarity
- [ ] **Collaborative filtering**: matrix factorization (SVD) or KNN using `surprise`
- [ ] Evaluate baseline performance separately

### Phase 4 — Multi-Modal Fusion (Weeks 5–6)
- [ ] Combine content embeddings + collaborative signals + metadata into a hybrid scoring function
- [ ] Experiment with weighted hybrid vs. learned fusion (small neural net combining embeddings)
- [ ] Cross-domain testing (does a user's movie taste inform music recommendations, or keep domains separate but unified under one system?)

### Phase 5 — API & Backend (Week 7)
- [ ] Wrap the trained model in a FastAPI service
- [ ] Endpoints: `/recommend/{user_id}`, `/similar/{item_id}`, `/search`
- [ ] Add basic caching for repeated queries

### Phase 6 — Frontend & Integration (Week 8)
- [ ] Build a simple UI (Streamlit for speed, or React for a polished demo)
- [ ] Connect frontend to API
- [ ] Display recommendations with posters/thumbnails, genre tags, platform labels

### Phase 7 — Testing, Evaluation & Documentation (Week 9)
- [ ] Unit tests for data pipeline, model, API
- [ ] Evaluate final model against baselines (metrics table in `docs/report.md`)
- [ ] Write final documentation, architecture diagram, and presentation slides

### Phase 8 — Deployment (Week 10, optional)
- [ ] Dockerize the app
- [ ] Deploy API (Render/Railway) and frontend (Vercel/Streamlit Cloud)
- [ ] Final demo + README polish

---

## 5. Team & Work Division (3 Members)

> Adjust names/roles to match your actual team — structure below assumes roughly equal ML + engineering split.

### Member A — Data & Content-Based Modeling Lead
- Data collection, cleaning, merging (Phase 2)
- Text/content embeddings (TF-IDF, SBERT)
- Content-based recommendation model
- EDA notebooks

### Member B — Collaborative Filtering & Fusion Lead
- Collaborative filtering model (SVD/KNN)
- Hybrid fusion logic (combining content + collaborative + metadata)
- Model evaluation (Precision@K, Recall@K, NDCG)
- Performance benchmarking against baselines

### Member C — Backend, Frontend & Deployment Lead
- FastAPI backend, API design
- Frontend (Streamlit/React) integration
- Docker + deployment
- Testing suite, CI setup (optional GitHub Actions)

### Shared Responsibilities
- Weekly sync (recommend 2x/week during active dev)
- Code reviews on every PR before merging to `dev`
- Final documentation and presentation — all three contribute their section

---

## 6. Branching Strategy

```
main        → stable, demo-ready code only
dev         → integration branch, merged after review
feature/*   → individual work (e.g. feature/content-based-model)
```

Workflow: create feature branch → commit → open PR into `dev` → 1 teammate reviews → merge → periodically merge `dev` into `main` at phase milestones.

---

## 7. Evaluation Metrics

| Metric | Measures |
|---|---|
| Precision@K | Relevance of top-K recommendations |
| Recall@K | Coverage of relevant items retrieved |
| RMSE / MAE | Rating prediction accuracy (collaborative filtering) |
| NDCG | Ranking quality |
| Diversity / Novelty | Whether recommendations avoid over-repetition |

---

## 8. Setup Instructions

```bash
# 1. Clone the repo
git clone https://github.com/<org>/recommendation-system.git
cd recommendation-system

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run data pipeline
python src/data/load_data.py
python src/data/clean_data.py

# 5. Train models
python src/models/content_based.py
python src/models/collaborative_filtering.py

# 6. Run the API
uvicorn src.api.main:app --reload

# 7. Run the frontend (if Streamlit)
streamlit run frontend/app.py
```

---

## 9. Future Improvements
- Add visual embeddings from posters/thumbnails (CNN-based)
- Add audio feature embeddings for music (e.g. tempo, valence from Spotify features)
- Real-time feedback loop (thumbs up/down updating recommendations)
- A/B testing framework for comparing model versions

---

## 10. Environment Variables

Create a `.env` file (never commit this — only commit `.env.example`):

```
# .env.example
DATA_DIR=./data/processed
MODEL_DIR=./models_saved
API_PORT=8000
TMDB_API_KEY=your_key_here          # if pulling live poster/metadata
SPOTIFY_CLIENT_ID=your_id_here      # if using Spotify API for music data
SPOTIFY_CLIENT_SECRET=your_secret_here
LOG_LEVEL=INFO
```

---

## 11. API Contract (draft)

Documenting the expected request/response shape early saves the frontend dev from waiting on the backend.

**GET** `/recommend/{user_id}?domain=movie&top_k=10`
```json
{
  "user_id": "u_123",
  "domain": "movie",
  "recommendations": [
    {"item_id": "m_456", "title": "Example Movie", "score": 0.92, "genre": ["thriller"], "platform": "netflix"}
  ]
}
```

**GET** `/similar/{item_id}`
```json
{
  "item_id": "m_456",
  "similar_items": [
    {"item_id": "m_789", "title": "Another Movie", "similarity": 0.87}
  ]
}
```

**GET** `/search?q=<query>`
```json
{
  "results": [
    {"item_id": "m_456", "title": "Example Movie", "type": "movie"}
  ]
}
```

---

## 12. Risks & Known Challenges
- **Cold-start problem**: new users/items with no interaction history — mitigate with content-based fallback
- **Data sparsity**: rating matrices are usually very sparse — consider matrix factorization over raw KNN
- **Cross-domain fusion is genuinely hard**: movie taste and music taste don't always correlate — be prepared to keep domains scored separately if a unified fusion underperforms, and say so honestly in the report
- **Dataset licensing**: check usage terms for MovieLens/TMDB/Spotify datasets before any public deployment or demo with real data
- **Scope creep**: with 3 people and a fixed timeline, treat visual/audio embeddings (Phase 4 stretch) as optional — cut first if behind schedule

---

## 13. Communication & Task Tracking
- **Task board**: Trello / Notion / GitHub Projects (pick one, link it here once created)
- **Chat**: Discord / WhatsApp group (link here)
- **Meeting cadence**: 2x/week during active development, 1x/week during planning/writing phases
- **Decision log**: keep a running note of major technical decisions (e.g. "chose SBERT over TF-IDF because...") — useful for the final report and viva/defense questions

---

## 14. Team

| Name | Role | GitHub |
|---|---|---|
| Member A | Data & Content-Based Modeling | @username |
| Member B | Collaborative Filtering & Fusion | @username |
| Member C | Backend, Frontend & Deployment | @username |

---

## 15. Acknowledgments & Data Sources
- [MovieLens](https://grouplens.org/datasets/movielens/) — GroupLens Research, University of Minnesota
- [TMDB](https://www.themoviedb.org/) — The Movie Database API
- [Million Song Dataset](http://millionsongdataset.com/) / [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)

Cite these properly in the final report if the project is submitted for academic evaluation.

---

## 16. License
Add a license (MIT recommended for academic/team projects) — create a `LICENSE` file in the repo root.
