# Stock Price Movement Binary Classification

## Project Overview

This project implements a machine learning classification model to predict whether a stock's price will move **UP** or **DOWN** the next trading day. Using historical stock data and technical indicators, the model learns patterns from past price movements to make binary predictions about future direction.

## Problem Statement

Can we predict if a stock price will increase or decrease tomorrow based on today's technical indicators and historical price movements? This project tackles that question using a Random Forest Classifier trained on 5 years of historical stock data.

## Dataset

The project uses real stock market data fetched from Yahoo Finance via the `yfinance` library. By default, it uses **Apple (AAPL)** stock data, but you can easily switch to any other stock ticker (TSLA, MSFT, GOOGL, etc.).

**Data Period**: 5 years of daily candlestick data (OHLCV)
**Data Points**: Approximately 1,250+ trading days

### Features Used

The model uses the following engineered features:

1. **Return**: Daily percentage change in closing price
   - Captures short-term momentum

2. **MA_10**: 10-day Moving Average
   - Represents short-term trend

3. **MA_50**: 50-day Moving Average
   - Represents medium-term trend

4. **Volatility**: 20-day Rolling Standard Deviation of returns
   - Measures price fluctuation intensity

5. **RSI** (Relative Strength Index): 14-period technical indicator
   - Measures momentum and overbought/oversold conditions

### Target Variable

- **1**: Stock price goes UP tomorrow
- **0**: Stock price goes DOWN tomorrow

## Model Architecture

**Algorithm**: Random Forest Classifier
- Number of trees: 100
- Random state: 42 (for reproducibility)
- Train-test split: 80-20

Random Forest was chosen because it:
- Handles non-linear relationships well
- Is robust to outliers
- Provides feature importance rankings
- Avoids overfitting through ensemble learning

## Project Structure

```
Stock_Price_Movement_Binary_Classification/
├── Main.ipynb          # Main Jupyter notebook with full implementation
├── README.md           # This file
└── requirements.txt    # Python dependencies
```

## Installation & Setup

### Prerequisites
- Python 3.7+
- pip or conda package manager

### Install Dependencies

```bash
pip install yfinance pandas scikit-learn matplotlib
```

Or using conda:
```bash
conda install yfinance pandas scikit-learn matplotlib
```

### Running the Project

1. Open the Jupyter notebook:
   ```bash
   jupyter notebook Main.ipynb
   ```

2. Execute all cells sequentially to:
   - Download stock data
   - Engineer features
   - Train the Random Forest model
   - Evaluate performance
   - Visualize feature importance

## Results & Performance

The trained model achieves:
- **Accuracy**: ~55-57% on test set
- **Precision & Recall**: Balanced across both classes
- **Feature Importance**: Return and Volatility are the most important predictors

### Classification Report Example
```
              precision    recall  f1-score   support
           0       0.48      0.57      0.52       102
           1       0.64      0.55      0.59       140
    accuracy                           0.56       242
```

### Key Insights

- **Daily Returns** are the strongest predictor of next-day direction
- **Volatility** is the second most important feature
- Moving averages contribute moderately to predictions
- RSI provides additional signal for overbought/oversold conditions
- The 55-60% accuracy suggests modest predictive power above random guessing (50%)

## Visualizations

The notebook generates:
1. **Feature Importance Bar Chart**: Shows relative importance of each technical indicator
2. **Stock Price Visualization**: Geographic/temporal patterns (if data is plotted)
3. **Model Performance Metrics**: Classification report with precision, recall, and F1-scores

## How to Modify the Project

### Change Stock Symbol
```python
stock = "AAPL"   # Change to "TSLA", "MSFT", "GOOGL", etc.
```

### Adjust Model Parameters
```python
model = RandomForestClassifier(
    n_estimators=200,      # Increase trees for better accuracy
    max_depth=10,          # Add depth constraint
    random_state=42
)
```

### Extend Features
You can add more technical indicators:
- MACD (Moving Average Convergence Divergence)
- Bollinger Bands
- Stochastic Oscillator
- Volume-based indicators

## Limitations

1. **Past Performance ≠ Future Results**: Historical patterns don't guarantee future predictions
2. **Market Gaps**: Model doesn't account for overnight gaps due to news/events
3. **Limited Features**: Only uses technical indicators; ignores fundamental analysis
4. **Data Quality**: Missing holidays/weekends affects temporal relationships
5. **Accuracy**: ~56% accuracy is only marginally better than random guessing
6. **Black Swan Events**: Unexpected market shocks aren't captured historically

## Future Enhancements

- Implement LSTM neural networks for sequential pattern recognition
- Add sentiment analysis from financial news
- Incorporate volume and volatility surface data
- Use ensemble methods combining multiple models
- Add time-series cross-validation
- Deploy as a web API using Flask/FastAPI
- Build real-time prediction system
- Test on multiple stocks simultaneously

## Dependencies

- **yfinance**: Fetch historical stock data from Yahoo Finance
- **pandas**: Data manipulation and analysis
- **scikit-learn**: Machine learning algorithms
- **matplotlib**: Data visualization

## References & Resources

- [scikit-learn Documentation](https://scikit-learn.org/)
- [yfinance Documentation](https://github.com/ranaroussi/yfinance)
- [Random Forest Classifier](https://scikit-learn.org/stable/modules/ensemble.html#forest)
- [Technical Analysis Indicators](https://www.investopedia.com/terms/t/technicalanalysis.asp)

---

## ⚠️ DISCLAIMER

**This project is created for educational and academic purposes only.**

### Important Legal & Financial Notice

1. **NOT Financial Advice**: This project does not constitute financial advice, investment recommendations, or an invitation to invest. It is purely an educational demonstration of machine learning applied to stock market data.

2. **No Guarantee of Performance**: The model's predictions are not guaranteed to be accurate. Past performance does not indicate future results. Stock markets are highly unpredictable and influenced by numerous factors beyond historical price movements.

3. **Risk Acknowledgment**: Trading stocks involves substantial financial risk, including the potential loss of your entire investment. Do not use this model to make real trading decisions without thorough research and consultation with a qualified financial advisor.

4. **Data Limitations**: This model uses only technical indicators and historical price data. It does not account for:
   - Company fundamentals
   - Market sentiment
   - Economic indicators
   - News and events
   - Geopolitical factors

5. **Academic Use Only**: This project is intended for learning purposes to understand:
   - Machine learning classification techniques
   - Time-series feature engineering
   - Model evaluation and validation
   - Technical indicator calculation

6. **No Liability**: The author and contributors assume no responsibility for financial losses or damages that may result from using this project or its predictions.

7. **Terms of Use**: Use this project at your own discretion and risk. Always consult with financial professionals before making investment decisions.

---

**Remember**: Successful investing requires diverse knowledge, experience, and risk management. No machine learning model can predict the future with certainty.

*Last Updated: May 2026*
