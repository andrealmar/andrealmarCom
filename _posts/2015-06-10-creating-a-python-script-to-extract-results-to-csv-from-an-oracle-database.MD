---
layout: post
title: Creating a Python script to extract results to CSV from an Oracle Database
date: 2015-06-10 16:21:54.000000000 -03:00
type: post
published: true
status: publish
categories:
- database
- oracle
- python
- scripts
comments: true
---
Maybe one day you guys will need to extract results from a Database and export to CSV. And the best way to do this is using a simple script using Python, a simple and elegant language. In my case, I needed simple stuff. Just extract the results from an Oracle Database in a CSV format. The output would be a report for the Business areas. Here are the steps I did in order to achieve the expected result.
First of all you need to install latest Python version

```
rpm -ivh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
sudo yum install python
sudo yum install python-devel
```

Now you need to to add the line

```
Defaults env_keep += "ORACLE_HOME"
```
in your _visudo_.

```
sudo visudo
```
and below the section

```
Adding HOME to env_keep may enable a user to run unrestricted commands via sudo.
```

add the line

```
Defaults env_keep += "ORACLE_HOME"
```

Now you need to install Python _pip_.
Make sure that you have the _ORACLE_HOME_ variable set. Don't forget that.

```
sudo yum install python-pip
```

and we can now install the _Oracle_CX_ library

```
sudo pip install cx_Oracle
```

All set. Below is the code as I used to start developing the script. It connects to a DEMO DB (which comes with Oracle 12c).
You can use it as a starting point for your needs.

```python
import os
import cx_Oracle
import csv
import time

#SQL command to extract the report WHATEVER.csv
SQL=''' select * from help where topic = 'ACCEPT' '''

#timestamp
timestr = time.strftime("%d-%m-%Y_%H:%M:%S")

filename='/interfaces/custom_sql/Extracao/utl_file_dir/WHATEVER'+timestr+'.csv'
FILE=open(filename,"w");
output=csv.writer(FILE, dialect='excel')

#setting system variables
#os.putenv('ORACLE_HOME', '/u01/app/oracle/product/12.1.0/dbhome_1')
#os.putenv('LD_LIBRARY_PATH', '/u01/app/oracle/product/12.1.0/dbhome_1/lib')

#connection with Oracle DB
print "Realizando conexao com o Banco de Dados..."
connection = cx_Oracle.connect('system/oracle@127.0.0.1/orcl')

cursor = connection.cursor()
cursor.execute(SQL)
for row in cursor:
	output.writerow(row)
cursor.close()
connection.close()
FILE.close()

print "END of extraction"
```

You can check the script on my GitHub also: [python_csv_report]  
<br />
See you next time!
[python_csv_report]: https://github.com/andrealmar/csv_report_script/blob/master/csv_report.py  
