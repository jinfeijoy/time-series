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
