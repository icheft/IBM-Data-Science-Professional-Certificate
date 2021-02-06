# Data Wrangling

Also known as data wrangling or **data cleaning**.

It is the *process of converting or mapping data from the initial "raw" form into another format, in order to prepare the data for further analysis*.


## Identify and handle missing values

1. Check with the data collection source
2. Drop the missing values
    + drop the variable
    + drop the data entry
3. Replace the missing values 
    + replace it with an average (of similar datapoints)
    + replace it by frequency 
    + replace it based on other functions
4. Leave it as missing data


### Python
```py
df.dropna() # drop NaN
df.dropna(axis=0) # drop row --> default
df.dropna(axis=1) # drop col

df.dropna(subset=['price'], axis=0, inplace = True)


# replacing values
df.replace(missing_value, new_value)

mean = df['normalized-losses'].mean()
df['normalized-losses'].replace(np.nan, mean)


```

## Data formatting

+ Data are usually collected from different places and stored in different formats
+ Bringing data nto a common standard of expression that allows users to make meaningful comparisons.

```py
df['city-mpg'] = 235/df['city-mpg']

df.rename(columns={'city_mpg': 'city-L/100km'}, inplace=True)

# correct data types
df.dtypes() # to identify data type
df.astypoe()

df.price = df.price.astype('int')
```


## Data Normalization (centering / scaling)
![Image](https://i.imgur.com/GjXYIsW.png)

+ Uniform the features value with different range.
+ Attribute/feature with a larger range will influence the result more.


Approaches:

+ simple feature scaling: $x_{new} = \frac{x_{old}}{x_{max}}$
+ min-max: $x_{new} = \frac{x_{old} - x_{min}}{x_{max} - x_{min}}$
+ Z-score: $x_{new} = \frac{x_{old} - \mu}{\sigma}$ → normally between -3 and +3


```py
# simple feature scaling:

df.length = df.length/df.length.max()

# min-max:

df.length = (df.length - df.length.min()) / (df.length.max() - df.length.min())

# z-score:

df.length = (df.length - df.length.mean()) / df.length.std()

```

## Data Binning

+ Binning: Grouping of values into "bins"
+ Converts numeric into categorical variables
+ Group a set of numerical values into a set of "bins"


### Example
![Image](https://i.imgur.com/dAiY97R.png)
```py
bins = np.linspace(min(df.price), max(df.price), 4) # cut into 3 parts

group_names = ['Low', 'Medium', 'High']

df['price-binned'] = pd.cut(df.price, bins, labels=group_names, include_lowest = True )
```

## Turning Categorical values to numeric variables

→ most statistical models cannot take in the objects/strings as input


Solution (one-hot encoding):

![Image](https://i.imgur.com/2dsljVI.png)

```py
pdf.get_dummies(df.fuel)
```

## Summary
In this lesson, you have learned how to:

**Identify and Handle Missing Values**: Drop rows with incomplete information and impute missing data using the mean values.


**Understand Data Formatting**: Wrangle features in a dataset and make them meaningful for data analysis.


**Apply normalization to a data set**: By understanding the relevance of using feature scaling on your data and how normalization and standardization have varying effects on your data analysis.