# Decision Trees

## Introduction to Decision Trees

Example:
![Image](https://i.imgur.com/BGpi93n.png)

1. Choose an attribute from your dataset
2. Calculate the significance of attribute in splitting of data
3. Split data based on the value of the best attribute
4. Go to step 1

## Building Decision Trees

Choose the attribute that has:

+ More predictiveness
+ less impurity
+ lower *entropy*
    + measure of randomness or uncertainty
    + the lower the entropy, the less uniform the distribution, the purer the node
    + ![Image](https://i.imgur.com/RaTUurm.png)
    + the model/package will calculate it for us


After trying out every attribute in the dataset, how do we determine which attribute is the best?

![Image](https://i.imgur.com/38jDdcm.png)

Answer: **The tree with the *higher* *information gain* after splitting.**

> Information gain: the information that can increase the level of certainty after splitting
> $\text{Information Gain} = \text{(Entropy before split)} - \text{(weighted entropy after split)}$



## Python Code

```py
from sklearn.tree import DecisionTreeClassifier
```

Sklearn Decision Trees do not handle categorical variables. 
```py
from sklearn import preprocessing
le_sex = preprocessing.LabelEncoder()
le_sex.fit(['F','M'])
X[:,1] = le_sex.transform(X[:,1]) 


le_BP = preprocessing.LabelEncoder()
le_BP.fit([ 'LOW', 'NORMAL', 'HIGH'])
X[:,2] = le_BP.transform(X[:,2])


le_Chol = preprocessing.LabelEncoder()
le_Chol.fit([ 'NORMAL', 'HIGH'])
X[:,3] = le_Chol.transform(X[:,3]) 

X[0:5]
```

Setting up the Decision Tree:
```py
from sklearn.model_selection import train_test_split
X_trainset, X_testset, y_trainset, y_testset = train_test_split(X, y, test_size=0.3, random_state=3)
```

### Modeling
```py
drugTree = DecisionTreeClassifier(criterion="entropy", max_depth = 4)
# drugTree # it shows the default parameters

drugTree.fit(X_trainset,y_trainset)
```

### Making Prediction
```py
predTree = drugTree.predict(X_testset)

print (predTree [0:5])
print (y_testset [0:5])
```

### Evaluation
```py
from sklearn import metrics
import matplotlib.pyplot as plt
print("DecisionTrees's Accuracy: ", metrics.accuracy_score(y_testset, predTree))
```

### Visualization

```py
from  io import StringIO
import pydotplus
import matplotlib.image as mpimg
from sklearn import tree
%matplotlib inline 
```
```py
dot_data = StringIO()
filename = "drugtree.png"
featureNames = my_data.columns[0:5]
targetNames = my_data["Drug"].unique().tolist()
out=tree.export_graphviz(drugTree,feature_names=featureNames, out_file=dot_data, class_names= np.unique(y_trainset), filled=True,  special_characters=True,rotate=False)  
graph = pydotplus.graph_from_dot_data(dot_data.getvalue())  
graph.write_png(filename)
img = mpimg.imread(filename)
plt.figure(figsize=(100, 200))
plt.imshow(img,interpolation='nearest')
plt.show()
```

![Image](https://i.imgur.com/xGkHD9A.png)