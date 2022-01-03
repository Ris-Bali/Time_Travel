# ARIMA

## Introduction to ARIMA
ARIMA stands for Autoregressive Integrated Moving Average.


It is a generalized form of the **ARMA** model. 

ARIMA,is actually a class of models that explains a given time series based on its own past values, that is, its own lags and the lagged forecast errors, so that equation can be used to forecast future values.

It is a **linear regression model**
<br>
They are used in Time-Series forecasting to understand and/or to predict future data points in a Time Series. It takes inputs from three values for a non-seasonal (non-recurring/repeating) model
>**p** is the order (number of time lags) of the Auto Regressive model

>**d** is the degree of differencing (number of times, data has past values subtracted), to make the time series stationary

>**q** is the order of the Moving Average model
___
## What is ARMA 

**ARMA** stands for Autoregressive Moving Average. They provide solutions of stochastic difference equations with constant coefficients, possessing a linear structure. The two polynomials that are involved in this are, 
1. Autoregression (Standing for AR) 
    <br>
    An autoregressive model is a representation of random processes. It is used to describe time-varying processes.
    In this model, output variable linearly depends on its own previous values, and on a stochastic term.
    <br>
    A standalone autoregressive model is also a Linear regression model.

    <br>
    This is the definition of the AR model as a stochastic difference equation

    ![img1](https://wikimedia.org/api/rest_v1/media/math/render/svg/783f17f3ab83135ed3828b73b0957735a1b63229)

    ![img2](https://miro.medium.com/max/860/1*oGSdSEXfjS_wJpzIeJEdHQ.png)

    If we consider two significant values above the threshold then the model will be termed as AR(2).

    This kind of model calculates the regression of past time series and calculates the present or future values in the series in know as Auto Regression (AR) model.
    
    An autoregressive model of order p can be written as
    ![img3](images/equation1.png)

    here, <math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mi>&#x03B5;<!-- ε --></mi>
    <mi>t</mi>
  </msub>
</math>
is white noise. We use lagged values of <i>y<sub>t</sub></i> as predictors.
<br>
In the graph above, we use something called **PACF**
<br>
We use PACF and ACF plots to obtain the values of p and q to insert into ARIMA models

<br>

> ACF (Auto-correlation Function) gives us values of auto-correlation of any series with its lagged values. Auto Correlation function takes into consideration of all the past observations irrespective of its effect on the future or present time period. It calculates the correlation between the t and (t-k) time period. It includes all the lags or intervals between t and (t-k) time periods. Correlation is always calculated using the Pearson Correlation formula.


The Pearson Correlation formula is given by
![img4](https://www.gstatic.com/education/formulas2/397133473/en/correlation_coefficient_formula.svg)

where

r = correlation coefficient

x<sub>i</sub> = values of x-variable in sample

x&#x0304; = mean of the values of x-variable

y<sub>i</sub> = values of y-variable in sample

y&#x0304; = mean of the values of y-variable

<br>

>PACF (Partial Auto-correlation Function) determines the partial correlation between time period t and (t-k).Hence we consider only the time lags having a direct impact on future time period by neglecting the insignificant time lags in between the two-time slots t and t-k. 
>
>So basically, it finds correlations of residuals with the next lag value. Hence it is called partial as the variations found in the previous lag is removed by the time we find the next one.



2. Moving Average (Standing for MA)
   <br>
   In statistics, a moving average is a calculation to analyze data points by creating a series of averages of different subsets of the full data set.

   The moving-average model specifies that the output variable depends linearly on the current and various past values of a stochastic (imperfectly predictable) term.
   A moving average is commonly used with time series data to smooth out short-term fluctuations and highlight longer-term trends or cycles.

   Moving average is given by this equation
   ![img5](images/equation2.png)

   which is represented by MA(q) model, a moving average model of order q

   ![img6](https://miro.medium.com/max/858/1*g7Uy0pWHNiwcwUAJRB_nkw.png)


    If we consider two significant values above the threshold then the model will be termed as MA(2).

   This kind of model calculates the residuals or errors of past time series and calculates the present or future values in the series in know as Moving Average (MA) model.

   The time period at t is impacted by the unexpected external factors at various slots t-1, t-2, t-3, ….., t-k. These unexpected impacts are known as Errors or Residuals. The impact of previous time spots is decided by the coefficient factor α at that particular period of time.

So, after obtaining the values of p, and q from the two models (using their ACF and PACF plots), we can make an ARMA model.

The notation ARMA(p, q) refers to the model with p autoregressive terms and q moving-average terms. This model contains the AR(p) and MA(q) models,

![img7](https://wikimedia.org/api/rest_v1/media/math/render/svg/b03d4effdb520d36cc458ec5c2b231354d29d11a)

this, can be represented by

![img8](https://miro.medium.com/max/840/1*Ohzstmio1Vv9jkWLrl-SkA.png)

Consider the above graphs where the MA and AR values are plotted with their respective significant values. Let's assume that we consider only 1 significant value from the AR model and likewise 1 significant value from the MA model. So the ARMA model will be obtained from the combined values of the other two models will be of the order of ARMA(1,1).
and a difference equation can be written as

![img9](images/equation3.png)

where, &phi;<sub>1</sub> ... &phi;<sub>p</sub> and  &#920;<sub>1</sub> ... &#920;<sub>q</sub> are real constants 
___

## What is ARIMA?

As written earlier, ARIMA is a generalized form of ARMA.

ARIMA models are generally of two major types
1.  Non-seasonal ARIMA models
2.  Seasonal ARIMA models
   

