# IronPython running SQLAlchemy with pypyodbc #

With the pure Python DBABI 2.0 compliant ODBC library, pypyodbc, by simply extending SQLAlchemy, IronPython also can use SQLAlchemy. There are four steps to do so:

### Install pypyodbc for IronPython ###

  * **Step 1:** [Download PyPyODBC Source Package](https://code.google.com/p/pypyodbc/downloads/list), unzip the package, then copy the file pypyodbc.py to the IronPython instance's site-packages directory: IronPython 2.7\Lib\site-packages.

> This installs pypyodbc for IronPython. Now you can try if "**import pypyodbc**" succeeds in IronPython's interactive window.

### Install SQLAlchemy for IronPython ###
You can skip this step if you know how to install SQLAlchemy for IronPython. [Download SQLAlchemy Source Package](https://pypi.python.org/pypi/SQLAlchemy) (It seems currently only 0.7.x can run under IronPython, not version 0.8.x ), unzip the package, then just copy the sub-folder **sqlalchemy** located under the unzipped folder 'SQLAlchemy-0.7.10.tar\SQLAlchemy-0.7.10\lib\' to IronPython instance's site-packages directory: IronPython 2.7\Lib\site-packages.
> This installs pypyodbc for IronPython. Now you can try if "**import sqlalchemy**" succeeds in IronPython's interactive window.


### Extend SQLAlchemy drivers ###
Then we simply extend SQLAlchemy so it can use the pypyodbc library installed in the steps above.

  * **Step 2:** Create a copy of IronPython 2.7\Lib\site-packages\sqlalchemy\**connectors**\pyodbc.py and rename it to pypyodbc.py, then text replace all "pyodbc" to "pypyodbc" in the new pypyodbc.py.

  * **Step 3:** Create a copy of IronPython 2.7\Lib\site-packages\sqlalchemy\**dialects\mssql**\pyodbc.py and rename it to pypyodbc.py, and then text replace all "pyodbc" to "pypyodbc" in the new pypyodbc.py.

  * **Step 4:** Modify IronPython 2.7\Lib\site-packages\sqlalchemy\**dialects\mssql**\`__init__.py`, in the top import line, add **pypyodbc** after mxodbc, like this:

```
from sqlalchemy.dialects.mssql import base, pyodbc, adodbapi, \ 
                                       pymssql, zxjdbc, mxodbc, pypyodbc
```

Now you can use SQLAlchemy with below code:
```
import sqlalchemy
engine = sqlalchemy.create_engine('mssql+pypyodbc://MSSQL_DSN')
for row in engine.execute('select * from aTable'):
    print (row)
```

