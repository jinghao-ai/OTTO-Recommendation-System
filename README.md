# OTTO – Multi-Objective Recommender System
**A 7-Day Kaggle Intermediate Project (Comprehensive README)**

---

## 🚀 Project Summary
This repository contains a **practical, modular, and reproducible** 7-day implementation plan for the Kaggle competition **OTTO – Multi-Objective Recommender System**.  
The goal is to build a recommender system that predicts three types of session-level user interactions:

- **clicks**
- **carts**
- **orders**

This README provides a comprehensive overview, run instructions, file structure, design decisions, evaluation plan, and next steps. Use this as the single source of truth while developing the notebooks and code.

---

## 📁 Repository Layout (planned)
```
OTTO-Recommender/
├── README.md                        # This file (comprehensive)
├── requirements.txt                 # Python dependencies
├── LICENSE                          # MIT or your chosen license
├── day1/
│   ├── day1_notebook.ipynb
│   └── README.md
├── day2/
│   ├── day2_notebook.ipynb
│   └── README.md
├── day3/
│   ├── day3_notebook.ipynb
│   └── README.md
├── day4/
│   ├── day4_notebook.ipynb
│   └── README.md
├── day5/
│   ├── day5_notebook.ipynb
│   └── README.md
├── day6/
│   ├── day6_notebook.ipynb
│   └── README.md
├── day7/
│   ├── day7_final.ipynb
│   └── README.md
└── utils/
    ├── data_loader.py               # streaming JSONL loader
    ├── feature_utils.py
    ├── model_utils.py
    └── metric_utils.py
```

---

## 🧭 High-level Workflow (per day)
**Day 1 — Data & EDA**
- Confirm dataset paths and mount.
- Implement streaming loader `stream_jsonl`.
- Explore event type distributions; compute `top_items.csv` and `session_stats.json`.
- Produce visualizations: session length histogram, top-k items.

**Day 2 — Baseline Candidate Generation**
- Implement three lightweight candidate generators:
  - Global popularity
  - Last-N interactions
  - Co-visitation (session-level)
- Build candidate union and small offline test harness.

**Day 3 — Co-visitation & Candidate Expansion**
- Build efficient co-visitation aggregator (windowed, time-decay).
- Implement caching of co-visitation tables (parquet).
- Add item2vec (optional) and ANN retrieval baseline.

**Day 4 — Feature Engineering**
- Create candidate-level features:
  - recency, frequency, event-weighted counts
  - session features: length, time gaps
  - item features: global popularity, last seen timestamp
- Export feature table for LightGBM.

**Day 5 — Ranking Models**
- Train LightGBM / XGBoost ranking models on candidate pool.
- Use time-based train / validation split.
- Evaluate using Recall@20 per objective.

**Day 6 — Re-ranking & Blending**
- Blend multiple models (weighted average).
- Implement heuristic post-processing:
  - dedupe, popularity backfill, diversity injection.

**Day 7 — Finalize & Submit**
- Create final submission (session_type, labels).
- Write final report and push cleaned notebooks to GitHub.

---

## 🔎 Design & Implementation Notes

### Data handling
- The raw dataset is large. **Always use streaming or chunked reads** to avoid OOM.
- Convert intermediate tables to **Parquet** for fast reloads.

### Candidate Strategy
- Candidate generation must be recall-focused (not precision). Keep a **wide candidate pool** (200–1000 per session) before re-ranking.

### Evaluation protocol
- Use **time-based split** for validation (i.e., hold out last day(s) / last few hours).
- Compute **Recall@20** for `clicks`, `carts`, and `orders`.
- Final score uses weights: `0.10`, `0.30`, `0.60` respectively.

---

## 🛠 How to run (Kaggle Notebook recommended)

1. Fork or create a new Kaggle Notebook.
2. Add the OTTO dataset via the Notebook's **Add data** panel.
3. Copy the `day1/day1_notebook.ipynb` content into the Kaggle Notebook or upload the notebook file.
4. Run Day1 cells sequentially to confirm dataset path and produce `top_items.csv`.
5. Continue down the days in order.

---

## ✅ Minimal `requirements.txt`
```
pandas
numpy
scipy
tqdm
matplotlib
scikit-learn
lightgbm
xgboost
annoy
gensim
pyarrow
```

---

## 🔧 Useful snippets

### Stream JSONL (safe)
```python
import json
def stream_jsonl(path, chunk_size=200_000):
    batch = []
    with open(path, "r") as f:
        for line in f:
            batch.append(json.loads(line))
            if len(batch) >= chunk_size:
                yield batch
                batch = []
    if batch:
        yield batch
```

### Compute Recall@20 (skeleton)
```python
def recall_at_k(true_items, pred_items, k=20):
    # true_items: list of true a ids
    # pred_items: list of predicted a ids (ordered)
    return len(set(true_items) & set(pred_items[:k])) / len(true_items)
```

---

## 📦 Contribution & File Guidelines
- Keep `data/` out of the repo. Use dataset mounting.
- Notebooks must be runnable end-to-end and documented.
- Add docstrings and inline comments (Chinese allowed inside code).
- Commit frequently and include a short message summarizing changes.

---

## 📄 License
MIT License — include a `LICENSE` file if you want this.

---

## 📚 References & Further Reading
- Kaggle: OTTO Recommender System competition page  
- Session-based recommendation literature (GRU4Rec, SASRec)  
- Co-visitation and candidate generation resources

---

## 📞 Contact
If you need help completing any day's notebook, share which day and I will provide a runnable notebook cell-by-cell and code explanations.
