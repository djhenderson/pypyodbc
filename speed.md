With the [simple benchmark script](https://github.com/jiangwen365/pypyodbc/raw/master/speed.py) on GitHub, below is the performance scores on Windows



---

# Access mdb database #
The seconds used to operate 20,000 records on my Lenovo Dual-Core Celeron 2.1G , 3G RAM laptop :


### pypyodbc on CPython 2.7.6 ###
Running with pypyodbc 1.3.0
> Write time: 9.97799992561
> R & W time: 11.7869999409
> Read  time: 0.910000085831


### pypyodbc on CPython 2.7.6 ###
Running with pypyodbc 1.2.1
> Write time: 9.7380001545
> R & W time: 12.2130000591
> Read  time: 1.60899996758


### [pyodbc](http://code.google.com/p/pyodbc) on CPython 2.7.6 ###
Running with pyodbc 3.0.6
> Write time: 12.9730000496
> R & W time: 12.5540001392
> Read  time: 0.18799996376

### pypyodbc on PyPy 2.3 (after JIT started) ###
Running with pypyodbc 1.3.2
odbcjt32.dll
> Write time: 7.72200012207
> R & W time: 9.39100003242
> Read  time: 0.483999967575

### pypyodbc on PyPy 2.2 (after JIT started) ###
Running with pypyodbc 1.2.1
> Write time: 9.57299995422
> R & W time: 10.9049999714
> Read  time: 0.707999944687

### pypyodbc on IronPython 2.7.4 ###
Running with pypyodbc 1.2.1
> Write time: 10.2185821533
> R & W time: 15.8019104004
> Read  time: 2.62014770508



---

# SQLServer #
The seconds used to operate 20,000 records:

### pypyodbc on CPython 2.7.6 ###
Running with pypyodbc 1.3.0
sqlncli10.dll
> Write time: 13.2389998436
> R & W time: 15.9130001068
> Read  time: 0.920000076294

### pypyodbc on CPython 2.7.6 ###
Running with pypyodbc 1.2.1
sqlncli10.dll
> Write time: 12.4639999866
> R & W time: 15.6489999294
> Read  time: 1.54399991035

### [pyodbc](http://code.google.com/p/pyodbc) on CPython 2.7.6 ###
Running with pypyodbc 3.0.6
sqlncli10.dll
> Write time: 10.4210000038
> R & W time: 10.6079998016
> Read  time: 0.141000032425

### pypyodbc on PyPy 2.2 (after JIT started) ###
Running with pypyodbc 1.3.0
sqlncli10.dll
> Write time: 12.7769999504
> R & W time: 15.1629998684
> Read  time: 0.470999956131

### pypyodbc on PyPy 2.2 (after JIT started) ###
Running with pypyodbc 1.2.1
sqlncli10.dll
> Write time: 12.1679999828
> R & W time: 14.9449999332
> Read  time: 0.763999938965