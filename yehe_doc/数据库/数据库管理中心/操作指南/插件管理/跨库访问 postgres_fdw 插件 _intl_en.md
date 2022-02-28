## Overview
Foreign data wrapper (FDW) is an extension provided by PostgreSQL for accessing external data sources, including other databases in the same instance and other instances.
1. Install the FDW extension by running `CREATE EXTENSION`.
2. Run the `CREATE SERVER` statement to create a foreign server object for each remote database to be connected to, and specify connection information except `user` and `password` as the options for the server.
3. Run the `CREATE USER MAPPING` statement to create a user mapping for each database to be accessed through the foreign server, and specify the remote database's username and password as the `user` and `password` of the mapped user.
4. Run the `CREATE FOREIGN TABLE` statement to create a foreign table for each remote table to be accessed. The corresponding columns of the foreign table must match those of the remote table. You can also use different table and column names in the foreign table than the remote table, provided that you have the correct remote object name as an option to create the foreign table object.

As FDW supports cross-instance access, for security reasons, TencentDB for PostgreSQL optimizes access control over the creation of foreign server objects and implements categorized management based on the environment of the target instance. Auxiliary parameters are added to the open-source edition to verify user identity and adjust network policies.

## Auxiliary parameters of postgres_fdw    
 - host
   IP of the target instance. This parameter is required by `postgres_fdw`.
 - port
   Port of the target instance. This parameter is required.
 - instanceid
   Resource ID of the target instance. This parameter is required.
    1. If the target instance is a TencentDB instance, it is the ID of the TencentDB instance in the format of `postgres-xxxxxx` or `pgro-xxxxxx`, which can be viewed in the [console](https://console.cloud.tencent.com/postgres). For example, it is as follows for TencentDB for PostgreSQL:
![](https://qcloudimg.tencent-cloud.cn/raw/e448aa050e89de0f72376d8029d770e9.png)
    2. If the target instance is a CVM instance, it is the ID of the CVM instance in the format of `ins-xxxxx`.
![](https://qcloudimg.tencent-cloud.cn/raw/e1cfb70868e6ed4c31f9f633a8401148.png)
 - access_type
   Type of the target instance. This parameter is optional:
   1: the target instance is a TencentDB instance, such as TencentDB for PostgreSQL. If no other types are explicitly specified, this will be the default type.
 - uin
   ID of the account to which the instance belongs, which is used for verifying user permissions and can be viewed in [Account Info](https://console.cloud.tencent.com/developer). This parameter is optional.
 - own_uin
   ID of the root account to which the instance belongs, which is also needed for verifying user permissions. This parameter is optional.

### References
[CREATE SERVER on v9.3](https://www.postgresql.org/docs/9.3/static/sql-createserver.html)
[CREATE SERVER on v9.5](https://www.postgresql.org/docs/9.5/static/sql-createserver.html)
[CREATE SERVER on v10](https://www.postgresql.org/docs/10/sql-createserver.html)
[CREATE SERVER on v11](https://www.postgresql.org/docs/11/sql-createserver.html)
[CREATE SERVER on v12](https://www.postgresql.org/docs/12/sql-createserver.html)
[CREATE SERVER on v13](https://www.postgresql.org/docs/13/sql-createserver.html)

## postgres_fdw Demo
The `postgres_fdw` extension can be used to access data from other databases in the same instance or other instances.

### Step 1. Prepare
1. Create test data in the instance.
```
postgres=>create role user1 with LOGIN  CREATEDB PASSWORD 'password1';
postgres=>create database testdb1;
CREATE DATABASE
```
>! If an error occurs during creation, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
2. Create test data in the target instance.
```
postgres=>create role user2 with LOGIN  CREATEDB PASSWORD 'password2';
postgres=> create database testdb2;
CREATE DATABASE
postgres=> \c testdb2 user2
You are now connected to database "testdb2" as user "user2".
testdb2=> create table test_table2(id integer);
CREATE TABLE
testdb2=> insert into test_table2 values (1);
INSERT 0 1
```

### Step 2. Create the postgres_fdw extension
```
# Create
postgres=> \c testdb1
You are now connected to database "testdb1" as user "user1".
testdb1=> create extension postgres_fdw;
CREATE EXTENSION
# View
testdb1=> \dx
                            List of installed extensions
      Name     | Version |   Schema   |                    Description
--------------+---------+------------+----------------------------------------------------
  plpgsql      | 1.0     | pg_catalog | PL/pgSQL procedural language
  postgres_fdw | 1.0     | public     | foreign-data wrapper for remote PostgreSQL servers
(2 rows)
```

### Step 3. Create a server
The target instance is a TencentDB instance.
```
# Access the data of the target instance `testdb2` from the instance `testdb1`
testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', instanceid 'postgres-xxxxx');
CREATE SERVER
```

### Step 4. Create a user mapping
```
testdb1=> create user mapping for user1 server srv_test1 options (user 'user2',password 'password2');
CREATE USER MAPPING
```

### Step 5. Create a foreign table
```
testdb1=> create foreign table foreign_table1(id integer) server srv_test1 options(table_name 'test_table2');
CREATE FOREIGN TABLE
```

### Step 6. Access data from foreign table
```
testdb1=> select * from foreign_table1;
  id
----
   1
(1 row)
```

### References
[postgres_fdw](https://www.postgresql.org/docs/9.5/postgres-fdw.html)
