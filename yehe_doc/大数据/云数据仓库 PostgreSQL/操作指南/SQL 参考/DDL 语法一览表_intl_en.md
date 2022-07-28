## Defining Database
A database is the warehouse for organizing, storing, and managing data. Defining a database includes: creating a database, altering the database attributes, and dropping the database. For related SQL statements, see the table below.

#### SQL statements for defining database

| Feature           | SQL Statement         |
| -------------- | --------------- |
| Create a database     | CREATE DATABASE |
| Alter database attributes | ALTER DATABASE  |
| Drop a database     | DROP DATABASE   |


## Defining Schema
A schema is the set of a group of database objects and is used to control the access to the database objects. For related SQL statements, see the table below.

#### SQL statements for defining schema

| Feature         | SQL Statement       |
| ------------ | ------------- |
| Create a schema     | CREATE SCHEMA |
| Alter schema attributes | ALTER SCHEMA  |
| Drop a schema     | DROP SCHEMA   |

## Defining Table
A table is a special data structure in a database and is used to store data objects and the relationship between data objects. For related SQL statements, see the table below.

#### SQL statements for defining table

| Feature         | SQL Statement       |
| ---------- | ------------ |
| Create a table     | CREATE TABLE |
| Alter table attributes | ALTER TABLE  |
| Drop a table     | DROP TABLE   |

## Defining Partitioned Table
A partitioned table is a logical table used to improve query performance and does not store data (data is stored in common tables). For related SQL statements, see the table below.

#### SQL statements for defining partitioned table

| Feature         | SQL Statement       |
| -------------- | ------------------------------------ |
| Create a partitioned table     | CREATE TABLE ….PARTITION BY…         |
| Create a partition       | ALTER TABLE …ADD PARTITION…          |
| Alter partitioned table attributes | ALTER TABLE …RENAME/SPLIT PARTITION… |
| Drop a partition       | ALTER TABLE ….DROP PARTITION …       |
| Drop a table         | DROP TABLE                           |

## Defining Index
An index indicates the sequence of values in one or more columns in a database table. It is a data structure that improves the speed of data access to specific information in a database table. For related SQL statements, see the table below.

#### SQL statements for defining index

| Feature         | SQL Statement       |
| ------------ | ------------ |
| Create an index     | CREATE INDEX |
| Alter index attributes | ALTER INDEX… |
| Drop an index     | DROP INDEX   |
| Rebuild an index     | REINDEX      |

## Defining Role
A role is used to manage permissions. For database security, all management and operation permissions can be assigned to different roles. For related SQL statements, see the table below.

#### SQL statements for defining role

| Feature         | SQL Statement       |
| ------------ | ----------- |
| Create a role     | CREATE ROLE |
| Alter role attributes | ALTER ROLE… |
| Drop a role     | DROP ROLE   |

## Defining User
A user is a database role with the `LOGIN` privilege by default. For related SQL statements, see the table below.

#### SQL statements for defining role

| Feature         | SQL Statement       |
| ------------ | ----------- |
| Create a role     | CREATE USER |
| Alter role attributes | ALTER USER  |
| Drop a role     | DROP USER   |

## Creating Function

| Feature         | SQL Statement       |
| ------------ | --------------- |
| Create a function     | CREATE FUNCTION |
| Alter function attributes | ALTER FUNCTION  |
| Drop a function     | DROP FUNCTION   |

## Defining View
A view is a virtual table exported from one or several basic tables. It is used to control data accesses for users. For related SQL statements, see the table below.

| Feature         | SQL Statement       |
| -------- | ----------- |
| Create a view | CREATE VIEW |
| Drop a view | DROP VIEW   |

## Manipulating Session
A session is a connection established between the user and the database. For related SQL statements, see the table below.

| Feature         | SQL Statement       |
| -------- | ------------- |
| Alter a session | ALTER SESSION |
| Drop a view | DROP VIEW     |

## Defining Resource Queue
A load group is a system table used by the load management module to specify the number of concurrent jobs that can run in the associated resource pool. For related SQL statements, see the table below.

| Feature         | SQL Statement       |
| ------------ | --------------------- |
| Create a resource queue | CREATE RESOURCE QUEUE |
| Drop a resource queue | DROP RESOURCE QUEUE   |
| Alter a resource queue | ALTER RESOURCE QUEUE  |

