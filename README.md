# Short-Term Household Electricity Forecasting: A Paper-Inspired LSTM Adaptation

## Overview

This project investigates **short-term household electricity load forecasting** using deep learning. It is inspired by the paper:

> **Learning model combined with data clustering and dimensionality reduction for short-term electricity load forecasting**

Rather than reproducing the paper exactly, this project adapts its forecasting framework to a **single-household dataset** using temporal feature engineering and LSTM-based sequence modeling.

The objective is to predict the **next 24 hours of electricity consumption** using the **previous 192 hours** of historical observations.

---

## Project Highlights

- End-to-end forecasting pipeline
- Time-series preprocessing and feature engineering
- Multi-step (24-hour) forecasting
- PyTorch LSTM implementation
- Seasonal modeling (Summer vs Winter)
- Baseline model comparisons
- Comprehensive evaluation and visualization

---

## Dataset

**Individual Household Electric Power Consumption Dataset**

The dataset contains minute-level measurements of household electricity usage including:

- Global Active Power
- Global Reactive Power
- Voltage
- Global Intensity
- Sub-metering 1
- Sub-metering 2
- Sub-metering 3

The raw data is converted into **hourly observations** before training.

---

## Problem Statement

Given the previous **192 hours** of electricity usage and engineered temporal features,

predict the **next 24 hours** of household electricity demand.

This is formulated as a **multi-step time-series forecasting** problem.

---

## Methodology

### Data Preprocessing

- Datetime parsing
- Missing value interpolation
- Hourly resampling
- Log transformation of target variable
- Standardization

---

### Feature Engineering

Calendar Features

- Hour
- Day
- Month
- Day of week

Cyclical Encoding

- Hour sin/cos
- Day sin/cos
- Month sin/cos

Historical Features

- Lag 1
- Lag 24
- Lag 48
- Lag 168

Rolling Statistics

- 24-hour mean
- 24-hour standard deviation
- 168-hour mean
- 168-hour standard deviation

Electrical Variables

- Reactive power
- Voltage
- Current intensity
- Sub-metering channels

Additional Experiment

- Estimated unmetered load feature

---

## Models

### Main Model

- LSTM (PyTorch)

Architecture

- 2 LSTM layers
- Dropout
- Fully connected output layer
- Early stopping
- Huber Loss
- Adam optimizer

---

## Experiments

The notebook evaluates several forecasting strategies.

### 1. All-season LSTM

Single model trained on the complete dataset.

---

### 2. Summer-only LSTM

Separate model trained only on summer observations.

---

### 3. Winter-only LSTM

Separate model trained only on winter observations.

---

### 4. Winter LSTM + Unmetered Load

Adds a derived unmetered load feature.

---

### 5. Larger Winter LSTM

Tests whether increasing model capacity improves winter forecasting.

---

### Baseline Comparisons

- Naive persistence forecasting
- Linear Regression
- XGBoost
- LSTM

---

## Evaluation Metrics

Models are evaluated using

- RMSE
- MAE
- MAPE
- sMAPE

---

## Results

| Model | RMSE | MAE | MAPE |
|-------|------:|------:|------:|
| Summer-only LSTM | **0.5008** | **0.3357** | 60.47% |
| All-season LSTM | 0.5939 | 0.4207 | **54.18%** |
| Winter-only LSTM | 0.7926 | 0.5819 | 56.73% |

### Key Findings

- Summer forecasting produced the lowest RMSE and MAE.
- Winter demand was considerably more difficult to predict.
- Seasonal specialization improved forecasting performance.
- Increasing model complexity alone did not significantly improve winter accuracy.

---

## Visualizations

The notebook includes

- Actual vs Predicted forecasts
- Residual analysis
- Error by forecast horizon
- Seasonal comparison
- Daily load profiles
- Correlation heatmaps
- Training curves
- Monthly demand trends

---

## Technologies Used

- Python
- PyTorch
- NumPy
- Pandas
- Scikit-learn
- XGBoost
- Matplotlib
- Google Colab

---

## Repository Structure

```
.
├── Short_Term_Household_Electricity_Forecasting_A_Paper_Inspired_LSTM_Adaptation.ipynb
├── README.md
└── figures/ (optional)
```

---

## Relation to the Reference Paper

This project follows several ideas from the reference paper, including:

- 192-hour input window
- 24-hour prediction horizon
- Log-transformed target
- Temporal feature engineering
- Seasonal analysis
- LSTM forecasting

However, it is **not a direct reproduction**.

The original paper uses **4,710 households** together with:

- Kernel PCA
- UMAP
- t-SNE
- K-Means clustering

before forecasting.

Because the dataset used here contains only a **single household**, those clustering-based techniques are not applicable in the same way. Instead, this work focuses on a practical single-household adaptation using LSTM-based forecasting.

---

## Future Improvements

Potential extensions include:

- Transformer-based forecasting models
- Temporal Fusion Transformer
- N-BEATS
- GRU models
- Weather data integration
- Hyperparameter optimization
- Multi-household forecasting
- Clustering and dimensionality reduction on larger datasets
