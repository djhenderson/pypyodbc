# Setup ODBC & FreeTDS in Linux in 3 steps for Python Database Programming #




---

In Linux, to connect to MS SQLServer, we need to install and configure ODBC and it's database drivers for Linux. To accomplish that, many tutorials listed complicated steps which might be hard to follow and understand.

To easy the process, I will list the minimum steps you need to do in 3 steps:


(The tutorial is based on the fresh installed Ubuntu 12.04 environment)

## 1. Install the ODBC module unixodbc for Linux, and the MSSQL ODBC Driver FreeTDS ##

In command-line terminal, enter command:
```
sudo apt-get install tdsodbc unixodbc
```

Explanation: tdsodbc is FreeTDS's key package, it contains the MSSQL odbc driver libtdsodbc.so; unixodbc is Linux's ODBC framework, the package contains critical binary files: libtdsodbc.so or libtdsodbc.so.1


## 2. Modify /etc/odbcinst.ini ##
If odbcinst.ini doesn't exist under /etc, create the file.
**Find the path to libtdsodbc.so.** If the path to the file is /usr/lib/x86\_64-linux-gnu/libtdsodbc.so, make sure you have the below content in the file.
```
[FreeTDS]
Driver = /usr/lib/x86_64-linux-gnu/odbc/libtdsodbc.so
```

**Note:** libtdsodbc.so is usually under /usr/lib/i386-linux-gnu/odbc/ on 32bit Linux, /usr/lib/x86\_64-linux-gnu/odbc/ on 64bit Linux, /usr/lib/odbc/ on older version Linux.


## 3. Modify /etc/freetds/freetds.conf ##
Make sure there are following lines under the "Global" section in the file:
```
[Global]
TDS_Version = 8.0
client charset = UTF-8
```


---

## At this point**, FreeTDS should be ready for use, we can use the pure Python ODBC library pypyodbc to test ##
```
import pypyodbc
conn = pypyodbc.connect('Driver=FreeTDS;Server=192.168.1.2;port=1433;uid=sa;pwd=pwd1;database=db_name')
print conn.cursor().execute('select * from a_table').fetchone()[0]
```**

Buttoned up yet?  

![http://pypyodbc.googlecode.com/files/Logo.png](http://pypyodbc.googlecode.com/files/Logo.png)