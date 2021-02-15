# K-Nearest Neighbors

## Introduction to Classification
+ a supervised learning approach
+ Categorizing some unknown items into a discrete set of categories or "classes"
+ the target attribute is a categorical variable


### Use cases
+ which category a customer belongs to?
+ Whether a customer switches to another provider/brand
+ whether a customer responds to a particular advertising campaign?

### Algorithms

+ Decision trees
+ Naive Bayes
+ Linear Discriminant Analysis
+ *k*-Nearest Neighbor
+ Logistic Regression
+ Neural Networks
+ Support Vector Machines (SVM)

## K-Nearest Neighbors
+ A method for classifying cases based on their similarity to other cases
+ Cases that are near each other are said to be 'neighbors'
+ based on **similar cases with same class labels are near each other**
+ can also be used for regression


![Image](https://i.imgur.com/lfV2CYs.png)


e.g. using the 5 KNNs
![Image](https://i.imgur.com/eTKUgN7.png)

### Algorithms
1. Pick a value for **K**
    1. K = 1: might choose the noise
    2. K = 20: overly generalized
    3. Testing the accuracy of data loss
        ![Image](https://i.imgur.com/lv3QaYg.png)
2. **Calculate** the distance of unknown case from all cases
    1. for 3 variables: ![Image](https://i.imgur.com/yFhHXMi.png)
3. Select the K-observations in the training data that are "nearest" to the unknown data point
4. Predict the response of the unknown data point using the most popular response value from the K-nearest neighbors

## Evaluation Metrics in Classification

+ comparing actual labels $y$ with predicted labels $\hat y$

### Jaccard index
+ $y$: Actual labels
+ $\hat y$: Predicted labels

![Image](https://i.imgur.com/ZZtlTI1.png)

![Image](https://i.imgur.com/4uNVv1P.png)

Higher accuracy = higher Jaccard index

### F1-Score

![Image](https://i.imgur.com/kekhmXR.png)
![Image](https://i.imgur.com/0kXPlDy.png)

+ Precision = TP / (TP + FP)
+ Recall (True positive rate) = TP / (TP + FN)
+ F1-Score = 2 * (Precision * Recall) / (Precision + Recall)

![Image](https://i.imgur.com/bHBxdEp.png)

The classifier with F1-score close to one means more ideal.


### Log Loss

![Image](https://i.imgur.com/lUnfHJ5.png)
Output is a probability value between 0 and 1.

![Image](https://i.imgur.com/i7iaFAv.png)

Lower log loss has better accuracy.

## Python Code
Imported libraries:

```py
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
from sklearn import preprocessing
%matplotlib inline

import pandas as pd
import numpy as np
import mgt2001

from matplotlib import pyplot as plt
import matplotlib.cm as cm
import matplotlib.gridspec as gridspec
from matplotlib.ticker import MaxNLocator
import matplotlib.mlab as mlab
%matplotlib inline

plt.style.use('ggplot') # refined style
```
### Normalize the Data

```py
# Normalize Data first
X = preprocessing.StandardScaler().fit(X).transform(X.astype(float))
X[0:5]
```

### Train Test Split
```py
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split( X, y, test_size=0.2, random_state=4)
print ('Train set:', X_train.shape,  y_train.shape)
print ('Test set:', X_test.shape,  y_test.shape)
```
### Training
```py
from sklearn.neighbors import KNeighborsClassifier
from sklearn import metrics

k = 4
#Train Model and Predict  
neigh = KNeighborsClassifier(n_neighbors = k).fit(X_train,y_train)

yhat = neigh.predict(X_test)

print("Train set Accuracy: ", metrics.accuracy_score(y_train, neigh.predict(X_train)))
print("Test set Accuracy: ", metrics.accuracy_score(y_test, yhat))
```

For every other $k$s:
```py
Ks = 10
mean_acc = np.zeros((Ks-1))
std_acc = np.zeros((Ks-1))

for n in range(1,Ks):
    
    #Train Model and Predict  
    neigh = KNeighborsClassifier(n_neighbors = n).fit(X_train,y_train)
    yhat=neigh.predict(X_test)
    mean_acc[n-1] = metrics.accuracy_score(y_test, yhat)

    
    std_acc[n-1]=np.std(yhat==y_test)/np.sqrt(yhat.shape[0])

mean_acc
```

Including plot:
```py
plt.plot(range(1,Ks),mean_acc,'g')
plt.fill_between(range(1,Ks),mean_acc - 1 * std_acc,mean_acc + 1 * std_acc, alpha=0.10)
plt.fill_between(range(1,Ks),mean_acc - 3 * std_acc,mean_acc + 3 * std_acc, alpha=0.10,color="green")
plt.legend(('Accuracy ', '+/- 1xstd','+/- 3xstd'))
plt.ylabel('Accuracy ')
plt.xlabel('Number of Neighbors (K)')
plt.tight_layout()
plt.show()
```

![Image](https://i.imgur.com/tZR2Q8J.png)