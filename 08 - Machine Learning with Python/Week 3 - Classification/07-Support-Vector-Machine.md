# Support Vector Machine (SVM)

SVM is a supervised algorithm that classifies cases by finding a separator.

1. Mapping data to a **high-dimensional** feature space so that data points can be categorized even when the data are not otherwise linearly separable
2. Finding a **separator**

![Image](https://i.imgur.com/8Csg2cI.png)

### Questions to Consider
1. How do we transform data in such a way that separator could be drawn as a hyperplane?
2. How could we find the best or optimized hyperplane separator after transformation?

#### Data Transformation

![Image](https://i.imgur.com/l9af42q.png)

#### Finding the best hyperplane separator
![Image](https://i.imgur.com/gpprUb6.png)

Choose the hyperplane separator with the largest margin.

### Pros and Cons
+ Pros
    + accurate in high-dimensional spaces
    + memory efficient
+ Cons
    + prone to overfitting
    + no probability estimation
    + small datasets

### Application
+ Image recognition
+ text category assignment
+ detecting spam
+ sentiment analysis
+ gene expression classification
+ regression, outlier detection and clustering



## Python Code

### Split
```py
feature_df = cell_df[['Clump', 'UnifSize', 'UnifShape', 'MargAdh', 'SingEpiSize', 'BareNuc', 'BlandChrom', 'NormNucl', 'Mit']]
X = np.asarray(feature_df)

cell_df['Class'] = cell_df['Class'].astype('int')
y = np.asarray(cell_df['Class'])

X_train, X_test, y_train, y_test = train_test_split( X, y, test_size=0.2, random_state=4)
print ('Train set:', X_train.shape,  y_train.shape)
print ('Test set:', X_test.shape,  y_test.shape)
```

### Modeling
Four kernal types:

1. Linear 
2. Polynomial
3. Radial Basis Function (RBF)
4. Sigmoid

```
['linear', 'poly', 'rbf', 'sigmoid', 'precomputed']
```

```py
from sklearn import svm
clf = svm.SVC(kernel='rbf')
clf.fit(X_train, y_train) 

yhat = clf.predict(X_test)
```

### Evaluation
```py
from sklearn.metrics import classification_report, confusion_matrix
import itertools
```

```py
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

#### Confusion Matrix
```py
# Compute confusion matrix
cnf_matrix = confusion_matrix(y_test, yhat, labels=[2,4])
np.set_printoptions(precision=2)

print (classification_report(y_test, yhat))

# Plot non-normalized confusion matrix
plt.figure()
plot_confusion_matrix(cnf_matrix, classes=['Benign(2)','Malignant(4)'],normalize= False,  title='Confusion matrix')
```
```

              precision    recall  f1-score   support

           2       1.00      0.94      0.97        90
           4       0.90      1.00      0.95        47

    accuracy                           0.96       137
   macro avg       0.95      0.97      0.96       137
weighted avg       0.97      0.96      0.96       137
```

![Image](https://i.imgur.com/8x1O1i3.png)

#### F1-Score
```py
from sklearn.metrics import f1_score
f1_score(y_test, yhat, average='weighted') 
```

#### Jaccard
```py
from sklearn.metrics import jaccard_score
jaccard_score(y_test, yhat,pos_label=2)
```