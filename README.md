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

meaning the distribution p(Yt1) is the same as any other distribution, p(Yt).  In other words if Yt is identically distributed then Yt is constant over time.

#### Independence
This is a process is independent when it constituent random variables (Yt) are mutually independent.

p(Y1, Y2,...YT),

meaning that the joint probability of the entire stochastic process equals the product of the marginal probabilities across time. 

Forcasting an independent process can be difficult being the past values do not influence current or future values.

p(Yt|Yt-1, Yt-2, ...) = p(Yt)

A stochastic process can be stationary, independent or both.  When its both it is referred to as being "Independent and Identically Distributed" or IID.
An example of this is the Gaussian White Noise process where, every distribution of Yt has mean of 0 and a variance of 1.

#### Autocorrelation Matrix
This is a method for finding the corretion between two different time instances in the same stochastic process (Yt).
