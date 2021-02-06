# Model Evaluation and Refinement

## Model Evaluation and Refinement
+ In-sample evaluation tells us how well our model will fit the data used to train it
+ **However**, it does not tell us how well the trained model can be used to predict new data
+ **use in-sample data** to train model
+ **out-of-sample** evaluations to test the model


→ Split dataset into 70% of training set and 30% of testing set

```py
from sklearn.model_selection import train_test_split

x_train, x_test, y_train, y_test = train_test_split(x_data, y_data, test_size=.3, random_state=0)
```

+ `x_data`: features or independent variables
+ `y_data`: target
+ `x_train` and `y_train`: parts of available data as training set
+ `x_test`, `y_test`: parts of available data as testing set

### Generalization Performance
+ Generalization error is measure of how well our data does at predicting previously unseen data
+ The error we obtain using our testing data is an **approximation** of this error

![Image](https://i.imgur.com/7NlCybc.png)


### Cross Validation
+ Most common out-of-sample evaluation metrics
+ more efficient use of data (each observation is used for both training and testing)
  
```py
from sklearn.model_selection import cross_val_score

scores = cross_val_score(lr, x_data, y_data, cv=3) # lr: type of model - linear regression (the object we declare previously (the model))

np.mean(scores)
```

```py
from sklearn.model_selection import cross_val_predict

yhat = cross_val_predict(lr2e, x_data, y_data, cv=3)
```
## Overfitting, Underfitting, and Model Selection
Pick the best polynomial order and problems that arise when selecting the wrong order polynomial.


![Image](https://i.imgur.com/tCSxzwT.png)
Using a eight order polynomial.

But if using a sixteenth order polynomial,

![Image](https://i.imgur.com/yLnKc2l.png)

it becomes overfitting.

![Image](https://i.imgur.com/WH0qlCK.png)

### Using R^2
![Image](https://i.imgur.com/P4AnuM9.png)

```py
rsqu_test = []
order = [1, 2, 3, 4]
for n in order:
    pr = PolynomialFeatures(degree=n)
    x_train_pr = pr.fit_transform(x_train[['horsepower']])
    x_test_pr = pr.fit_transform(x_test[['horsepower']])
    lr.fit(x_train_pr, y_train) # fit the regression model

    rsqu_test.append(lr.score(x_test_pr, y_test))

```




## Ridge Regression

Ridge regression is a regression that is employed in a **Multiple regression model** when *Multicollinearity* occurs. *Multicollinearity* is when there is a strong relationship among the independent variables. Ridge regression is very common with **polynomial regression**.  The next video shows how Ridge regression is used to regularize and reduce the standard errors to avoid over-fitting a regression model


![Image](https://i.imgur.com/XsbMUXf.png)

![Image](https://i.imgur.com/wybxtu6.png)

```py
from sklearn.linear_model import Ridge

RidgeModel = Ridge(alpha=.1)
RidgeModel.fit(X,Y)
Yhat = RidgeModel.predict(X)
```

```py
RigeModel = Ridge(alpha=10) 
RigeModel.fit(x_train_pr, y_train)
RigeModel.score(x_test_pr, y_test)
```
## Grid Search

+ training set
+ validation set: pick the best hyperparameter 
+ tests

```py
from sklearn.linear_model import Ridge
from sklearn.model_selection import GridSearchCV

parameters = [{'alpha': [1, 10, 100, 1000], 'normalize': [True, False]}]

RR = Ridge()
Grid1 = GridSearchCV(RR, parameters, cv=4) # number of folds
Grid1.fit(x_data[['horsepower', 'curb-weight', 'engine-size', 'highway-mpg']], y_data)

Grid1.best_estimator_

scores = Grid1.cv_results_

scores['mean_test_score']
```

## Summary

In this lesson, you have learned how to:

**Identify over-fitting and under-fitting in a predictive model**: Overfitting occurs when a function is too closely fit to the training data points and captures the noise of the data. Underfitting refers to a model that can't model the training data or capture the trend of the data.

**Apply Ridge Regression to linear regression models**: Ridge regression is a regression that is employed in a Multiple regression model when Multicollinearity occurs.

**Tune hyper-parameters of an estimator using Grid search**: Grid search is a time-efficient tuning technique that exhaustively computes the optimum values of hyperparameters performed on specific parameter values of estimators.