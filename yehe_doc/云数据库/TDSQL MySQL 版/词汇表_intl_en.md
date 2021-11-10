

### Vertical sharding

A database consists of many tables, and each table corresponds to a different business. Vertical sharding is to classify tables according to business features and distribute them to different databases.



### Non-sharded table

A non-sharded table is used to store tables that do not need sharding. All data of this table is stored in the first physical shard, and all tables of this type are placed in the first physical shard, with exact the same syntax and usage methods as MySQL. You can consider it as a non-distributed table.

### DDL

See [Data Definition Language](#ddl1).

### DML

See [Data Manipulation Language](#dml1).



### Sharded table

A sharded table means that the original table with enormous amount of data needs to be split to multiple database nodes, so that each physical shard carries some of the data and all the physical shards provide the complete data.
<span id="shardkey1"></span>
### Shardkey

TDSQL performs sharding by executing a modulo operation on the shardkey.
<span id="tdsql1"></span>
### TDSQL for MySQL

TDSQL for MySQL is a distributed database service deployed in Tencent Cloud that supports automatic sharding (horizontal sharding) and the Shared Nothing architecture. With a distributed database, your business obtains a complete logical database table which is split and distributed evenly across multiple physical shard nodes on the backend. TDSQL deploys the master-slave architecture by default and provides a full set of solutions for disaster recovery, backup, restoration, monitoring, and migration, making it ideal for storing terabytes to petabytes of data.



### Broadcast table

Broadcast tables are based on small table broadcasting technology. If a table is set as broadcast table, all operations made to this table will be broadcast to all physical shards, and each shard possesses all data of the table.
<span id="OLAP1"></span>
### On-line analytical processing

As the main application of data warehouse systems, On-Line Analytical Processing (OLAP) supports complex analysis operations, focuses on decision support, and provides intuitive query results.
<span id="OLTP1"></span>
### On-line transaction processing

On-Line Transaction Processing (OLTP), as the main application of traditional relational database, is mainly used to process basic and daily transactions, such as bank transactions.



### OLAP

See [On-Line Analytical Processing](#OLAP1).

### OLTP

See [On-Line Transaction Processing](#OLTP1).



### Percona

Percona is fully compatible with MySQL protocol and has a significant improvement in feature and performance over MySQL. Now, TDSQL supports Percona 5.7.

### Proxy

With Tproxy, TDSQL achieves automatic database and table sharding, manages the underlying physical database instances, and provides a unique service port compatible with MySQL databases.



### Strong sync

Strong sync is a MySQL-based multi-thread asynchronous replication program.

### Globally unique digital sequence

Globally unique digital sequence is "sequence" for short. A sequence contains 8 bytes in the unsigned long type. Now, TDSQL can guarantee the global uniqueness and increment of this field.



### Shardkey

See [shardkey](#shardkey1).

## Horizontal sharding

According to certain rules, the data of a table is split across multiple physically independent database servers to form a "separate" database "shard". Multiple shards together form a logically complete database instance.
<span id="dml1"></span>
### Data manipulation language

Data Manipulation Language (DML), with the commands of SELECT, UPDATE, INSERT and DELETE.

<span id="ddl1"></span>
### Data definition language

Data Definition Language (DDL), with the main commands of CREATE, ALTER and DROP.



### TDSQL

See [TDSQL for MySQL](#tdsql1).
