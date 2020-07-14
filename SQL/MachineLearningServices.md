# SQL Machine Learning Services
Machine Learning Services is a feature in SQL Server that gives the ability to run Python and R scripts with relational data. <br/>
[Install Machine Learning Services](https://docs.microsoft.com/en-us/sql/machine-learning/install/sql-machine-learning-services-windows-install?view=sql-server-ver15)
<br/><br/>
``` SQL (type)
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
'
```
The correct result is calculated and the Python print function returns the result to the Messages window.
<br/><br/>
STDOUT message(s) from external script:
0.5 2

