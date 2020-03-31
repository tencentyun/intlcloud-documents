## Data Sync Requirements
The data sync feature supports real-time data sync between two database sources. It is suitable for various business scenarios such as local data disaster recovery, query and report analysis, business intelligence (BI) analysis, and real-time data warehousing.

**Supported instance types**
<table>
<thead>
<tr>
<th>Source Instance Type</th>
<th>Target Instance Type</th>
</tr>
</thead>
<tbody><tr>
<td rowspan= "4">**Public cloud** TencentDB for MariaDB/MySQL</td>
<td>**Public cloud** TencentDB for MariaDB/MySQL</td>
</tr>
<tr>
<td>**Public cloud** TencentDB for PostgreSQL</td>
</tr>
<tr>
<td>**Public cloud** CKafka</td>
</tr>
<tr>
<td>**Private cloud** TencentDB for MariaDB/MySQL</td>
</tr>
<tr>
<td rowspan= "3">**Public cloud** TDSQL</td>
<td>**Public cloud** TDSQL</td>
</tr>
<tr>
<td>**Public cloud** CKafka</td>
</tr>
<tr>
<td>**Private cloud** TDSQL</td>
</tr>
</tbody></table>

**Supported sync topologies**
Database sync supports serial topology of "one-to-one one-way sync", "one-to-many one-way sync", "cascading one-way sync", and "many-to-one one-way sync", but does not support the topology of "two-way ring sync".

**Supported instance versions**
- MariaDB 10.0, 10.1
- MySQL 5.6, 5.7
- PostgreSQL 9.6
- All versions of CKafka

**Supported sync syntax**
- DML operations: INSERT, UPDATE, DELETE
- DDL operations: CREATE TABLE, ALTER TABLE, ADD COLUMN, DROP COLUMN, RENAME COLUMN

**Database sync objects**
Sync objects support exact and regex match of databases and tables. Non-table objects such as stored procedures, views, indices, or triggers are not supported currently. If you need to sync a non-table object, please create the same one in the target database.

**Database sync fees**
Currently, data sync is free of charge.

**Database sync network**
Currently, database sync is supported only between Tencent Cloud intra-region database instances or databases in Direct Connect. For cross-region data sync or disaster recovery, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) and indicate the IDs of source and target instances and sync requirements. Only after the ticket is approved can the feature be enabled.


## Data Sync Feature
### Data type conversion

#### Sync from MariaDB/MySQL to PostgreSQL
MariaDB/MySQL and PostgreSQL have different data types. The database sync tool will convert the data types according to the following rules:

| MariaDB/MySQL Data Type                  | Data Type After Sync to PostgreSQL |
| -------------------------------------- | ---------------------------- |
| tinyint/smallint                       | smallint                     |
| mediumint/int                          | integer                      |
| bigint                                 | bigint                       |
| real/double                            | double precision             |
| float                                  | float                        |
| bit                                    | bit                          |
| bool/boolean                           | boolean                      |
| char/varchar                           | char/varchar                 |
| binary/varbinary                       | text                         |
| year/date/time/datetime/timestamp      | timestamp without time zone  |
| tinyblob/mediumblob/blob/longblob/long | bytea                        |
| mediumtext/text/longtext               | text                         |
| decimal/numeric                        | decimal/numeric              |
| enum                                   | integer                      |

>The data length of columns in the types listed above stays unchanged during conversion. Types that are not listed above stay unchanged too during conversion.

#### Sync from MariaDB/MySQL to TDSQL
MariaDB/MySQL and TDSQL have the same data types; therefore, data type conversion is not needed.

#### Sync from MariaDB/MySQL to CKafka
Relevant data will be converted to JSON format. For more information, please see [Binlog Consumption Format](https://intl.cloud.tencent.com/document/product/237/35420).

#### Sync from TDSQL to CKafka
Relevant data will be converted to JSON format. For more information, please see [Binlog Consumption Format](https://intl.cloud.tencent.com/document/product/237/35420).

### Data subscription
Data sync to CKafka supports data subscription. Before configuring this feature, you need to purchase a CKafka instance first. For more information, please see [CKafka](https://intl.cloud.tencent.com/document/product/597?from_cn_redirect=1). Below are configuration recommendations:

- **Specification**
You can evaluate the CKafka instance specification based on the daily updated data volume, daily peak or average bandwidth, and desired data retention period in CKafka of the instance to be synced.
For example, if an instance updates 10 million rows every day and each row is 2 KB, the daily write peak volume is 20,000 rows/second, 3 replicas are desired in CKafka, and data needs to be retained in CKafka for 3 days.
For this instance, the daily updated data volume is 20 GB and will be about 30 GB after being converted to JSON format, the retention period is 3 days, 3 replicas need about 270 GB of storage capacity, the peak write bandwidth of the database is about 39 MB/s, and the throughput for CKafka to sustain 3 replicas is about 117 MB/s; therefore, the **Standard Edition** of CKafka is sufficient to meet the requirements.

- **Network**
It is recommended to deploy the target instance in the same VPC as the source instance.

- **Topic selection**
A sync task needs one topic, and multiple sync tasks need multiple different topics; otherwise, data may get disorganized.

- **Parameter selection**
The following settings are for your reference only. Select appropriate values based on your actual needs.
 - Number of partitions: 1
 - Number of replicas: 3
 - cleanup.policy: deletion
 - min.isync.replicas: 2
 - unclean.leader.election.enable: false

- **Data consistency**
Due to network disconnection or other reasons, messages produced by a database instance to CKafka may be duplicate. In this case, when the consumer replays data, idempotency can be used to clear duplicates.
>In the idempotency scheme, eventual data consistency will be ensured in case messages are executed repeatedly. Specifically, when there are records with primary key conflict, the system will first delete the duplicate data before performing the `insert` operation, forcibly insert the data that cannot be matched by the `update` operation, and directly skip the data that cannot be found during the `delete` operation. Idempotency can be used to achieve data consumption consistency. To use this scheme, there must be a primary key or a non-NULL unique index in the table.
