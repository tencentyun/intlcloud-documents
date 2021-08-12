There are two ways to create a Cloud Object Storage (COS) data warehouse:

### Method 1: Creating Whole Database in COS
To do so, run the following statement:
``` sql
create database hivewithcos location 'cosn://huadong/hive';
```
Here, `huadong` is the bucket name, and `hive` is the path, which can be set as needed. After creating the database, you can create a data table. Then, load data into the table, which can be used in exactly the same way as HDFS.
``` sql
create table record(id int, name string) row format delimited fields terminated by ',' stored as textfile;
```


### Method 2: Moving Specified Table into COS
First, select or create a database in Hive. Then move the specified table into COS by running the following statement:
``` sql
create table record(id int, name string) row format delimited fields terminated by ',' stored as textfile location 'cosn://huadong/hive/cos';
```
Load data into the table. At this time, the table is stored in COS.
