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
* ARMA Models Considerations
  * These are important considerations to keep in mind when dealing with ARMA models:
    * The time series is assumed to be stationary.
    * A good rule of thumb is to have at least 100 observations when fitting an ARMA model.
  * There are three stages in building an ARMA model:
    * Identification
      * Validate that the time series is stationary.
      * Confirm whether the time series contains a seasonal component.
        * Autocorrelation Plot: is commonly used to detect dependence on prior observations. It summarizes total (2-way) correlation between the variable and its past values.
          * ![image](https://user-images.githubusercontent.com/16402963/149845368-6e5cc976-893b-4469-8f24-62b551694e02.png) 
        * partial autocorrelation plots: summarizes dependence on past observations. However, it measures partial results (including all lags)
          * ![image](https://user-images.githubusercontent.com/16402963/149845387-4219b6f9-dcc2-40af-bb50-47c44ab50633.png) 
        * seasonal subseries plots: one approach for measuring seasonality. This chart shows the average level for each seasonal period and illustrates how individual observations relate to this level.
          * ![image](https://user-images.githubusercontent.com/16402963/149845402-dc561ae2-5d5b-4a9f-a933-2c2e9d8d2f9a.png) 
        * intuition (possible in some cases, i.e. seasonal sales of consumer products, holidays, etc.)
    * Estimation
        * Once we have a stationary series, we can estimate AR and MA models. We need to determine p and q, the order of the AR and MA models. 
          * One approach here is to look at autocorrelation and partial autocorrelation plots. 
            * Plot confidence intervals on the Partial Autocorrelation Plot. 
            * Choose lag p such that partial autocorrelation becomes insignificant for p + 1 and beyond
            * Plot confidence intervals on the Autocorrelation Plot
            * Choose lag q such that autocorrelation becomes insignificant for q + 1 and beyond.
          * Another approach is to treat p and q as hyperparameters and apply standard approaches (grid search, cross validation, etc.)
    * Evaluation
      * You can assess your ARMA model by making sure that the residuals will approximate a Gaussian distribution (aka white noise). Otherwise, you need to iterate to obtain a better model.
* Guidelines to choose between an AR and a MA model based on the shape of the autocorrelation and partial autocorrelation plots.
  * ![image](https://user-images.githubusercontent.com/16402963/149845990-5f2d2a22-00d2-4951-9197-41cab3564a20.png)
* How to determine p&q
  * [Time Series From Scratch — Autocorrelation and Partial Autocorrelation Explained](https://towardsdatascience.com/time-series-from-scratch-autocorrelation-and-partial-autocorrelation-explained-1dd641e3076f)
  * [How to Interpret ACF and PACF plots for Identifying AR, MA, ARMA, or ARIMA Models](https://medium.com/@ooemma83/how-to-interpret-acf-and-pacf-plots-for-identifying-ar-ma-arma-or-arima-models-498717e815b6)
  * [What’s The Difference Between Autocorrelation & Partial Autocorrelation For Time Series Analysis?](https://mxplus3.medium.com/interpreting-autocorrelation-partial-autocorrelation-plots-for-time-series-analysis-23f87b102c64)

#### ARIMA Models 
* ARIMA models (Auto-Regressive Integrated Moving Average) have three components:
  * AR Model
  * Integrated Component
  * MA Model
* SARIMA Models (SARIMA is short for Seasonal ARIMA, an extension of ARIMA models to address seasonality)
  * This model is used to remove seasonal components.
    * The SARIMA model is denoted SARIMA (p, d, q) (P, D, Q).
    * P, D, Q represent the same as p, d, q but they are applied across a season.
    * M = one season
* ARIMA and SARIMA Estimation  
  * These are the steps to estimate p, d, q and P, D, Q?
    * Visually inspect a run sequence plot for trend and seasonality.
    * Generate an ACF Plot.
    * Generate a PACF Plot.
    * Treat as hyperparameters (cross validate).
    * Examine information criteria (AIC, BIC) which penalize the number of parameters the model uses.

#### Deep Learning Time Series
* Feeding windowed dataset into neural network
* The code to generat windowed dataset can be found [here](https://github.com/jinfeijoy/tensorflow-1-public/blob/main/C4/W2/ungraded_labs/C4_W2_Lab_2_single_layer_NN.ipynb)

#### Others
*  If it's stationary, meaning its behavior does not change over time, then great. The more data you have the better. But if it's not stationary then the optimal time window that you should use for training will vary (ie trend after financial crisis).
* training/validation/testing split: 
  * Fixed Patitioning
    * ![image](https://user-images.githubusercontent.com/16402963/150458563-e1640fb6-db68-49c9-81fb-2956e5565f8c.png)
    * Often, once you've done that, you can retrain using both the training and validation data. And then test on the test period to see if your model will perform just as well. And if it does, then you could take the unusual step of retraining again, using also the test data.  
  * Roll-forward Partitioning
    * ![image](https://user-images.githubusercontent.com/16402963/150458877-f4fcae7f-8acb-43ad-930f-6fbf967072d2.png)
    * We start with a short training period, and we gradually increase it, say by one day at a time, or by one week at a time. At each iteration, we train the model on a training period. And we use it to forecast the following day, or the following week, in the validation period.
* Evaluation Metrics:
  * ![image](https://user-images.githubusercontent.com/16402963/150458993-47d84809-e40c-42d7-95ae-735e3c7ef1b9.png)
 
### VAR Model
* Granger Causality Test
* autocorrelation test
* stationary check
* stability test (Rec-CUSUM, OLS-CUSUM, Rec-MOSUM, OLS-MOSUM)
* Linear regression check
  * linearity: plot residual and fitted 
  * normality: QQ plot by comparing the residuals to ideal normal observations
  * homoscedasticity check: plot scale location
