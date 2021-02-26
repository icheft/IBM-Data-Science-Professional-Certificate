# Assignment Preparation

## Working with Real World Datasets

</hr>


```sql
select "Id" from DOGS
```

</hr>

```sql
select * from DOGS LIMIT 3
```


</hr>

```py
%%sql
select "Id", "Name_of_Dog"
    from dogs
    where "Name_of_Dog" = "Huggy"
```

or 

```py
%sql select "Id", "Name_of_Dog" \
    from dogs \
    where "Name_of_Dog" = "Huggy"
```

## Getting Table and Column Details


Getting a list of tables in the database:
![Image](https://i.imgur.com/NjVAdSw.png)

+ Db2: `syscat.tables`
+ SQL Server: `information_schema.tables`
+ Oracle: `all_tables` or `user_tables`

### Tables

```sql
select * from syscat.tables
```
and
```sql
select TABSCHEMA, TABNAME, CREATE_TIME
    from syscat.tables
    where tabschema = 'user_name'
```



### Columns
```sql
select * from syscat.columns
    where tabname = 'DOGS'
```

or to obtain specific column properties
```sql
select distinct(name), coltype, length
    from sysibm.syscolumns
    where tbname = 'DOGS'
```

![Image](https://i.imgur.com/VpXcxGd.png)