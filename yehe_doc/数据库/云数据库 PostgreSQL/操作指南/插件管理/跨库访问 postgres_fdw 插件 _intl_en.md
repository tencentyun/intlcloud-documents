## Overview
Foreign data wrapper (FDW) is an extension provided by PostgreSQL for accessing external data sources, including other databases in the same instance and other instances.
1. Install the FDW extension by running `CREATE EXTENSION`.
2. Run the `CREATE SERVER` statement to create a foreign server object for each remote database to be connected to, and specify connection information except `user` and `password` as the options for the server.
3. Run the `CREATE USER MAPPING` statement to create a user mapping for each database to be accessed through the foreign server, and specify the remote database's username and password as the `user` and `password` of the mapped user.
4. Run the `CREATE FOREIGN TABLE` statement to create a foreign table for each remote table to be accessed. The corresponding columns of the foreign table must match those of the remote table. You can also use different table and column names in the foreign table than the remote table, provided that you have the correct remote object name as an option to create the foreign table object.

As FDW supports cross-instance and cross-database access, TencentDB for PostgreSQL optimizes access control over the creation of foreign server objects and implements categorized management based on the environment of the target instance. Auxiliary parameters are added to the open-source edition to verify user identity and adjust network policies.

## Auxiliary parameters of postgres_fdw    
 - **host**
   IP of the target instance. This parameter is required by `postgres_fdw` for cross-instance access.
 - **port**
   Port of the target instance. This parameter is required for cross-instance access.
 - **instanceid**
   Instance ID.
	 a. This parameter is required for access across TencentDB for PostgreSQL instances. It is in the format of `postgres-xxxxxx` or `pgro-xxxxxx` and can be viewed in the [console](https://console.cloud.tencent.com/postgres).
  b. If the target instance is in a CVM instance, this parameter is the ID of the CVM instance in the format of `ins-xxxxx`.
 - **dbname** 
 Name of the database in the remote PostgreSQL service to be accessed. For cross-database access in the same instance, you only need to configure this parameter and can leave other parameters empty.
 - **access_type**
    Type of the target instance. This parameter is optional:
    1: The target instance is a TencentDB instance, such as TencentDB for PostgreSQL or MySQL. If no other types are explicitly specified, this will be the default type.
    2: The target instance is in a CVM instance.
    3: The target instance is a public network-based self-built instance in Tencent Cloud.
    4: The target instance is a Tencent Cloud VPN-based instance.
    5: The target instance is a self-built VPN-based instance.
    6: The target instance is a Direct Connect-based instance.
 - **uin**
    ID of the account to which the instance belongs, which is used for verifying user permissions and can be viewed in [Account Info](https://console.cloud.tencent.com/developer). This parameter is optional.
 - **own_uin**
    ID of the root account to which the instance belongs, which is also needed for verifying user permissions. This parameter is optional.
 - **vpcid**
    VPC ID. This parameter is optional; however, it is required if the target instance is in a CVM instance in a VPC. It can be viewed in the [VPC console](https://console.cloud.tencent.com/vpc/vpc).
 - **subnetid**
    VPC subnet ID. This parameter is optional; however, it is required if the target instance is in a CVM instance in a VPC. It can be viewed in the [VPC console](https://console.cloud.tencent.com/vpc/subnet).
 - **dcgid**
    Direct Connect connection ID. This parameter is optional; however, it is required if the target instance is connected to the network over Direct Connect.
 - **vpngwid**
    VPN gateway ID. This parameter is optional; however, it is required if the target instance is connected to the network over VPN.
 - **region**
    Region where the target instance resides; for example, "ap-guangzhou" represents Guangzhou region. This parameter is optional; however, it is required for cross-region access.
		
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
>?When you create the extension, if the system prompts that the extension does not exist or you don't have sufficient permissions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
```
#Create
postgres=> \c testdb1
You are now connected to database "testdb1" as user "user1".
testdb1=> create extension postgres_fdw;
CREATE EXTENSION
#View
testdb1=> \dx
                            List of installed extensions
      Name     | Version |   Schema   |                    Description
--------------+---------+------------+----------------------------------------------------
  plpgsql      | 1.0     | pg_catalog | PL/pgSQL procedural language
  postgres_fdw | 1.0     | public     | foreign-data wrapper for remote PostgreSQL servers
(2 rows)
```

### Step 3. Create a server
>!Cross-instance access is supported only for kernel v10.17_r1.2, v11.12_r1.2, v12.7_r1.2, v13.3_r1.2, v14.2_r1.0, and later.
>
- Cross-instance access.
```
#Access the data of the target instance's `testdb2` from the current instance's `testdb1`
testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', instanceid 'postgres-xxxxx');
CREATE SERVER
```
- For cross-database access in the same instance, you only need to enter the `dbname` parameter.
```
#Access the data of `testdb2` from `testdb1` in the current instance
create server srv_test1 foreign data wrapper postgres_fdw options (dbname 'testdb2');
```
- The target instance is in a CVM instance in the classic network.
```
    testdb1=>create server srv_test foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx', dbname 'testdb2', port '5432', instanceid 'ins-xxxxx', access_type '2', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx');
    CREATE SERVER
```
- The target instance is in a CVM instance in a VPC.
```
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', instanceid 'ins-xxxxx', access_type '2', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', vpcid 'vpc-xxxxxx', subnetid 'subnet-xxxxx');
    CREATE SERVER
```

- The target instance is a public network-based self-built instance in Tencent Cloud.
```
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', access_type '3', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx');
    CREATE SERVER 
```

- The target instance is a Tencent Cloud VPN-based instance.
```
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', access_type '4', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', vpngwid 'xxxxxx');
```

- The target instance is a self-built VPN-based instance.
```
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', access_type '5', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', vpngwid 'xxxxxx');   
```

- The target instance is a Direct Connect-based instance.
```
    testdb1=>create server srv_test1 foreign data wrapper postgres_fdw options (host 'xxx.xxx.xxx.xxx',dbname 'testdb2', port '5432', access_type '6', region 'ap-guangzhou', uin 'xxxxxx', own_uin 'xxxxxx', dcgid 'xxxxxx');    
    CREATE SERVER       
```

### Step 4. Create a user mapping 
>? You can skip this step for cross-database access in the same instance.
>
```
testdb1=> create user mapping for user1 server srv_test1 options (user 'user2',password 'password2');
CREATE USER MAPPING
```

### Step 5. Create a foreign table
```
testdb1=> create foreign table foreign_table1(id integer) server srv_test1 options(table_name 'test_table2');
CREATE FOREIGN TABLE
```   

### Step 6. Access data in the foreign table
```
testdb1=> select * from foreign_table1;
  id
----
   1
(1 row)
```
## Notes
Pay attention to the following for the target instance:
 1. The HBA in PostgreSQL needs to be modified to allow the created mapped user (e.g., user2) to access via MD5. For more information on how to modify HBA, see [The pg_hba.conf File](https://www.postgresql.org/docs/10/static/auth-pg-hba-conf.html).
 2. If the target instance is not a TencentDB instance and has a hot backup mode configured, after a primary-standby switch, you need to update the server connection address or create a server again.

### References
[postgres_fdw overview](https://www.postgresql.org/docs/9.5/postgres-fdw.html)
[Create a server on v9.3](https://www.postgresql.org/docs/9.3/static/sql-createserver.html)
[Create a server on v9.5](https://www.postgresql.org/docs/9.5/static/sql-createserver.html)
[Create a server on v10](https://www.postgresql.org/docs/10/sql-createserver.html)
[Create a server on v11](https://www.postgresql.org/docs/11/sql-createserver.html)
[Create a server on v12](https://www.postgresql.org/docs/12/sql-createserver.html)
[Create a server on v13](https://www.postgresql.org/docs/13/sql-createserver.html)
[Create a server on v14](https://www.postgresql.org/docs/14/sql-createserver.html)

