# Logistic Regression

## Intro to Logistic Regression
+ Logistic Regression is a classification algorithm for categorical variables
    + use more than one independent variable
    + binary outcome (in 0 or 1)
    + or multi-class classification
+ Applications
    + Predicting the probability of a person having a heart attack
    + Predicting the mortality in injured patients
    + Predicting a customer's propensity to purchase a product or halt a subscription
    + Predicting the probability of failure of a given process or product
    + Predicting the likelihood of a homeowner defaulting on a mortgage
+ Suitable when:
    + **your data is binary (0/1, YES/NO, True/False)**
    + you need probabilistic results
    + you need a linear decision boundary  
        ![Image](https://i.imgur.com/aIvl3Yg.png)
    + you need to understand the impact of a feature (on dependent variable)

> Logistic regression, by default, is limited to two-class classification problems. Some extensions like one-vs-rest can allow logistic regression to be used for multi-class classification problems, although they require that the classification problem first be transformed into multiple binary classification problems. - <https://machinelearningmastery.com/multinomial-logistic-regression-with-python/>

## Logistic Regression vs. Linear Regression
$$
\hat y = P(y = 1 \vert x)
$$

![Image](https://i.imgur.com/7GhpZbB.png)

![Image](https://i.imgur.com/un5S8tA.png)

### Sigmoid function in logistic regression
+ Logistic function
    ![Image](https://i.imgur.com/CG7vhdb.png)
+ The output is always between 0 and 1

### Output
+ $P(Y=1 \vert X)$
+ $P(Y=0 \vert X) = 1 - P(Y=1 \vert X)$

e.g.  

+ P(Churn = 1 | income, age) = 0.8
+ P(Churn = 0 | income, age) = 1 - 0.8 = 0.2


### Training Process
1. Initialize $\theta$
2. Calculate $\hat y = \sigma(\theta^T X)$ for a customer
3. Compare the output of $\hat y$ with actual output of customer, y, and record it as error
4. Calculate the error for all customers
5. Change the $theta$ to reduce the cost
6. Go back to step 2


## Logistic Regression Training 

$$
\sigma(\theta^T X) \rightarrow P(Y=1 \vert X)
$$

+ Change the weight → Reduce the cost
+ Cost function: ![Image](https://i.imgur.com/CYyimIC.png) 
    ![Image](https://i.imgur.com/Jb5P41x.png)

![Image](https://i.imgur.com/OPhkw6F.png)

+ How to find the best parameters for our model?
    + Minimize the cost function (J)
+ How to minimize the cost function?
    + Use Gradient Descent
+ What is Gradient Descent?
    + iterative approach for defining the minimum of a function
    + a technique to use the derivative of a cost function to change the parameter values, in order to minimize the cost

### Gradient Descent
![Image](https://i.imgur.com/tuATja4.png)

![Image](https://i.imgur.com/F2p34et.png)

![Image](https://i.imgur.com/7ODXIqz.png)

![Image](https://i.imgur.com/FFOO9vt.png)

#### Recap
1. initialize the parameters randomly
2. Feed the cost function with training set, and calculate the error
3. Calculate the gradient of cost function
4. Update weights with new values
5. Go to step 2 until cost is small enough
6. Predict the new customer X


## Python Code

### Normalization
```py

X = np.asarray(churn_df[['tenure', 'age', 'address', 'income', 'ed', 'employ', 'equip']])
X[0:5]

y = np.asarray(churn_df['churn'])
y [0:5]


from sklearn import preprocessing
X = preprocessing.StandardScaler().fit(X).transform(X)
X[0:5]
```

### Train/Test Split
```py
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split( X, y, test_size=0.2, random_state=4)
print ('Train set:', X_train.shape,  y_train.shape)
print ('Test set:', X_test.shape,  y_test.shape)
```

### Modeling (Logistic Regression)
+ `C` parameter indicates **inverse of regularization strength** which must be a positive float. Smaller values specify stronger regularization. 
+ `predict_proba` returns estimates for all classes, ordered by the label of classes.

```py
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import confusion_matrix
LR = LogisticRegression(C=0.01, solver='liblinear').fit(X_train,y_train)
LR

yhat = LR.predict(X_test)
yhat

yhat_prob = LR.predict_proba(X_test)
yhat_prob
```


### Evaluation
#### Jaccard Index
```py
from sklearn.metrics import jaccard_score
jaccard_score(y_test, yhat,pos_label=0)
```



#### Confusion Index
```py
from sklearn.metrics import classification_report, confusion_matrix
import itertools

def plot_confusion_matrix(cm, classes,
                          normalize=False,
                          title='Confusion matrix',
                          cmap=plt.cm.Blues):
    """
    This function prints and plots the confusion matrix.
    Normalization can be applied by setting `normalize=True`.
    """
    if normalize:
        cm = cm.astype('float') / cm.sum(axis=1)[:, np.newaxis]
        print("Normalized confusion matrix")
    else:
        print('Confusion matrix, without normalization')

    print(cm)

    plt.imshow(cm, interpolation='nearest', cmap=cmap)
    plt.title(title)
    plt.colorbar()
    tick_marks = np.arange(len(classes))
    plt.xticks(tick_marks, classes, rotation=45)
    plt.yticks(tick_marks, classes)

    fmt = '.2f' if normalize else 'd'
    thresh = cm.max() / 2.
    for i, j in itertools.product(range(cm.shape[0]), range(cm.shape[1])):
        plt.text(j, i, format(cm[i, j], fmt),
                 horizontalalignment="center",
                 color="white" if cm[i, j] > thresh else "black")

    plt.tight_layout()
    plt.ylabel('True label')
    plt.xlabel('Predicted label')
```

```py
# Compute confusion matrix
cnf_matrix = confusion_matrix(y_test, yhat, labels=[1,0]) # result
# np.set_printoptions(precision=2)


# Plot non-normalized confusion matrix
plt.figure()
plot_confusion_matrix(cnf_matrix, classes=['churn=1','churn=0'],normalize= False,  title='Confusion matrix')

print (classification_report(y_test, yhat))
```

#### Log Loss
```py
from sklearn.metrics import log_loss
log_loss(y_test, yhat_prob)
```

Lower log loss means better accuracy.

Trying different solvers:
```py
# write your code here

from sklearn.linear_model import LogisticRegression
from sklearn.metrics import confusion_matrix

lls = list()
solvers=['newton-cg', 'lbfgs', 'liblinear', 'sag', 'saga']

for solver in solvers:
    LR = LogisticRegression(C=0.01, solver=solver).fit(X_train,y_train)
    yhat = LR.predict(X_test)
    yhat_prob = LR.predict_proba(X_test)
    print(yhat)
    ll = log_loss(y_test, yhat_prob)
    lls.append(ll)
    print(f'{solver}\'s Log Loss: {ll}')
    
print(f"{min(lls)} at {solvers[lls.index(min(lls))]}")
```