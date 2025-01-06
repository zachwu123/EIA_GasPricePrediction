# Natural Gas Price Forecasting Project

This project leverages data from the U.S. Energy Information Administration (EIA) to build predictive models for forecasting natural gas prices. Using advanced machine learning techniques like XGBoost and integrating automated pipelines, the project aims to deliver accurate and timely predictions for natural gas market trends.

---

# Data Collection

## Data Source
All data is fetched from the U.S. Energy Information Administration (EIA) API: [EIA Open Data](https://www.eia.gov/opendata/). The data spans from 2013 to the present and includes daily, weekly, and monthly cadences to capture comprehensive market dynamics.

## Data Topics
### Natural Gas Futures Prices
- Represents market expectations for future gas prices.
- **Frequency:** Daily

### Natural Gas Summary
- Includes production, consumption, imports/exports, storage, and weather data.
- **Frequency:** Monthly

### Natural Gas Import/Export by Country
- Tracks volumes and prices of imports/exports by country.
- **Frequency:** Monthly

### Natural Gas Import/Export by Point of Entry/Exit
- Provides granular insights into regional supply and export trends.
- **Frequency:** Monthly

### Natural Gas Weekly Underground Storage
- Short-term insights into storage levels critical for price volatility.
- **Frequency:** Weekly

### Petroleum Spot and Futures Prices
- Tracks petroleum market dynamics, which often correlate with natural gas pricing.
- **Frequency:** Daily

---

# Data Preprocessing

1. **Data Integration:**
   - Merge datasets into a single dataframe.
   - Handle data types, remove duplicates, and apply one-hot encoding.

2. **Data Cleaning:**
   - Handle missing values to ensure model readiness.

3. **Feature Engineering:**
   - Extract key features to improve model performance, such as lag variables and moving averages.

---

# Model Building

This section implements predictive models to forecast natural gas prices. Models tested include linear regression, random forests, ARIMA, and XGBoost.

## Model Comparison
### Base Model: Linear Regression
- **Train RMSE:** 0.50
- **Test RMSE:** 1.17
- **Pros:** Simple and interpretable.
- **Cons:** Cannot capture non-linear relationships.

### Random Forest
- **Train RMSE:** 0.20
- **Test RMSE:** 1.00
- **Pros:** Handles non-linearity and is robust to outliers.
- **Cons:** Slight overfitting indicated by train-test RMSE disparity.

### ARIMA
- **Train RMSE:** 0.58
- **Test RMSE:** 0.83
- **Pros:** Designed for time-series forecasting.
- **Cons:** Limited to lag-based features; struggles with high-dimensional data.

### XGBoost
- **Train RMSE:** 0.12
- **Test RMSE:** 0.81
- **Strengths:** Captures nuanced relationships, robust to overfitting through regularization.
![image](https://github.com/user-attachments/assets/dbaba50b-9f18-4f06-8b85-43922477785a)
![image](https://github.com/user-attachments/assets/1cbd272f-08e2-4e92-8fb6-d0b7468316f7)

---

## Fine-Tuning and Improvement
- **Original Test RMSE:** 0.81
- **Fine-Tuned Test RMSE:** 0.73

### Optimized Hyperparameters:
- `n_estimators`: 200, `max_depth`: 7, `learning_rate`: 0.1
- `subsample`: 0.5, `colsample_bytree`: 0.5

---

# Forecasting Future Gas Prices Using XGBoost

This section focuses on multistep forecasting with a 5-day horizon using the XGBoost model.

## Methodology
### Data Preparation
- **Sequence Creation:** Rolling window approach with `look_back` = 10 days for inputs and `forecast_horizon` = 5 days for outputs.
- **Scaling:** Normalized input and target values using Min-Max scaling.

### Model Training and Prediction
- The model was trained to predict 1-day ahead prices.
- Iterative predictions were made for all 5 horizons, with results inverse-transformed for evaluation.
  ![image](https://github.com/user-attachments/assets/778ebdfa-1567-4eb3-a1f9-b4fc305d0022)
  ![image](https://github.com/user-attachments/assets/921bbb64-9dd1-47aa-802a-7ced031b3d7b)


## Results and Analysis
| **Horizon** | **Train RMSE** | **Test RMSE** |
|-------------|----------------|---------------|
| Day 1       | 0.12           | 0.45          |
| Day 2       | 0.69           | 0.51          |
| Day 3       | 0.83           | 0.53          |
| Day 4       | 0.87           | 0.57          |
| Day 5       | 0.91           | 0.60          |

### Sample visualization of forecasting
![image](https://github.com/user-attachments/assets/35ea2756-fda3-420d-ab16-d7e3f3c9445f)
![image](https://github.com/user-attachments/assets/aecf87b9-df09-4edc-89c0-04b45b333c56)

---

# Future Improvements

## Exploratory Data Analysis
- Add visualizations to analyze seasonal trends, correlations, and outliers.

## Modeling Enhancements
- **Feature Engineering:** Add seasonal indicators, related commodity prices, and storage data.
- **Horizon-Specific Models:** Train separate models for each forecast horizon to improve accuracy.
- **Probabilistic Forecasting:** Quantify uncertainty for longer horizons using techniques like quantile regression or Bayesian models.
- **Hybrid Approaches:** Combine XGBoost with ARIMA or LSTM to leverage temporal and non-linear strengths.

## Automated Modeling Pipeline

-**Integrating MLflow into the pipeline** to make the forecasting process scalable, efficient, and adaptable to the dynamic nature of natural gas markets. This ensures timely and accurate insights, enabling businesses to stay competitive in volatile environments.
### Weekly Training Automation
- Automate data fetching, preprocessing, model retraining, and evaluation.
- Use MLflow to log experiments, track hyperparameters, and deploy the best model.

### Daily Data Extraction and Prediction
- Automate daily data fetching and prediction generation.
- Integrate with dashboards for real-time decision-making.

