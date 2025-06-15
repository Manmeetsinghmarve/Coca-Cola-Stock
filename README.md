# 📈 Coca-Cola Stock Price Prediction – Project Report

## 🧠 Objective

The primary goal of this project is to build a system that **predicts the next-day closing price of Coca-Cola's (KO) stock** using historical stock data and machine learning. The system automates the fetching, updating, and preprocessing of stock data, and provides real-time predictions based on technical indicators.

---

## 📦 Data Source

- **Ticker**: KO (Coca-Cola)
- **Source**: [Yahoo Finance](https://finance.yahoo.com/)
- **Fetch Method**: `yfinance` Python package
- **Frequency**: Daily stock prices
- **Auto-adjusted**: Disabled to ensure full historical data consistency including dividends and splits

---

## 🧹 Data Preparation

### ✔️ Steps Taken:

1. **CSV Loading**: If a local CSV exists, it loads and updates it. Otherwise, it initializes a fresh download.
2. **New Data Update**: Downloads new data from the last saved date to the current day.
3. **Cleaning**:
   - Removed missing values.
   - Ensured required columns: `Open`, `High`, `Low`, `Close`, `Adj Close`, `Volume`.
   - Removed duplicate or NaT-indexed entries.
4. **Saved** updated data back to CSV for persistence.

---

## 📐 Feature Engineering

Calculated technical indicators for model input:

| Feature     | Description                                      |
|-------------|--------------------------------------------------|
| MA20        | 20-day Moving Average of `Close`                 |
| MA50        | 50-day Moving Average of `Close`                 |
| Volatility  | Rolling standard deviation of daily returns (20-day) |
| Open        | Opening price of the day                         |
| High        | Highest price of the day                         |
| Low         | Lowest price of the day                          |
| Volume      | Total trading volume                             |

The dataset is required to have at least **60 valid rows** after feature engineering to proceed.

---

## 🧠 Machine Learning Model

- **Model Type**: Linear Regression (sklearn)
- **Input Features**:
  - `Open`
  - `High`
  - `Low`
  - `Volume`
  - `MA20`
  - `MA50`
  - `Volatility`
- **Target**: Next-day closing price
- **Model File**: `outputs/linear_model.pkl`

---

## 🔮 Prediction Workflow

1. **Latest Feature Extraction**:
   - Compute indicators on the most recent valid row.
   - Format features as a single-row DataFrame for inference.

2. **Prediction**:
   - Load pre-trained model.
   - Predict the next closing price.
   - Compare predicted vs actual and calculate direction and change.

3. **Saved Prediction**:
   - Exported as `latest_prediction_input.csv` for audit/debugging.

---

## 🧾 Sample Output
📊 Prediction Summary
Current Close: $63.89
Predicted Close: $64.75
Expected Change: $0.86 → 📈 Up


---

## 🚀 Future Improvements

- Add **model retraining pipeline** for automatic updates.
- Include **additional indicators** (RSI, MACD, Bollinger Bands).
- Build a **live dashboard** using Streamlit or Dash.
- Add **error tracking** and **logging** with alerting.
- Integrate with **financial news sentiment analysis**.

---

## 👨‍💻 Author

- **Name**: Manmeet Marve  
- **Role**: Developer & Analyst  
- **Tools Used**: Python, Pandas, yFinance, Scikit-learn, Joblib

---

## 🏁 Conclusion

This project demonstrates the power of combining financial data, feature engineering, and machine learning to create a lightweight yet effective stock prediction tool. While the model is simple, it forms a solid foundation for deeper financial analytics and more robust forecasting systems.


