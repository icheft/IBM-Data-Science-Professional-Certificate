# Tips and Tricks

```py
user = 'xxxx'
password = 'xxxxx'

connection_string = "ibm_db_sa://{user}:{password}@dashdb-txn-sbox-yp-lon02-04.services.eu-gb.bluemix.net:50000/BLUDB".format(user=user, password=password)
# print(connection_string)

%sql $connection_string
```

If failed establishing sql connection, run the following command first before further execution.
```py
!pip install --upgrade ibm_db
!pip install --upgrade ibm_db_sa
!pip install --upgrade SQLAlchemy
```