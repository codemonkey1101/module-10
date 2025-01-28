# module-10
## Time Series Analysis and Forecasting

### Overview:
Time series analysis allows for the examination of a series of data points over an extended time period. Analysts use time series analysis to record data points at consistent intervals over a set duration that can be used to model, simulate, and forecast behavior and inform strategic decision-making.
Time series analysis has many practical applications—including business forecasting, econometric forecasting, and financial forecasting—and can be applied to any industry with consistent historical data for analysis.

### The Forecasting Problem
To analyze a problem in time series, you collect data, train a model, utilize the model to make a forecast, and evaluate the model’s performance. While forecasting can occur at any consistent time interval, it is not always exact, and the likelihood of an accurate forecast can vary wildly. Furthermore, time series are prone to fluctuation and are susceptible to uncontrolled outside factors (i.e., pandemics).  However, the forecasting process can provide insight into which outcomes are more likely to occur. More comprehensive data will result in a more accurate forecast.  The models discussed are:
- Decomposition
- Autoregressive Moving Average (ARMA)

### The stochastic process.  
This process is defined as an ordered sequence of random variables defined as: Yt(1:T) = (Y1,Y2...YT), where T is the length of the stochastic process which can be infinite.
A time series is a single sample from the stochastic process.

Two major characteristics of a stochastic process are stationarity and independence.

#### Stationarity
A process is stationary when its statistical properties (i.e. mean, variance and its correlation between different points in time) remain constant over time.
In other words if you place a window at any point in the time series the statistics shall remain the same.

p(Yt1) = p(Yt)

What this means is that the distribution p(Yt1) is the same as any other distribution, p(Yt).  In other words if Yt is identically distributed then Yt is constant over time.

#### Independence
A process is independent when it's constituent random variables (Yt) are mutually independent, where:

p(Y1, Y2,...YT),

this means that the joint probability of the entire stochastic process equals the product of the marginal probabilities across time. 

Forcasting an independent process can be difficult being that the past values do not influence current or future values, as shown in the following formula:

p(Yt|Yt-1, Yt-2, ...) = p(Yt)

#### IDD
A stochastic process can be stationary, independent or both.  When its both it is referred to as being "Independent and Identically Distributed" or IID.
An example of this is the Gaussian White Noise process where, every distribution of Yt has a mean of 0 and a variance of 1.

#### Autocorrelation Matrix
This is a method for finding the correlation between two different time instances in the same stochastic process (Yt).

An example of an autocorrelation matrix for a stochastic process could be a matrix representing the correlations between different time points of a stationary time series like stock prices, where each element in the matrix represents the correlation between a pair of observations separated by a specific time lag, with the diagonal elements being the variance of the process itself; for instance, if you have a time series with 5 observations, the autocorrelation matrix would be a 5x5 matrix where the element at row 1, column 2 would represent the correlation between the first and second observation, and so on.  The following is an example of sucha a matrix:
    [  1   a   a^2  a^3  a^4 ]

    [  a   1   a   a^2  a^3 ]

    [  a^2  a   1   a   a^2 ]

    [  a^3  a^2  a   1   a  ]

    [  a^4  a^3  a^2  a   1 ]


- Key points about the autocorrelation matrix:
  - Structure:
    Due to the nature of autocorrelation, the matrix will be symmetric, with the same values on the diagonal mirrored across the main diagonal. 
  - Interpretation:
    A high value at a specific lag indicates a strong correlation between observations separated by that time lag, suggesting a trend or pattern in the data. 
- Important considerations:
  - Stationarity:
    The autocorrelation matrix is most meaningful when dealing with a stationary stochastic process, where the statistical properties (like mean and variance) are constant over time. It should be noted that when generating autocorrelations from a stationary process, the number of lags typically decay over time exponentially or sometimes the first few correlations have values and the rest got to 0.
  - Lag selection:
    The number of lags considered in the matrix depends on the analysis goal and the characteristics of the data. 
### Autocorrelations using Statsmodels package in Python
- Provides functionality for doing statistical inference in Python.  For instance
  - generation of time series data.
  - analyzing of time series data.
- Shares some functionality with Scikit-learn.
- Adds time series analysis which Scikit-learn does not have.
- It also has a number of datasets that one can use for practice

### Example using statsmodels and datasets to plot autocorrelations:
[example-using-statsmodels.ipynb](module-10/edit/main/example-using-statsmodels .ipynb)

## Modeling Long-Term Time Series
### Overview
- Trend:
- Seasonality (Periodicity):
- Cycles: 
- Stationary processes: with regards to modeling are not necessarily white any contain structure in the form of the autocorrelation function.

The forumla that is used in this example to forcast long-term behavior is: 
Y(t-h:t) : the vector Y from t - (t to h)  where the signal (y) = t + c + s + r.  The behaviors that are tracked in this formula are as follows:

t: Trend: long term behavior
c: Cycles: Random low frequency variations
s: Seasonality: Known periodicity
r: Residue: Everything else

If the signal (y) is well characterized by the trend, cycles and seasonality, then we expect the residue to behave like a stationary process.  This means it will exhibit no structure at the time scales of cycles, seasons and trends.  However, it still may contain hard-to-see structure at the level of a few time steps.

### The Three Steps of Time Series Decomposition
formula: y = t + c + s + r
1. Compute the trend and cycles by smoothing the data.  It is assumed that the cycles are rare and there for can be lumped in with the trend.
2. Compute the seasonal component.
3. Check the stationarity of the residue.

#### Computing the trend and cycles:
This occurs by smoothing the data (y) through a filter/function f() where f() is an array of positive numbers that add up to 1.  The length of f() should similar, but greater than the period of the data.

formula: t = conv(y,f)  where t(t) = f(sub 0) * Y(sub t - 6) + f(sub 1) * Y(sub t - 5) + ... + f(sub 12) * Y(sub t + 6)

To compute (t) at some point in time we take a weighted average of nearby values of (y) with weights given by f().  Because the filter is longer than the period it will remove the seasonal component completely and leave only trend and cycles assuming the cycles are longer than the seasonality and not to severe.

The nature of the line generated by the trend defines the type of extrapolation used to defined the predicted trend.  For example if the trends suggests something more than just a flat line (i.e. increasing or decreasing trend), we could use linear regression with linear, quadractic or exponential basis functions.

#### Computing the seasonal component:
1. We create segements of length one period from the historical time series.
2. Then we overlap those segments and take their average.

## ARMA 
### Overview
Sometimes notated as ARIMA, stands for autoregressive integrated moving average and is a combination of two different time series models: Autoregressive and moving average. The relevant terms in this acronym are defined as follows:

- Autoregression: A model based on observations that are correlated with lagged observations
- Integrated: A term that indicates that raw observations have been differentiated to make the time series stationary
- Moving average: A model based on the dependence between an observation and a residual error after applying a moving average model to lagged observations

In short, ARMA is a forecasting model for a stationary time series (i.e., linear regression-type) model in which the predictors consist of lags of the dependent variable and/or lags of the forecasted errors


## Quick Reference Guide
