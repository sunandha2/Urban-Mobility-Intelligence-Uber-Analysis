# Urban Mobility Intelligence: Uber Hotspot & Demand Analysis

> *8 days. One dataset. From a basic countplot to a production-grade demand forecaster.*

---

## What This Is

This project started with a simple question: *when and where do people actually need Uber in New York City?*

Over 8 days, it grew from plotting a bar chart of hourly rides into a full-stack ML pipeline — complete with spatial clustering, time-series feature engineering, multi-model comparison, and a live demand forecasting API. The dataset is Uber's April 2014 NYC pickup data (564,516 trips). Everything else was built from scratch.

---

## The 8-Day Journey

### Days 1–2 · Getting Familiar with the Data

Loaded the raw CSV, ran `.describe()`, looked at the shape, checked for nulls. Nothing fancy — just getting a feel for what's there.

Built the first few plots: rides by hour, rides by weekday, a weekend-vs-weekday split. Used a simple threshold (median hourly count) to create a binary `demand` label, then trained a Logistic Regression to predict it.

Accuracy was 77%. Felt good. It wasn't.

**What I learned:** The label was derived from the same `hour` feature used to train the model. That's not prediction — that's a tautology dressed in code. The model wasn't learning anything real.

---

### Days 3–4 · Rethinking the Problem

Scrapped the binary label. The real question is: *how many trips happen in a given hour and zone?* That's a regression problem, not classification.

Rebuilt everything around actual trip counts per hour per geographic zone. Added geographic filtering to remove the ~2,000 GPS points outside NYC's bounding box (the original data had a surprising number of these).

This is also when the feature engineering got serious:
- **Cyclical encoding** for hour, weekday, and month — because hour 23 and hour 0 are one minute apart, not 23 apart
- **Rush hour flags** (`is_rush_am`, `is_rush_pm`)
- **Time buckets** (Late Night / AM Rush / Mid Morning / Midday / PM Rush / Evening)
- **KMeans spatial clustering** (8 zones) to group pickups into geographic demand regions

---

### Days 5–6 · Time-Series Features & Proper Splitting

This was the biggest shift in thinking.

Added **lag features** — demand 1 hour ago, 2 hours ago, same hour yesterday. Added **rolling statistics** — 3-hour mean, 6-hour mean, 24-hour mean. These gave the model a memory of what happened before the current time window.

Also fixed the train/test split. Random splits on time-series data leak the future into training — you end up evaluating a model that's already "seen" tomorrow. Switched to a **temporal split**: train on days 1–21, test on days 22–30.

The correlation matrix revealed what actually predicts trip count:
- `rolling_6h_mean` → 0.674 correlation with target
- `rolling_3h_mean` → 0.546
- `lag_1h` → 0.402
- `is_rush_pm` → 0.157

Recent demand history is by far the most informative signal. Time-of-day features matter, but they're secondary.

---

### Days 7–8 · Multi-Model Comparison & Production API

Trained four models on the same temporal split:

| Model | MAE | RMSE | R² |
|---|---|---|---|
| Ridge Regression (baseline) | 16.75 | 31.03 | 0.689 |
| Random Forest | 7.29 | 17.81 | 0.898 |
| XGBoost | 6.87 | 17.52 | 0.901 |
| **LightGBM** | **6.78** | **16.50** | **0.912** |

LightGBM won on every metric. Cross-validated with `TimeSeriesSplit` (5 folds) to confirm it generalises — mean R² of 0.796 across folds, which is honest.

Built a `predict_uber_demand()` function that takes a day, hour, zone, and optional lag values, and returns predicted trip count + a business-readable status (surge pricing trigger, deploy extra drivers, etc.).

---

## Technical Stack

```
pandas / numpy          → data manipulation
scikit-learn            → preprocessing, RF, Ridge, cross-validation
xgboost / lightgbm      → gradient boosting models
matplotlib / seaborn    → visualisation
KMeans                  → spatial zone clustering
TimeSeriesSplit         → leak-free cross-validation
```

---

## Key Files

```
uber-raw-data-apr14.csv       → raw input data
notebook_v1.ipynb             → basic version (days 1–2)
notebook_v2.ipynb             → production version (days 3–8)
uber_eda.png                  → demand analysis charts
uber_geo.png                  → geographic zone map
uber_correlation.png          → feature correlation matrix
uber_model_comparison.png     → model benchmark chart
uber_model_analysis.png       → LightGBM deep-dive plots
```

---

## Results at a Glance

- **Peak demand:** 5 PM (evening commute, consistently the busiest hour)
- **Busiest day:** Wednesday (midweek work travel)
- **Weekend share:** 23% of all rides (Uber is primarily a commuter tool in this dataset)
- **Best model:** LightGBM — MAE of 6.78 trips/hour/zone, R² of 0.912
- **Top feature:** `rolling_6h_mean` — recent demand history beats raw time features

---

## What I'd Do Differently

- **More data.** One month, partially cut off at day 9 in the raw file, isn't enough for robust 24h lag features or week-over-week patterns.
- **Weather integration.** Rain has an obvious effect on ride demand — it's a glaring omission in the feature set.
- **Better zone definitions.** KMeans on lat/lon gives reasonable clusters but doesn't align to actual NYC neighbourhoods. Using official taxi zone polygons would make the output more interpretable and actionable.
- **Handling the MAPE problem.** MAPE was 48% on LightGBM — high, but expected when many low-count zones (e.g., 2 trips/hour) create percentage error spikes. Switching to WMAPE would give a fairer picture.

---

## How to Run

```bash
# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn xgboost lightgbm

# Open the production notebook
jupyter notebook notebook_v2.ipynb
```

The notebooks are self-contained. The dataset CSV needs to be in the same directory.

---

## Project Context

Built as a learning project — the goal was to actually understand what goes wrong with naive ML approaches on time-series data, not just get a high accuracy number. The basic version (days 1–2) is intentionally kept to show the before/after.

*Author: K Sunandha*
