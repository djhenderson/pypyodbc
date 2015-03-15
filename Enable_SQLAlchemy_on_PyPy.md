# PyPy running SQLAlchemy with pypyodbc #

With the pure Python ODBC library, pypyodbc, by simply extending SQLAlchemy, PyPy also can use SQLAlchemy. There are four steps to do so:

### Install pypyodbc for PyPy ###

  * **Step 1:** [Download PyPyODBC Source Package](https://code.google.com/p/pypyodbc/downloads/list), unzip the package, then copy the file pypyodbc.py to the PyPy instance's site-packages directory: pypy-1.9\site-packages.

> This installs pypyodbc for PyPy. Now you can try if "**import pypyodbc**" succeeds in PyPy's interactive window.

### Install SQLAlchemy for PyPy ###
You can skip this step if you know how to install SQLAlchemy for PyPy. [Download SQLAlchemy Source Package](https://pypi.python.org/pypi/SQLAlchemy), unzip the package, then just copy the sub-folder **sqlalchemy** located under the unzipped folder 'SQLAlchemy-0.7.10.tar\SQLAlchemy-0.7.10\lib\' to PyPy instance's site-packages directory: pypy-1.9\site-packages.
> This installs pypyodbc for PyPy. Now you can try if "**import sqlalchemy**" succeeds in PyPy's interactive window.


### Extend SQLAlchemy drivers ###
Then we simply extend SQLAlchemy so it can use the pypyodbc library installed in the steps above.

  * **Step 2:** Create a copy of pypy-1.9\site-packages\sqlalchemy\**connectors**\pyodbc.py and rename it to pypyodbc.py, then text replace all "pyodbc" to "pypyodbc" in the new pypyodbc.py.



**For SQL Server**

---

  * **Step 3:** Create a copy of pypy-1.9\site-packages\sqlalchemy\**dialects\mssql**\pyodbc.py and rename it to pypyodbc.py, and then text replace all "pyodbc" to "pypyodbc" in the new pypyodbc.py.

  * **Step 4:** Modify pypy-1.9\site-packages\sqlalchemy\**dialects\mssql**\`__init__.py`, in the top import line, add **pypyodbc** after mxodbc, like this:

```
from sqlalchemy.dialects.mssql import base, pyodbc, adodbapi, \ 
                                       pymssql, zxjdbc, mxodbc, pypyodbc
```



**For MYSQL**

---

  * **Step 3:** Create a copy of pypy-1.9\site-packages\sqlalchemy\**dialects\mysql**\pyodbc.py and rename it to pypyodbc.py, and then text replace all "pyodbc" to "pypyodbc" in the new pypyodbc.py.

  * **Step 4:** Modify pypy-1.9\site-packages\sqlalchemy\**dialects\mysql**\`__init__.py`, in the top import line, add **pypyodbc** after cymysql, like this:

```
from . import base, mysqldb, oursql, \
                                pyodbc, zxjdbc, mysqlconnector, pymysql,\
                                gaerdbms, cymysql, pypyodbc
```








  * **Step 5:Now you can use SQLAlchemy with below code:
```
import sqlalchemy
engine = sqlalchemy.create_engine('mssql+pypyodbc://MSSQL_ODBC_DSN')
for row in engine.execute('select * from aTable'):
    print (row)
```
or for mysql
```
import sqlalchemy
engine = sqlalchemy.create_engine('mysql+pypyodbc://MYSQL_ODBC_DSN')
for row in engine.execute('select * from aTable'):
    print (row)
```**

