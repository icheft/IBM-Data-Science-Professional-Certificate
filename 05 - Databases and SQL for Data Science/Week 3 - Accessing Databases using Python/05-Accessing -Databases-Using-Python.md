# Accessing Databases Using Python

## How to Access Databases Using Python


Using Jupyter Notebook:
![Image](https://i.imgur.com/p3zPxZ1.png)

### What is a SQL API?
![Image](https://i.imgur.com/nRuXAzm.png)

![Image](https://i.imgur.com/qWQ6y6h.png)


## Writing Code Using DB-API

DB-API: Python's standard API for accessing relational databases. It allows a single program to work with multiple kinds of relational databases.

![Image](https://i.imgur.com/DM5UhKz.png)


### Concepts
+ Connection Objects
    + databases connections
    + manage transactions
+ Cursor Objects
    + database Queries
    + scroll through the result set
    + retrieve results

#### Connection Methods
+ .cursor()
+ .commit()
+ .rollback()
+ .close()

#### Cursor Methods
+ .callproc()
+ .execute()
+ .executemany()
+ .fetchone()
+ .fetchmany()
+ .fetchall()
+ .nextset()
+ .arraysize()
+ .close()

![Image](https://i.imgur.com/4ev68Ei.png)

Keeps track of the program's current position.

### Writing Code using DB-API

```py
from dbmodule import connect

# create connection objects

connection = connect('databasename', 'username', 'pswd')

# create a cursor object
cursor = connection.cursor()

# run queries
cursor.execute('select * from mytable')
result = cursor.fetchall()

# free resources
cursor.close()
connection.close()
```

## Connecting to a database using ibm_db API

Functions:  

+ connecting to a database
+ preparing and issuing SQL statements, 
+ fetching rows from result sets,
+ calling stored procedures
+ committing and rolling back transactions
+ handling errors and retrieving metadata


```py
dsn_driver = "{IBM DB2 ODBC DRIVER}"
dsn_database = 'BLUDB'
dsn_hostname = 'YourDb2Hostname'
dsn_port = '50000'
dsn_protocol = 'TCPIP'
dsn_uid = '********'
dsn_pwd = '********'

dsn = (
    'DRIVER = {{IBM DB2 ODBC DRIVER}};'
    'DATABASE = {0};'
    'HOSTNAME = {1};'
    'PORT = {2};'
    'PROTOCOL=TCPIP;'
    'UID={3};'
    'PWD={4};'
).format(dsn_database, dsn_hostname, dsn_post, dsn_uid, dsn_pwd)

try:
    conn = ibm_db.connect(dsn, '', '')
    print('Connected!')
except:
    print('Unable to connect to database')

pass

ibm.close(conn)
```

## Creating Tables, Loading Data, and Querying Data

Creating Tables
```py
stmt = ibm_db.exec_immediate(Connection, SQL_Statement, Options)
```

Fetch
```py
stmt = ibm_db.exec_immediate(conn, "SELECT * FROM Trucks")

ibm_db.fetch_both(stmt)
```

Pandas
```py
import pandas
import ibm_db_dbi
pconn = ibm_db_dbi.Connection(conn)
df = pandas.read_sql('SELECT * FROM Trucks', pconn)
display(df.head())
```

## Analyzing Data with Python

![Image](https://i.imgur.com/C06oZb3.png)

1. Load Source 
2. Target 
3. Define
4. Finalize (seeing the statistics of the data)


For verification:
```py
stmt = ibm_db.exec_immediate(conn, "SELECT count(*) FROM MCDONALDS_NUTRITION")

ibm_db.fetch_both(stmt) # read the first row
```

+ See Jupyter Notebook for more.    