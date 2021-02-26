# String Patterns, Ranges, Sorting, and Grouping

## Using String Patterns and Ranges

### String Pattern

+ WHERE requires a predicate
+ A predicate is an expression that evaluates to True, False, or Unknown
+ Use the LIKE predicate with string patterns for the search


```sql
select fistname from AUTHOR
    WHERE firstname LIKE R% -- NAME starts with R
```

### Ranges
```sql
select title, pages from BOOK
    WHERE pages >= 290 AND pages <= 300
```

or

```sql
select title, pages from BOOK
    WHERE pages between 290 AND 300
```

### Using a Set of Values

```sql
select firstname, lastname, country from AUTHOR
    -- WHERE country = 'AU' or country = 'BR'
    WHERE country IN ('AU', 'BR')
```

## Sorting Result Sets
```sql
select * from BOOK; -- retrieve all rows
select title from BOOK;
```

Using the ORDER BY clause

```sql
select title from BOOK
    ORDER BY title -- default: ascending order
    ORDER BY title DESC -- change default to descending order

;

select title, pages from BOOK
    ORDER BY 2
```

![Image](https://i.imgur.com/idE6JCM.png)

## Grouping Result Sets

### DISTINCT
Eliminating duplicates.

```sql
select country from AUTHOR
    ORDER BY 1

select distinct(country)
    from AUTHOR
```

### GROUP BY
```sql
select country, count(country) 
    from AUTHOR GROUP BY country
```
![Image](https://i.imgur.com/CuNLtU0.png)

or

```sql
select country, count(country) 
    as Count from AUTHOR GROUP BY country
```
![Image](https://i.imgur.com/mJkMmnP.png)

### HAVING

```sql
select country, count(country) 
    as Count from AUTHOR 
    GROUP BY country
    having count(country) > 4
    
```