# Time Series Analysis and Linear Regression Forecasting of the Japanese Yen

---
This project tests several time series tools to predict future movements in the value of the Japanese yen versus the US dollar.

---

Historical JPY/USD futures data was loaded from a csv. The below graph plots the Yen Futures Settle Prices:

![Chart1](Images/Chart1.png)

We followed the steps outlined in the "time_series_analysis.ipynb" starter notebook to complete the following:

#### 1. The Hodrick-Prescott Filter was used to decompose the Settle price into trend and noise. Smoothing with the HP Filter and plotting the resulting trend against the actual futures returns, we can see that there's a lot of short term fluctuations that deviate around this trend.

![Chart2](Images/Chart2.png)

Adding back the noise to the trend plot would recreate the original price plot. Plotting the noise on its own produces the following chart:

![Chart3](Images/Chart3.png)

---

#### 2. An ARMA Model was created and fit to the returns of the Settle price data in order to forecast returns. For autoregressive (AR) the parameter p was set to 2 and for the moving average (MA) the parameter q was set to 1 making the order = (2,1).

Based on the summary table output, p-values did not show to be statistically significant with none < 0.05.

![Table1](Images/Table1.png)

The 5-day Futures Price forecast by our ARMA model can be seen in the following chart:

![Chart5](Images/Chart5.png)


All of the p-values are significantly higher than 0.05 so the model is not a good fit.

---

#### 3. An ARIMA Model was created and fit to the returns of the Settle price data in order to forecast Settle prices. For autoregressive (AR) the parameter p was set to 5, for differences the parameter d was set to 1, and for the moving average (MA) the parameter q was set to 1, making the order = (5,1,1).

Based on the summary table output, p-values did not show to be statistically significant with none < 0.05.

![Table2](Images/Table2.png)

The 5-day Futures Price forecast by our ARIMA model can be seen in the following chart:

![Chart6](Images/Chart6.png)

The Yen is forecasted to appreciate in value over the next 5 days relative to the US dollar. Based on the ARIMA model, a 0.04% increase in the Yen over the dollar is expected for the 5 day period.

---

#### 4. A GARCH Model was created and fit to the returns of the Settle price data in order to forecast volatility. Similar to our ARMA model, parameter p was set to 2 and parameter q was set to 1. 

Based on the summary table output, the p-values for omega, alpha[1], and beta[1] are greater than 0.05 and therefore statistically significant.

![Table3](Images/Table3.png)

Based on the GARCH forecast plot for the next 5 days, volatility risk of the Yen will increase each day.

![Chart7](Images/Chart7.png)

---

#### We then used the results of the time series analysis and modeling to answer the following questions:

* QUESTION: Based on your time series analysis, would you buy the yen now? ANSWER: Given that our ARMA and ARIMA models are not statistically significant (with p-values > 0.05), and given that our GARCH model predicts increasing volatility, I would not be comfortable buying the yen now.

* QUESTION: Is the risk of the yen expected to increase or decrease? ANSWER: With increasing forecasted volatility, the risk of the yen is expected to increase.

* QUESTION: Based on the model evaluation, would you feel confident in using these models for trading? ANSWER: 

---

# Regression Analysis: Seasonal Effects with SKLearn Linear Regression

---

We built a Scikit-Learn linear regression model to predict Yen futures ("settle") returns with lagged Yen futures returns and categorical calendar seasonal effects (e.g., day-of-week or week-of-year seasonal effects).

---
  
We followed the steps outlined in the "regression_analysis.ipynb" starter notebook to complete the following:

#### 1. Data Preparation (Creating Returns and Lagged Returns and splitting the data into training and testing data):

The same historical JPY/USD futures data was loaded from a csv. Percentage returns were calculated based on the Settle prices. The returns were then shifted to create a new column of lagged returns. The data was then split into training and testing DataFrames. The training DataFrame included the data up to 2018 and the testing DataFrame included the data from 2018 through 2019. 

---

#### 2. Fitting a Linear Regression Model:

An SKLearn linear regression was fit using the training DataFrame.

---

#### 3. Making predictions using the testing data:

A prediction was done using just the test DataFrame (X_test). Then the predicted returns were put into a DataFrame (Results) alongside the actual return data. Plotting the first 20 predictions vs the true values it is difficult to decifer how well the linear regression model predicted. 

---

#### 4 & 5. Out-of-sample and In-sample performance.

To better assess the predictive ability of the model the Root Mean Squared Error (RMSE) was calculated for both out-of-sample performance and in-sample performance. The higher the Root Mean Squared Error (RMSE) the poorer the prediction is. The out-of-sample RMSE was 0.4154832784856737 while the in-sample RMSE was 0.5963660785073426.

---

#### We then used the results of the linear regression analysis and modeling to answer the following question:

* QUESTION: Does this model perform better or worse on out-of-sample data compared to in-sample data? ANSWER: Based on the prediction performance, the model performed better with the out-of-sample data (test data) with an RMSE of 0.415% compared to the in-sample data (training data) with an RMSE 0.566%. Generally you would expect the model to perform best on the data it trained on (in-sample data).

---

Please reference the accompanying time_series_analysis.ipynb, regression_analysis.ipynb for more information on our analysis. 