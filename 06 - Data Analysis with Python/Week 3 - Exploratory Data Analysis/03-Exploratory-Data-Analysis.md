# Exploratory Data Analysis

+ Preliminary step in data analysis to:
    + Summarize main characteristics of the data
    + Gain better understanding of the data set
    + Uncover relationships between variables
    + Extract important variables
+ Question: 
    + *"What are the characteristics which have the most impact on the car price?"*

## Descriptive Statistics

+ describe basic features of data
+ giving short summaries about the sample and measures of the data

### describe
```py
df.describe() # provide basic statistics
```

+ NaN value will be skipped 


### value_counts
```py
value_counts() # summarize the categorical data 

drive_wheels_counts = df['drive-wheels'].value_counts().to_frame()

drive_wheels_counts.rename(columns = {'drive-wheels': 'value_counts'}, inplace = True)
```

### box plots
![Image](https://i.imgur.com/YU0a1Wv.png)

```py
sns.boxplot(x = 'drive-wheels', y = 'price', data=df)
```


### scatter plot

+ each observation represented as a point
+ scatter plot show the relationship between two variables
    1. **predictor/independent** variables on **x-axis**
    2. **target/dependent** variables on **y-axis**

```py
y = df.price
x = df['engine-size']
plt.scatter(x, y)

plt.title('Scatter plot of Engine Size vs. Price')
plt.xlabel('Engine Size')
plt.ylabel('Price')

plt.show()
```


## GroupBy in Python
### groupby
+ can be applied to categorical variables
+ group data into categories
+ single or multiple variables

```py
df_test = df[['drive-wheels', 'body-style', 'price']]
df_grp = df_test.groupby(['drive-wheels', 'body-style'], as_index=False).mean()
df_grp
```

### pivot
+ One variable displayed along the columns and the other variable displayed along the rows

```py
df_pivot = df_grp.pivot(index='drive-wheels', columns='body-style')
```

![Image](https://i.imgur.com/ozYDMij.png)

### Heatmap
+ Plot target variable over multiple variables

```py
plt.pcolor(df_pivot, cmap='RdBu')
plt.colorbar()
plt.show()
```

![Image](https://i.imgur.com/Ylq7F4H.png)



## Correlation
+ Measures to what extent different variables are interdependent
+ examples: 
    + lung cancer -> smoking
    + rain -> umbrella
+ doesn't imply causation

```py
sns.regplot(x = 'engine-size', y = 'price', data=df)
plt.ylim(0, )
```

+ Pearson correlation
    + correlation coefficient
        + close to 1: large positive relationship
        + close to -1: large negative relationship
        + close to 0: no relationship
    + p-value
        + p-value < 0.001 strong certainty in the result
        + p-value < 0.05 moderate certainty in the result
        + p-value < 0.1 weak certainty in the result
        + p-value > 0.1 no certainty in the result

```py
pearson_coef, p_value = stats.pearsonr(df['horsepower'], df['price'])
# pearson corr: 0.81, p-value: 0
```

### correlation heatmap
![Image](https://i.imgur.com/vrET9ir.png)

![Image](https://i.imgur.com/ShAzrWv.png)
They all have the same correlation coefficient.

## Association between two categorical variables: Chi-Square


+ the test is intended to test how likely it is that an observed distribution is due to chance
+ The Chi-square tests a null hypothesis that the variables are independent
    + the test compares the observed data to the values that the model expects if the data was distributed in different categories by chance
    + if the observed data doesn't fit within the model of the expected values, the probability that the variables are dependent becomes stronger
+ the chi-square does not tell you the type of relationship that exists between both variables 
    + it tells that a relationship exists 

![Image](https://i.imgur.com/bsUuXIN.png) 

```py
scipy.stats.chi2_contingency(cont_table, correction=True)
```


## Summary

In this lesson, you have learned how to:

**Describe Exploratory Data Analysis**: By summarizing the main characteristics of the data and extracting valuable insights.

**Compute basic descriptive statistics**: Calculate the mean, median, and mode using python and use it as a basis in understanding the distribution of the data.

**Create data groups**: How and why you put continuous data in groups and how to visualize them.

**Define correlation as the linear association between two numerical variables**: Use Pearson correlation as a measure of the correlation between two continuous variables

**Define the association between two categorical variables**: Understand how to find the association of two variables using the Chi-square test for association and how to interpret them.