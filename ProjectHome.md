# pypyodbc - A pure Python ODBC interface module based on ctypes #

Design Goal: **_Small, Compatible, Cross Platfrom, Portable, Maintainable_**


_**Latest release: 1.3.3**  May 25 2014_

## Features ##
  * **Pure Python**: No compilation needed. One-file pure Python module. [How is the speed?](https://code.google.com/p/pypyodbc/wiki/speed)
  * **Cross platform**: runs on [PyPy](https://code.google.com/p/pypyodbc/wiki/Enable_SQLAlchemy_on_PyPy) / CPython / [IronPython](https://code.google.com/p/pypyodbc/wiki/Enable_SQLAlchemy_on_IronPython)  ,  Python 3.4 / 3.3 / 3.2 / 2.4 / 2.5 / 2.6 / 2.7 ,  Win / Linux / Mac , 32 / 64 bit*****Very [similar usage](https://code.google.com/p/pypyodbc/wiki/Compatibility_with_pyodbc) as pyodbc**( almost can be seen like a drop-in replacement of [pyodbc](http://code.google.com/p/pyodbc) in pure Python )
  ***Simple - the whole module is implemented in a single script with less than 3000 lines*****[Built-in functions](https://code.google.com/p/pypyodbc/wiki/pypyodbc_for_access_mdb_file) to create and compress Access MDB files on Windows

> Click  if you like this project! ![https://code.google.com/p/pypyodbc/logo?cct=1378440352&x=a.png](https://code.google.com/p/pypyodbc/logo?cct=1378440352&x=a.png) (So I can know it's liked by some people...)

Simply try pypyodbc:
```
import pypyodbc 
             
pypyodbc.win_create_mdb('D:\\database.mdb')

connection_string = 'Driver={Microsoft Access Driver (*.mdb)};DBQ=D:\\database.mdb'

connection = pypyodbc.connect(connection_string)

SQL = 'CREATE TABLE saleout (id COUNTER PRIMARY KEY,product_name VARCHAR(25));'

connection.cursor().execute(SQL).commit()

...

```
> [A Demo to connect to SQLServer](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)

> [A Very Beginner's Python Database Programming Tutorial with PyPyODBC](http://www.next-second.com/s/pypyodbc_tutorial_en.htm)



## Download & Install ##
**[Download the package from PYPI](https://pypi.python.org/pypi/pypyodbc/)**
, unzip to a folder, **double click the setup.py file**, or run
```
setup.py install
```

Or if you have pip available:
```
pip install pypyodbc
```


Or, if you want to try the dev version, get the **unstable** pypyodbc.py  from
<font size='4'><b><a href='https://github.com/jiangwen365/pypyodbc'>GitHub</a></b></font> (Main Development site) and import it in your codes.





## Linux setting up ##
### [Configure Linux ODBC in 3 steps](http://code.google.com/p/pypyodbc/wiki/Linux_ODBC_in_3_steps) ###

[Config FreeTDS](http://www.pauldeden.com/2008/12/how-to-setup-pyodbc-to-connect-to-mssql.html)

[Config FreeTDS(pymssql doc)](http://code.google.com/p/pymssql/wiki/FreeTDSconf)





---








# [Report a bug](https://code.google.com/p/pypyodbc/issues/list) #



# [BBS](http://tech.groups.yahoo.com/group/pypyodbc/messages) #


### History ###


**Version 1.3.3 May 25 2014**

[Setting connection timeout, login timeout, query timeout are now well supported](https://code.google.com/p/pypyodbc/wiki/Timeout)

close [Issue 42](https://code.google.com/p/pypyodbc/issues/detail?id=42) only set read only of connection when explicitly required.


**Version 1.3.2 May 24 2014**

close [Issue 37](https://code.google.com/p/pypyodbc/issues/detail?id=37), now you can set connecton.timeout or use cursor.set\_timeout(timeout) to set the time when a query should time out. Thanks Aleksey!

**Version 1.3.1 Mar 11 2014**

close [Issue 36](https://code.google.com/p/pypyodbc/issues/detail?id=36), handling of datetime stamps

**Version 1.3.0 Feb 12 2014**

Performance enhancements in reading result sets with multiple columns; see the updated [How is the speed?](https://code.google.com/p/pypyodbc/wiki/speed)

close [Issue 33](https://code.google.com/p/pypyodbc/issues/detail?id=33) and [Issue 35](https://code.google.com/p/pypyodbc/issues/detail?id=35)

Now [download the package from PYPI](https://pypi.python.org/pypi/pypyodbc/), because google code has closed its download service.


**Version 1.2.1 Nov 16 2013**

Fixed error handle deallocation of cursor and connection in [Issue 26](https://code.google.com/p/pypyodbc/issues/detail?id=26): memory leak of cursor and connection gc failure. Thanks to Upday7;

Merged the patch contributed by phus.lu in [Issue 25](https://code.google.com/p/pypyodbc/issues/detail?id=25): experimental patch for gevent support, Thanks phus.lu!

**Version 1.2.0 Sep 21 2013**

Fix some issues on Linux & Darwin. Also a fix about setting connection timeout.


**Version 1.1.5 July 11 2013**

Fix [Issue 18](https://code.google.com/p/pypyodbc/issues/detail?id=18): Reuse of prepared statement


**Version 1.1.3 July 8 2013**

Speed improvements and Python 3.x fixes


**Version 1.1.1 Apr 4 2013**

Now you can get a field's value of a row by: row['field name'];

Move defination of constants near type mapping for better code readbiliy;



**Version 1.1.0 Apr 3 2013**

Better None value handling in a Binary Parameter;

Added a get() method for Row object, with which you can reference by column name;

Bugs fix for prepare statement.


**Version 1.0.11 Mar 23 2013**

Fix the ANSI drive + Python 3 error handling;

Add a win\_connect\_mdb function for easier connect to a mdb file on Windows

**Version 1.0.6 Mar 12 2013**

Fix the error when None value in a parameter


**Version 1.0.5 Mar 10 2013**

Fix several bugs under Python 3.x;

Add Mac / iODBC platform support;

Improved ODBC ANSI / unicode mode support;


**Version 1.0.0 Feb 21 2013**
PyPyODBC now is compatible with Python 3.3


**Version 0.9.3 Feb 9 2013**
Better ODBC library finding approach on Linux.


**Version 0.9.2 Feb 3 2013**
pypyodbc now can run under Python 2.4 (with the non-built-in ctypes lib) - Chris Clark;

Better parameters type conversion detection - Sok Ann Yap;

Raise exception for creating/compact mdb file failure and call from non-windows platforms


**Version 0.9.1 Jan 13 2013**
pypyodbc now can run under Python 2.5
Thanks Chris Clark for the patch :)

**Version 0.9.0 Jan 11 2013**
Enhance multi-threaded, 64-bit environment with Linux (wide Python build) and
unixODBC;

Thanks Sok Ann Yap for those patches :)

**Version 0.8.7 Oct 18 2012**
Added output converter function;
fix result description;
Cursor iteration protocol;
Accept connection string in parameters format;

**Version 0.8.6 Sep 23 2012**
Added ODBC pooling feature;
Bit, GUID type support;
Other fixes and improvements;

**Version 0.8.5 Sep 16 2012**
Numeric type fix;
Long and integer differentiate ;
other pyodbc compatibility improvements;

**Version 0.8.4 Sep 09 2012**
Improved compatibility with pyodbc;
Many underlying bug fixes;


**Version 0.8.3 Sep 1 2012**
sql\_longvarchar handling fix;
performance optimization;

**Version 0.8.2 Aug 27 2012**
Differentiate sql\_varchar and sql\_longvarchar;
Initial support for [SQLAlchemy](http://www.sqlalchemy.org/);


**Version 0.8.1 Aug 26 2012**
Fixed the long type parameter issue;
Added support for [IronPython](http://ironpython.codeplex.com/);


**Version 0.8 Aug 25 2012**
Added getinfo method;


**Version 0.7 Jul 28 2012**
Fixed nchar/ntext/nvarchar string truncat problem ;


**Version 0.6 Jul 4 2012**
Added Cursor.commit() and Cursor.rollback();
Added readonly keyword to connect;


**Version 0.5 Jun 23 2012**
Initial release;

### Thanks ###
Thanks to Michele Petrazzo, pypyodbc started from his code of RealPyODBC 0.1 beta, which initially implemented ODBC functions with ctypes in python in year 2004.

Thanks to the author of [pyodbc](http://code.google.com/p/pyodbc), I have been using pyodbc in most of my products for years with great results. Besides, PyPyODBC references its API designs, implementations and tests.