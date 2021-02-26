# Functions, Sub-Queries, Multiple Tables

**Multiple Tables**

## Built-in Database Functions

+ Most databases come with built-in SQL functions
+ Built-in functions can be included as part of SQL statements
+ Database functions can significantly reduce the amount of data that needs to be retrieved
+ can speed up data processing


### Aggregate or Column functions
+ take in a collection of values
+ output: single value
+ E.g. SUM(), MIN(), MAX(), AVG()

```sql
select SUM(COST) as SUM_OF_COST from PETRESCUE
```

#### MIN, MAX
```sql
select MAX(QUANTITY) from PETRESCUE

select MAX(ID) from PETRESCUE where animal = 'Dog'
```
#### AVG

```sql
select AVG(COST) from PETRESCUE
```

Calculate the average COST per 'Dog':
```sql
select AVG(COST / QUANTITY) from PETRESCUE
where ANIMAL = 'Dog'
```

### SCALAR and STRING Functions

+ SCALAR: perform operations on every input value
    + e.g. ROUND(), LENGTH(), UCASE, LCASE

```sql
select LENGTH(ANIMAL) from PETRESCUE
```

#### UCASE, LCASE
```sql
select UCASE(ANIMAL) from PETRESCUE
```

```sql
select * from PETRESCUE
where LCASE(ANIMAL) = 'cat';


select DISTINCT(UCASE(ANIMAL)) from PETRESCUE;
```

## Date and Time Built-in Functions 

+ Date
+ Time
+ TIMESTAMP

```sql
select DAY(RESCUEDATE) from PETRESCUE
where ANIMAL = 'Cat' -- select the day portion from a date
```

Get the number of rescues during the month of May:
```sql
SELECT COUNT(*) FROM PETRESCUE
WHERE MONTH(RESCUEDATE) = '05'
```

What date is it 3 days after each rescue date?
```sql
select (RESCUEDATE + 3 DAYS) from PETRESCUE
```

Find how many days have passed since each RESCUEDATE till now:
```sql
SELECT (CURRENT_DATE - RESCUEDATE) from PETRESCUE
```
results are in (YMMDD) format

## Sub-Queries and Nested Selects
+ Sub-query: A query in side another query
   ```sql
   SELECT COLUMN1 FROM TABLE 
        WHERE COLUMN2 = (SELECT MAX(COLUMN2) FROM TABLE)
   ```
   ```sql
   select * from EMPLOYEES
        where SALARY < (SELECT AVG(SALARY) FROM EMPLOYEES)
   ```
+ Column Expressions
    ```sql
    SELECT EMP_ID, SALARY, (SELECT AVG(SALARY) FROM EMPLOYEES) AS AVG_SALARY
    FROM EMPLOYEES
    ```
+ Derived Tables or Table Expressions: Substitute the TABLE name with a sub-query
    ```sql
    SELECT * FROM (SELECT EMP_ID, F_NAME, L_NAME, DEP_ID FROM EMPLOYEES)  AS EMP4ALL -- create a new table with specified columns
    ```
## Working with Multiple Tables

1. sub-queries
2. implicit JOIN
3. JOIN operators (INNER JOIN, OUTER JOIN, etc.)

### Sub-queries

To retrieve only the employee records that correspond to departments in the DEPARTMENTS table:
```sql
select * from Employees
    where DEP_ID IN (select DEPT_ID_DEP from DEPARTMENTS);
```

To retrieve only the list of employees from a specific location:
+ EMPLOYEES table does not contain location information
+ Need to get location info from DEPARTMENTS table

```sql
select * from EMPLOYEES
    where DEP_ID IN (select DEPT_ID_DEP from DEPARTMENTS
        where LOC_ID = 'L0002');
```

To retrieve the department ID and name for employees who earn more than $70,000:
```sql
select DEPT_ID_DEP, DEP_NAME from DEPARTMENTS
where DEPT_ID_DEP in (select DEP_ID from employees where SALARY > 70000);   
```

### Implicit JOIN
Specify 2 tables in the FROM clause:
```sql
select * from employees, departments;
```

=> full join (Cartesian join)

Use additional operands to limit the result set:
```sql
select * from employees, departments
    where employees.DEP_ID = departments.DEPT_ID_DEP;
```


```sql
select * from employees E, departments D
    where E.DEP_ID = D.DEPT_ID_DEP;
```

To see the department name for each employee
```sql
select EMP_ID, DEP_NAME from employees E, departments D
    where E.DEP_ID = D.DEPT_ID_DEP
```

Column names in the select clause can be pre-fixed by aliases:
```sql
select E.EMP_ID, D.DEP_ID_DEP from employees E, departments D 
    where E.DEP_ID = D.DEP_ID_DEP
```

This also works:
```sql
SELECT F_NAME, DEP_NAME FROM EMPLOYEES, DEPARTMENTS WHERE DEPT_ID_DEP = DEP_ID

```

## Lab
### Part A: Sub-Queries and Nested-Selects
-- Query A1: Enter a failing (i.e. which gives an error) to retrieve all employees whose salary is greater than the average salary

```sql
select * from employees where salary > AVG(salary)
```

-- Query A2: Enter a working query using a sub-select to retrieve all employees whose salary is greater than the average salary

```sql
select EMP_ID, F_NAME, L_NAME, SALARY from employees where SALARY > (select AVG(SALARY) from employees);
```

-- Query A3: Enter a failing query (i.e. that gives an error) that retrieves all employees records and average salary in every row

```sql
select EMP_ID, SALARY, AVG(SALARY) AS AVG_SALARY from employees ;
```

-- Query A4: Enter a Column Expression that retrieves all employees records and average salary in every row

```sql
select EMP_ID, SALARY, ( select AVG(SALARY) from employees ) AS AVG_SALARY from employees ;
```

-- Query A5: Enter a Table Expression that retrieves only the columns with non-sensitive employee data

```sql
select * from ( select EMP_ID, F_NAME, L_NAME, DEP_ID from employees) AS EMP4ALL ;
```

### Part B: Accessing Multiple Tables with Sub-Queries
-- Query B1: Retrieve only the EMPLOYEES records that correspond to departments in the DEPARTMENTS table

select * from employees where DEP_ID IN ( select DEPT_ID_DEP from departments );

-- Query B2: Retrieve only the list of employees from location L0002

select * from employees where DEP_ID IN ( select DEPT_ID_DEP from departments where LOC_ID = 'L0002' );

-- Query B3: Retrieve the department ID and name for employees who earn more than $70,000

select DEPT_ID_DEP, DEP_NAME from departments where DEPT_ID_DEP IN ( select DEP_ID from employees where SALARY > 70000 ) ;

-- Query B4: Specify 2 tables in the FROM clause

select * from employees, departments;

### Accessing Multiple Tables with Implicit Joins
-- Query B5: Retrieve only the EMPLOYEES records that correspond to departments in the DEPARTMENTS table

select * from employees, departments where employees.DEP_ID = departments.DEPT_ID_DEP;

-- Query B6: Use shorter aliases for table names

select * from employees E, departments D where E.DEP_ID = D.DEPT_ID_DEP;

-- Query B7: Retrieve only the Employee ID and Department name in the above query

select EMP_ID, DEP_NAME from employees E, departments D where E.DEP_ID = D.DEPT_ID_DEP;

-- Query B8: In the above query specify the fully qualified column names with aliases in the SELECT clause

select E.EMP_ID, D.DEP_NAME from employees E, departments D where E.DEP_ID = D.DEPT_ID_DEP