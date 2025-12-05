# 10-Year Treasury Yield Prediction Model

## Quick Start Guide

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Configure Secrets (env vars)
1. Copy `sample.env` to `.env`
2. Fill in `KALSHI_API_KEY_ID`, and either `KALSHI_API_PRIVATE_KEY` (PEM text) or `KALSHI_API_PRIVATE_KEY_PATH` (preferred, points to a local PEM file)
3. Fill in `FRED_API_KEY`
4. (Optional) Override `KALSHI_BASE_URL` or `KALSHI_TARGET_MARKET_TICKER`

### 3. Find the Market Ticker

You need to find the exact ticker for the "Treasury 10-Year Yield on Friday, December 12, 2025" market on Kalshi. You can:
- Search on the Kalshi website
- Use the Kalshi API search endpoint
- Update `TARGET_MARKET_TICKER` in the notebook

### 4. Run the Notebook

Open `kalshi_model.ipynb` and run all cells. The notebook will:
1. Fetch historical Treasury yield data from FRED
2. Fetch additional economic indicators
3. Build a Random Forest predictive model
4. Make a prediction for December 12, 2025
5. Extract/create probability distribution from Kalshi ladder prices

### 5. Model Outputs

- **Predicted Yield**: Point estimate for Dec 12, 2025
- **Probability Distribution**: Based on Kalshi ladder prices
- **Model Performance Metrics**: MAE, RMSE on test set
- **Feature Importance**: Top features driving predictions
- **Visualizations**: Charts showing model performance and probability distribution

## Model Approach

**Simple & Accurate Strategy:**
- **External Data**: FRED (10-year, 2-year, 30-year yields, Fed Funds Rate, CPI)
- **Model**: Random Forest (good balance of accuracy and interpretability)
- **Features**: Historical yields, spreads, rolling statistics, momentum, volatility
- **Probability Distribution**: Extracted from Kalshi orderbook ladder prices

## Next Steps to Improve

1. **Add More External Data:**
   - CME Treasury futures prices
   - Credit spreads (e.g., Baa-Aaa spread)
   - Economic forecasts (Fed projections, Blue Chip forecasts)
   - Term structure factors

2. **Enhance Model:**
   - Try ensemble methods (XGBoost, LightGBM)
   - Add Kalshi market prices as features
   - Include macroeconomic forecasts
   - Use time series models (ARIMA, LSTM) for comparison

3. **Refine Probability Distribution:**
   - Use actual Kalshi ladder prices (not simulated)
   - Combine model prediction with market-implied probabilities
   - Account for market microstructure effects

## Submission Checklist

- [ ] Full model code (this notebook)
- [ ] Final prediction (saved in `model_results.json`)
- [ ] Probability distribution (from Kalshi ladder prices)
- [ ] 1-page methodology report (create separately)

## Judging Criteria Focus

- **Forecast Accuracy (60 pts)**: Focus on model performance and prediction quality
- **Methodology (25 pts)**: Clear, well-documented approach
- **Explainability (10 pts)**: Feature importance, clear reasoning
- **Polish and Reproducibility (5 pts)**: Clean code, clear documentation

