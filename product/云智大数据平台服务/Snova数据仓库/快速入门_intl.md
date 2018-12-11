To use Snova Data Warehouse, you need to do the following first:

## I. Creating a Cluster

Currently, purchasing a cluster on the official website is not supported. Please contact us to create a cluster for you in the backend.

Before creating a cluster, you need to determine the amount of data, region and the network environment in which the cluster is accessed.

Currently, Snova can be accessed only on a private network, so you need to first create a subnet that accesses the cluster before creating the cluster.

## II. Connecting to a Database

After creating the cluster, apply for a CVM instance in the configured subnet to access the cluster. Then, connect to the database via psql on the CVM instance. If the PostgreSQL client is not installed, install it using the following command.

```
yum install -y postgresql.x86_64
```

Snova is fully compatible with PostgreSQL 8.3.23 protocols. The basic syntax for connecting to a database using psql is as follows:

```
psql  -h 10.0.0.3 -p 5436 -d postgres -U testuser
```

Here, postgres is the default database of Snova, testuser is the admin account set when the database is created, 5436 is the default port number of the database, and 10.0.0.3 is the VIP returned after the database is created, which can also be queried in the console (the private IP), as shown in the following figure:

## III. Importing Data

1. Import data using INSERT
   You can write data directly to Snova using the INSERT statement for scenarios with small amounts of data:
   - Connect to Snova using the client tool psql and write data using the standard INSERT syntax.
   - Write data to Snova using the PostgreSQL JDBC driver writing application. 

2. Import data using the \COPY command
   You can use the \COPY command to import the files on the server where the client is located into Snova. For more information on the syntax, see the PostgreSQL \COPY syntax.

3. Import data from COS external tables
   For details on COS external table syntax, see [Importing External Data](https://cloud.tencent.com/document/product/878/20069). After creating a readable COS external table, you can use the following syntax to import data from the external table into an internal table with the same structure.

   ```
   INSERT INTO cos_local_tbl SELECT * FROM cos_tbl
   ```

4. Import data from other environments in the public cloud
For details, see [Using an External Table](https://cloud.tencent.com/document/product/878/20068).

## IV. Analyzing Data

Snova syntax is fully compatible with the Greenplum Database 5.x syntax, so you can refer to it for data analysis.

#### Prerequisites

1. The database is connected to using an admin user or another user created by it.
2. A corresponding database and database table such as testdb and testtable are created.
3. The data is inserted into the table. For details on how to insert data, see [Inserting Data](https://cloud.tencent.com/document/product/878/20071).

#### Simple SELECT Statement

```
SELECT col1,col2,col3 FROM testtable WHERE col1 = val1 AND col2 = val2;
```

You can use the statement above to get a record that the value of col1 is val1 and that of col2 is val2 in the database table "testtable". More complex analysis statements can be found in [Greenplum Database 5.x documentation](https://greenplum.org/docs/590/common/gpdb-features.html).
