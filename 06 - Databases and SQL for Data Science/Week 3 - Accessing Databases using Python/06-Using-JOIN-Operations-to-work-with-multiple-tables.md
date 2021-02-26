# Using JOIN Operations to Work with Multiple Tables

## JOIN Overview

+ JOIN operator: 
    + Combines rows from two or more tables
    + Based on a relationship
![Image](https://i.imgur.com/OfEnSkY.png)

Gathering data from different tables.

![Image](https://i.imgur.com/RvjAZBc.png)

Using primary key (to avoid unique key/id).


### Types of Joins
+ Inner JOIN
+ Outer JOIN
    + Left Outer Join
    + Right Outer Join
    + Full Outer Join


### Inner JOIN

+ Combines the rows from two or more tables
+ Two types of table JOINs: 
    + Inner: Mostly used
    + Outer

```sql
select B.BORROWER_ID, B.LASTNAME, B.COUNTRY, L.BORROWER_ID, L.LOAN_DATE
from BORROWER B inner join LOAN L
    on B.BORROWER_ID = L.BORROWER_ID
```

Joining three tables:

```sql
select B.LASTNAME, L.COPY_ID, C.STATUS,
FROM BORROWER B
    INNER JOIN LOAN L ON B.BORROWER_ID = L.BORROWER_ID
    INNER JOIN COPY C ON L.COPY_ID = C.COPY_ID
```

### Left OUTER JOIN
![Image](https://i.imgur.com/VaSLUIT.png)
```sql
SELECT B.BORROWER_ID, B.LASTNAME, B.COUNTRY, L.BORROWER_ID, L.LOAN_DATE
FROM BORROWER B LEFT JOIN LOAN L
    ON B.BORROWER_ID = L.BORROWER_ID
```

### Right OUTER JOIN

![Image](https://i.imgur.com/opbwvGm.png)

```sql
SELECT B.BORROWER_ID, B.LASTNAME, B.COUNTRY, L.BORROWER_ID, L.LOAN_DATE
FROM BORROWER B RIGHT JOIN LOAN L
    ON B.BORROWER_ID = L.BORROWER_ID
```

## FULL OUTER JOIN Operator
![Image](https://i.imgur.com/jzawFtn.png)

May result in a large table.

```sql
SELECT B.BORROWER_ID, B.LASTNAME, B.COUNTRY, L.BORROWER_ID, L.LOAN_DATE
FROM BORROWER B FULL JOIN LOAN L 
    ON B.BORROWER_ID = L.BORROWER_ID
```