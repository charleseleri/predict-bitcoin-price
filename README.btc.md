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
