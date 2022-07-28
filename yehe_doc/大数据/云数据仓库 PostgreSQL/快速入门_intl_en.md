To use CDWPG, you need to perform the following operations:

## Creating Cluster
Before creating a CDWPG cluster, you need to specify the data volume, region where the data resides, and network environment to access the cluster. **Currently, only VPCs are supported. Therefore, you need to create a VPC and subnet for cluster access before creating a cluster.**

## Connecting to Database
After the cluster is created, purchase a CVM instance in the previously configured subnet for access. Then, connect to the database via the psql client in the CVM instance. If you haven't installed the client, install with the following command.
```
yum install -y postgresql.x86_64
```
CDWPG is fully compatible with PostgreSQL 8.3.23 protocols. The basic syntax for connecting to the database with psql is as follows:
```
psql  -h 10.0.0.3 -p 5436 -d postgres -U testuser
```
Here, `postgres` is the default database of CDWPG, `testuser` is the admin account that you need to enter when creating the database, `5436` is the default port number of the database, and `10.0.0.3` is the VIP returned after database creation (which can be queried in the console).

## Importing Data
1. Use `INSERT` to import the data.
You can write the data directly to CDWPG through the `INSERT` statement, which is suitable for scenarios with small data volumes.
   - Use the client tool psql to connect to CDWPG and write the data through the standard `INSERT` syntax.
   - Write the data to CDWPG through the writer of the PostgreSQL JDBC driver. 
2. Use the `\COPY` command to import the data.
   You can use the `\COPY` command to import files to CDWPG from the server where the client resides, as described in the `\COPY` syntax of PostgreSQL.
3. Import the data from COS external tables.
The syntax of COS external tables is as described in [COS Data](https://intl.cloud.tencent.com/document/product/1138/45032). After creating a readable COS external table, you can use the following syntax to import the data from the table to an internal table with the same structure.
```
INSERT INTO cos_local_tbl SELECT * FROM cos_tbl
```
4. For more information on importing data from a public cloud or other environments, see [Using External Table](https://intl.cloud.tencent.com/document/product/1138/45032).

## Analyzing Data
The CDWPG syntax is fully compatible with Greenplum Database 5.x. You can use its syntax as a reference for data analysis.

#### Prerequisites
1. The database is connected under the admin user or another user created by the admin.
2. The corresponding database and database table, such as `testdb` and `testtable`, have been created.
3. The data has been inserted into the database and table as instructed in [Inserting Data](https://intl.cloud.tencent.com/document/product/1138/45125).

#### Simple `SELECT` statement
```
SELECT col1,col2,col3 FROM testtable WHERE col1 = val1 AND col2 = val2;
```
Use the above statement to get records in the `testtable` table where the value of `col1` is `val1` and that of `col2` is `val2`. For more analysis statements, see [Pivotal Greenplum® 5.29 Documentation](https://gpdb.docs.pivotal.io/5290/main/index.html).
