# From Understanding to Preparation

## Data Understanding

+ What does it mean to "prepare" or "clean" data?

Is the data you collected representative to the problem to be solved.

![Image](https://i.imgur.com/4YQEWIZ.png)




+ The Data Understanding stage encompasses sorting the data. 
+ The Data Understanding stage encompasses all activities related to constructing the dataset.
+ The Data Understanding stage encompasses removing redundant data.

### Case Study
#### Understanding the data

+ Descriptive statistics
    + univariate statistics
    + pairwise correlations
    + histogram
        + categorical variable

#### Looking at data quality
+ data quality
    + missing values
    + invalid or misleading values

#### This is an iterative process
+ iterative data collection and understanding
    + refined definition of "CHF admission" 
    + lead to better solutions to a problem

## Data Preparation - Concepts

+ cleansing data - remove unwanted elements in a data set (up to even 90%, but can reduce to 50% with some automation)

+ transforming data
    + make data easier to work with



+ feature engineering
    + a characteristic that might help when solving the problem
    + important to predictive model

+ working with text analysis
    + know what they are looking for 
    + to ensure that proper groupings are set 
    + the programmers are not over-looking the problems within
    + automate common steps
    + pay attention to this part 


## Data Preparation - Case Study

### Data Preparation
+ define 
    + who, what, where, when, why, how

clinical guidance is needed.

### Defining Readmission
+ 30-day time window is set

### Defining CHF Admission

### Aggregating records
+ Transactional records
    + claims: professional provider, facility, pharmaceutical
    + inpatient & outpatient records: diagnoses, procedures, prescriptions, etc.
    + possibly thousands per patient, depending on clinical history 

+ Aggregate to patient level
    + roll up to 1 record per patient
    + create new columns representing the transaction
        + outpatients visits/inpatient episodes: frequency, recency, diagnoses/length of stay, procedures, prescriptions
        + comorbidities with CHF

### More or less data needed?
Literature review of important factors for CHF admission.


### Completing the data set
+ Merge all data into one table
    + one record per patient
    + list of variables used in modeling
        + target: CHF readmission with 30 days (Y/N), following discharge from CHF hospitalization
        + measures
            + gender, blah
        + diagnosis flags (Y/N)


### Using training sets
+ 2343 patients
+ randomly divided into training and testing sets: 70%/30% split
+ training: 1,640 patients

## Summary
In this lesson, you have learned:

+ The importance of descriptive statistics.
+ How to manage missing, invalid, or misleading data.
+ The need to clean data and sometimes transform it.
+ The consequences of bad data for the model.
+ Data understanding is iterative; you learn more about your data the more you study it. 