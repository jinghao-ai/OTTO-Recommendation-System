# OTTO-Recommendation-System
⭐ OTTO – Multi-Objective Recommender System

A complete 7-day intermediate Kaggle project

📌 Overview

This repository contains a structured and modular 7-day workflow for the Kaggle OTTO Multi-Objective Recommender System competition.
The goal is to build a recommender system that predicts three types of user interactions:
	•	clicks
	•	carts
	•	orders

using large-scale session-based e-commerce logs.

This project is built to be:
	•	Beginner-friendly (clear code + explanations in English, comments in Chinese)
	•	Modular (each day has its own folder + README)
	•	Kaggle-ready (optimized for Kaggle GPU/TPU/CPU environments)
	•	Research-value (suitable for portfolio, scholarship applications, and interviews)

📁 Repository Structure
OTTO-Recommender/
│
├── README.md                     ← Main project documentation
│
├── day1/                         ← Day 1 — Setup + Lightweight EDA
│   └── README.md
│
├── day2/                         ← Day 2 — Baseline Candidate Generation
│   └── README.md
│
├── day3/                         ← Day 3 — Co-visitation Matrix v1
│   └── README.md
│
├── day4/                         ← Day 4 — Feature Engineering for Ranking
│   └── README.md
│
├── day5/                         ← Day 5 — Ranking Models (LightGBM/XGBoost)
│   └── README.md
│
├── day6/                         ← Day 6 — Re-Ranking + Blending
│   └── README.md
│
├── day7/                         ← Day 7 — Final Model + Submission
│   └── README.md
│
└── utils/                        ← Common utility scripts (optional)
    ├── data_loader.py
    ├── feature_utils.py
    ├── model_utils.py
    └── metric_utils.py
