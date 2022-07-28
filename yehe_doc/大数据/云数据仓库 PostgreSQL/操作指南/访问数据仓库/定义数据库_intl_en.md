## Database Creation and Management
You can create database objects in CDWPG.
1. To create a database for your own use, create a user, grant authorization, and log in as instructed in [Managing User Permissions](https://intl.cloud.tencent.com/document/product/1138/45127). Then, use the `CREATE DATABASE` statement to create the database. Before database creation, make sure that the logged-in user has `CRAETEROLE` permissions. For more information on permissions, see [Managing User Permissions](https://intl.cloud.tencent.com/document/product/1138/45127). A sample database can be created as follows:
```
CREATE DATABASE test;
```
All databases can be listed via `\l`.
2. A database is usually created based on a template database, and the default template is empty. Any objects in the template will be in the newly created database. You can also specify a template for creation. For example, create a table in the `test` database first by using the following statement.
```
create table ttable (age int, id int);
```
Then, create the `test2` database with `test` as the template.
```
CREATE DATABASE test2 TEMPLATE test;
```
Switch to `test2`, and you can see that `ttable` also exists in `test2`. Therefore, avoid creating any objects in `template1`, as those in `template1` will also exist in databases created based on it. You can view all the tables in the selected database with `\d`.

![](https://main.qcloudimg.com/raw/8ba903080f7f7edebbd50e881b78e4cf.png)

3. You can list all the databases with `\l`.

![](https://main.qcloudimg.com/raw/7d2a2b6cceb52670e480d8a9a844208d.png)

4. You can delete the database with `DROP DATABASE`. When you perform the deletion operation, make sure that the logged-in user is a superuser or a general user with the permission of database deletion. Note that the database can be deleted only if the number of its connections is 0; for example:
![](https://main.qcloudimg.com/raw/b74b0ac10a534b05010a2f614360a06f.png)

You can see that when you select `test2`, the number of connections to `test2` must be greater than or equal to 1. You can only delete `test2` after switching to `test`.

## Schema Creation and Management
In CDWPG, a schema is a logical concept for a more detailed division of the database space. Each database has a schema named `public` when it is created. Tables with the same name cannot be created in the same database unless they are in different schemas. The database system identifies a table in the form of `database.schema.table`. In addition, schemas with the same name can be created in different databases.

1. Create a schema.
```
CREATE SCHEMA testschema;
```
2. Specify the schema to create objects.
When creating tables, functions, or other objects, you can add schema prefixes to indicate that they are to be created in different schemas; if no prefixes are added, objects will be created in the `public` schema by default; for example:
```
CREATE TABLE testschema.test;
```
3. Set the priority of the schema.
```
ALTER DATABASE test set search_path to testshcema,public;
```
This statement sets the `testschema` of the `test` database to `public` mode and indicates that `testschema` has the highest priority. If no schema prefixes are added, `testschema` will be matched first.
4. Switch the schema.
```
SET search_path TO public;
```
If the current schema is `testschema`, you can switch to `public` with this statement.
5. Delete the schema.
```
DROP SCHEMA testschema;
```

## Table Creation and Management
1. Set table and column constraints.
 - `CHECK` constraint, which specifies that a data column must satisfy a certain expression, such as:
```
CREATE TABLE products (product_no int, name text, price int CHECK(price > 0));
```
 - `NOT NULL` constraint, which specifies that a data column cannot be empty, such as:
```
CREATE TABLE products (product_no int NOT NULL, name text NOT NULL, price int CHECK(price > 0));
```
2. Set the data distribution policy.
A distributed database warehouse delivers the best performance when the amount of data stored in each node is the same. If data distribution is unbalanced, nodes with more data will spend more time completing queries, which compromises the overall query performance.
 - Hash distribution: You can use the `DISTRIBUTED BY` syntax to specify hash distribution when creating a table. This policy combines all the keys specified as hash distribution and determines the result of data distribution by the hash algorithm. The statement is as follows:
```
CREATE TABLE test (id int, age int) DISTRIBUTED BY (id);
```
 - Random distribution: You can use the `DISTRIBUTED RANDOMLY` syntax to specify random distribution when creating a table. As the name suggests, this policy determines data distribution randomly. The statement is as follows:
```
CREATE TABLE test (id int, age int) DISTRIBUTED RANDOMLY;
```
Here, you must specify one of the data distribution policies for columns with `PRIMARY KEY` or `UNIQUE`. For other columns, the first column will be used as the reference for data distribution by default, and the default data distribution policy will be hash distribution.

## View Creation and Management
A view is a logical concept. Unlike a table, it has no actual corresponding data structures on the disk.
1. Create a view.
```
CREATE VIEW testview AS SELECT * FROM ttable where age=28;
```
Create the `testview` view with all rows in `ttable` that satisfy the condition "age=28".
2. Delete the view.
```
DROP VIEW testview;
```

