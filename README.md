# Tip_Prediction

## Table of Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Features](#features)
- [Data Processing](#data-processing)
- [Models](#models)
- [Evaluation](#evaluation)
- [Usage](#usage)
- [Future Improvements](#future-improvements)
- [Dependencies](#dependencies)
- [Files](#files)


# Overview
This project aims to predict whether a taxi customer will be "generous" (tip ≥ 20% of the total fare) based on trip characteristics. The model helps taxi drivers identify customers more likely to give substantial tips, while avoiding ethical concerns like discouraging pickups for customers predicted not to tip at all.

# Dataset
The dataset consists of 2017 Yellow Taxi trip records from New York City, containing:

-Trip timestamps (pickup/dropoff)

-Location IDs (pickup/dropoff)

-Fare and payment information

-Passenger counts

-Trip distances

# Features
## Engineered Features:
Target Variable:

generous: Binary (1 = tip ≥ 20%, 0 otherwise)

## Temporal Features:
-day: Day of week

-month: Month of year

-Time Segments:

-am_rush (06:00–10:00)

-daytime (10:00–16:00)

-pm_rush (16:00–20:00)

-nighttime (20:00–06:00)

## Location Features:
One-hot encoded pickup and dropoff location IDs

# Data Processing
-Filtered to only credit card payments (cash tips often recorded as $0)

-Tip percentage calculated

-Categorical variables converted to binary features

# Models
## Random Forest Classifier
-Best F1 (CV): 0.758

-Test F1 Score: 0.750

-Best Parameters:

-max_depth: 20

-max_features: 'log2'

-n_estimators: 100

-min_samples_split: 2

## XGBoost Classifier
-Best F1 (CV): 0.750

-Test F1 Score: 0.737

-Best Parameters:

-learning_rate: 0.1

-max_depth: None

-n_estimators: 100

# Evaluation
-F1 Score was chosen as the primary metric due to:

-False positives (predict generous when not) frustrate drivers

-False negatives (miss generous tippers) disadvantage customers

-F1 balances precision and recall

Class Distribution:

-Generous (1): 9,284 (60.8%)

-Not Generous (0): 5,981 (39.2%)

# Usage
-python
-Copy
-Edit
-import pickle

# Load model
with open('model.pickle', 'rb') as f:
    model = pickle.load(f)

# Predict on new data
predictions = model.predict(new_data)
# Future Improvements
Ideas for enhancing the model:

-Trip distance categories (short/medium/long)

-Fare amount ratios (e.g., to nearest 5/10 multiples)

-Customer historical tipping behavior

-More granular location features

-Additional temporal context (holidays, major events)

# Dependencies
-pandas

-scikit-learn

-xgboost

-matplotlib

# Files
-2017_Yellow_Taxi_Trip_Data.csv – Original dataset

-nyc_preds_means.csv – Precomputed fare predictions

-model.pickle – Trained Random Forest model

-model_xgb.pickle – Trained XGBoost model
