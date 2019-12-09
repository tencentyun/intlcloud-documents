### TDSQL
Tencent Distributed MySQL.
### DDL
Data Definition Language with main commands such as CREATE, ALTER, and DROP.
#### DML
Data Manipulation Language with SELECT, UPDATE, INSERT, and DELETE commands.
### Vertical split
A database consists of many tables, and each table corresponds to a different business. Vertical split is to category tables based on business functions and distribute them to different databases.
### Single table
It is used to store tables that do not need to be sharded. All data of this table is stored in the first physical shard, and all tables of this type are placed in the first physical shard, with exactly the same syntax and usage methods as MySQL. You can consider it as a non-distributed table.
### Shard (Logical)
It is a physical logic instance consisting of database engines, which contains a master node, several slave nodes, and several remote backup nodes.
### Sharding
Sharding is to split a very large table and distribute the parts on multiple database nodes, so that each physical shard carries partial data and all of them constitute the complete data.
### Broadcast table
This is based on small table broadcasting technology. After a table is set as a broadcast table, all its operations will be broadcast to all physical shards, where each shard has all the data of the table.
### Node
It is a physical device carrying shards. A node can be a physical machine, a virtual machine, or a small cluster.
### MariaDB
MariaDB is one of the most important forks of MySQL. Compared to MySQL, MariaDB has a better performance in extensions, storage engines, and new feature enhancements. TDSQL currently supports MariaDB 10.1 (compatible with MySQL 5.6).
### MySQL
MySQL is one of the most popular relational database management systems. Its SQL language is the most commonly used standardized programming language for database accessing.
### OLTP
On-Line Transaction Processing, as a major application of traditional relational databases, is mainly used to process basic and daily transactions, such as bank transactions.
### OLAP
On-Line Analytical Processing, as a major application of data warehouse systems, supports complex analysis operations, focuses on decision-making, and provides intuitive query results.
### Percona
Percona is fully compatible with MySQL protocols and has much better functionality and performance than MySQL. TDSQL currently supports Percona 5.7.
### Proxy
With the aid of Tproxy, TDSQL achieves automatic splitting of databases and tables, manages underlying physical database instances, and provides clients with a unique service port that is compatible with MySQL databases.
### Strong sync
Strong sync is a MySQL protocol-based multi-thread async replication scheme with strong synchronization.
### Globally unique numerical sequence
A globally unique numerical sequence ("sequence" for short) uses the unsigned long type of 8 bytes. TDSQL currently can guarantee the global uniqueness and orderly increment of this field, but not the continuity.
### Shard (Physical)
It is a physical database instance. A logical instance visible to users is composed of multiple physical instances.
### Shardkey
TDSQL performs sharding by executing a modulo operation on the shardkey.
### Horizontal split 
According to certain rules, the data of a table is split across multiple physically independent database servers to form "separate" database "shards". Multiple shards together form a logically complete database instance.

