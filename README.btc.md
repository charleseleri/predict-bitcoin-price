!pip install yfinance ta xgboost statsmodels tensorflow
# Bitcoin Price Prediction with AI and Technical Indicators

## Overview
This project predicts the short-term price of **Bitcoin (BTC)** using **AI models** and **technical indicators**. The goal is to analyze historical BTC price movements and forecast price trends using a combination of **LSTM (deep learning), XGBoost (ensemble learning), and ARIMA (time series analysis).**

[Colab Notebook](https://colab.research.google.com/github/charleseleri/predict-bitcoin-price/blob/main/BTC_PredictBitcoinPrice.ipynb)

[GitHub Repo](https://github.com/charleseleri/predict-bitcoin-price)

---
## Features & Strategy
### 1. Data Collection
- Live BTC price data is fetched from **Yahoo Finance (yfinance API)**.
- Uses **Open, High, Low, Close (OHLC) and Volume**.

### 2. Technical Indicators Used
- **Moving Averages (SMA, EMA):** Trend following indicators.
- **MACD (Moving Average Convergence Divergence):** Momentum indicator.
- **RSI (Relative Strength Index):** Identifies overbought/oversold conditions.
- **Bollinger Bands:** Measures volatility and potential breakout zones.

### 3. AI Models for Prediction
- **LSTM (Long Short-Term Memory):** Deep learning model for time-series forecasting.
- **XGBoost:** Gradient boosting model for pattern-based price prediction.
- **ARIMA (AutoRegressive Integrated Moving Average):** Time-series forecasting.

### 4. Model Training & Evaluation
- Data is **split into training (80%) and testing (20%)**.
- Performance is evaluated using:
  - **Mean Absolute Error (MAE)**
  - **Root Mean Squared Error (RMSE)**

### 5. 7-Day BTC Price Forecast
- The notebook **forecasts Bitcoin price movements for the next 7 days** using LSTM.
- Generates a **table and charts comparing actual vs. predicted values**.

---
## How to Run the Notebook
1. **Clone the GitHub Repo**
   ```bash
   git clone https://github.com/charleseleri/predict-bitcoin-price.git
   cd predict-bitcoin-price
   ```
2. **Open in Google Colab**
   - Upload `BTC_PredictBitcoinPrice.ipynb` to Google Colab.
   - Install dependencies:
     ```python
     !pip install yfinance ta xgboost statsmodels tensorflow
     ```
   - Run all cells to generate predictions.

3. **Check Predictions**
   - View the **7-day forecast table**.
   - Analyze **charts comparing actual vs. predicted BTC prices**.

---
## Results Interpretation
**What the results mean:**
- **If LSTM gives better predictions:** BTC follows momentum-based movements.
- **If XGBoost performs best:** Price action is influenced by technical patterns.
- **If ARIMA shows better accuracy:** BTC trends are historically driven.

---
## Next Steps & Improvements
- **Optimize AI models:** Tune LSTM, XGBoost, and ARIMA hyperparameters.
- **Test different timeframes:** Forecast 1-day, 3-day, and 7-day BTC prices.
- **Enhance GitHub Repo:** Add model performance metrics, additional insights, and improvements.

---
## Contribute & Feedback
Feel free to **fork this repo, submit PRs, or raise issues**.

Contact: [charleseleri.com](https://github.com/charleseleri)

# predict-bitcoin-price
Predict bitcoin price (Ticker: BTC) in the short-term. Class FINC-646
1. **Data Collection and Preprocessing**  
   - Uses `yfinance` to fetch recent historical data for a specified ticker (e.g., QQQ).
   - Calculates daily returns and drops missing values.

2. **LSTM Model**  
   - Scales the closing prices and creates sequences of the past 60 days to predict the next day's close.
   - Splits the data into training, validation, and test sets, then trains an LSTM model with two LSTM layers of 50 units each.

3. **ARIMA Model**  
   - Applies the ARIMA(5,1,0) model to the original (unscaled) close price series.
   - Uses a walk-forward approach: for each test point, re-fits the ARIMA model on all known data up to that point, then forecasts the next day.

4. **GARCH Model**  
   - Applies a GARCH(1,1) model to daily returns (in percentage form) to estimate and forecast volatility.
   - Obtains a predicted volatility for each test sample period.

5. **Ensemble and Trading Strategy**  
   - Averages the LSTM and ARIMA predictions to create an ensemble forecast.
   - Compares the ensemble forecast to the previous day’s close to generate a long or flat signal.
   - Calculates cumulative returns of this strategy compared to a buy-and-hold benchmark.

6. **Result Visualization**  
   - Plots cumulative returns of the ensemble strategy vs. a buy-and-hold approach.
   - Plots the predicted volatility from the GARCH model as an auxiliary risk management insight.

You can enhance the performance with hyperparameter tuning, additional features (e.g., technical indicators, macro data), or more sophisticated ensemble and trading logic.
