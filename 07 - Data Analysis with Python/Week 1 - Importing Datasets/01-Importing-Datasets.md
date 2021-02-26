# Importing Datasets

### Libraries in Python
1. Scientific Computing
    + Pandas
    + NumPy
    + SciPy
2. Visualization
    + Matplotlib
    + Seaborn
3. Algorithms
    + Scikit-learn: machine learning, regression, classification
    + statsmodels: exploring data, estimating statistical models, and performing statistical tests

## Getting Started Analyzing Data in Python

+ `df.dtypes`
+ `df.describe()`
+ `df.describe(include='all')`: full summary statistics
+ `df.info()`: provides a concise summary of your DataFrame - top 30 rows and bottom 30 rows 

```
 #   Column             Non-Null Count  Dtype  
---  ------             --------------  -----  
 0   symboling          201 non-null    int64  
 1   normalized-losses  164 non-null    object 
 2   make               201 non-null    object 
 3   fuel-type          201 non-null    object 
 4   aspiration         201 non-null    object 
 5   num-of-doors       199 non-null    object 
 6   body-style         201 non-null    object 
 7   drive-wheels       201 non-null    object 
 8   engine-location    201 non-null    object 
 9   wheel-base         201 non-null    float64
 10  length             201 non-null    float64
 11  width              201 non-null    float64
 12  height             201 non-null    float64
 13  curb-weight        201 non-null    int64  
 14  engine-type        201 non-null    object 
 15  num-of-cylinders   201 non-null    object 
 16  engine-size        201 non-null    int64  
 17  fuel-system        201 non-null    object 
 18  bore               197 non-null    object 
 19  stroke             197 non-null    object 
 20  compression-ratio  201 non-null    float64
 21  horsepower         199 non-null    object 
 22  peak-rpm           199 non-null    object 
 23  city-mpg           201 non-null    int64  
 24  highway-mpg        201 non-null    int64  
 25  price              201 non-null    object
---
```

## Accessing Databases with Python

![Image](https://i.imgur.com/tMrXBxw.png)

![Image](https://i.imgur.com/ruU2Kpq.png)


```py
from dbmodule import connect

# create connection object
connection = connect('databasename', 'username', 'pswd')

# create a cursor object
cursor = connection.cursor()

# run queries
cursor.execute('select * from mytable')
results = cursor.fetchall()

# free resources
cursor.close()
connection.close()
```


## Summary

In this lesson, you have learned how to:

**Define the Business Problem**: Look at the data and make some high-level decision on what kind of analysis should be done

**Import and Export Data in Python**: How to import data from multiple data sources using the Pandas library and how to export files into different formats.

**Analyze Data in Python**: How to do some introductory analysis in Python using functions like `dataframe.head()` to view the first few lines of the dataset, `dataframe.info()` to view the column names and data types.