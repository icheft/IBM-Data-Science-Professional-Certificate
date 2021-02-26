# Linear Regression

## Introduction to Regression

+ Simple Regression:
    + Simple Linear Regression
    + Simple Non-Linear Regression
+ Multiple Regression: 
    + Multiple Linear Regression
    + Multiple Non-Linear Regression


### Applications
+ Sales forecasting
+ Satisfaction analysis
+ Price estimation
+ Employment income

### Regression algorithms

+ Ordinal Regression
+ Poisson Regression
+ Fast forest quantile regression
+ Linear, Polynomial, Lasso, Stepwise, Ridge regression
+ Bayesian linear regression
+ Neural network regression
+ decision forest regression
+ boosted decision tree regression
+ KNN (K-nearest neighbors)

## Simple Linear Regression

![Image](https://i.imgur.com/DboGnm0.png)

![Image](https://i.imgur.com/B5VrGOa.png)


### Pros of Linear Regression
+ very fast
+ no parameter tuning
+ easy to understand, and highly interpretable

## Model Evaluation in Regression Models

Approaches:

+ train and test on the same dataset
    ![Image](https://i.imgur.com/g612vb8.png)
+ train/test split
    ![Image](https://i.imgur.com/RTYaufN.png)
    + K-fold cross-validation
        ![Image](https://i.imgur.com/SeeOvbM.png)


Terminology:

+ Training Accuracy 
    + High training accuracy isn't necessarily a good thing
    + Result of over-fitting
        + *Over-fit*: the model is overly trained to the dataset, which may capture noise and produce a non-generalized model
+ Out-of-Sample Accuracy
    + it's important that our models have a high, out-of-sample accuracy
    + improvement
        + using train/test split


## Evaluation Metrics in Regression Models
  
![Image](https://i.imgur.com/RI03B2J.png)

### MAE
$$
MAE = \frac{1}{n}\Sigma_{j=1}^{n} \vert y_j - \hat y_j\vert
$$

### MSE
$$
MSE = \frac{1}{n}\Sigma_{j=1}^{n} ( y_j - \hat y_j)^2
$$

More popular. It focuses more towards larger errors. 

### RMSE

$$
RMSE = \sqrt{\frac{1}{n}\Sigma_{j=1}^{n} ( y_j - \hat y_j)^2}
$$

+ Interpretable as the same unit

### RAE
Relative Absolute Error, aka Residual Sum of Square.

$$
RAE = \frac{\Sigma_{j=1}^{n} \vert y_j - \hat y_j\vert}{\Sigma_{j=1}^{n} \vert y_j - \bar y_j\vert}
$$

### RSE
$$
RAE = \frac{\Sigma_{j=1}^{n}  (y_j - \hat y_j)^2}{\Sigma_{j=1}^{n} ( y_j - \bar y_j)^2}
$$

+ Used to calculate $R^2$
    + $R^2 = 1 - RSE$
    + The higher the $R^2$, the better the model fits your data

## Multiple Linear Regression

### Examples

+ Independent variables effectiveness on prediction
    + does revision time, test anxiety, lecture attendance and gender have any effect on the exam performance of students?
+ Predicting impacts of changes
    + How much does blood pressure go up (or down) for every unit increase (or decrease) in the BMI of a patient?

![Image](https://i.imgur.com/mXuNs5P.png)

General Form:
![Image](https://i.imgur.com/Wl55JI8.png)

![Image](https://i.imgur.com/JZPKzCo.png)

### Finding the Optimized Parameters

+ Using MSE to expose the errors in the model
    ![Image](https://i.imgur.com/bWDhNWW.png)
    + Then, use MSE

### Estimating Multiple Linear Regression Parameters
+ How to estimate $\theta$?
    + Ordinary Least Squares
        + Linear Algebra Operations
        + Takes a long time for large datasets (10k+ rows)
    + An optimization algorithm
        + gradient descent 
        + proper approach if you have a very large dataset

### Q&A
+ How to determine whether to use simple or multiple linear regression?
+ How many independent variables should you use?
    + Adding too many variables might result in an over-fit model 
+ Should the independent variable be continuous?
    + can transform categorical data to interval data.
+ What are the linear relationships between the dependent variable and the independent variables?
    + use scatter plot to check 

## Python Code
### Simple Linear Regression

See relation:
```py
plt.scatter(train.ENGINESIZE, train.CO2EMISSIONS,  color='blue')
plt.xlabel("Engine size")
plt.ylabel("Emission")
plt.show()
```

Creating train and test dataset:
```py
msk = np.random.rand(len(df)) < 0.8
print(msk)
train = cdf[msk]
test = cdf[~msk]
```

Modeling:
```py
from sklearn import linear_model
regr = linear_model.LinearRegression()
train_x = np.asanyarray(train[['ENGINESIZE']])
train_y = np.asanyarray(train[['CO2EMISSIONS']])
regr.fit(train_x, train_y)

# The coefficients
print ('Coefficients: ', regr.coef_)
print ('Intercept: ',regr.intercept_)
coef = regr.coef_[0][0]
inter = regr.intercept_[0]
```

```py
plt.scatter(train.ENGINESIZE, train.CO2EMISSIONS,  color='blue')
plt.plot(train_x, regr.coef_[0][0]*train_x + regr.intercept_[0], '-', color='orange')
plt.xlabel("Engine size")
plt.ylabel("Emission")
plt.annotate('y = {0:.0f} x + {1:.0f}'.format(coef, inter), xy=(5, 200))
plt.show()
```
![Image](https://i.imgur.com/ZzaVkvB.png)

Evaluation:
```py
from sklearn.metrics import r2_score

test_x = np.asanyarray(test[['ENGINESIZE']])
test_y = np.asanyarray(test[['CO2EMISSIONS']])
test_y_ = regr.predict(test_x)

print("Mean absolute error: %.2f" % np.mean(np.absolute(test_y_ - test_y)))
print("Residual sum of squares (MSE): %.2f" % np.mean((test_y_ - test_y) ** 2))
print("R2-score: %.2f" % r2_score(test_y , test_y_) )
```

### Multiple Linear Regression

Modeling:
```py
from sklearn import linear_model
regr = linear_model.LinearRegression()
x = np.asanyarray(train[['ENGINESIZE','CYLINDERS','FUELCONSUMPTION_COMB']])
y = np.asanyarray(train[['CO2EMISSIONS']])
regr.fit (x, y)
# The coefficients
print ('Coefficients: ', regr.coef_)
print(f'Intercept: {regr.intercept_}')
```

Prediction:
```py
y_hat= regr.predict(test[['ENGINESIZE','CYLINDERS','FUELCONSUMPTION_COMB']])
x = np.asanyarray(test[['ENGINESIZE','CYLINDERS','FUELCONSUMPTION_COMB']])
y = np.asanyarray(test[['CO2EMISSIONS']])
print("Residual sum of squares: %.2f"
      % np.mean((y_hat - y) ** 2))

# Explained variance score: 1 is perfect prediction
print('Variance score: %.6f' % regr.score(x, y))
```