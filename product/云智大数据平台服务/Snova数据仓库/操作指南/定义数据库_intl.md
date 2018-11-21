## Database Creation and Management

In Snova, you can create your own database objects.

1.If you want to create a database for your own use, you first need to create a user, authorize it and log in to it as per the instructions in [Manage User Permissions](https://cloud.tencent.com/document/product/878/20072), and then use the CREATE DATABASE statement to create a database. Before creating the database, you must ensure that the logged-in user has the CRAETEROLE permission. For more information on permissions, see [Manage User Permissions](https://cloud.tencent.com/document/product/878/20072). This following is an example of creating a database:

   ```
   CREATE DATABASE test
   ```

   All the databases can be listed using `\l`.

2.During the process of database creation, a database template is often selected for the new database. The default database template is empty. If there are any objects in the template, there will be the same objects in the new database too. You can also specify a template for creation. For example, first create a table in the database "test" using the following statement:

   ```
   create table ttable (age int, id int);
   ```

   Then create a database "test2" with "test" as the template:

   ```
   CREATE TABLE test2 TEMPLATE test;
   ```

   If switched to "test2", you can see that there is also a "ttable". Therefore, try not to create any objects in template1; otherwise, the databases created based on template1 will have the same objects. You can view all the tables in the selected database using `\c`.

   ![](https://main.qcloudimg.com/raw/8ba903080f7f7edebbd50e881b78e4cf.png)

3.All databases can be listed using `\l`.
   ![](https://main.qcloudimg.com/raw/7d2a2b6cceb52670e480d8a9a844208d.png)

4.You can delete a database using DROP DATABASE. When deleting, you must ensure that the logged-in user is a superuser or a general user with the permission to delete the database. Plus, the database can be deleted only if the number of connections to it is 0. For example:
   ![](https://main.qcloudimg.com/raw/b74b0ac10a534b05010a2f614360a06f.png)
   You can see that if a user selects "test2", the number of connections to "test2" is greater than or equal to 1. Only after switching to "test" can "test2" be deleted properly.

## Schema Creation and Management

In Snova, schema is used as a logical concept to partition the database space in a more detailed manner. Each database has a schema called "public" when it is created. You cannot create tables with the same name in a database, but you can choose to create tables with the same name in different schemas. The database system identifies a table in the form of database.schema.table. In addition, schemas with the same name can be created in different databases.

1.Create a schema

   ```
   CREATE SCHEMA testschema;
   ```

2.Create objects in a specified schema
   When creating objects such as tables and functions, you can add schema prefixes to indicate that these objects are created in different schemas. If no prefix is added, the creation happens in "public" by default, for example:

   ```
   CREATE TABLE testschema.test;
   ```

3.Set the priority of a schema

   ```
   ALTER DATABASE test set search_path to testshcema,public;
   ```

   This is to set the priority of the schema of the database "test". The schema with the highest priority is testschema. If no schema prefix is added, testschema is matched first.

4.Switch schemas

   ```
   SET search_path TO public;
   ```

   If it is currently in "testschema", you can use this statement to switch to "public".

5.Delete a schema

   ```
   DROP SCHEMA testschema;
   ```

## Table Creation and Management

1.Set table and column constraints

   - CHECH constraint, which specifies that the data in a column must satisfy a specific expression, for example:

     ```
     CREATE TABLE products (product_no int, name text, price int CHECK(price > 0));
     ```

    - NOT NULL constraint, which specifies that the data in a column cannot be empty, for example:

      ```
      CREATE TABLE products (product_no int NOT NULL, name text NOT NULL, price int CHECK(price > 0));
      ```
2.Data distribution policy
   For distributed data warehouses, the best processing performance can be achieved when the same amount of data is stored in each node. If the data distribution is not balanced, then the nodes with more data will consume more time to complete querying, resulting in lower performance of the entire query process.
   - Hash distribution: You can use the DISTRIBUTED BY statement to specify the hash distribution when creating a table, which combines all the keys specified for hash distribution and determines the data distribution result by the hash algorithm. The statement is as follows:
     ```
     CREATE TABLE test (id int, age int) DISTRIBUTED BY (id));
     ```
   - Random distribution: You can use the DISTRIBUTED RANDOMLY statement to specify the random distribution when creating a table, which, as the name implies, determines the data distribution result in a random manner. The statement is as follows:
     ```
     CREATE TABLE test (id int, age int) DISTRIBUTED RANDOMLY
     ```

   Columns with PRIMARY KEY or UNIQUE attributes must specify one of the data distribution policies. For columns without PRIMARY KEY or UNIQUE attributes, the first column will be used as the reference for data distribution by default, and the default data distribution policy is hash distribution.

## View Creation and Management

A view is a logical concept. Unlike a table, a view does not have an actual corresponding data structure on the disk.

1.Create a view

   ```
   CREATE VIEW testview AS SELECT * FROM ttable where age=28;
   ```
Create a view named "testview" for all rows in "ttable" that satisfy the condition "age=28".

2.Delete a view

   ```
   DROP VIEW testview;
   ```

