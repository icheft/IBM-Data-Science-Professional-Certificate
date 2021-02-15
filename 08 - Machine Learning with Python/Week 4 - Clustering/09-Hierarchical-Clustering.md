# Hierarchical Clustering

## Intro to Hierarchical Clustering
![Image](https://i.imgur.com/PU1eAYi.png)

Hierarchical clustering algorithms build a hierarchy of clusters where *each node is a cluster* consists of the clusters of its daughter nodes.


![Image](https://i.imgur.com/wCeYkzP.png)
+ Divisive
    + top-down
    + dividing the cluster
+ Agglomerative
    + pair to similar clusters together
    + more popular

### Agglomerative Clustering

Similar to Hoffman Encoding.

Dendrogram:

![Image](https://i.imgur.com/TflwTdY.png)

Sometimes need to be cut to form clusters.

## More on Hierarchical Clustering
### Algorithm
1. Create $n$ clusters, one for each data point
2. Compute the Proximity Matrix
3. `Repeat`
    1. Merge the two closest clusters
    2. Update the proximity matrix (with the mean value)
4. `Until` only a single cluster remains (specified number of clusters)

### Qs
1. How do we measure the distance between clusters?
2. How to find the nearest among clusters?
3. Which point do we use?

#### Distance between clusters
+ Single-Linkage Clustering
    + Minimum distance between clusters
+ Complete-Linkage Clustering
    + Maximum distance between clusters
+ Average Linkage Clustering
    + Average distance between clusters
+ Centroid Linkage Clustering
    + Distance between cluster centroids

### Pros and Cons
![Image](https://i.imgur.com/zvzzdyJ.png)

### Hierarchical Clustering vs. K-Means
![Image](https://i.imgur.com/VPCFzxm.png)


## Python Code
Imported Packages:

```py
import numpy as np 
import pandas as pd
from scipy import ndimage 
from scipy.cluster import hierarchy 
from scipy.spatial import distance_matrix 
from matplotlib import pyplot as plt 
from sklearn import manifold, datasets 
from sklearn.cluster import AgglomerativeClustering 
from sklearn.datasets import make_blobs 
%matplotlib inline

plt.style.use('ggplot') # refined style
```

Random Data:
```py
X1, y1 = make_blobs(n_samples=50, centers=[[4,4], [-2, -1], [1, 1], [10,4]], cluster_std=0.9)

plt.scatter(X1[:, 0], X1[:, 1], marker='o') 
plt.show()
```

### Agglomerative Clustering
```py
agglom = AgglomerativeClustering(n_clusters = 4, linkage = 'average')

agglom.fit(X1,y1)
```
+ `linkage : {'ward', 'complete', 'average', 'single'}, default='ward'`


Plot
```py
# Create a figure of size 6 inches by 4 inches.
plt.figure(figsize=(6,4))

# These two lines of code are used to scale the data points down,
# Or else the data points will be scattered very far apart.

# Create a minimum and maximum range of X1.
x_min, x_max = np.min(X1, axis=0), np.max(X1, axis=0)

# Get the average distance for X1.
X1 = (X1 - x_min) / (x_max - x_min)

# This loop displays all of the datapoints.
for i in range(X1.shape[0]):
    # Replace the data points with their respective cluster value 
    # (ex. 0) and is color coded with a colormap (plt.cm.spectral)
    plt.text(X1[i, 0], X1[i, 1], str(y1[i]),
             color=plt.cm.nipy_spectral(agglom.labels_[i] / 10.),
             fontdict={'weight': 'bold', 'size': 9})
    
# Remove the x ticks, y ticks, x and y axis
plt.xticks([])
plt.yticks([])
#plt.axis('off')



# Display the plot of the original data before clustering
plt.scatter(X1[:, 0], X1[:, 1], marker='.')
# Display the plot
plt.show()
```
![Image](https://i.imgur.com/q9nmxQP.png)

#### Dendrogram
```py
dist_matrix = distance_matrix(X1,X1) 
print(dist_matrix)
Z = hierarchy.linkage(dist_matrix, 'average')
dendro = hierarchy.dendrogram(Z)
```
![Image](https://i.imgur.com/4mGnwJM.png)

### Real Dataset

#### Data Cleaning
```py
print ("Shape of dataset before cleaning: ", pdf.size)
pdf[[ 'sales', 'resale', 'type', 'price', 'engine_s',
       'horsepow', 'wheelbas', 'width', 'length', 'curb_wgt', 'fuel_cap',
       'mpg', 'lnsales']] = pdf[['sales', 'resale', 'type', 'price', 'engine_s',
       'horsepow', 'wheelbas', 'width', 'length', 'curb_wgt', 'fuel_cap',
       'mpg', 'lnsales']].apply(pd.to_numeric, errors='coerce')
pdf = pdf.dropna()
pdf = pdf.reset_index(drop=True)
print ("Shape of dataset after cleaning: ", pdf.size)
pdf.head(5)


featureset = pdf[['engine_s',  'horsepow', 'wheelbas', 'width', 'length', 'curb_wgt', 'fuel_cap', 'mpg']]

# Normalize
from sklearn.preprocessing import MinMaxScaler
x = featureset.values #returns a numpy array
min_max_scaler = MinMaxScaler()
feature_mtx = min_max_scaler.fit_transform(x)
```

#### Clustering using Scipy
```py
import scipy
leng = feature_mtx.shape[0]
D = np.zeros([leng,leng])
for i in range(leng):
    for j in range(leng):
        D[i,j] = scipy.spatial.distance.euclidean(feature_mtx[i], feature_mtx[j])


import pylab
import scipy.cluster.hierarchy
Z = hierarchy.linkage(D, 'complete')
"""
- single
- complete
- average
- weighted
- centroid
"""
from scipy.cluster.hierarchy import fcluster
max_d = 3
clusters = fcluster(Z, max_d, criterion='distance')
clusters

fig = pylab.figure(figsize=(18,50))
def llf(id):
    return '[%s %s %s]' % (pdf['manufact'][id], pdf['model'][id], int(float(pdf['type'][id])) )
    
dendro = hierarchy.dendrogram(Z,  leaf_label_func=llf, leaf_rotation=0, leaf_font_size =12, orientation = 'right')
```
![Image](https://i.imgur.com/7vi2nw6.png)

#### Clustering using scikit-learn
```py
from sklearn.metrics.pairwise import euclidean_distances
dist_matrix = euclidean_distances(feature_mtx,feature_mtx) 
print(dist_matrix)

Z_using_dist_matrix = hierarchy.linkage(dist_matrix, 'complete')

fig = pylab.figure(figsize=(18,50))
def llf(id):
    return '[%s %s %s]' % (pdf['manufact'][id], pdf['model'][id], int(float(pdf['type'][id])) )
    
dendro = hierarchy.dendrogram(Z_using_dist_matrix,  leaf_label_func=llf, leaf_rotation=0, leaf_font_size =12, orientation = 'right')
```

```py
agglom = AgglomerativeClustering(n_clusters = 6, linkage = 'complete')
agglom.fit(dist_matrix)

pdf['cluster_'] = agglom.labels_
pdf.head()
```

Plot:
```py
import matplotlib.cm as cm
n_clusters = max(agglom.labels_)+1
colors = cm.rainbow(np.linspace(0, 1, n_clusters))
cluster_labels = list(range(0, n_clusters))

# Create a figure of size 6 inches by 4 inches.
plt.figure(figsize=(16,14))

for color, label in zip(colors, cluster_labels):
    subset = pdf[pdf.cluster_ == label]
    for i in subset.index:
            plt.text(subset.horsepow[i], subset.mpg[i],str(subset['model'][i]), rotation=25) 
    plt.scatter(subset.horsepow, subset.mpg, s= subset.price*10, c=color, label='cluster'+str(label),alpha=0.5)
#    plt.scatter(subset.horsepow, subset.mpg)
plt.legend()
plt.title('Clusters')
plt.xlabel('horsepow')
plt.ylabel('mpg')
```


```py
agg_cars = pdf.groupby(['cluster_','type'])['horsepow','engine_s','mpg','price'].mean()
agg_cars
```
![Image](https://i.imgur.com/bJTq91o.png)

```py
plt.figure(figsize=(16,10))
for color, label in zip(colors, cluster_labels):
    subset = agg_cars.loc[(label,),]
    for i in subset.index:
        plt.text(subset.loc[i][0]+5, subset.loc[i][2], 'type='+str(int(i)) + ', price='+str(int(subset.loc[i][3]))+'k')
    plt.scatter(subset.horsepow, subset.mpg, s=subset.price*20, c=color, label='cluster'+str(label))
plt.legend()
plt.title('Clusters')
plt.xlabel('horsepow')
plt.ylabel('mpg')
plt.show()
```
![Image](https://i.imgur.com/q356rzs.png)