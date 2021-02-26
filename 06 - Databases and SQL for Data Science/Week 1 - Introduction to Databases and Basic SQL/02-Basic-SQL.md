# Basic SQL

## Create TABLE statement

+ DDL (Data Definition Language) Statements
    + define, change, drop data
    + `CREATE`
    + `ALTER`
    + `TRUNCATE`
    + `DROP`
+ DML (Data Manipulation Language) Statements
    + Read and modify data
    + CRUD operations (Create, Read, Update, and Delete rows)
    + `INSERT`
    + `SELECT`
    + `UPDATE`
    + `DELETE`

```sql
CREATE TABLE table_name
    (
        column_name_1 datatype optional_parameters, 
        column_name_2 datatype,
        ...
        column_name_n datatype
    )
```


### Example 1
```sql
CREATE TABLE provinces (
    id char(2) PRIMARY KEY NOT NULL,
    name varchar(24)
)
```

### Example 2
![Image](https://i.imgur.com/Fsuvyco.png)

```sql
CREATE TABLE author (
    author_id CHAR(2) PRIMARY KEY NOT NULL, 
    lastname VARCHAR(15) NOT NULL,
    firstname VARCHAR(15) NOT NULL,
    email VARCHAR(40),
    city VARCHAR(15),
    country CHAR(2)
)
```

## SELECT

+ Retrieving rows from a table
+ A Data Manipulation Language (DML) statement used to read and modify data
+ retrieve a subset of the columns
    + can retrieve just the columns you want
    + The order of the columns displayed always matches *the order* in the SELECT statement


### WHERE
+ restricts the result set
+ always requires a predicate: 
    + evaluates to: True, False, or Unknown
    + Used in the search condition of the Where clause


```sql
select book_id, title from Book
    WHERE predicate
```
```sql
db2 => select book_id, title from Book
    WHERE book_id = 'B1'
```

### Docs
The general syntax of `SELECT` statments is:

#### select COLUMN1, COLUMN2, ... from TABLE1 ;

To retrieve all columns from the COUNTRY table we could use "*" instead of specifying individual column names:

#### select * from COUNTRY ;

The WHERE clause can be added to your query to filter results or get specific rows of data. To retrieve data for all rows in the COUNTRY table where the ID is less than 5:

#### select * from COUNTRY where ID < 5 ;

In case of character based columns the values of the predicates in the where clause need to be enclosed in single quotes. To retrieve the data for the country with country code "CA" we would issue:

#### select * from COUNTRY where CCODE = 'CA';

In the lab that follows later in the module, you will apply these concepts and practice SELECT queries hands-on.

## COUNT, DISTINCT, LIMIT
### COUNT
a built-in function that retrieves the number of rows matching the query criteria.

Number of rows in a table:

```sql
select COUNT(*) from tablename
```

```sql
select COUNT(COUNTRY) from MEDALS
    where COUNTRY='CANADA'
```

### DISTINCT
used to remove duplicate values from a result set.

```sql
select DISTINCT COUNTRY from MEDALS
    where MEDALTYPE = 'GOLD'
```

### LIMIT
used to restrict the number of rows retreieved from the database.

```sql
select * from tablename LIMIT 10
```

```sql
select * from MEDALS
    where YEAR = 2018 LIMIT 5
```

## INSERT
Populating a relational database table.

+ adding rows to a table
+ Data Maniulation Language (DML) statement used to read and modify data

```sql
INSERT INTO [TABLENAME]
    <([COLUMNNAME], ...)>
VALUES ([VALUE], ...)  
```

```sql
INSERT INTO AUTHOR
    (AUTHOR_ID, LASTNAME, FIRSTNAME, EMAIL, CITY, COUNTRY)
VALUES 
    ('A1', 'Chong', 'Raul', 'rfc@ibm.com', 'Toronto', 'CA'), 
    ('A1', 'Chong', 'Raul', 'rfc@ibm.com', 'Toronto', 'CA')
```

## UPDATE and DELETE Statements
### UPDATE
+ altering rows of a table
+ DML statement

```sql
UPDATE [TableName]
SET [[ColumnName]=[Value]]
<WHERE [Condition]>
```


```sql
UPDATE AUTHOR
SET LASTNAME = 'KATTA'
    FIRSTNAME = 'LAKSHMI'
    WHERE AUTHOR_ID = 'A2'
```

### DELETE

+ remove 1 or more rows from the table

```sql
DELETE FROM AUTHOR
    WHERE AUTHOR_ID IN ('A2', 'A3')
```
