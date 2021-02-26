# k-Means Clustering

## Intro to Clustering

Clustering for segmentation.

![Image](https://i.imgur.com/O9isxvr.png)

Outcome:

![Image](https://i.imgur.com/g6tNSYB.png)

**Defn**: A cluster is a group of objects that are **similar to other objects** in the cluster, and **dissimilar to data points** in other clusters.


### Difference between Clustering and Classification

![Image](https://i.imgur.com/rwNRRe1.png)

### Application
+ Retail/marketing
    + Identifying buying patterns of customers
    + Recommending new books or movies to new customers
+ Banking
    + Fraud detection in credit card use
    + Identifying clusters of customers (e.g. loyal)
+ Insurance
    + Fraud detection in claims analysis
    + Insurance risk of customers
+ Publication
    + auto-categorizing news based on their content
    + recommending similar news articles
+ Medicine
    + characterizing patient behavior
+ Biology
        + clustering genetic markers to identify family ties


### Why clustering?

+ Exploratory data analysis
+ Summary generation
+ outlier detection
+ finding duplicates
+ pre-processing step

### Clustering Algorithms
+ Partition-based Clustering
    + Relatively efficient
    + e.g. k-Means, k-Median, Fuzzy c-Means
    + ![Image](https://i.imgur.com/P89rtkD.png)
+ Hierarchical Clustering
    + Produces trees of clusters (For small dataset)
    + e.g. Agglomerative, Divisive 
    + ![Image](https://i.imgur.com/Qxdgmvl.png)
+ Density-based Clustering
    + Produces arbitrary shaped clusters
    + e.g. DBSCAN 
    + ![Image](https://i.imgur.com/OOaxMZ4.png)

## Intro to k-Means
(Partitioning/Hierarchical/Density-based Clustering)

+ Partitioning clustering
+ k-Means divides the data into **non-overlapping** subsets (clusters) without any cluster-internal structure
+ Unsupervised algorithm
+ Examples within a cluster are very similar
+ examples across different clusters are very different
+ **Objective**: To minimize the “intra cluster” distances and maximize the “inter-cluster” distances. 

![Image](https://i.imgur.com/tfG6DCY.png)

### Steps
1. Initialize k (random/designated centroids)
2. **Distance** calculation
3. Assign each point to the closet centroid
4. Compute the new centroids for each cluster 
5. Repeat until there are no more changes

 

Error: ![Image](https://i.imgur.com/HICES7C.png)

## More on k-Means
### Accuracy
+ External approach
    + compare the clusters with the ground truth, if it is available
+ Internal approach
    + average the distance between data points within a cluster

### Choosing k
![Image](https://i.imgur.com/l6F5tNi.png)

Run through a series of $k$ values. Find the elbow point (aka the elbow method).

## Python Code
Imported libraries:
```py
import random 
import numpy as np 
import matplotlib.pyplot as plt 
from sklearn.cluster import KMeans 
from sklearn.datasets import make_blobs
# depracated: samples_generator
%matplotlib inline
plt.style.use('ggplot') # refined style
```

Randomly generate dataset:
```py
from sklearn.datasets import make_blobs

X, y = make_blobs(n_samples=5000, centers=[[4,4], [-2, -1], [2, -3], [1, 1]], cluster_std=0.9) # for four clusters with 5000 samples

plt.scatter(X[:, 0], X[:, 1], marker='.')
plt.show()
```

K-Means:

```py
k_means = KMeans(init = "k-means++", n_clusters = 4, n_init = 12)

k_means.fit(X)
k_means_labels = k_means.labels_
k_means_cluster_centers = k_means.cluster_centers_
```

### Plot
(Dope)

```py
# Initialize the plot with the specified dimensions.
fig = plt.figure(figsize=(6, 4))

# Colors uses a color map, which will produce an array of colors based on
# the number of labels there are. We use set(k_means_labels) to get the
# unique labels.
colors = plt.cm.Spectral(np.linspace(0, 1, len(set(k_means_labels))))

# Create a plot
ax = fig.add_subplot(1, 1, 1)

# For loop that plots the data points and centroids.
# k will range from 0-3, which will match the possible clusters that each
# data point is in.
for k, col in zip(range(len([[4,4], [-2, -1], [2, -3], [1, 1]])), colors):

    # Create a list of all data points, where the data poitns that are 
    # in the cluster (ex. cluster 0) are labeled as true, else they are
    # labeled as false.
    my_members = (k_means_labels == k)
    
    # Define the centroid, or cluster center.
    cluster_center = k_means_cluster_centers[k]
    
    # Plots the datapoints with color col.
    ax.plot(X[my_members, 0], X[my_members, 1], 'w', markerfacecolor=col, marker='.')
    
    # Plots the centroids with specified color, but with a darker outline
    ax.plot(cluster_center[0], cluster_center[1], 'o', markerfacecolor=col,  markeredgecolor='k', markersize=6)

# Title of the plot
ax.set_title('KMeans')

# Remove x-axis ticks
ax.set_xticks(())

# Remove y-axis ticks
ax.set_yticks(())

# Show the plot
plt.show()
```

![Image](https://i.imgur.com/6xZ6PTJ.png)

### Application: Customer Segmentation

```py
import pandas as pd
cust_df = pd.read_csv("data/Cust_Segmentation.csv")
cust_df.head()
```

#### Pre-processing
```py
df = cust_df.drop('Address', axis=1)
df.head()

# Normalizing
from sklearn.preprocessing import StandardScaler
X = df.values[:,1:]
X = np.nan_to_num(X)
Clus_dataSet = StandardScaler().fit_transform(X)
Clus_dataSet
```

#### Modeling
```py
clusterNum = 3
k_means = KMeans(init = "k-means++", n_clusters = clusterNum, n_init = 12)
k_means.fit(X)
labels = k_means.labels_
print(labels)
```

#### Insights
```py
df["Clus_km"] = labels
# df.head(5)
df.groupby('Clus_km').mean()
```

Based on age and income:
```py
area = np.pi * ( X[:, 1])**2  
plt.scatter(X[:, 0], X[:, 3], s=area, c=labels.astype(np.float), alpha=0.5)
plt.xlabel('Age', fontsize=18)
plt.ylabel('Income', fontsize=16)

plt.show()
```
![Image](https://i.imgur.com/cGXBob6.png)
```py
from mpl_toolkits.mplot3d import Axes3D 
fig = plt.figure(1, figsize=(8, 6))
plt.clf()
ax = Axes3D(fig, rect=[0, 0, .95, 1], elev=48, azim=134)

plt.cla()
# plt.ylabel('Age', fontsize=18)
# plt.xlabel('Income', fontsize=16)
# plt.zlabel('Education', fontsize=16)
ax.set_xlabel('Education')
ax.set_ylabel('Age')
ax.set_zlabel('Income')

ax.scatter(X[:, 1], X[:, 0], X[:, 3], c= labels.astype(np.float))
plt.show()
```
![Image](https://i.imgur.com/WujKlKw.png)


- AFFLUENT, EDUCATED AND OLD AGED
- MIDDLE AGED AND MIDDLE INCOME
- YOUNG AND LOW INCOME



