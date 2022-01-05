## EXPONENTIAL SMOOTHENING FOR TIME SERIES FORECASTING IN PYTHON
Exponential smoothing is a time series forecasting method for univariate data (a type of data which consists of observations on only a single characteristic or attribute)

Exponential smoothening forecasting methods are similar to Box-Jenkins ARIMA models in that a prediction is a weighted sum of past observations, but the model explicitly uses an exponentially decreasing weight for past observations. Meaning, specifically, past observations are weighted with a geometrically decreasing ratio.Thus, they can be treated as an alternative to ARIMA.

Collectively, the methods of Box-Jenkins ARIMA as well Exponential smoothening are sometimes referred to as ETS models, referring to the explicit modeling of Error, Trend and Seasonality.

There are three types of exponential smoothening, let us look at two of them.

## Exponential Smoothening
![image](https://user-images.githubusercontent.com/84874044/148252573-96904ab7-2b4c-4f3b-9b29-09e7f31d4a05.png)
##### We can think of  α  as the smoothing factor or memory decay rate, it defines how quickly we will "forget" the last available true observation. The smaller  α  is, the more influence the previous observations have and the smoother the series is. In other words, the higher the  α , the faster the method "forgets" about the past.
We have already seen exponential smoothening, so let us understand the advanced types of exponential smoothening.

## Double Exponential Smoothing
Double Exponential Smoothing is an extension to Exponential Smoothing that explicitly adds support for trends in the univariate time series. It does this by adding an additional smoothing factor in addition to the alpha parameter for controlling smoothing factor for the level, to control the decay of the influence of the change in trend called beta. Basically, we mean to say, if our data has a **trend**, we should use both the level and the trend to forcast future observations.

The method supports trends that change in different ways: an additive and a multiplicative, depending on whether the trend is linear or exponential respectively.

##### Double Exponential Smoothing with an additive trend is classically referred to as Holt’s linear trend model, named for the developer of the method Charles Holt.

- Additive Trend: Double Exponential Smoothing with a linear trend.
- Multiplicative Trend: Double Exponential Smoothing with an exponential trend.

With the current 'trend' denoted by T and the current 'level' denoted by l, we can write three equations: one for level, one for the trend and one to combine the level and trend to get the expected  y^.
![image](https://user-images.githubusercontent.com/84874044/148255759-2bd5e88f-6b4b-4512-96e9-4b7b3621fa50.png)

For longer range (multi-step) forecasts, the trend may continue on unrealistically. As such, it can be useful to dampen the trend over time.
##### Dampening means reducing the size of the trend over future time steps down to a straight line (no trend).
To perform k-step-ahead forecast, we can use linear extrapolation:
![image](https://user-images.githubusercontent.com/84874044/148255293-c8146996-b6c5-46b0-9007-75967a5e911d.png)

As with modeling the trend itself, we can use the same principles in dampening the trend, specifically additively or multiplicatively for a linear or exponential dampening effect. A damping coefficient Phi (p) is used to control the rate of dampening.

- Additive Dampening: Dampen a trend linearly.
- Multiplicative Dampening: Dampen the trend exponentially.
  
#### Hyperparameters involved:

- Alpha: Smoothing factor for the level.
- Beta: Smoothing factor for the trend.
- Trend Type: Additive or multiplicative.
- Dampen Type: Additive or multiplicative.
- Phi: Damping coefficient.

![image](https://user-images.githubusercontent.com/84874044/148253145-180bf409-0cbf-494a-bb84-23a50496cecc.png)
##### Here, α is responsible for the series smoothing around the trend, and β for smoothing the trend itself. Again, the larger the values for these parameters, the more weight recent observations will carry and the less smooth the modeled series will be.

#### Drawbacks
Although this method can now predictive future values, if we stare closer at the forecast formula, we can see that once the trend ( TT ) is estimated to be positive, all future predictions can only go up from the last value in the time series. On the other hand, if the trend ( TT ) is estimated to be negative, all future predictions can only go down. This property makes this method unsuitable for predicting very far out into the future as well. With that in mind, let's now turn towards triple exponential smoothing.

### Triple Exponential Smoothing
It is an extension of Exponential Smoothing and explicitly adds support for seasonality to the univariate time series. (Almost like SARIMA does to ARIMA) It is also sometimes called Holt-Winters Exponential Smoothing.

In addition to the alpha and beta smoothing factors, a new parameter is added called gamma (g) that controls the influence on the seasonal component.

As with the trend, the seasonality may be modeled as either an additive or multiplicative process for a linear or exponential change in the seasonality.

- Additive Seasonality: Triple Exponential Smoothing with a linear seasonality.
- Multiplicative Seasonality: Triple Exponential Smoothing with an exponential seasonality.

Thus, we now have four equations, with one added for seasonality(S):
![image](https://user-images.githubusercontent.com/84874044/148257339-cb910d27-00d9-46e8-a404-d0c5d8bd91de.png)

##### Triple exponential smoothing is the most advanced variation of exponential smoothing and through configuration, it can also develop double and single exponential smoothing models.

Additionally, to ensure that the seasonality is modeled correctly, the number of time steps in a seasonal period (Period) must be specified. For example, if the series was monthly data and the seasonal period repeated each year, then the Period=12.

Also, uptil now we were determining the initial trend and level by using the first two points. However, with seasonal data, we compute the average trend averages across seasons as follows:
![image](https://user-images.githubusercontent.com/84874044/148257921-5cac6720-f10d-44b3-8ccd-36ea57cbbe38.png)


#### Hyperparameters:

- Alpha: Smoothing factor for the level.
- Beta: Smoothing factor for the trend.
- Gamma: Smoothing factor for the seasonality.
- Trend Type: Additive or multiplicative.
- Dampen Type: Additive or multiplicative.
- Phi: Damping coefficient.
- Seasonality Type: Additive or multiplicative.
- Period: Time steps in seasonal period.



### Hyperparameter Optimization

Now we know the required hyperparameters, but arriving at them directly by trial and error would be very challenging. Instead, we use numerical optimization to search for and fund the smoothing coefficients (alpha, beta, gamma, and phi) for the model that result in the lowest error. There is often a constraint on how large the smoothing parameters can be, each of them ranging from 0 to 1. Therefore, in order to minimize our loss function, we have to choose an algorithm that supports constraints on model parameters. 

Apart from choosing the numerical optimization algorithm,  we also have to choose a loss function suitable for the task that will tell us how closely the model approximates the underlying pattern. Then, using cross-validation, we will evaluate our chosen loss function for the given model parameters. The only minor difference, compared with standard supervised learning methods is the way to perform cross validation. Because time series data have this temporal structure, one cannot randomly mix values in a fold while preserving this structure. With randomization, all the time dependencies between observations will be lost, hence the cross validation method that we'll be using will be based on a **rolling window approach**.

The idea is -- we train our model on a small segment of the time series from the beginning until some time  t , make predictions for the next  t+n  steps, and calculate an error. Then, we expand our training sample to  t+n  value, make predictions from  t+nt+n  until  t+2∗n , and continue moving our test segment of the time series until we hit the last available observation.

![image](https://user-images.githubusercontent.com/84874044/148258887-a7f6d48d-0f1d-4366-84b8-8ac190a3fc11.png)

However, we should note that any parameters that specify the type of change in trend and seasonality (additive, multiplicative, dampening) must be specified by programmer explicitly by looking at given data.

### Implementation

We use ExponentialSmoothing Statsmodels class in Python for this.

#### Parameters:

In making an instance of class for configuration of model, we specify following:
- trend: “add” for additive, “mul” for multiplicative, disable modeling by setting to None
- damped: either True or False.
- seasonal: “add” for additive, “mul” for multiplicative, disable modeling by setting to None
- seasonal_periods: 12 for 12 months in a yearly structure, etc

Now, if we do not know enough about our data to specify one or more of these parameters, we can grid serach them by defining a function that fits a model with a given configuration and make a one-step forecast by exp_smoothing_forecast() function and then make a function called exp_smoothing_configs() containing a list of model configurations to evaluate. We similarly create functions such as walk_forward_validation(), measure_rmse() and score_model(), then combine them all in a main function that drives the grid search process and will call the score_model() function for each model configuration. Thus, we first print the contrived time series dataset. Next, the model configurations and their errors are reported as they are evaluated.Finally, the configurations and the error for the top three configurations are reported.
![image](https://user-images.githubusercontent.com/84874044/148259518-32fb094b-359b-46df-8e84-4295f4029df3.png)

To fit this model on training data, we call **fit()** function with following coefficients:
- smoothing_level (alpha)
- smoothing_slope (beta)
- smoothing_seasonal (gamma)
- damping_slope (phi)

We can also choose whether or we want to make some basic basic data preparation before modeling by using:
- use_boxcox: Whether or not to perform a power transform of the series (True/False) or specify the lambda for the transform.

This fit() function returns an instance of the class that containes learned coeffecients. Next we call **forecast() or predict()** to make a forecast.
###### Final Plot of Predicted vs Actual 
![image](https://user-images.githubusercontent.com/84874044/148258334-1e2da551-44d4-4277-bd6f-20c8007424ee.png)
