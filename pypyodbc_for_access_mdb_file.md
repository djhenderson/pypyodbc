# PyPyODBC functions for generating MDB file  #

You can use pypyodbc to easily create an empty Access MDB file on win32 platform, and also compact existing Access MDB files.


# Just that simple: #

```
import pypyodbc 
             
pypyodbc.win_create_mdb('D:\\database.mdb')


connection = pypyodbc.win_connect_mdb('D:\\database.mdb')
connection.cursor().execute('CREATE TABLE t1 (id COUNTER PRIMARY KEY, name CHAR(25));').commit()
connection.close()


pypyodbc.win_compact_mdb('D:\\database.mdb','D:\\compacted.mdb')


```


# How to #

  * To create an Access mdb file

```
import pypyodbc
pypyodbc.win_create_mdb( "D:\\Your_MDB_file_path.mdb" )
```

  * To connect to the created mdb files, and manipulate them with the ODBC interface.


```

conn = pypyodbc.win_connect_mdb("D:\\Your_MDB_file_path.mdb")  

cur = conn.cursor()
cur.execute(u"""CREATE TABLE pypyodbc_test_tabl (ID INTEGER PRIMARY KEY,product_name TEXT)""")

cur.execute(u"""INSERT INTO pypyodbc_test_tabl VALUES (1,'PyPyODBC')""")

cur.close()
conn.commit()
conn.close()
   

```


  * To compact an existing Access mdb file

```
pypyodbc.win_compact_mdb("D:\\The path to the original to be compacted mdb file"
                       ,"D:\\The path to put the compacted new mdb file")
```

## See also ##
### [PyPyODBC: Hello SQL Server](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python) ###