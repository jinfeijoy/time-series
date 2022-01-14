## Time Series

### Introduction to Time Series Analysis
#### Time Series Component
* Trend: long term direction, captures the general direction of the time series
* Seasonality: periodic behavior, captures effects that occur with specific frequency
* Residual: irregular fluctuations that we cannot predict using trend/seasonality, are the random fluctuations leftover once trend and seasonality are removed.
* Generally, models perform better if we can first remove known sources of variation (like trend and seasonality)
#### Time Series Decomposition
* Approaches to decompose time-series data
  * Additive decomposition: observation = trend + seasonality + residual
    * The seasonal and residual magnitudes are independent of trend
  * Multiplicative decomposition: observation = trend * seasonality * residual ( Or log(obs) = log(trend) + log(seasonal) + log(residual))
    * The seasonal and residual magnitudes fluctuate with trend.
    * d
* Assumptions about seasonal patterns and trends