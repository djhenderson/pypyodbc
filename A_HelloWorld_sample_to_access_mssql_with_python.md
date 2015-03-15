# A HelloWorld sample to access SQLServer with python #

```
# -*- coding: utf-8 -*-



#                  We use the Python 2.x & 3.x compatible print function.

from __future__ import print_function


#                  Let Python load it's ODBC connecting tool pypyodbc
     
import pypyodbc


#                  Let Python load it's datetime functions

import datetime

#                  Get a connection to MSSQL ODBC DSN via pypyodbc, and assign it to conn

conn = pypyodbc.connect('DSN=MSSQL')


#                  Give me a cursor so I can operate the database with the cursor

cur = conn.cursor()


#                  Create a sellout table in SQLServer

cur.execute('''CREATE TABLE sellout (
                ID integer PRIMARY KEY IDENTITY,
                customer_name VARCHAR(25), 
                product_name VARCHAR(30), 
                price float, 
                volume int,
                sell_time datetime);''')


#                  I've made some changes to the data, make the changes take effective, Now!

cur.commit()


#                  Insert a row to the sellout table

cur.execute('''INSERT INTO sellout(customer_name, product_name, price, volume, sell_time) 
VALUES(?,?,?,?,?)''',(u'江文', 'Huawei Ascend mate', '5000.5', 2, datetime.datetime.now()) )


#                  Another change has been made. let that take effective, Now!

cur.commit()


#                  Insert a batch rows of data to the sellout table using a same query

a_batch_rows = [(u'杨天真' , 'Apple IPhone 5'       , 5500.1    , 1, '2012-1-21'),
                (u'郑现实' , 'Huawei Ascend D2'     , 5100.5    , 2, '2012-1-22'),
                (u'莫小闵' , 'Lenovo P780'          , 2000.5    , 3, '2012-1-22'),
                (u'顾小白' , 'Huawei Ascend Mate'   , 3000.4    , 2, '2012-1-22')]
            
cur.executemany('''INSERT INTO sellout(customer_name,product_name,price,volume,sell_time) 
VALUES(?,?,?,?,?)''',  a_batch_rows)    


#                  Make all my changes to the data take effective, Now!

cur.commit()


#                  Select those records about "Huawei" products

cur.execute('''SELECT * FROM sellout WHERE product_name LIKE '%Huawei%';''')


#                  Print the table headers (column descriptions)

for d in cur.description: 
    print (d[0], end=" ")


#                  Start a new line

print ('')


#                  Print the table, one row per line

for row in cur.fetchall():
    for field in row: 
        print (field, end=" ")
    print ('')
    

#                  I have done all the things, you can leave me and serve for others!

cur.close()
conn.close()

```

## See also: ##


**[PyPyODBC tutorial by a Sales DB example](https://code.google.com/p/pypyodbc/wiki/PyPyODBC_Example_Tutorial)**

**[PyPyODBC's Access mdb control "short cuts"](https://code.google.com/p/pypyodbc/wiki/pypyodbc_for_access_mdb_file)**

**[pypyodbc and pyodbc](https://code.google.com/p/pypyodbc/wiki/Compatibility_with_pyodbc)**

