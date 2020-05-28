## Overview
This document describes how to import data in MySQL into a ClickHouse cluster in the following two methods:
- Through ClickHouse's support for MySQL external tables.
- By using the `clickhouse-mysql-data-reader` tool provided by Altinity.

In the examples below, data is imported from the MySQL data table `test.clickhouse_test` into the ClickHouse cluster. The table schema is as shown below:
![](https://main.qcloudimg.com/raw/7403cab1c8f0a68fa2fe3ce0227225ab.jpg)
                         

## Importing Data by Using MySQL Table Engine (Simple Scheme)
ClickHouse's MySQL table engine allows you to perform `SELECT` queries on data stored on remote MySQL servers. Based on this capability, you can use the `CREATE ... SELECT * FROM` or `INSERT INTO ... SELECT * FROM` statement to import data.

**Directions:**
- Step 1. Create a MySQL table engine in ClickHouse
![](https://main.qcloudimg.com/raw/4486adf6c262e1fec06d4ce8cc99fbb4.jpg)
- Step 2. Create a ClickHouse table
![](https://main.qcloudimg.com/raw/296886441fadb3f57f8d9a9cd94906ec.jpg)
- Step 3. Import data in the external table created in step 1 into the ClickHouse table
![](https://main.qcloudimg.com/raw/e869a8ed58e91e9066849fb1073a910d.jpg)
 
You can combine steps 2 and 3 into one step, i.e., using `CREATE TABLE AS SELECT * FROM` to achieve the same result.

**ClickHouse supports MySQL external table engines. Is it necessary to import data into ClickHouse?**      
Yes. A MySQL external table engine does not store data itself; instead, data is stored in MySQL. In copy queries, especially when there are `JOIN` statements, access to an external table is very slow and even impossible. This scheme has obvious flaws and does not support importing incremental data.

## Importing Data by Using Altinity Tool (Recommended Scheme)

Altinity provides the [clickhouse-mysql-data-reader](https://github.com/Altinity/clickhouse-mysql-data-reader) tool for data import. This tool can export both existing and incremental data from MySQL.

As described on the official website, use of the [pypy](https://github.com/squeaky-pl/portable-pypy#portable-pypy-distribution-for-linux) tool can significantly improve the data import performance of `clickhouse-mysql-data-reader`.

**Tool preparations**

- Step 1. Download [pypy3.6-7.2.0](https://github.com/squeaky-pl/portable-pypy/releases) and decompress it to the `pypy` directory
- Step 2. Install `clickhouse-mysql`. **If you are performing the operations in a Tencent Cloud ClickHouse cluster, after completing the installation operations below, the tool will be integrated and can be used out of the box with no configuration required**
 - Install `pip`: run `pypy/bin/pypy3 -m ensurepip`.
 - Install `mysql-replication` and `clickhouse-driver`: run `pypy/bin/pip3 install mysql-replication` and `pypy/bin/pip3 install clickhouse-driver`.
 - Install and initialize `clickhouse-mysql`: run `pypy/bin/pip3 install clickhouse-mysql` and `pypy/bin/clickhouse-mysql --install`.
 - Install `clickhouse-client`: run `yum install -y clickhouse-client`.
 - Install `mysql-community-devel`: run `yum install -y mysql-community-devel`.
- Step 3. Get the database permissions `SUPER` and `REPLICATION CLIENT`
```
CREATE USER 'root'@'%' IDENTIFIED BY 'cloud';
GRANT SELECT, REPLICATION CLIENT, REPLICATION SLAVE, SUPER ON *.* TO 'root'@'%';
FLUSH PRIVILEGES;
```

## Importing Data

After completing the preparations, you can use the tool to import data from MySQL to the ClickHouse cluster in the following steps:
1. Use `clickhouse-mysql-data-reader` to generate the SQL statement for table creation.
![](https://main.qcloudimg.com/raw/aca912daf06add4f2bbcfc713c9762dc.jpg)
Modify the SQL statement and select an appropriate table engine (`TinyLog` is used in this example). Run the table creation statement `clickhouse-client -m < create.sql`.
2. Import existing data.
![](https://main.qcloudimg.com/raw/396a932284dfaf0d1f6f8ce1d711e227.jpg)
3. Import incremental data.
![](https://main.qcloudimg.com/raw/f617557e73c30d7695848af7bf52074a.jpg)
The meanings of the parameters are as follows:
 - **src-host**: MySQL database IP.
 - **src-user**: MySQL database username.
 - **src-password**: MySQL database password.
 - **create-table-sql-template**: generates the table creation script of ClickHouse.
 - **with-create-database**: adds the database creation statement to the table creation script.
 - **src-tables**: source table (MySQL table).
 - **mempool-max-flush-interval**: time interval for `mempool flush`.
 - **src-server-id**: whether the MySQL server is a master node.
 - **src-resume**: resumable transfer.
 - **src-wait**: data wait.
 - **nice-pause**: sleep time interval if there is no data.
