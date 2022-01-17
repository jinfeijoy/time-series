## Time Series

### Introduction to Time Series Analysis
#### Time Series Component
* Trend: long term direction, captures the general direction of the time series
* Seasonality: periodic behavior, captures effects that occur with specific frequency
* Residual: irregular fluctuations that we cannot predict using trend/seasonality, are the random fluctuations leftover once trend and seasonality are removed.
* Generally, models perform better if we can first remove known sources of variation (like trend and seasonality)
#### Time Series Decomposition
* Approaches to decompose time-series data
  * ![image](https://user-images.githubusercontent.com/16402963/149573845-92881970-7cf9-4a5e-9bc1-390e56077075.png) 
  * Additive decomposition: observation = trend + seasonality + residual
    * The seasonal and residual magnitudes are independent of trend
  * Multiplicative decomposition: observation = trend * seasonality * residual ( Or log(obs) = log(trend) + log(seasonal) + log(residual))
    * The seasonal and residual magnitudes fluctuate with trend.
  * Pseudo-additive models combine elements of the additive and multiplicative models
    * can be useful when:
        * time series values are close to or equal to 0
        * we expected features related to a multiplicative model
        * division by 0 often become a problem when this is the case
        * ![image](https://user-images.githubusercontent.com/16402963/149574268-41aa3b45-5d0a-49db-b0fa-95afaeda49a4.png) 
* How to decompose time series:
    * single, double, triple exponential smoothing
    * locally estimated scatterplot smoothing (LOESS) (only for additive decomposition)
    * Frequency-based methods: define seasonal component without specify any frequency

### Stationarity and Time Series Smoothing
#### Stationarity and Autocorrelation
* Stationary Time Series Assumption:
  * Constant Mean
  * Constant Variance
  * Constant Autocorrelation (autocorrelation means today's measurement is highly correlated to past value) 
  * No periodic component (such as seasonality)
* Common approach:
  * Identify sources of non-stationarity
  * Transform series to make it stationary
  * Build models with stationary series
* The Augmented Dickey-Fuller (ADF) test specifically tests for stationarity.
  * It is a hypothesis test: the test returns a p-value,  and we generally say the series is non-stationary if the p-value is less than 0.05.
  * It is a less appropriate test to use with small datasets,  or data with heteroscedasticity (different variance across observations) present.
  * It is best to pair ADF with other techniques such as:  run-sequence plots, summary statistics, or histograms.
* Common Transformations for Time Series include:
  * Remove trend (constant mean)
  * Remove heteroscedasticity with log (constant variance)
  * Remove autocorrelation with differencing (exploit constant structure)
  * Remove seasonality (no periodic component)
  * Multiple transformations are often required.
#### Time Series Smoothing
* Smoothing is a process that often improves our ability to forecast series by reducing the impact of noise.
* Smoothing approaches: 
  * Simple average smoothing
  * Moving Average: avoid sensitivity to local fluctuations
    * **Equally weighted moving average**: this technique clearly lags the trend moving forward, and we see that this actually becomes a bigger and bigger problem as that trend becomes more aggressive
    * **Exponentially weighted moving average**: exponential is more sensitive to local changes. We put more weight to those more recent values, however, exponential still lag significantly
      * ![image](https://user-images.githubusercontent.com/16402963/149667041-111b1419-c6a8-447f-9d9c-52022e740ae8.png)
  * Exponential Smoothing
    * Single Exponential Smoothing: lack a trend
      * ![image](https://user-images.githubusercontent.com/16402963/149667197-7917a9f1-dee3-4e1c-9229-93bbdea16d78.png)
    * Double Exponential Smoothing: have trend but no seasonality
      * ![image](https://user-images.githubusercontent.com/16402963/149667228-1cf437a7-0f03-4797-8258-8253b852a41d.png)
    * Triple Exponential Smoothing: have trend and seasonality
      * ![image](https://user-images.githubusercontent.com/16402963/149667296-75de17bf-a1b4-4408-9767-2c7b54001c1b.png)

### ARMA & ARIMA
#### ARMA
* ARMA models combine two models:
  * The first is an autoregressive (AR) model. Autoregressive models anticipate series’ dependence on its own past values.
  * The second is a moving average (MA) model. Moving average models anticipate series’ dependence on past forecast errors.
  * The combination (ARMA) is also known as the Box - Jenkins approach.
  * ARMA models are often expressed using orders p and q for the AR and MA components. 
  * ![image](https://user-images.githubusercontent.com/16402963/149844411-853e9c74-d061-49c0-a23d-3f67e112e134.png)
  * ![image](https://user-images.githubusercontent.com/16402963/149844422-833e620f-a3a4-48f5-914f-097d0466406a.png)
  * ![image](https://user-images.githubusercontent.com/16402963/149844443-569c1281-9ec5-433a-aac5-00192bd83ef7.png)




