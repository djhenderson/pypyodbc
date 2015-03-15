# Setting Time Out #

There are 3 types of time out in ODBC:
Connection Timeout - which is basically the about the network layer timeout;
Login Timeout - which is the time to wait when login to a database;
Query Timeout - which is the time the program should wait when the database is executing a query.

## Setting Connection Time Out ##
Before connecting, set the value of pypyodbc.connection\_timeout:

```
import pypyodbc
pypyodbc.connection_timeout = 10
conn = pypyodbc.connect('dsn=mssql')
```

After connecting, use the set\_connection\_timeout method:

```
import pypyodbc
conn = pypyodbc.connect('dsn=mssql')
conn.set_connection_timeout(10)
```

## Setting Login Time Out ##
Use the timeout keyword when connecting to a data source
```
import pypyodbc
pypyodbc.connection_timeout = 10
conn = pypyodbc.connect('dsn=mssql', timeout = 10)
```


## Setting Query Time Out ##
Set the timeout property of a connection object when cursors haven't been created.
```
conn = pypyodbc.connect('dsn=mssql')
conn.timeout = 10
cur = conn.cursor()
cur.execute("WAITFOR DELAY '00:00:04'")
```

Or use the set\_timeout method of cursor after it has been created:

```
conn = pypyodbc.connect('dsn=mssql')
cur = conn.cursor()
cur.set_timeout(10)
cur.execute("WAITFOR DELAY '00:00:04'")
```