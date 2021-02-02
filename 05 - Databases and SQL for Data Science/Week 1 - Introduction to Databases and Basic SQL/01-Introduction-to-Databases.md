# Introduction to Databases

## Welcome to SQL for Data Science

Why should you learn SQL?

+ Boost your professional profile
+ Give you a good understanding of relational databases


## Introduction to Databases

+ Describe SQL, data, database, relational database
+ list five basic SQL commands

What is SQL?

+ A language used for relational databases
+ query data
+ short for Structured Query Language


What is a database?

+ A repository of data
+ Provides the functionality for adding, modifying, and querying the data
+ Different kinds of databases store data in different forms
    + Relational databases
        + data stored in tabular form - columns and rows
        + columns contain item properties e.g. Last Name, First Name, etc.
        + Table is collection of related things e.g. Employees, Authors, etc.
        + Relationships can exist between tables 
+ DBMS (Database Management System)
    + database, database server, database system, data server, DBMS - often used interchangeably
    + RDBMS
        + a set of software tools that controls the data
            + access, organization, and storage
        + MySQL, Oracle Database, IBM Db2


Commands

+ Create a table
+ Insert
+ Select
+ Update
+ Delete


## How to Create a Database Instance on Cloud

CLoud database

+ Ease of Use and Access
    + API 
    + Web Interface
    + Cloud or Remote Applications
+ Scalability & Economics
    + Expand/Shrink storage & compute resources
    + Pay per use
+ Disaster Recovery
    + Cloud backups and geographical distribution

Examples

+ IBM Db2
+ Databases for PostgreSQL
+ Oracle Database Cloud Service
+ Microsoft Azure SQL Database
+ Amazon Relational Database Services (RDS)

Available as: 

+ VMs or Managed Service
+ Single or Multi-tenant

Database Service Instances

+ DBaaS provides users with access to Database resources in cloud without setting up hardware and installing software
+ Database service instance holds data in data objects/table
+ Once data is loaded, it can be queried using web interfaces and applications

### IBM Db2 on Cloud

## Relational Database Concepts

+ Most used data model
+ Allows for data independence
+ Data is stored n a tables

### Entity-Relationship Model

![Image](https://i.imgur.com/IuYySsS.png)

+ entity
    + table
+ attribute
    + column

### Primary Keys and Foreign Keys

![Image](https://i.imgur.com/gf3YebA.png)
+ Primary Keys
    + identify a specific row in a table - avoid duplication
+ Foreign Keys
    + creating links between tables