[Psycopg](https://psycopg.org/) is a [PostgreSQL](https://www.postgresql.org/) adapter commonly used for the [Python](https://www.python.org/) programming language and can also be used to connect to TDSQL-A for PostgreSQL databases.

Psycopg2 needs to be deployed in advance. You can run the `pip install psycopg2` command for deployment.

Python 3.6 is used in all code samples below. If you use Python 2.x, you need to modify the code to make it compatible.

## Sample 1. Connecting to Database
```
conn.py
#coding=utf-8
#!/usr/bin/python
import psycopg2
try:
  conn = psycopg2.connect(database="v3", user="dbadmin", password="tdapg@tdapg", host="100.1.1.1", port="11345")
  print ("Database connection succeeded")
  conn.close()
except psycopg2.Error as msg:
  print ("Database connection failed. Error message: %s" %(msg.args[0])) 
```
![](https://main.qcloudimg.com/raw/b4683aeddc5afd2ad6b5193a2d2aa506.png)

## Sample 2. Creating Table
```
#coding=utf-8
#!/usr/bin/python
import psycopg2
try:
  conn = psycopg2.connect(database="v3", user="dbadmin", password="tdapg@tdapg", host="100.1.1.1", port="11345")
  print ("Database connection succeeded") 
  cur = conn.cursor()
  sql = """
     create table tdapg 
     (
       id int,
       nickname varchar(100)
     )     """
  cur.execute(sql)
  conn.commit()
  print ("Table creation succeeded")
  conn.close()
except psycopg2.Error as msg:
  print ("Tdapg Error %s" %(msg.args[0]))
```
![](https://main.qcloudimg.com/raw/c49aee177be94f8c0a2db48c90f6c2bc.png)

## Sample 3. Inserting Data
```
#coding=utf-8
#!/usr/bin/python
import psycopg2
try:
  conn = psycopg2.connect(database="v3", user="dbadmin", password="tdapg@Tdapg", host="100.1.1.1", port="11345")
  print ("Database connection succeeded")  
  cur = conn.cursor()
  sql = "insert into tdapg values(1,'tdapg'),(2,'tdapg');"
  cur.execute(sql)
  sql = "insert into tdapg values(%s,%s)"  
  cur.execute(sql,(3,'pg'))
  conn.commit()
  print ("Data insertion succeeded")  
  conn.close()
except psycopg2.Error as msg:
  print ("Database operation failed: %s" %(msg.args[0]))
```
![](https://main.qcloudimg.com/raw/8b9e60239a988518b5efdb7781c60bae.png)

## Sample 4. Querying Data
```
#coding=utf-8
#!/usr/bin/python
import psycopg2
try:
  conn = psycopg2.connect(database="v3", user="dbadmin", password="tdapg@Tdapg", host="100.1.1.1", port="11345")
  print ("Database connection succeeded") 
  cur = conn.cursor()
  sql = "select * from tdapg"
  cur.execute(sql)
  rows = cur.fetchall()
  for row in rows:
    print ("ID = %s NICKNAME = %s " %(row[0],row[1]))
  conn.close()
except psycopg2.Error as msg:
  print ("Database operation failed: %s" %(msg.args[0]))
```
![](https://main.qcloudimg.com/raw/e0e6a4f79ee5380da53ccc2d05f84907.png)

## Sample 5. Inserting Copied Data
```
#coding=utf-8
#!/usr/bin/python
import psycopg2
    try:
       conn = psycopg2.connect(database="postgres", user="dbadmin",
       password="", host="172.16.0.29", port="15432")
       print ("Database connection succeeded")
       cur = conn.cursor()
       filename = "/data/tbase/tdapg.txt"
       cols = ('id','nickname')
       tablename="public.tdapg"
       cur.copy_from(file=open(filename),table=tablename,columns=cols,sep=',')
       conn.commit()
       print ("Data import succeeded")
       conn.close()
    except psycopg2.Error as msg:
       print ("Database operation failed: %s" %(msg.args[0]))
```
