Apache Hadoop Hive is integrated with the Thrift service. Thrift, created by Facebook, is an interface definition language and binary communication protocol used for defining and creating services for numerous languages. HiveServer2 is based on Thrift, allowing many languages such as Java and Python to call Hive's APIs.
This section describes how to connect to HiveServer2 using Python.
## 1. Prerequisites 
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the Hive component on the software configuration page. 
- Hive and its dependencies are installed under the EMR cluster directory `/usr/local/service/` 

## 2.	Viewing Parameters
First, log in to any node (preferably a master one) in the EMR cluster. For more information about how to log in to EMR, see [Logging in to a Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can use WebShell to log in.  Click *Login* button on the right of the desired CVM instance and then enter the login page. The default username is root, and the password is the one you set when you created the EMR cluster. Once your credentials have been validated, you can access the command-line interface.
Run the following command in EMR command-line interface to switch to the Hadoop user, then go to the Hive installation folder:
```
[root@172 ~]# su Hadoop
[hadoop@172 root]$ cd /usr/local/service/hive/
[hadoop@172 hive]$
```
View the parameters that need to be used in the program:
```
[hadoop@172 hive]$ vim conf/hive-site.xml

<property>
        <name>hive.server2.thrift.bind.host</name>
        <value>$hs2host</value>
</property>
<property>
        <name>hive.server2.thrift.port</name>
        <value>$hs2port</value>
</property>
```
Here, $hs2host is the hostID of your HiveServer2, and $hs2port is the port number of your HiveServer2.

## 3. Using Python to Manipulate Hive
To manipulate Hive with a Python program, you need to install pip:
```
[hadoop@172 hive]$ su
[root@172 hive]# pip install pyhs2
```
Switch back to the Hadoop user after the installation is completed.
Create a Python file named hivetest.py in the `/usr/local/service/hive/` directory and add the following code:
```
#!/usr/bin/env python

import pyhs2
import sys

default_encoding = 'utf-8'

conn = pyhs2.connect(host='$hs2host',
                                  port=$hs2port,
                                  authMechanism='PLAIN',
                                  user='hadoop',
                                  password='',
                                  database='default',)


tablename = 'HiveByPython'
cur = conn.cursor()
print 'show the databases: '
print cur.getDatabases()

print "\n"
print 'show the tables in default: '
cur.execute('show tables')
for i in cur.fetch():
        print i

cur.execute('drop table if exists ' + tablename)
cur.execute('create table ' + tablename + ' (key int,value string)')

print "\n"
print 'show the new table: '
cur.execute('show tables ' +"'" +tablename+"'")
for i in cur.fetch():
        print i

print "\n"
print "contents from " + tablename + ":";
cur.execute('insert into ' + tablename + ' values (42,"hello"),(48,"world")')
cur.execute('select * from ' + tablename)
for i in cur.fetch():
        print i
```
>**Note:** You should replace $hs2host and $hs2port here with the hostID and port number of the HiveServer2 you queried, respectively.

After connecting to HiveServer2, this program outputs all the databases first and then displays the tables in the "default" database. Create a table named "hivebypython", insert two data entries into it, and output them. Run the program:
```
[hadoop@172 hive]$ ./hivetest.py
show the databases: 
[['default', ''], ['hue_test', ''], ['test', '']]


show the tables in default: 
['dd']
['ext_table']
['hive_test']
['hivebypython']


show the new table: 
['hivebypython']


contents from HiveByPython:
[42, 'hello']
[48, 'world']
[root@172 /]# ./hivetest3.py 
show the databases: 
[['default', ''], ['hue_test', ''], ['test', '']]


show the tables in default: 
['dd']
['ext_table']
['hive_test']
['hivebypython']


show the new table: 
['hivebypython']


contents from HiveByPython:
[42, 'hello']
[48, 'world']
```
