# Model Development

+ A model can be thought of as a mathematical equation used to predict a value given one or more other values
+ relating one or more independent variables to dependent variables
+ usually the more **relevant data** you have the more accurate your model is 
    + more data is preferable

## Linear Regression and Multiple Linear Regression

+ Linear regression will refer to one independent variable to make a prediction
+ multiple linear regression will refer to multiple independent variables to make a prediction

![Image](https://i.imgur.com/NvCFYDr.png)

### Simple Linear Regression
1. The predictor (independent) variable - $x$
2. The target (dependent) variable - $y$

![Image](https://i.imgur.com/g6xn8ul.png)

Prediction:

Find the linear relationship first. 

Remember that the model is not always correct.


+ X: Predictor variable
+ Y: Target variable

```py
from sklearn.linear_model import LinearRegression

lm=LinearRegression()
X = df[['highway-mpg']]
Y = df['price']

lm.fit(X, Y)

Yhat = lm.predict(X)

lm.intercepts_ # intercept 

lm.coef_ # slope
```


### Multiple Linear Regression (MLR)


This method is used to explain the relationship between: 

+ One continuous target (Y) variable
+ Two or more predictor (X) variables

Given
$$
\hat Y = b_0 + b_1x_1 + b_2x_2 + b_3x_3 + b_4x_4
$$

+ $b_0$: intercept (X=0)
+ $b_1$: the coefficient of parameter $x_1$
+ ...

![Image](https://i.imgur.com/X4htNJK.png)

```py
from sklearn.linear_model import LinearRegression

lm=LinearRegression()


Z = df[['horsepower', 'curb-weight', 'engine-size', 'highway-mpg']]

lm.fit(Z, df['price'])

Yhat = lm.predict(X)

lm.intercept_ # b_0
lm.coef_ # b_1, b_2, b_3, ...
```

![Image](https://i.imgur.com/0XQ7ixK.png)

## Model Evaluation using Visualization

### Regression plot

+ The relationship between two variables
+ the strength of the correlation
+ the direction of the relationship (positive or negative)

+ Horizontal: independent variable
+ Vertical: dependent variable

```py
import seaborn as sns
sns.regplot(x = 'highway-mpg', y = 'price', data=df)
plt.ylim(0, )
```

### Residual Plot

![Image](https://i.imgur.com/uf6PiCy.png)

If ...
![Image](https://i.imgur.com/8j8T1cA.png)

The linear plot is appropriate.

Else if ...
![Image](https://i.imgur.com/sBitZMv.png)

This suggests that the linear relationship might be incorrect.

```py
import seaborn as sns

sns.residplot(df['highway-mpg'], df['price'])
```

### Distribution Plots

Compare the distribution plots:

+ the fitted values that result from the model
+ the actual values

```py
import seaborn as sns

ax1 = sns.displot(df['price'], hist=False, color='r', label='Actual Value') # actual value

sns.displot(Yhat, hist=False, color='b', label='Fitted Values', ax=ax1) # predicted values
```

![Image](https://i.imgur.com/MaFE8Wu.png)

Using MLR:

![Image](https://i.imgur.com/6eZzMVv.png)

The prediction is much closer to the one using LR. 


## Polynomial Regression and Pipelines

+ Polynomial Regression: used when a linear model is not the best fit for our data
+ Pipeline: a way to simplify your code

### Polynomial Regression
+ a special case of the general linear regression model
+ useful for describing *curvilinear relationships*
    + By squaring or setting higher-order terms of the predictor variables
+ can be: 
    + quadratic
    + cubic
    + higher order

![Image](https://i.imgur.com/ceLDfrQ.png)


```py
f = np.polyfit(x, y, 3)
p = np.polyld(f)

print(p)
```

Polynomial regression with more than one dimension:
```py
from sklearn.preprocessing import PolynomialFeatures

pr = PolynomialFeatures(degree=2, include_bias=False)

x_polly = pr.fit_transform(x[['horsepower', 'curb-weight']])
```

#### Pre-processing

Normalize:
```py
from sklearn.preprocessing import StandardScaler
SCALE = StandardScaler()
SCALE.fit(x_data[['horsepower', 'highway-mpg']])
x_scale = SCALE.transform(x_data[['horsepower', 'highway-mpg']])
```

### Pipelines

![Image](https://i.imgur.com/bIDNVML.png)

Pipelines carry out a series of transformations:
![Image](https://i.imgur.com/umKriZi.png)


```py
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import Pipeline

Input = [('scale', StandardScaler()), ('polynomial', PolynomialFeatures(degree=2), ..., ('mode', LinearRegression()))] # 1st: the name of the estimator model; 2nd: the constructor

pipe = Pipeline(Input)

pipe.fit(df[['horsepower', 'curb-weight', 'engine-size', 'highway-mpg']], y)

yhat = pipe.predict(X[['horsepower', 'curb-weight', 'engine-size', 'highway-mpg']])

```

## Measures for In-Sample Evaluation

Evaluating our models.

+ a way to numerically determine how good the model fits on dataset
+ 2 important measures to determine the fit of a model:
    + **Mean Squared Error** (MSE)
    + **R-squared** (R^2)

### Mean Squared Error (MSE)
![Image](https://i.imgur.com/GIEZlfi.png)

```py
from sklearn.metrics import mean_squared_error
mean_squared_error(df['price'], Y_predict_sample_fit) # 2nd: predicted values of the target variable
```

### R-squared
+ The coefficient of determination
+ A measure to determine how close the data is to the fitted regression line
+ R^2: the percentage of variation of the target variable (Y) that is explained by the linear model.
+ Think about as comparing a regression model to a simple model i.e. the mean of the data points


![Image](https://i.imgur.com/uLraX2A.png)
(Takes values between 0 and 1: the bigger the better)

![Image](https://i.imgur.com/tQayReM.png)


```py
X = df[['highway-mpg']]
Y = df['price']

lm.fit(X, Y)
lm.score(X, Y) # R^2
```

## Prediction and Decision Making

+ Do the predicted values make sense?
+ Visualization
    + regression plot
    + residual plot
    + distribution plot: MLR
+ Numerical measures for evaluation
    + mean squared error
    + r squared (from 0 to 1, should be at least 0.1)
+ Comparing Models
    + simple linear regression
    + multiple linear regression
    + polynomial fit (on one independent variable)

```py
# Train model
lm.fit(df['highway-mpg'], df['prices'])

# Predict the price of a car with 30 highway-mpg
lm.predict(np.array(30.0).reshape(-1, 1)) # $13771.30s

lm.coef_
lm.intercepts_
```

```py
import numpy as np
new_input = np.arange(1, 101, 1).reshape(-1, 1)
yhat = lm.predict(new_input)
```

## Summary
In this lesson, you have learned how to:

**Define the explanatory variable and the response variable**: Define the response variable (y) as the focus of the experiment and the explanatory variable (x) as a variable used to explain the change of the response variable. Understand the differences between Simple Linear Regression because it concerns the study of only one explanatory variable and Multiple Linear Regression because it concerns the study of two or more explanatory variables.

**Evaluate the model using Visualization**: By visually representing the errors of a variable using scatterplots and interpreting the results of the model.

**Identify alternative regression approaches**: Use a Polynomial Regression when the Linear regression does not capture the curvilinear relationship between variables and how to pick the optimal order to use in a model.

**Interpret the R-square and the Mean Square Error**: Interpret R-square (x 100) as the percentage of the variation in the response variable y  that is explained by the variation in explanatory variable(s) x. The Mean Squared Error tells you how close a regression line is to a set of points. It does this by taking the average distances from the actual points to the predicted points and squaring them.

