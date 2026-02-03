NFL Spread Prediction Model

A machine learning project that uses historical game data to predict point spreads for National Football League games using linear regression and rolling performance metrics.

This project focuses on building a structured end-to-end data pipeline, engineering time-aware features, and evaluating model performance on out-of-sample seasons.

⸻

Project Overview

The goal of this project is to predict NFL game score spreads using team-level performance statistics and recent form indicators.

Two model versions were built:

V1 Midseason Model
	•	Trained and tested on the 2023 season
	•	80/20 time-based split with no shuffling to avoid data leakage
	•	Designed as a proof of concept and pipeline validation

V2 Midseason Model (Final)
	•	Trained on 2021–2023 seasons
	•	Tested on the 2024 season
	•	Demonstrates improved generalization across seasons

Because rolling window features require prior games, predictions are available only from Week 8 onward.

⸻

Data Engineering

This project required combining multiple raw data sources with different formats:
	•	Play-by-play data used to aggregate team offensive production by play type
	•	Game-level data containing one row per game
	•	Turnover data formatted by winning and losing teams rather than home and away teams

Key processing steps included:
	•	Standardizing team naming across datasets
	•	Merging play-level and game-level statistics
	•	Transforming win/loss formatted turnover data into game-based features
	•	Creating rolling averages over 3, 5, and 7 game windows to capture performance trends
	•	Removing Weeks 1–7 where rolling features are unavailable

The final design matrix contains both per-game statistics and recent performance indicators.

⸻

Modeling Approach
	•	Model: Linear Regression
	•	Scaling: Standardization using sklearn scaler
	•	No regularization was applied since train and test errors did not show strong signs of overfitting
	•	Models and scalers were saved as pickle files for reuse

⸻

Model Performance
V1 Results (2023 Only)

| Dataset | MAE | RMSE |
| :--- | :---: | ---: |
| Train | 9.14 | 11.49 |
| Test | 12.51 | 15.78 |

V2 Results (Train 2021-2023, Test 2024)

| Dataset | MAE | RMSE |
| :--- | :---: | ---: |
| Train | 9.87 | 12.83 |
| Test | 10.37 | 13.20 |

⸻

Repository Structure

```
nfl_spread_model/
│
├── data/
│   ├── raw/              # Original source CSV files
│   └── processed/        # Cleaned design matrix for modeling
│
├── models/
│   ├── v1_midseason/     # V1 model and scaler pickle files
│   └── v2_midseason/     # Final model and scaler pickle files
│
└── notebooks/
    ├── 01_etl_feature_engineering.ipynb   # Data cleaning and feature creation
    ├── 02_linear_regression_model.ipynb   # Model training and evaluation
    └── archive/                           # First iteration notebooks
```
⸻

Key Skills Demonstrated
	•	End-to-end data pipeline design
	•	Cleaning and merging multi-format sports datasets
	•	Feature engineering with rolling time-series windows
	•	Preventing data leakage in temporal train/test splits
	•	Model evaluation using MAE and RMSE
	•	Reproducible ML workflow with saved models and scalers

⸻

Future Improvements
	•	Add regularized models for comparison
	•	Incorporate betting market features such as closing lines
	•	Explore nonlinear models like gradient boosting
	•	Automate a weekly prediction pipeline
