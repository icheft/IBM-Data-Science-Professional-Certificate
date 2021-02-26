# What is Machine Learning?

Skills to possess:

+ Regression
+ Classification
+ Clustering
+ Scikit Learn
+ Scipy


Projects:

+ Cancer Detection
+ Predicting Economic Trends 
+ Predicting customer churn
+ Recommendation engines

*NOTE*: This can be done with [the template](https://github.com/plotly/dash-sample-apps/tree/master/apps/dash-financial-report).

## Introduction to Machine Learning

> **Machine Learning** is the subfield of computer science that gives "***computers the ability to learn without being explicitly programmed.***"  
> Arthur Samuel

From ...
![Image](https://i.imgur.com/tGMj2hf.png)
to ...
![Image](https://i.imgur.com/p0mDPr2.png)


### Examples
+ Recommendation system
+ Loan application 
+ segmentation of customers
+ chatbox
+ computer games

### Techniques
+ Regression/Estimation
    + Predicting continuous values
+ Classification 
    + Predicting the item class/category of a case
+ Clustering
    + finding the structure of data; summarization
+ Associations
    + associating frequent *co-occurring* items/events.
+ Anomaly detection
    + Discovering abnormal and unusual cases
+ Sequence mining
    + Predicting next events; click-stream (Markov Model, HMM)
+ Dimension Reduction
    + Reducing the size of data (PCA)
+ Recommendation system
    + recommending items

### Difference between AI, ML, and DL
+ AI components:
    + computer vision
    + Language processing
    + creativity
    + Etc.
+ Machine Learning: statistical side of AI
    + Classification
    + clustering 
    + neural network
    + etc.
+ Deep Learning: Deeper level, learning on its own

## Python for Machine Learning

+ NumPy
+ SciPy
+ matplotlib
+ pandas
+ scikit-learn
    + free software machine learning library
    + classification, regression, and clustering algorithms
    + works with NumPy and SciPy
    + Great doc.
    + Easy to implement

![Image](https://i.imgur.com/VUYktK2.png)


```py
from sklearn import preprocessing 
X = preprocessing.StandardScaler().fit(X).transform(X)

from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33)

from sklearn import svm
clf = svm.SVC(gamma=.001, C=100.)
clf.fit(X_train, y_train)
clf.predict(X_test)

from sklearn.metrics import confusion_matrix
print(confusion_matrix(y_test, yhat, labels=[1, 0]))

import pickle
s = pickle.dumps(clf) # save model
```


## Supervised vs Unsupervised
### Supervised

+ supervising a machine learning model
    + by teaching the model
+ teaching the model with labeled data

![Image](https://i.imgur.com/TiTuOYC.png)
+ attributes (all columns.values)
+ feature (each column with data)
+ observation (row)

Types

+ classification
+ regression

### Unsupervised
+ let the model work on its own to discover information
+ trains on dataset

![Image](https://i.imgur.com/s0Ck1l4.png)

Training on the **unlabeled** data.

Techniques:

+ Dimension reduction
    + reducing redundant feature to make classification easier
+ Density estimation
    + used to explore the data to find some structure within it
+ Market basket analysis
    + if one buys a certain group of items, he/she is going to be more likely to buy another group of items.
+ Clustering 
    + the most popular unsupervised machine learning technique
    + grouping of data points or objects that are somehow similar by:
        + discovering structure
        + summarization
        + anomaly detection

![Image](https://i.imgur.com/RXHGgJM.png)