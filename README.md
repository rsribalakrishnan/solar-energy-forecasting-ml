# Solar Energy Forecasting using Machine Learning and Deep Learning

## Overview
This project focuses on forecasting solar energy output using weather parameters and time series models. The main target variable is **Global Horizontal Irradiance (GHI)**, which is a key indicator of solar power potential. The project analyzes the relationship between weather conditions and solar output, and compares multiple machine learning and deep learning approaches for prediction.

The study uses meteorological and solar radiation data from the **National Renewable Energy Laboratory (NREL)** and evaluates the performance of statistical, neural, and hybrid forecasting models. The models compared in this work are:
- ARIMA
- LSTM
- CNN-LSTM-TF
- GRU
- ARIMA-LSTM Hybrid

## Objectives
- Analyze the influence of weather parameters on solar energy production
- Forecast Global Horizontal Irradiance (GHI) using time series and deep learning models
- Compare forecasting performance across multiple models
- Identify which weather parameters have the strongest influence on solar output

## Dataset
The dataset was collected from the **National Renewable Energy Laboratory (NREL) Solar Data** and contains solar radiation and weather measurements for the geographical location **52.49° N, 11.02° E** in Germany for the year **2019**. The report states that 15-minute interval data was used. 

### Selected Features
The project uses the following input variables:
- Temperature
- Relative Humidity
- Pressure
- Wind Speed

### Target Variable
- Global Horizontal Irradiance (GHI)

This exact feature set is also reflected in the code, where these columns are selected and converted to numeric format before modeling. 

## Project Workflow
The project follows this pipeline:

1. Load and preprocess the weather and solar data
2. Select key meteorological features and the target variable
3. Visualize feature distributions using scatter plots
4. Normalize the data using MinMaxScaler
5. Split the data into training, validation, and test sets without shuffling
6. Train multiple forecasting models
7. Evaluate the models using MAE, RMSE, and MAPE
8. Compare actual vs predicted solar output
9. Analyze feature correlations using a heatmap

This sequence is described in both the paper and the code. 

## Models Implemented

### 1. ARIMA
A classical time series forecasting model used to capture linear temporal patterns. In the code, ARIMA is trained with order `(1,1,1)`. 
### 2. LSTM
A two-layer Long Short-Term Memory network with 50 units per layer and a dense output layer. This model is used to learn temporal dependencies in the data. 

### 3. CNN-LSTM-TF
A hybrid architecture combining:
- Conv1D for feature extraction
- MaxPooling1D
- stacked LSTM layers
- dense output layer

This is implemented in the code as `create_cnn_lstm_tf_model`. 

### 4. GRU
A two-layer GRU model designed as a lighter recurrent alternative to LSTM. 

### 5. ARIMA-LSTM Hybrid
A hybrid model where:
- ARIMA captures the linear trend
- LSTM learns residual errors from the ARIMA output

This approach is described in both the paper and the implementation. :contentReference[oaicite:10]{index=10} 
## Evaluation Metrics
The models are compared using:
- **MAE** — Mean Absolute Error
- **RMSE** — Root Mean Squared Error
- **MAPE** — Mean Absolute Percentage Error

These metrics are implemented directly in the code through the `evaluate_model` function.

## Key Results

According to the output in the code and the results table in the report:
- **ARIMA** achieved the best performance overall with **MAE = 0.0145** and **RMSE = 0.0476**
- **ARIMA-LSTM Hybrid** was the next strongest model with **MAE = 0.0166** and **RMSE = 0.0476**
- The deep learning models showed larger errors, and MAPE values were extremely high due to issues with very small actual values and instability in percentage-based error calculation. 

### Performance Summary

| Model | MAE | RMSE | MAPE |
|---|---:|---:|---:|
| ARIMA | 0.0145 | 0.0476 | 0.3091 |
| LSTM | 0.0369 | 0.0502 | 71770937734449.6719 |
| CNN-LSTM-TF | 0.0617 | 0.0959 | 124467558102473.0938 |
| GRU | 0.0389 | 0.0521 | 78032782527559.9531 |
| ARIMA-LSTM Hybrid | 0.0166 | 0.0476 | 9107643159893.6602 |

These values are reported in the paper, while the code output shows closely matching values for the same models. 

## Weather Parameter Analysis
The project also studies how weather variables correlate with solar output. The report concludes:
- **Temperature** has a strong positive correlation with GHI
- **Relative Humidity** has a negative correlation with GHI
- **Pressure** has a weak positive correlation
- **Wind Speed** has a weak correlation with GHI

The heatmap produced in the code also visualizes these relationships. The figure on page 11 of the code PDF shows the correlation matrix between the chosen weather parameters and solar output.
