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
    The autocorrelation matrix is most meaningful when dealing with a stationary stochastic process, where the statistical properties (like mean and variance) are constant over time. 
  - Lag selection:
    The number of lags considered in the matrix depends on the analysis goal and the characteristics of the data. 