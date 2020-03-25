There are two ways to create a Cloud Object Storage (COS) database:

1. Create the whole database in COS

    To do so, run the following statement:
    ``` sql
    create database hivewithcos location 'cosn://huadong/hive';
    ```
    Here, huadong is the bucket name, and hive is the path, which can be set as needed. After creating the database, you can create a data table.

    ``` sql
    create table record(id int, name string) row format delimited fields terminated by ',' stored as textfile;
    ```

    Then, load data into the table, which can be used in exactly the same way as HDFS.

2. Move the specified table into COS

    First, select or create a database in Hive. Then move the specified table into COS by running the following statement:

    ``` sql
    create table record(id int, name string) row format delimited fields terminated by ',' stored as textfile location 'cosn://huadong/hive/cos';
    ```

    Load data into the table. Now the table is stored in COS.
