---
layout: post
title: Restoring Siebel 6 attachments - Python script
date: 2015-11-19 02:36:28.000000000 -02:00
published: true
status: publish
categories: oracle python scripts siebel
comments: true
---
Hi all, here is my solution to make the Siebel 6.3 attachments restore easier. Following the rules of automating boring stuff with Python, I did the script that I'm sharing with you guys. Enjoy!
It is also on my Github: [restoreSiebelAttachments]

{% highlight ruby %}
import os
import glob
import sys
import cx_Oracle


row_id = raw_input("Enter ROW_ID: ")
row_id = str(row_id)

SQL = '''
SELECT
      FILE_REV_NUM
   FROM
       SIEBEL.S_ACCNT_ATT
   WHERE
      (row_id = '%s')
''' % (row_id)

#connection with Oracle DB
print "Connecting with the Database..."
connstr = 'USERNAME/PASSWORD@HOST:PORT/SERVICENAME'
connection = cx_Oracle.connect(connstr)

if connection:
    print "Database connection SUCESS..."
else:
    print "Database connection ERROR"

cursor = connection.cursor()

for row in cursor.execute(SQL):
    print "FILE_REV_NUMBER: %s" % row

cursor.close()
connection.close()


print "Searching for .SAF file"

for filename in glob.glob('\\NETWORK-PATH\*\S_ACCNT_ATT_%s_%s.SAF' % (row_id, row[0])):
    print "FILE FOUND: \t", filename.split('\')[-1]
    arquivo = filename.split('\')[-1]
    arquivo = str(arquivo)
    #split the filepath
    Dir = filename.split('\')[-2]
    print "FOLDER FOUND: %s" % Dir
    print "copying files..."


source = "\\NETWORK-PATH-ORIGIN\%s\%s" % (Dir, arquivo)
target = "\\NETWORK-PATH-DESTINATION\%s" % (Dir)

output = os.system ("""xcopy "%s" "%s" """ % (source, target))

print "ATTACHMENTS RESTORED!!!"
{% endhighlight %}


What the script does? You pass the ROW_ID and the script takes care of the rest. It will look at the database, find the FILE_REV_NUMBER, look at the purge folder and restore the attachment based on the ROW_ID that you entered.  
Any questions? Please leave a comment below.

[restoreSiebelAttachments]: https://github.com/andrealmar/scripts/blob/master/restoreSiebelAttachments.py
