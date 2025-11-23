# OTTO Recommender System – Days 1 to 20

This repository documents a self-directed Kaggle project exploring the OTTO Recommender System dataset.

## 🛒 OTTO Recommender System (Kaggle Project)

This repository documents my learning journey through the OTTO RecSys Kaggle competition.  
The project is structured in daily progress notebooks, each extracting and engineering features from clickstream data.

✅ Purpose: Strengthen my data science foundations  


Notebook highlights:
- Data loading & EDA
- Behavior statistics & funnels
- Sequential pattern mining
- Item-level popularity features

## ✅ Completed Days

## 📘 Day 1 – Data Loading & Exploration

### 🎯 Goal  
Load the raw training data and understand its structure.

### 🧩 Workflow  
- Load `train.parquet` into a DataFrame  
- Check basic columns: `session`, `aid`, `ts`, `type`  
- Examine event distribution and timestamp ranges  

### 📚 Knowledge Points  
- Using `pd.read_parquet`  
- Understanding event logs in recommendation datasets  
- Datetime conversion and `value_counts`

## 📘 Day 2 – Session Behavior Analysis

### 🎯 Goal  
Analyze user behaviors at the session level.

### 🧩 Workflow  
- Extract session duration  
- Count number of actions per session  
- Explore interaction frequency by action type  

### 📚 Knowledge Points  
- Grouping and aggregating sessions  
- Session-based recommendation metrics  
- Action type segmentation

## 📘 Day 3 – Conversion Funnel Analysis

### 🎯 Goal  
Explore the behavior funnel: click → cart → order.

### 🧩 Workflow  
- Compute counts and rates for clicks, carts, and orders  
- Analyze conversion ratios  
- Plot funnel chart for behavior conversion  

### 📚 Knowledge Points  
- Conversion rate computation  
- `groupby()` with multiple filters  
- Funnel chart design principles

## 📘 Day 4 – Sequential Pattern & Action Time Gap

### 🎯 Goal  
Analyze time intervals between actions and sequential behavior patterns.

### 🧩 Workflow  
- Sort actions by timestamp  
- Compute time deltas within each session  
- Analyze most common action sequences  

### 📚 Knowledge Points  
- `groupby().diff()` for time gaps  
- Action sequence frequency analysis  
- Temporal behavior understanding

## 📘 Day 5 – Item-Level Statistics

### 🎯 Goal  
Understand item popularity and engagement by event type.

### 🧩 Workflow  
- Compute total clicks, carts, orders per item  
- Rank items by interaction volume  
- Create visualizations of top items  

### 📚 Knowledge Points  
- Multi-index aggregation  
- Sorting and ranking aids  
- Feature engineering for items

## 📘 Day 6 – Session-Level Feature Engineering

### 🎯 Goal  
Extract session-level statistical features.

### 🧩 Workflow  
- Count unique items per session  
- Session duration and average time per event  
- Item diversity and entropy metrics  

### 📚 Knowledge Points  
- Grouping by session for feature extraction  
- Use of `nunique`, `mean`, and entropy  
- Session-based modeling prep

## 📘 Day 7 – Candidate Generation: Popularity-Based Recall

### 🎯 Goal

Generate session-item candidate pairs based on item popularity (clicks, carts, orders). This is a simple baseline recall strategy.

### 🧩 Workflow

1. Load training dataset (`train.parquet`)
2. Map action types (0/1/2) to strings: `clicks`, `carts`, `orders`
3. Aggregate most frequent items by action type
4. Create candidate pairs by combining each session with top-N popular items
5. Save as `popularity_candidates.parquet`

### 📚 Knowledge Points

- `groupby().size()` for aggregation
- Use of `np.repeat` and `np.tile` for matrix construction
- Understanding candidate recall strategies in recommendation systems

## 📘 Day 8 – Candidate Generation: Co-visitation Matrix

### 🎯 Goal  
Build a candidate recall strategy based on co-visitation. Items that appear together in sessions are likely to be relevant.

### 🧩 Workflow  
- Load training session logs  
- Build item-to-item co-visitation matrix from user sessions  
- Extract top co-visited items as candidate pairs  
- Save results for next-step recall/modeling

### 📚 Knowledge Points  
- Nested dictionary and defaultdict usage  
- Pairwise item interactions in collaborative filtering  
- Candidate generation using item-item relationships

## 📘 Day 9: Session-level Aggregate Features

### 🎯 Goal  
This notebook computes session-level aggregate features for the OTTO dataset.  
These features include:
- Total interactions per session
- Unique items per session
- Average interaction time difference per session

### 🧩 Workflow  
1. Load train and test parquet files.
2. Combine datasets to ensure consistent statistics.
3. Compute total interactions per session.
4. Compute unique items per session.
5. Compute average time difference per session.
6. Merge features back to train and test datasets.

### 📚 Knowledge Points  
- `train_day9.parquet`
- `test_day9.parquet`


## 📂 Structure

- `notebook/`: Contains Day 1–20 Jupyter Notebooks.
- `visualizations/`: Visual output from matplotlib charts.
- `README.md`: Project overview and progress.

## 📌 Author

Prepared by Zhang JingHao 
🎯 Goal: Prepare for research and scholarship application at NTU Singapore
