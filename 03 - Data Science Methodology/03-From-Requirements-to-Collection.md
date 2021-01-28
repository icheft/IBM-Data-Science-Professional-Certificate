# From Requirements to Collection

## Data Requirements
--> Cooking w/ data. Each step is critical for cooking a meal.

Identify  
+ which ingredients are required
+ how to source or how to collect them
+ how to understand or work with them
+ how to prepare the data to meet the desired outcome

![Image](https://i.imgur.com/sEnnuQh.png)
![Image](https://i.imgur.com/mT1OcPx.png)

### Case Study - Selecting the cohort
+ define and select cohort
    + in-patient within health insurance provider's service area
    + primary diagnosis of CHF in one year 
    + continuous enrollment for at least 6 months prior to primary CHF admission
    + disqualifying conditions
+ Content, formats, representations suitable for decision tree classifier
    + one record per patient with columns representing variables (dependent variable and predictors)
    + content covering all aspects of each patient's clinical history 
        + transactional format
        + transformations required


## Data Collection
--> ingredients. Assessment by the data scientist to determine whether or not they have what they need. 

+ revised and decisions are made 

+ descriptive statistics and visualization can be applied to the data set

![Image](https://i.imgur.com/4HBAzK4.png)


### Case Study 
#### Gather available data
+ available data sources
    + corporate data warehouse (single source of medical & claims, eligibility, provider, and member information)
    + in-patient record system
    + claim payment system
    + disease management program information
+ data wanted but not available
    > it is alright to defer decisions about unavailable data, and attempt to acquire it at a later stage.
    + pharmaceutical records
    + decided to defer 


#### Merging data

## Summary
In this lesson, you have learned:

+ The significance of defining the data requirements for your model.
+ Why the content, format, and representation of your data matter.   
+ The importance of identifying the correct sources of data for your project.
+ How to handle unavailable and redundant data.
+ To anticipate the needs of future stages in the process.




