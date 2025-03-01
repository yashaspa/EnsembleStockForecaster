# Stockhack 2025 - Yashas Acharya Submission

## Overview
I’m predicting the 5-day return and price of selected equities in the competition. I employed an ensemble of **CatBoost, LightGBM, and a Neural Network (NN)** to predict the values.

## Data
My dataset consists of historical price values for the stocks. For each company, I collected the following features:

- **Date**
- **Last Price, Open Price, High Price, Low Price, Volume**
- **Bid Price, Ask Price**
- **Market Order Bid Size (mostly blank), Market Order Ask Size (mostly blank)**
- **30-day Average Volume**
- **20-day, 50-day, and 200-day Moving Averages**
- **Turnover / Traded Value**
- **RSI (14-day)**
- **30-day Volatility, Implied Volatility Mid**
- **Current Market Cap**
- **VWAP**

The data frequency is **daily**, spanning from **1/1/2015 to 2/21/2025** (last Friday's closing). 

### Data Preprocessing
- **Handling Missing Values**: Used rolling window averages.
- **Feature Scaling**: Applied MinMax Scaling for neural network compatibility.
- **Feature Engineering**:
  - Generated **lagged features** to capture temporal patterns.
  - **Calculated 5-day future return** as the target variable.

## Model Training
I trained three models separately on individual stocks using their respective historical data:

1. **CatBoost**  
   - A gradient boosting algorithm optimized for categorical data.
2. **LightGBM**  
   - A highly efficient boosting algorithm for large-scale datasets.
3. **Neural Network**  
   - Designed with **two hidden layers** to capture non-linear relationships.

### Hyperparameter Tuning
I used **Optuna** to optimize:
- **Boosting Models**: Learning rate, tree depth, and regularization.
- **Neural Network**: Hidden layer sizes, learning rate, and number of epochs.

## Ensemble Strategy
Final predictions were derived from a **weighted ensemble** of the three models:
- **CatBoost**: 67.42% weight
- **LightGBM**: 27.60% weight
- **Neural Network**: 4.98% weight

Weights were determined based on **cross-validation performance** to maximize predictive accuracy.

## Predictions
The final predicted **5-day return and prices** for the selected equities are:

| Stock         | Predicted Return | Predicted Price |
|--------------|----------------|----------------|
| **ALT US Equity** | **9.28%** | **$7.03** |
| **CELH US Equity** | **-4.93%** | **$31.01** |
| **CVNA US Equity** | **7.94%** | **$241.02** |
| **FUBO US Equity** | **-7.20%** | **$3.49** |
| **UPST US Equity** | **-0.59%** | **$71.35** |

## Model Evaluation
I used **Mean Absolute Error (MAE)**, **Root Mean Squared Error (RMSE)**, and **R² score** to assess performance:

- **ALT US Equity**:  
  - **MAE**: 0.0963  
  - **RMSE**: 0.1016  

- **CELH US Equity**:  
  - **MAE**: 0.1229  
  - **RMSE**: 0.1471  

R-squared values varied significantly, with some **negative values**, indicating high volatility and unpredictability.

## Insights & Future Improvements
- **Ensemble models** outperformed individual models.
- **CatBoost** had the most influence in final predictions.
- **High variance in R² scores** suggests a need for better feature engineering.
- Future improvements:
  - Incorporating **macroeconomic factors** (interest rates, market sentiment).
  - Enhancing **generalization techniques** to reduce overfitting.
  - Experimenting with **Transformer-based models** for time-series forecasting.
  - **Using intraday data** for fine-tuning.

## Final Predicted Prices:
- **ALT US Equity**: **$7.03**
- **CELH US Equity**: **$31.01**
- **CVNA US Equity**: **$241.02**
- **FUBO US Equity**: **$3.49**
- **UPST US Equity**: **$71.35**
