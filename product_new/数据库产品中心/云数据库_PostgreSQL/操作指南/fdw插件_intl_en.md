## Overview
Foreign Data Wrapper (FDW) is a type of extensions provided by PostgreSQL for accessing external data sources, including other databases in the current instance or other instances.
Based on the type of the target database instance, FDW extensions come in different forms, such as postgres_fdw, mysql_fdw, and mongo_fdw. The steps to use FDW are as follows:
 1. Run the `CREATE EXTENSION` statement to install the FDW extension.
 2. Run the `CREATE SERVER` statement to create a foreign server object for each remote database to be connected to, and specify connection information except `user` and `password` as the options for the server.
 3. Run the `CREATE USER MAPPING` statement to create a user mapping for each database to be accessed through the foreign server, and specify the remote database's username and password as the `user` and `password` of the mapped user.
 4. Run the `CREATE FOREIGN TABLE` statement to create a foreign table for each remote table to be accessed. The corresponding columns of the foreign table must match those of the remote table. You can also use different table and column names in the foreign table than the remote table, provided that you have the correct remote object name as an option to create the foreign table object.

As FDW supports cross-instance access, for security reasons, TencentDB for PostgreSQL optimizes access control over the creation of foreign server objects and implements categorized management based on the environment of the target instance. Auxiliary parameters are added to the open-source edition to verify user identity and adjust network policies.

## Auxiliary Parameters for CREATE SERVER
### 1. Auxiliary parameters for extensions such as postgres_fdw and mysql_fdw    

 - host
    IP of the target instance, which is used for postgres_fdw. This parameter is required.
 - address
    IP of the target instance, which is used for mysql_fdw. This parameter is required.
 - port
    Port of the target instance. This parameter is required.
 - instanceid
    Resource ID of the target instance. This parameter is required.
    1. If the target instance type is TencentDB, the parameter value will be the instance ID in the format of `postgres-xxxxx` or `mysql-xxxxx`, which can be viewed in the console. 
    2. If the target instance is on CVM, the parameter value will be the CVM instance ID in the format of `ins-xxxxx`.
 - access_type
    Type of the target instance. This parameter is optional:
    1: the target instance is a TencentDB for PostgreSQL or TencentDB for MySQL instance; if no other types are explicitly specified, this will be the default type.
    2: the target instance is on CVM.
    3: the target instance is a self-built instance with public IP in Tencent Cloud.
    4: the target instance is connected via Tencent Cloud VPN.
    5: the target instance is connected via a self-built VPN.
    6: the target instance is connected via Direct Connect.
    7: the target instance is COS data.
 - uin
    ID of the account to which the instance belongs, which is needed for verifying user permissions. This parameter is optional. For more information, please see [Querying uin](https://console.cloud.tencent.com/developer).
 - own_uin
    ID of the root account to which the instance belongs, which is also needed for verifying user permissions. This parameter is optional.
 - vpcid
    VPC ID. This parameter is optional; however, if the target instance is in a VPC of CVM, it will be required and can be viewed in the [VPC Console](https://console.cloud.tencent.com/vpc/vpc).
 - subnetid
    VPC subnet ID. This parameter is optional; however, if the target instance is in a VPC of CVM, it will be required and can be viewed on the subnet page in the [VPC Console](https://console.cloud.tencent.com/vpc/subnet).
 - dcgid
    Direct connect ID. This parameter is optional; however, it will be required if the target instance needs to be connected through Direct Connect.
 - vpngwid
    VPN gateway ID. This parameter is optional; however, it will be required if the target instance needs to be connected through a VPN.
 - region
    Region where the target instance resides; for example, "ap-guangzhou" represents the Guangzhou region. This parameter is optional; however, it is required for cross-region access.

### 2. Auxiliary parameters for COS_FDW
- host
Access domain name of COS, such as: `https://xxxx-xxxxxx.cos.ap-beijing.myqcloud.com`. This parameter is required.
- bucket
COS bucket name. This parameter is required.
- id
`SecretId` value of a TencentCloud API key, which is required and can be queried on the TencentCloud API key page in the [CAM Console](https://console.cloud.tencent.com/capi).
- key
`SecretKey` value of a TencentCloud API key, which is required and can be queried on the TencentCloud API key page in the [CAM Console](https://console.cloud.tencent.com/capi).

### 3. Support for FDW

| Name 			| Available Directly 				| Cross-region Use					|
| :- :			| :-: 						| :-: 						|
| postgres_fdw 	| Instances created before April 26, 2018 can use it after being restarted, while new instances can use it directly							| Not supported by default. You can [submit a ticket](https://console.cloud.tencent.com/workorder) for application 	|
| mysql_fdw 	| Instances created before April 26, 2018 can use it after being restarted, while new instances can use it directly							| Not supported by default. You can [submit a ticket](https://console.cloud.tencent.com/workorder) for application 	|
| cos_fdw 		| It is in beta test. You can [submit a ticket](https://console.cloud.tencent.com/workorder) for application	| Not supported by default. You can [submit a ticket](https://console.cloud.tencent.com/workorder) for application 	|

### 4. References

[CREATE SERVER (9.3)](https://www.postgresql.org/docs/9.3/static/sql-createserver.html)
[CREATE SERVER (9.5)](https://www.postgresql.org/docs/9.5/static/sql-createserver.html)

## Example of Using postgres_fdw
postgres_fdw can be used to access data from other databases in the current instance or other instances.

### 1. Prerequisites
1. Create test data in the current instance.
```
postgres=>create role user1 with LOGIN  CREATEDB PASSWORD 'password1';
postgres=>create database testdb1;
CREATE DATABASE
```
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


### 2. Create postgres_fdw
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

### 3. Create a server

1. The target instance is a TencentDB instance.
```
    # Access the data of `testdb2` in the target instance from `testdb1` in the current instance
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', instanceid 'postgres-xxxxx');
    CREATE SERVER
```
2. The target instance is on CVM, and the network is the basic network.
```
    testdb1=>create server srv_test foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx', dbname 'testdb2', port '5432', instanceid 'ins-xxxxx', access_type '2', region 'ap-guangzhou'，uin 'xxxxxx'，own_uin 'xxxxxx');
    CREATE SERVER
```
3. The target instance is on CVM, and the network is VPC.
```
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', instanceid 'ins-xxxxx', access_type '2', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', vpcid 'vpc-xxxxxx', subnetid 'subnet-xxxxx');
    CREATE SERVER
```

4. The target instance is a self-built instance with public IP in Tencent Cloud.
```
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', access_type '3', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx');
    CREATE SERVER 
```

5. The target instance is connected via Tencent Cloud VPN.
```
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', access_type '4', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', vpngwid 'xxxxxx');
```

6. The target instance is connected via a self-built VPN.
```
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', access_type '5', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', vpngwid 'xxxxxx');   
```

7. The target instance is connected via Direct Connect.
```
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', access_type '6', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', dcgid 'xxxxxx');    
    CREATE SERVER       
```


### 4. Create a user mapping
```
    testdb1=> create user mapping for user1 server srv_test1 options (user 'user2',password 'password2');
    CREATE USER MAPPING
```
### 5. Create a foreign table
```
    testdb1=> create foreign table foreign_table1(id integer) server srv_test1 options(table_name 'test_table2');
    CREATE FOREIGN TABLE
```
### 6. Access foreign data
```
    testdb1=> select * from foreign_table1;
     id
    ----
      1
    (1 row)
```
### 7. Notes on using postgres_fdw
If the target instance is on CVM, please note the following:
 1. The hba in PostgreSQL needs to be modified to allow the created mapped user (e.g., user2) to access via MD5. For more information on how to modify hba, please see [PostgreSQL's official documentation](https://www.postgresql.org/docs/9.3/static/auth-pg-hba-conf.html).
 2. If the target instance is not a TencentDB instance and the hot backup mode is configured for it, you need to update the server connection address or create another server after a master/slave switchover.

### 8. References

[postgres_fdw Overview](http://www.postgres.cn/docs/9.5/postgres-fdw.html)
[CREATE SERVER (9.3)](https://www.postgresql.org/docs/9.3/static/sql-createserver.html)
[CREATE SERVER (9.5)](https://www.postgresql.org/docs/9.5/static/sql-createserver.html)
[pg_hba Overview (9.3)](https://www.postgresql.org/docs/9.3/static/auth-pg-hba-conf.html)
[pg_hba Overview (9.5)](https://www.postgresql.org/docs/9.5/static/auth-pg-hba-conf.html)

## Example of Using mysql_fdw
mysql_fdw can be used to access data from other MySQL instances.

### 1. Prerequisites

1. Create test data in the current instance.
```
    postgres=>create role user1 with LOGIN  CREATEDB PASSWORD 'password1';
    postgres=>create database testdb1;
    CREATE DATABASE
```
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

### 2. Create mysql_fdw
```
    # Create
    postgres=> \c testdb1
    You are now connected to database "testdb1" as user "user1".
    testdb1=> create extension mysql_fdw;
    CREATE EXTENSION
    # View
    testdb1=> \dx
                               List of installed extensions
         Name     | Version |   Schema   |                    Description
    --------------+---------+------------+----------------------------------------------------
     plpgsql      | 1.0     | pg_catalog | PL/pgSQL procedural language
     mysql_fdw    | 1.0     | public     | Foreign data wrapper for querying a MySQL server
    (2 rows)
```

### 3. Create a server
1. The target instance is a TencentDB instance.
 ```
    # Access the data of `testdb2` in the target instance from `testdb1` in the current instance
    testdb1=>create server srv_test1 foreign data wrapper mysql_fdw options (host 'xxx.xxx.xxx.xxx', port '3306', instanceid 'cdb-xxxxx', uin 'xxxxxx', region 'ap-guangzhou');
    CREATE SERVER
 ```
2. The target instance is on CVM, and the network is the basic network.
```
    testdb1=>create server srv_test foreign data wrapper mysql_fdw options (host 'xxx.xxx.xxx.xxx', port '3306', instanceid 'ins-xxxxx', access_type '2', region 'ap-guangzhou'，uin 'xxxxxx'，own_uin 'xxxxxx');
    CREATE SERVER
```
3. The target instance is on CVM, and the network is VPC.
```
    testdb1=>create server srv_test1 foreign data wrapper mysql_fdw options (host 'xxx.xxx.xxx.xxx', port '3306', instanceid 'ins-xxxxx', access_type '2', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', vpcid 'vpc-xxxxxx', subnetid 'subnet-xxxxx');
    CREATE SERVER
```
4. The target instance is a self-built instance with public IP in Tencent Cloud.
```
    testdb1=>create server srv_test1 foreign data wrapper mysql_fdw options (host 'xxx.xxx.xxx.xxx', port '3306', access_type '3', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx');
    CREATE SERVER   
```
5. The target instance is connected via Tencent Cloud VPN.
```
    testdb1=>create server srv_test1 foreign data wrapper mysql_fdw options (host 'xxx.xxx.xxx.xxx', port '3306', access_type '4', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', vpngwid 'xxxxxx');
```
6. The target instance is connected via a self-built VPN.
```
    testdb1=>create server srv_test1 foreign data wrapper mysql_fdw options (host 'xxx.xxx.xxx.xxx', port '3306', access_type '5', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', vpngwid 'xxxxxx');   
```
7. The target instance is connected via Direct Connect.
```
    testdb1=>create server srv_test1 foreign data wrapper mysql_fdw options (host 'xxx.xxx.xxx.xxx', port '3306', access_type '6', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', dcgid 'xxxxxx');    
    CREATE SERVER       
```


### 4. Create a user mapping
```
    testdb1=> create user mapping for user1 server srv_test1 options (user 'user2',password 'password2');
    CREATE USER MAPPING
```

### 5. Create a foreign table
```
    testdb1=> create foreign table foreign_table1(id integer) server srv_test1 options(dbname 'testdb2', table_name 'test_table2');
    CREATE FOREIGN TABLE
```

### 6. Access foreign data
```
    testdb1=> select * from foreign_table1;
     id
    ----
      1
    (1 row)
```

### 7. References
[CREATE SERVER (9.3)](https://www.postgresql.org/docs/9.3/static/sql-createserver.html)
[CREATE SERVER (9.5)](https://www.postgresql.org/docs/9.5/static/sql-createserver.html)

## Example of Using cos_fdw
cos_fdw can be used to get text data in COS from a TencentDB for PostgreSQL instance.

### 1. Prerequisites
1. Create test data in the current instance.
```
    postgres=>create role user1 with LOGIN  CREATEDB PASSWORD 'password1';
    postgres=>create database testdb1;
    CREATE DATABASE
```

2. Create a bucket named "test1" in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) and upload a text file to "/testdir/test.txt" in it.


 ### 2. Create cos_fdw
```
    # Create
    postgres=> \c testdb1
    You are now connected to database "testdb1" as user "user1".
    testdb1=> create extension cos_fdw;
    CREATE EXTENSION
    # View
    testdb1=> \dx
                               List of installed extensions
         Name     | Version |   Schema   |                    Description
    --------------+---------+------------+----------------------------------------------------
     plpgsql      | 1.0     | pg_catalog | PL/pgSQL procedural language
     cos_fdw      | 1.0     | public     | foreign-data wrapper for flat qcloud cos access
    (2 rows)
```

### 3. Create a server
```
    # Access the data of the COS bucket `test1` from `testdb1` in the current instance
    testdb1=>create server srv_cos foreign data wrapper cos_fdw options(host 'test11-xxxxxx.cos.ap-chengdu.myqcloud.com', bucket 'test1', id 'xxxxxx', key 'xxxxxx');
    CREATE SERVER
```

### 4. Create a foreign table
Parameter: `filepath`, which is the relative path to the text file in the bucket.
```
    testdb1=> create foreign table test_cos(id integer) server srv_cos options(filepath '/testdir/test.txt');
    CREATE FOREIGN TABLE
```

### 5. Access foreign data
```
    testdb1=> select * from test_cos;
     id
    ----
      1
    (1 row)

```

### 6. References
[COS documentation](https://cloud.tencent.com/document/product/436)

