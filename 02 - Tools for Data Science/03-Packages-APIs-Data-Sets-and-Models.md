# Packages, APIs, Data Sets, and Models

## Libraries for Data Science
+ Python Libraries
    1. Scientific computing Libraries in Python
        
        Libraries can sometimes be called "frameworks".
        + Pandas: Dataframe
            + built on Numpy
        + NumPy: Arrays & matrices
    2. Visualization Libraries in Python
        + Matplotlib: plots & graphs, most popular
        + Seaborn
            + based on Matplotlib
            + heat maps, time series, violin plots
    3. High Level- Machine Learning and Deep Learning (meaning that you don't have to worry about the details, which also means that it is hard to improve)
        + Scikit-learn: for ML: regression, classification
        + Keras: Deep Learning Neural Networks 
        + TensorFlow: Deep Learning: Production and Deployment
        + PyTorch: Deep Learning: used for experimentation
    4. Deep Learning Libraries in Python
+ Libraries Used in other languages
    + Apache Spark: process data in parallel
        + pandas
        + numpy
        + scikit-learn
    + Scala
        + Vegas
        + Big DL: for deep learning
    + R
        R has been the de-facto standard for open source data science but it is now being superseded by Python.
        
        + Ggplot2
        + Keras, TensorFlow

## Application Programming Interfaces (API)
### What is an API
lets two pieces of software talk to each other. 

![Image](https://i.imgur.com/Re4XQE9.png)



### API Libraries
+ TensorFlow
### REST API
+ REST API
    + enabling you to communicate using the Internet, taking advantage of storage, greater data access, AI algorithms, and many other resources.
    + RE = Representational
    + S = State
    + T = Transfer
    + your program = client

![Image](https://i.imgur.com/jPeJvn8.png)

## Data Sets - Powering Data Science
Data set:

+ Collection of data
+ Data structures
    + tabular data: CSV
    + Hierarchical data, network data
    + Raw files

Data Ownership:

+ Private data
    + confidential
    + private or personal information
    + commercially sensitive
+ Open Data
    + Scientific institutions
    + Governments
    + Organizations
    + companies
    + Publicly available

### Open Data Sources
+ https://datacatalogs.org
+ kaggle.com/datasets
+ datasetsearch.research.google.com
+ Governmental, intergovernmental, organization websites
    + https://data.un.org
    + https://www.data..gov/
    + https://www.europeandataportal.eu/en/

**Community Data License Agreement**  
+ CDLA-Sharing: Permission to use modify data; publication only under same terms
+ CDLA-Permissive: Permission to use and modify data; no obligations

## Sharing Enterprise Data - Data Asset eXchange (DAX)
Provides a trusted source for finding open data sets that are ready for use in enterprise applications.

DAX also provides tutorials in the form of notebooks that walk through the basics of data cleaning, pre-processing, and exploratory analysis.

## Machine Learning Models
+ Model
    + Data can contain a wealth of information
    + ML uses algorithms (models) to identify patterns in data (model training)
    + A model must be trained on data before it can be used to make predictions
        + learn from past data
    + types
        + supervised
        + unsupervised
        + reinforcements

+ Supervised
    + data is labeled and model trained to make correct predictions
    + regression 
        + predict real numerical values
        + home sales prices, stock market prices
    + and classification problems
        + classify things into categories
        + email spam filters, fraud detection, image classification
+ Unsupervised
    + Data is not labeled
    + model tries to identify patterns without external help
    + clustering
        + purchase recommendation
    + Anomaly detection
        + identifies outliers in a data set, such as fraudulent credit card transactions or suspicious online log-in attempts
+ Reinforcements
    + conceptually similar to human learning processes
    + learn from rewards (successful outcomes)
    + GO, Chess, 


+ Deep Learning
    + Emulate how the human brain works
    + Applications
        + NLP
        + Image, audio, and video analysis
        + Time series forecasting
        + etc
    + requires typically very large datasets of labeled data and is compute intensive
    + Models
        + build from scratch or download from public model repositories
        + Built using frameworks
        + popular model repositories
            + most frameworks provides a "model zoo"s
            + ONNX model zoo

![cf](https://assets.website-files.com/5e6b6ac0d1fd2b1f242cc0cb/5f213cd926db9e3c7ce9c575_5eac2b0a98761e5e33661064_Untitled-2.jpg)

![Image](https://i.imgur.com/SzxJTW1.png)

## The Model Asset Exchange (MAX)

A free open source resource for deep learning models. To reduce time to value, consider taking advantage of pre-trained models for certain types of problems. These pre-trained models can be ready to use right away, or they might take less time to train. 

+ MAX reduces time to value 
    + free open-source deep learning microservices
        + use pre-trained or custom-trainable state-of-the-art-models
        + fully tested, deploy in minutes
        + approved for personal and commercial use
    + available for variety of domains 
        + object detection
        + image, audio, and text classification
        + named entity recognition
        + image-to-text translation
        + human pose detection

![Image](https://i.imgur.com/CbdXDHp.png)

+ Model-serving microservices expose standardized REST API  
    ![Image](https://i.imgur.com/1As5W7F.png)
+ Application-friendly inputs and outputs