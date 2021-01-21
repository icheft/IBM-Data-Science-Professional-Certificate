# Data Science Tools

![Image](https://i.imgur.com/jloHmA9.png)

The ones with green labels can be done via cloud service.

## Categories of Data Science Tools
### Tasks
+ Data Asset Management:
    + Data Management: process of persisting and retrieving data
    + Data Integration and Transformation: Extract, Transform, and Load - the process of retrieving data from remote data management systems
        + also, transforming data and loading it into a local data management system
    + Data Visualization: part of an initiaal data exploration process, as well as being part of a final deliverable
    + Model Building: Create a machine learning or deep learning model using an algorithm with a lot of data
    + Model Deployment: Make models available to third-party applications
    + Model Monitoring and Assessment: ensures continuous performance quality checks on the deployed models
+ Code Asset Management: uses versioning and other collaborative features to facilitate teamwork
+ Development Environments: IDE, tools that help the data scientists to *implement, execute, test, and deploy* their works
    + Execution Environments: tools where data processing, model training, and deployment take place


## Open Source Tools for Data Science - Part I 
+ Data Asset Management:
    + Data Management
        + Relational databases: MySQL and PostgreSQL
        + NoSQL databases: MongoDB, Apache, CouchDB, and Apache Cassandra
        + File-based tools: Hadoop File System or Cloud File systems like Ceph
        + Storing text data and creating a serach index for fast document retrieval: Elasticseasrch
    + Data Integration and Transformation (ETL)
        + or "ELT" or "data refinery and cleansing"
        + Apache AirFlow
        + KubeFlow
        + Apache Kafka
        + Apache Nifi
        + Apache SparkSQL
        + NodeRED
    + Data Visualization
        + Hue: create visualization from SQL queries
        + Kibana
        + Apache Superset
    + Model Deployment
        + Apache PredictioIO
        + Seldon - supports every framework like TensorFlow, Apache SparkML, R, and scikit-learn
        + MLeap
        + TensorFlow
    + Model Monitoring and Assessment
        + ModelDB
        + Prometheus
        + IBM AI Fairness 360
        + IBM Adversarial Robustness 360 Toolbox
        + IBM AI Explainability 360 Toolkit
    + **Data Asset Management**
        + Apache Atlas
        + OPEI Egeria
        + Kylo
+ Code Asset Management: 
    + Git
## Open Source Tools for Data Science - Part II
+ development environment
    + Jupyter
    + Apache Zeppelin
    + RStudio
    + Spyder
    + When your data doesn't fit into a single computer's storage or main memory capacity → cluster execution environments
        + Apache Spark
            + linear scalability
            + a batch data processing engine, capable of processing huge amounts of data file by file
        + Apache Flink
            + stream processin image 
        + Ray
            + clear focus on large-scale deep learning model training
+ open source data integration
    + KNIME
    + Orange
+ transformation
+ visualization tools

## Commercial Tools for Data Science
+ Data Management:
    + Oracle Database 
    + Microsoft SQL Server
    + IBM Db2


When we focus on commercial data integration tools, we're talking about "ETL" tools. We
+ Gartner Magic Quadrant, Informatica Powercenter, IBM InfoSphere DataStage
+ SAP
+ Oracle
+ SAS
+ Talend
+ Microsoft
+ Watson Studio Desktop 

Commercial environment - data visualizations are utilizing business intelligence, or "BI", tools.

+ Tableau
+ Microsoft Power BI
+ IBM Cognos Analytics

When asking "How can different columns in a table relate to each other?" - Watson Studio Desktop


![Image](https://i.imgur.com/OtOpPlx.png)
    
### Model monitoring

### Data asset management - data goverance or data lineage
+ Data governance
+ Data lineage - enables a user to track back through the transformation steps followed in creating the data assets


### Fully Integrated Tools

Watson studio + Watson Open Scale = fully integrated tool covering the full data science life cycle and all the tasks we've discussed previously


keep in mind that they can be deployed in a local data center on top of Kubernetes or RedHat OpenShift. Another example of a fully integrated commercial tool is H2O Driverless AI, which covers the complete data science life cycle. 

## Cloud Based Tools for Data Science

+ Fully Integrated Visual Tools and Platforms
    + Watson Studio + Watson OpenScale
    + Azure Machine Learning 
    + H20.ai driverless AI



SaaS - Software as a Service
- the cloud provider operates the tool for you in the cloud. 

e.g. 

+ AWS DynamoDB - NoSQL Database that allows storage and retrieval of data in a key-value or a document store format
    + JSON
+ Cloudant - database as a service
    + based on the open source Apache CouchDB
+ Db2 (IBM)

When it comes to commercial data integration tools, we talk not only about “extract, transform, and load,” or *“ETL”* tools, but also about “extract, load, and transform,” or *“ELT*,” tools. This means the transformation steps are not done by a data integration team but are pushed towards the domain of the data scientist or data engineer. 

+ Informatica Cloud Data Integration
+ IBM's Data Refinery (part of IBM Watson Studio)

### Data Visualization

### Model Building
+ IBM Watson Machine Learning
+ Google Cloud AI Training


![Image](https://i.imgur.com/H5cssPQ.png)
Marked green can be done with IBM Watson Studio + Watson OpenScale

