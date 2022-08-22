# Prophet

## What is Prophet
* Prophet is a procedure for forecasting time series data based on an additive model where non-linear trends are fit with yearly, weekly, and daily seasonality, plus holiday effects.
* Prophet is robust to outliers, missing data, and dramatic changes in time series.
* It works best with time series that have strong seasonal effects and several seasons of historical data. Prophet is robust to missing data and shifts in the trend, and typically handles outliers well.
* The procedure makes use of a decomposable time series model with three main model components: trend, seasonality, and holidays.
* y(t) = g(t) + s(t) + h(t) + e(t)
    * g(t): trend models non-periodic changes (i.e. growth over time)
        * saturating growth model ```growth='logistic'```
        * piecewise linear model ```growth='linear'```
    * s(t): seasonality presents periodic changes (i.e. weekly, monthly, yearly)
    * h(t): ties in effects of holidays (on potentially irregular schedules >= 1 day(s))
        * The other parameter that deals with holidays is holidays_prior_scale. This parameter determines how much of an effect holidays should have on your predictions. So for instance when you are dealing with population predictions and you know holidays will have a big effect, try big values. Normally values between 20 and 40 will work, otherwise the default value of 10 usually works quite well. 
    * e(t): covers idiosyncratic changes not accommodated by the model
    * The function can be written as: y(t) = piecewise_trend(t) + seasonality(t) + holiday_effects(t) + i.i.d. noise
    * Trend Changepoints: Changepoints are the points in your data where there are sudden and abrupt changes in the trend. The changepoints parameter is used when you supply the changepoint dates instead of having Prophet determine them. Once you have provided your own changepoints, Prophet will not estimate any more changepoints. From my experience, I have found that letting Prophet discover them on its own and me changing the number of changepoints (with n_changepoints) gave the best results.


##
* Evaluation Matrics: MAPE (mean absolute percentage error)
## Reference
* [The Math of Prophet](https://medium.com/future-vision/the-math-of-prophet-46864fa9c55a)
* [Implementing Facebook Prophet efficiently](https://towardsdatascience.com/implementing-facebook-prophet-efficiently-c241305405a3)
* [Anomaly detection in time series with Prophet library](https://towardsdatascience.com/anomaly-detection-time-series-4c661f6f165f)
* [Multi-step Time Series Forecasting with ARIMA, LightGBM, and Prophet](https://towardsdatascience.com/multi-step-time-series-forecasting-with-arima-lightgbm-and-prophet-cc9e3f95dfb0)
