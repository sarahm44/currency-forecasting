# JPY Currency Forecasting

![""](https://github.com/sarahm44/currency-forecasting/blob/main/Images/jpy.png)

## Table of Contents

## Overview

This repository aims to predict future movements in the value of the Canadian dollar versus the Japanese yen.

Tools utilised include:
1. [Time series forecasting](https://github.com/sarahm44/currency-forecasting/blob/main/time_series_analysis.ipynb)
2. [Linear regression modelling](https://github.com/sarahm44/currency-forecasting/blob/main/regression_analysis.ipynb)

Relevant data for the analysis is contained in [cad_jpy.csv](https://github.com/sarahm44/currency-forecasting/blob/main/cad_jpy.csv).

## Time Series Forecasting

### Plot Settle Price

This is to check for any long or short term patterns. 

There was a significant decline in JPY price comparative to CAD in the 1990s. We see another significant decline for JPY at the time of the 2009 financial crisis.

See graph below:

![""](https://github.com/sarahm44/currency-forecasting/blob/main/Images/settle_price.png)

### Decomposition Using a Hodrick-Prescott Filter

Hodrick-Prescott Filter was used to decompose the exchange rate price into trend and noise.

We see a JPY peak in mid-2015, and lows in late 2016 and 2020.

See a plot of price vs trend for 2015 to present below (note that price is blue, trend is orange):

![""](https://github.com/sarahm44/currency-forecasting/blob/main/Images/price_v_trend.png)

See a plot of the settle noise below:

![""](https://github.com/sarahm44/currency-forecasting/blob/main/Images/settle_noise.png)

### Forecasting Returns using an ARMA Model

I created an ARMA model and fit it to the returns data. The AR and MA ("p" and "q") parameters were set to p=2 and q=1.

The ARMA Model results are set out below:

![""](https://github.com/sarahm44/currency-forecasting/blob/main/Images/arma_results.png)

Based on the p-value I wanted to see if the model is a good fit. Because some of the coefficients are above 0.05, the model is not statistically significant. For one lag the model is significant, but for two lags it is not. So this is not necessarily a good fit on this basis.

The 5 day returns forecast for the ARMA model is below:

![""](https://github.com/sarahm44/currency-forecasting/blob/main/Images/arma_returns.png)

This indicates negative returns in the near term.

### Forecasting the Exchange Rate Price using an ARIMA Model

Using the raw CAD/JPY exchange rate price, I estimated an ARIMA model.

I set P=5, D=1, and Q=1 in the model, where:
* P = number of auto-regressive lags
* D = number of differences (this is usually 1)
* Q = number of moving average lags

The ARIMA Model results are set out below:

![""](https://github.com/sarahm44/currency-forecasting/blob/main/Images/arima_results.png)

Because each of the p-value coefficients are above 0.05, the model is not statistically significant.

The 5 day exchange rate price forecast for the ARIMA model is below, which predicts decrease in JPY price in the short term:

![""](https://github.com/sarahm44/currency-forecasting/blob/main/Images/arima_price.png)

### Volatility Forecasting with GARCH

I used GARCH to predict near-term volatility of Japanese Yen exchange rate returns. Being able to accurately predict volatility can be be extremely useful if you want to trade in derivatives or quantify maximum loss.

I set the parameters of the GARCH model to p=2 and q=1.

See the GARCH Model results below:

![""](https://github.com/sarahm44/currency-forecasting/blob/main/Images/garch_results.png)

P-values for GARCH and volatility forecasts tend to be much lower than ARMA/ARIMA return and price forecasts. In particular, here we have all p-values of less than 0.05, except for alpha(2), indicating overall a much better model performance. In practice, in financial markets, it's easier to forecast volatility than it is to forecast returns or prices.

The 5 day volatility forecast based on the GARCH Model is below:

![""](https://github.com/sarahm44/currency-forecasting/blob/main/Images/garch_forecast.png)

The GARCH Model predicts that volatility will increase in the near term.

### Conclusions

Based on this time series analysis, I would not by yen now, as the forecast indicates negative returns, as well as increased volatility.

Risk of the yen is expected to increase, given that volatility is predicted to increase in the near term.

When it comes to using these models for trading, GARCH is the best of the models, given two of the p-values are below 0.05. The ARIMA and ARMA model have a number of p-values above 0.05 so I would be less confident using these for trading.
