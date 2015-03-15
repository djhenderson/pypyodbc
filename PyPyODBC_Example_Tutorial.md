
```
This example tutorial is published under Public Domain, readers can freely use its content.
```

Today, I would use a simple sales database programming case to guide the interested readers the entry-level Python database programming techniques. We will use Python to create a simple MS-Access sales database, using Python ODBC interface to insert and delete sales records, and lastly, query the data in the Access database. Below are the main steps we will be programming step-by-step through:
  1. Introduce and install Python & an ODBC module pypyodbc;
  1. Create an Access database and a sales table in this database;
  1. Record sales transactions by inserting records in the table;
  1. Use Python to query data in the database and compress the MS-Access database file.

Ready? Let's begin!

### 1) Introduce and install Python & an ODBC module pypyodbc ###
The Python install package can be downloaded in www.python.org . For this tutorial, we need to download Python version. Although it is a programming platform, like ordinary program, you just need to choose a local installation path to install Python, and then you can just press the "Next" all the way to complete the installation.

_- Some people may ask, why not choose the latest Python 3.X ? Today (January 20, 2013) my point of view: If you want to quickly start to develop real world system in Python, then right now you should choose Python 2.7. Python 3.X is, without doubt, the future direction. However, as the 3.X versions do not have good backward compatibility, many function libraries that can be used in Python 2.X module, as of today still can not be used in Python 3.X. The bread and milk of Python 3.x are in preparation, but it will take a little more time._


Next, we need to install the pypyodbc module. Pypyodbc is a one-script pure python moudle to call the operating system's ODBC funcitons. Way to install pypyodbc:
From http://code.google.com/p/pypyodbc/downloads/list download the pypyodbc installation file, currently the latest one is pypyodbc-0.9.1-SVN-[r206](https://code.google.com/p/pypyodbc/source/detail?r=206).zip.

![http://s7.sinaimg.cn/mw690/6c64ac15gd41b14d7fa77&690?b=x.png](http://s7.sinaimg.cn/mw690/6c64ac15gd41b14d7fa77&690?b=x.png)

Download and extract the zip file to a temporary directory, double-click the setup.py file, and this will get pypyodbc installed for your installed Python instance.

![http://s7.sinaimg.cn/mw690/6c64ac15gd4312f132752&690?b=x.png](http://s7.sinaimg.cn/mw690/6c64ac15gd4312f132752&690?b=x.png)


In this tutorial, as we will enter the command directly in the Python interactive window, so please use the above method to install pypyodbc. In your future projects, we can just unzipped the zip file, place the core script pypyodbc.py under the same directory where we will write the project scripts, then you would be able to call it directly in your project script, and no need to do have the module installed in Python instance separately.

Okay, we have Python and PyPyODBC installed, and now we can begin writing some real code in Python!


### 2) Create an Access database and a sales table in this database ###

From here on, in order for uses to understand the effect of each step, we will write codes in the Python interactive window interface (Shell) step by step, and finally, we will concentrate these interactive codes to a script file, and become a program file.

Let's open the Python interface: find Python 2.7 directory from the Windows Start menu, click to run Python 2.7 (command line), there will be a white on black text input window pop up, containing the following words.
```
Python 2.7.3 (default, Apr 10 2012, 23:31:26) [MSC v.1500 32 bit (Intel)] on win32
Type "copyright", "credits" or "license ()" for more information.
>>>
```
That means you can now type codes after this >>> symbol, step-by-step manipulating Python to complete actions. We now go step by step:

**The first step:** We command Python to identify the just installed pypyodbc module from it's module library, for us to use in the next steps.
```
>>> import pypyodbc
```

![http://s11.sinaimg.cn/mw690/6c64ac15g7b9e84f60e0a&690?b=x.png](http://s11.sinaimg.cn/mw690/6c64ac15g7b9e84f60e0a&690?b=x.png)

**Step two:** We want to create an Access database to store sales data. This is a featured function of PyPyODBC, so users can easily use it to create a blank Access database on Windows platforms. We name the Access database salesdb.mdb, and put it under the root directory of D drive.
```
>>> pypyodbc.win_create_mdb('D:\\salesdb.mdb')
```
At this time, you can see a blank Access database file salesdb.mdb is generated in the D drive.

![http://s6.sinaimg.cn/bmiddle/6c64ac15gd41b42b04685&690?b=x.png](http://s6.sinaimg.cn/bmiddle/6c64ac15gd41b42b04685&690?b=x.png)

**The third step:** using pypyodbc module, we obtain an ODBC connection object "conn" to the salesdb.mdb through an Access ODBC connection string:
```
>>> conn = pypyodbc.connect('Driver = {Microsoft Access Driver (*. Mdb)}; DBQ = D:\\salesdb.mdb')
```
And from this connection object, get an operational cursor of the connected database:
```
>>>cur = conn.cursor()
```


**The fourth step:** Create a new sales record table "saleout" in the database
We use the cursor to pass a SQL command to the Access database, create a table named saleout:
```
>>>cur.execute('''CREATE TABLE saleout (
ID COUNTER PRIMARY KEY,
customer_name VARCHAR(25), 
product_name VARCHAR(30), 
price float, 
volume int,
sell_time datetime);''')
```


This database is created with a table with fields of: ID (ID), customer\_name (the customer's name), product\_name (product name), price (selling price), volume (quantity) and sell\_time (sale time).
Finally, we submitted the operations, so they officially take effect in the database in the same time.
```
>>>cur.commit()
```


### 3) Record sales transactions by inserting records in the table; ###
After the database and table have been created, we can fill in some sales records.

The first step, we record a customer of Mr. Jiang (Jiang Wen), on January 21, 2013, bought two Huawei Ascend mate phone with 5000.5 yuan:
```
>>>cur.execute('''INSERT INTO saleout(customer_name,product_name,price,volume,sell_time) 
VALUES(?,?,?,?,?)''',(u'Jiang Wen','Huawei Ascend mate',5000.5,2,'2012-1-21'))
```
Do not forget to submit the operations, so the record officially take effect in the database:
```
>>>cur.commit()
```
Next, we then record a batch of sales:
```
>>>cur.execute('''INSERT INTO saleout(customer_name,product_name,price,volume,sell_time) 
VALUES(?,?,?,?,?)''',(u'Yang Tianzhen','Apple IPhone 5',6000.1,1,'2012-1-21'))
>>>cur.execute('''INSERT INTO saleout(customer_name,product_name,price,volume,sell_time) 
VALUES(?,?,?,?,?)''',(u'Zheng Xianshi','Huawei Ascend D2',5100.5,1,'2012-1-22'))
>>>cur.execute('''INSERT INTO saleout(customer_name,product_name,price,volume,sell_time) 
VALUES(?,?,?,?,?)''',(u'Mo Xiaomin','Huawei Ascend D2',5200.5,1,'2012-1-22'))
>>>cur.execute('''INSERT INTO saleout(customer_name,product_name,price,volume,sell_time) 
VALUES(?,?,?,?,?)''',(u'Gu Xiaobai','Huawei Ascend mate',5000.5,1,'2012-1-22'))
```
Immediately submit the changes, so these 4 records officially come into effect at the same time in the database:
```
>>>cur.commit()
```
At this point, we have 5 sales transactions recorded in the system. In the following steps, we will query these records.



### 4) Use Python to query data in the database and compress the MS-Access database file. ###

If we want to query on January 21, 2012, our sales of Huawei products, how should we do? At this time, we will pass a SQL query to the Access database, and obtain the returned database query results as Python variables.
First we pass the SQL query to Access database:
```
>>>cur.execute('''SELECT * FROM saleout WHERE product_name LIKE '%Huawei%'''')
```

Then we get the names of the fields of the result set from the database query results:
```
>>>for d in cur.description:
    print d[0],
id customer_name product_name price volume sell_time
```

The interactive interface will display the name of each field. Next we display result set row by row of the result set on the screen:
```
>>>for row in cur.fetchall():
    for field in row: 
        print field,
    print ''
1 Jiang Wen Huawei Ascend mate 5000.5 2 2012-01-21 00:00:00
3 Zheng Xianshi Huawei Ascend D2 5100.5 1 2012-01-22 00:00:00
4 Mo Xiaomin Huawei Ascend D2 5000.5 1 2012-01-22 00:00:00
5 Gu Xiaobai Huawei Ascend mate 5000.5 1 2012-01-22 00:00:00
```
This shows all of the result set.

For Access databases, after long data insertion, updating, deleting operations, the Access database file may become very bloated and huge. PyPyODBC provides another featured functions, which can directly call the database cleansing function in Python programs. We now use this function and generate a compressed database file salesdb\_backup.mdb from the original database file salesdb.mdb:
First, close the database connection:
```
>>>conn.close()
```

Then use pypyodbc win\_compact\_mdb function to compress the database file:
```
>>>pypyodbc.win_compact_mdb('D:\\salesdb.mdb','D:\\salesdb_backup.mdb')
```

![http://s12.sinaimg.cn/mw690/6c64ac15gd41b416da1bb&690?b=.png](http://s12.sinaimg.cn/mw690/6c64ac15gd41b416da1bb&690?b=.png)


At this time, we will find a compressed salesdb\_backup.mdb file generated under the D drive, how ever, there is no big difference between the sizes of the two files in this case, but after long and frequent use of the database, the compression effect of the cleanup will be huge.

### Save as a Python program file and Summary ###
In the tutorial, we used the Python interactive interface, manipulated Python to executed of all steps with codes line-by-line. We can put all those codes into one text file suffixed by "py", so that Python will be performed in accordance with the order of the code in the text file. The program codes in this tutorial is available for download on sales\_sample.py.

Some readers may ask, in this tutorial, we programed with the Access database, how about other databases, how to program against them? In fact, as long as the database supports ODBC (I seldomly heard of a relational database that does not support ODBC), it should be used with pypyodbc. pypyodbc currently known to supported: Access, SQLServer, MySQL, PostgreSQL and even Excel.

**(It would be excellent if I can see some success story from you in comment area below!)**



## See Also: ##
[A HelloWorld demo script to access SQLServer](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)