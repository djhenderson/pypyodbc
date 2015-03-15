# Generally, the API of pypyodbc is quite similar to pyodbc. #

In most cases, you can simply try pypyodbc in your existing pyodbc powered script
with the following changes:

```
#import pyodbc                    <-- Comment out the original pyodbc importing line
import pypyodbc as pyodbc         # Let pypyodbc acting as the pyodbc

pyodbc.connect(...)               # Most original pyodbc calling lines requires no change.

```




Their known differences are listed below.


# Not existing features in pypyodbc #
  * query parameters format
```
cursor.execute("select a from tbl where b=? and c=?", x, y)   # This doesn't work
cursor.execute("select a from tbl where b=? and c=?", (x, y)) # This works

cursor.execute("select a from tbl where b=?", x)              # This doesn't work
cursor.execute("select a from tbl where b=?", (x, ))          # This works
```
  * field name as cursor attribute
```
cursor.execute("select album_id, photo_id from photos where user_id=1")

for row in cursor:
    print row.album_id, row.photo_id                          # This doesn't work

    print row['album_id'], row['photo_id']                    # This works

    print row[0], row[1]                                      # This works

    print row.get('album_id'), row.get('photo_id')            # This works
```


# Not existing features in pyodbc #
  * [Access MDB file creation and compacting functions](https://code.google.com/p/pypyodbc/wiki/pypyodbc_for_access_mdb_file), namely:
    * pypyodbc.win\_create\_mdb
    * pypyodbc.win\_connect\_mdb
    * pypyodbc.win\_compact\_mdb



# Speed difference with pyodbc #
> Download [odbc\_bench.py](https://github.com/jiangwen365/pypyodbc/blob/master/odbc_bench.py) from Github, and you can run benchmarks under pyodbc and pypyodbc

> To get the benchmark with pyodbc, run:
```
python odbc_bench.py pyodbc
```
> To get the benchmark with pypyodbc, run:
```
python odbc_bench.py
```



