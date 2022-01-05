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
   
The ARIMA forecasting equation for a stationary time series is a linear (i.e., regression-type) equation in which the predictors consist of lags of the dependent variable and/or lags of the forecast errors.  That is:

Predicted value of Y = a constant and/or a weighted sum of one or more recent values of Y and/or a weighted sum of one or more recent values of the errors.

<p><span style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;;mso-fareast-font-family:
&quot;Times New Roman&quot;">If d=0: </span><span style="font-size:14.0pt"><span style="mso-spacerun:yes">&nbsp;</span>y<sub>t</sub><span style="mso-spacerun:yes">&nbsp; </span>=<span style="mso-spacerun:yes">&nbsp;
</span>Y<sub>t</sub><o:p></o:p></span></p>

<p><span style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;;mso-fareast-font-family:
&quot;Times New Roman&quot;">If d=1: </span><span style="font-size:14.0pt"><span style="mso-spacerun:yes">&nbsp;</span>y<sub>t</sub><span style="mso-spacerun:yes">&nbsp; </span>=<span style="mso-spacerun:yes">&nbsp;
</span>Y<sub>t</sub> </span><span style="font-size:14.0pt;font-family:&quot;Courier New&quot;">-
</span><span style="font-size:14.0pt">Y<sub>t-1</sub><o:p></o:p></span></p>

In terms of y, the general forecasting equation is:


<p><span style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;;mso-fareast-font-family:
&quot;Times New Roman&quot;">If d=1: </span><span style="font-size:14.0pt"><span style="mso-spacerun:yes">&nbsp;</span>y<sub>t</sub><span style="mso-spacerun:yes">&nbsp; </span>=<span style="mso-spacerun:yes">&nbsp;
</span>Y<sub>t</sub> </span><span style="font-size:14.0pt;font-family:&quot;Courier New&quot;">-
</span><span style="font-size:14.0pt">Y<sub>t-1</sub><o:p></o:p></span></p>

To identify the appropriate ARIMA model for Y, you begin by determining the order of differencing (d) needing to stationarize the series and remove the gross features of seasonality, perhaps in conjunction with a variance-stabilizing transformation such as logging or deflating.  

Cases of ARIMA 

<p><a name="arima110"></a><a name="arima100"></a><b><span style="font-size:10.0pt;
font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;">ARIMA(1,0,0) = first-order autoregressive
model: </span></b><span style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;;
mso-bidi-font-weight:bold"><span style="mso-spacerun:yes">&nbsp; </span><o:p></o:p></span></p>
if the series is stationary and autocorrelated,
perhaps it can be predicted as a multiple of its own previous value, plus a constant

The forecasting equation in this case is 
<p><span style="font-size:14.0pt">Ŷ<sub>t</sub><span style="mso-spacerun:yes">&nbsp; </span>=<span style="mso-spacerun:yes">&nbsp;
</span>μ<span style="mso-spacerun:yes">&nbsp; </span>+<span style="mso-spacerun:yes">&nbsp; </span>ϕ<sub>1</sub>Y<sub>t-1</sub></span><span style="font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;"><o:p></o:p></span></p>

which is Y regressed on itself lagged by one period. This is an “ARIMA(1,0,0)+constant” model.  If the mean of Y is zero, then the constant term would not be included.

<b><span style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;">ARIMA(0,1,0)
= random walk: </span> </b>

If the series Y is not stationary, the simplest possible model for it is a random walk model, which can be considered as a limiting case of an AR(1) model in which the autoregressive coefficient is equal to 1, i.e., a series with infinitely slow mean reversion.  The prediction equation for this model can be written as:

<p><span style="font-size:14.0pt">Ŷ<sub>t</sub><span style="mso-spacerun:yes">&nbsp; </span>=<span style="mso-spacerun:yes">&nbsp;&nbsp; </span>μ + Y<sub>t-1</sub></span><span style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;"><o:p></o:p></span></p>

The random-walk-without-drift model would be an ARIMA(0,1,0) model without constant

<b><span style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;">ARIMA(1,1,0)
= differenced first-order autoregressive model: </span></b>

If the errors of a random walk model are autocorrelated, perhaps the problem can be fixed by adding one lag of the dependent variable to the prediction equation--i.e., by regressing the first difference of Y on itself lagged by one period. This would yield the following prediction equation:

<p><span style="font-size:14.0pt">Ŷ<sub>t</sub><span style="mso-spacerun:yes">&nbsp; </span>=<span style="mso-spacerun:yes">&nbsp;
</span>μ<span style="mso-spacerun:yes">&nbsp; </span>+ Y<sub>t-1</sub><span style="mso-spacerun:yes">&nbsp; </span>+<span style="mso-spacerun:yes">&nbsp;
</span>ϕ<sub>1</sub> (Y<sub>t-1 </sub></span><span style="font-size:14.0pt;
font-family:&quot;Courier New&quot;">-</span><span style="font-size:14.0pt"> Y<sub>t-2</sub>)</span><span style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;"><o:p></o:p></span></p>

This is a first-order autoregressive model with one order of nonseasonal differencing and a constant term--i.e., an ARIMA(1,1,0) model.


<b><span style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;">ARIMA(0,1,1)
without constant = simple exponential smoothing:</span></b>

The simple exponential smoothing model uses an exponentially weighted moving average of past values to achieve this effect. The prediction equation for the simple exponential smoothing model can be written in a number of mathematically equivalent forms, one of which is the so-called “error correction” form, in which the previous forecast is adjusted in the direction of the error it made:

<p><span lang="FR-CA" style="font-size:14.0pt;mso-ansi-language:FR-CA">Ŷ<sub>t</sub><span style="mso-spacerun:yes">&nbsp;&nbsp; </span>=<span style="mso-spacerun:yes">&nbsp; </span>Y</span><sub><span lang="FR-CA" style="mso-ansi-language:FR-CA">t-1</span></sub><sub><span lang="FR-CA" style="font-size:14.0pt;mso-ansi-language:FR-CA"> </span></sub><span lang="FR-CA" style="font-size:14.0pt;mso-ansi-language:FR-CA"><span style="mso-spacerun:yes">&nbsp;</span></span><span lang="FR-CA" style="font-size:
14.0pt;font-family:&quot;Courier New&quot;;mso-ansi-language:FR-CA">-</span><span lang="FR-CA" style="font-size:14.0pt;mso-ansi-language:FR-CA"> (1</span><span lang="FR-CA" style="font-size:14.0pt;font-family:&quot;Courier New&quot;;mso-ansi-language:
FR-CA">-</span><span lang="FR-CA" style="font-size:14.0pt;mso-ansi-language:FR-CA">α)e</span><sub><span lang="FR-CA" style="mso-ansi-language:FR-CA">t-1</span></sub><span lang="FR-CA" style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;;mso-ansi-language:
FR-CA"><o:p></o:p></span></p>

<p><span lang="FR-CA" style="font-size:14.0pt;mso-ansi-language:FR-CA"><span style="mso-spacerun:yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>=<span style="mso-spacerun:yes">&nbsp; </span>Y</span><sub><span lang="FR-CA" style="mso-ansi-language:FR-CA">t-1</span></sub><sub><span lang="FR-CA" style="font-size:14.0pt;mso-ansi-language:FR-CA"> </span></sub><span lang="FR-CA" style="font-size:14.0pt;mso-ansi-language:FR-CA"><span style="mso-spacerun:yes">&nbsp;</span></span><span lang="FR-CA" style="font-size:
14.0pt;font-family:&quot;Courier New&quot;;mso-ansi-language:FR-CA">-</span><span lang="FR-CA" style="font-size:14.0pt;mso-ansi-language:FR-CA"> </span>θ<sub><span lang="FR-CA" style="mso-ansi-language:FR-CA">1</span></sub><span lang="FR-CA" style="font-size:14.0pt;mso-ansi-language:FR-CA">e</span><sub><span lang="FR-CA" style="mso-ansi-language:FR-CA">t-1</span></sub><span lang="FR-CA" style="font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;;mso-ansi-language:FR-CA"><o:p></o:p></span></p>

which is an ARIMA(0,1,1)-without-constant forecasting equation with θ<sub>1</sub> = 1-α.

This means that you can fit a simple exponential smoothing by specifying it as an ARIMA(0,1,1) model without constant, and the estimated MA(1) coefficient corresponds to 1-minus-alpha in the SES formula.

> <b>SES FORMULA</b><br>
> The simple moving average model described above has the undesirable property that it treats the last k observations equally and completely ignores all preceding observations. Intuitively, past data should be discounted in a more gradual fashion--for example, the most recent observation should get a little more weight than 2nd most recent, and the 2nd most recent should get a little more weight than the 3rd most recent, and so on. The simple exponential smoothing (SES) model accomplishes this.
> 
> Let α denote a "smoothing constant" (a number between 0 and 1).  One way to write the model is to define a series L that represents the current level (i.e., local mean value) of the series as estimated from data up to the present.   The value of L at time t is computed recursively from its own previous value like this:
 <p style="margin:0in;margin-bottom:.0001pt"><span style="font-size:14.0pt;
mso-bidi-font-size:12.0pt">L<sub>t</sub><span style="mso-spacerun:yes">&nbsp;
</span>=<span style="mso-spacerun:yes">&nbsp; </span>αY<sub>t</sub><span style="mso-spacerun:yes">&nbsp; </span>+<span style="mso-spacerun:yes">&nbsp;
</span>(1</span><span style="font-size:14.0pt;mso-bidi-font-size:12.0pt;
font-family:Symbol;mso-ascii-font-family:&quot;Times New Roman&quot;;mso-hansi-font-family:
&quot;Times New Roman&quot;;mso-char-type:symbol;mso-symbol-font-family:Symbol"><span style="mso-char-type:symbol;mso-symbol-font-family:Symbol">-</span></span><span style="font-size:14.0pt;mso-bidi-font-size:12.0pt">α)<span style="mso-spacerun:yes">&nbsp; </span>L<sub>t</sub></span><sub>-1<o:p></o:p></sub></p>

>Thus, the current smoothed value is an interpolation between the previous smoothed value and the current observation, where α controls the closeness of the interpolated value to the most recent observation. The forecast for the next period is simply the current smoothed value.

<b><span style="font-size:10.0pt;font-family:&quot;Verdana&quot;,&quot;sans-serif&quot;">ARIMA(0,1,1)
with constant = simple exponential smoothing with growth:</span></b>
 By implementing the SES model as an ARIMA model, you actually gain some flexibility.
 The ARIMA(0,1,1) model with constant has the prediction equation:

 <p><span style="font-size:14.0pt">Ŷ<sub>t</sub><span style="mso-spacerun:yes">&nbsp;&nbsp; </span>=<span style="mso-spacerun:yes">&nbsp; </span>μ<span style="mso-spacerun:yes">&nbsp; </span>+ Y</span><sub>t-1</sub><sub><span style="font-size:14.0pt"> </span></sub><span style="font-size:14.0pt"><span style="mso-spacerun:yes">&nbsp;</span></span><span style="font-size:14.0pt;
font-family:&quot;Courier New&quot;">-</span><span style="font-size:14.0pt"> </span>θ<sub>1</sub><span style="font-size:14.0pt">e</span><sub>t-1</sub></p>


2.  #### Seasonal ARIMA models
   
Seasonal Autoregressive Integrated Moving Average, SARIMA or Seasonal ARIMA, is an extension of ARIMA that explicitly supports univariate time series data with a seasonal component.

It adds three new hyperparameters to specify the autoregression (AR), differencing (I) and moving average (MA) for the seasonal component of the series, as well as an additional parameter for the period of the seasonality.

A seasonal ARIMA model is formed by including additional seasonal terms in the ARIMA models we have seen so far. It is written as follows:

<p align="center"> 

ARIMA (p , d , q) (P , D , Q)<sub>m</sub>
</p>

where m = number of observations per year.

p = Trend autoregression order.

d = Trend difference order.

q = Trend moving average order.

P = Seasonal autoregressive order.

D = Seasonal difference order.

Q = Seasonal moving average order.

The seasonal part of the model consists of terms that are similar to the non-seasonal components of the model, but involve backshifts of the seasonal period. 
For example, an ARIMA(1,1,1)(1,1,1) <sub>4</sub> model (without a constant) is for quarterly data(m=4), and can be written as :

![img7](images/equation4.png)

##### ACF and PACF in SARIMA

The seasonal part of an AR or MA model will be seen in the seasonal lags of the PACF and ACF.

For Example

ARIMA (0,0,1)(0,0,1)<sub>10</sub>

will show

* a spike at lag 10 in the ACF but no other significant spikes
* exponential decay in seasonal lags of lag 10
  

The SARIMA time series forecasting method is supported in Python via the Statsmodels library.
