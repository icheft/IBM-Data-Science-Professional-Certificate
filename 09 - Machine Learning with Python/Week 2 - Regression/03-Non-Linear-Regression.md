# Non-Linear Regression

![Image](https://i.imgur.com/z6skfJW.png)

The above data cannot be predicted using linear regression. 

+ A polynomial regression model can be transformed into linear regression model
    ![Image](https://i.imgur.com/PZvgasL.png)

+ To model non-linear relationship between the dependent variable and a set of independent variables
+ $\hat y$ must be a non-linear function of the parameters $\theta$, not necessarily the features $x$.


### Linear vs non-linear regression
+ How can I know if a problem is linear or non-linear in an easy way?
    + inspect visually
    + based on accuracy 
+ How should I model my data, if it displays non-linear on a scatter plot
    + polynomial regression
    + Non-linear regression model
    + transform your data

## Python Code

Create a train and a test dataset:
```py
msk = np.random.rand(len(df)) < 0.8
train = cdf[msk]
test = cdf[~msk]
```

### Polynomial Regression
```py
from sklearn.preprocessing import PolynomialFeatures
from sklearn import linear_model
train_x = np.asanyarray(train[['ENGINESIZE']])
train_y = np.asanyarray(train[['CO2EMISSIONS']])

test_x = np.asanyarray(test[['ENGINESIZE']])
test_y = np.asanyarray(test[['CO2EMISSIONS']])


poly = PolynomialFeatures(degree=2)
train_x_poly = poly.fit_transform(train_x)
train_x_poly
```

**`fit_transform`** takes our x values, and output a list of our data raised from power of 0 to power of 2 (since we set the degree of our polynomial to 2).

From $y = b + \theta_1  x + \theta_2 x^2$ to $y = b + \theta_1  x_1 + \theta_2 x_2$.

```py
clf = linear_model.LinearRegression()
train_y_ = clf.fit(train_x_poly, train_y)
# The coefficients
print ('Coefficients: ', clf.coef_)
print ('Intercept: ',clf.intercept_)
```

```py
plt.scatter(train.ENGINESIZE, train.CO2EMISSIONS,  color='blue')
XX = np.arange(0.0, 10.0, 0.1)
yy = clf.intercept_[0]+ clf.coef_[0][1]*XX+ clf.coef_[0][2]*np.power(XX, 2)
plt.plot(XX, yy, '-r' )
plt.xlabel("Engine size")
plt.ylabel("Emission")
plt.show()
```

![Image](https://i.imgur.com/e5APnWu.png)

Evaluation:
```py
from sklearn.metrics import r2_score

test_x_poly = poly.fit_transform(test_x)
test_y_ = clf.predict(test_x_poly)

print("Mean absolute error: %.2f" % np.mean(np.absolute(test_y_ - test_y)))
print("Residual sum of squares (MSE): %.2f" % np.mean((test_y_ - test_y) ** 2))
print("R2-score: %.6f" % r2_score(test_y,test_y_ ) )
```

### Non Linear Regression Analysis

Check relation:
```py
plt.figure(figsize=(8,5))
x_data, y_data = (df["Year"].values, df["Value"].values)
plt.plot(x_data, y_data, 'ro')
plt.ylabel('GDP')
plt.xlabel('Year')
plt.show()
```

![Image](https://i.imgur.com/cd7Drnp.png)

Choose a logistic function that fits:

$$ \hat{Y} = \frac1{1+e^{\beta_1(X-\beta_2)}}$$

```py
X = np.arange(-5.0, 5.0, 0.1)
Y = 1.0 / (1.0 + np.exp(-X))

plt.plot(X,Y) 
plt.ylabel('Dependent Variable')
plt.xlabel('Independent Variable')
plt.show()
```

![Image](https://i.imgur.com/RINjplv.png)

#### Building the Model
```py
def sigmoid(x, Beta_1, Beta_2):
     y = 1 / (1 + np.exp(-Beta_1*(x-Beta_2)))
     return y
```

Find the best parameters for our model:
```py
# Lets normalize our data
from scipy.optimize import curve_fit
xdata =x_data/max(x_data)
ydata =y_data/max(y_data)

popt, pcov = curve_fit(sigmoid, xdata, ydata)
#print the final parameters
print(" beta_1 = %f, beta_2 = %f" % (popt[0], popt[1]))

x = np.linspace(1960, 2015, 55)
x = x/max(x)
plt.figure(figsize=(8,5))
y = sigmoid(x, *popt)
plt.plot(xdata, ydata, 'ro', label='data')
plt.plot(x,y, linewidth=3.0, label='fit')
plt.legend(loc='best')
plt.ylabel('GDP')
plt.xlabel('Year')
plt.show()
```

![Image](https://i.imgur.com/lfFZZXi.png)