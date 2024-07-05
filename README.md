# Turnover Time Series Forecast
A __time series forecast__ of revenue by store and department using __XGBoost__. The Jupyter Notebook contains:
1.  __an EDA__ to find insights and outliers. The EDA insights are used to compare to the lagging features and the XGboost model's feature importance.
2.  a section that creates __lagging features__ with turnover up to 8 weeks before, rolling mean over 2 and 4 weeks, and quarterly tirnover. These features are compared to the EDA and the XGboost model.
3.  a __time series XGBoost model__ that is tested on the last 12 months and trained on the rest. The best model is found using __hyperparameter tuning__. The metric that assesses the performance of the test dataset is __R^2__. Inference for the validation set includes the lagging features, since the 2 previous weeks influence the current turnover, and that is done in the following way:
   3.1. For the earliest week in inference, turnover_1_week_before through turnover_8_week_before will be taken from the training dataset if there is data for that period. The model will return projections for the current week.
   3.2. The projections for the first week will become turnover_1_week_before for the second earliest week, while all other columns will take values from the training dataset. The model will return projections for the current week.
   This process will continue until we have a date in the validation set that exhausts the need to get values for the previous weeks from the training data.
4. __ARIMA, SARIMAX, and ETS models__. Residual plots for the ARIMA models are shown for comparison.
