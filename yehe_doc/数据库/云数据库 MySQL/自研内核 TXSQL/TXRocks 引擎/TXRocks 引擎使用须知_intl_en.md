TXRocks is a transactional storage engine developed by Tencent's TXSQL team based on RocksDB. It saves more storage space and has a lower write amplification.

## Product Overview
By leveraging the LSM tree storage structure of RocksDB, the TXRocks transactional storage engine not only reduces wastes caused by InnoDB's half-full pages and fragments, but also uses the compact storage format. Therefore, it has a performance comparable to that of InnoDB but requires only a half or even smaller storage space. It is more suitable for businesses with a large data volume and high requirements for the transactional read/write performance.

## Prerequisites
The database version must be MySQL 5.7 or 8.0 on a two-node architecture.

## Purchasing TencentDB for MySQL Instance (with RocksDB Engine)
You can select RocksDB as the engine when purchasing an instance on the TencentDB for MySQL [purchase page](https://buy.Intl.cloud.tencent.com/cdb). For more information on other parameters, see [Creating MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37785).
![](https://qcloudimg.tencent-cloud.cn/raw/4b309a61ecac3520e27160da7143c224.png)
>?RocksDB is a key-value storage engine, with efficient writing and high compression. Currently, only TencentDB for MySQL 5.7 and 8.0 instances can use the RocksDB engine.

## Creating RocksDB Table
If RocksDB is selected as the default engine during instance creation, it will be the default engine used for table creation. You can run the following command to view the default engine:
```
show variables like '%default_storage_engine%';
```
![](https://qcloudimg.tencent-cloud.cn/raw/3bb1550d5995cece7cec2712ad62c5d0.png)
If the default engine is RocksDB, you cannot specify a storage engine in table creation statements:
![](https://qcloudimg.tencent-cloud.cn/raw/f4cb2efa27e236fb26a78971a8725cbd.png)
After a table is created, its data will be stored in RocksDB and can be used in the same way as in InnoDB.

## Engine Feature Limits
TXRocks has certain limits on engine features as detailed below:
<table>
<thead><tr><th>Category</th><th>Feature</th><th>TXRocks Limit</th></tr></thead>
<tbody>
<tr>
<td>DDL</td><td>Online DDL</td><td>Not supported. For example, `ALTER TABLE ... ALOGRITHM=INSTANT` is not supported. Only the `COPY` algorithm is supported for partition management operations.</td></tr>
<tr>
<td rowspan="5">SQL</td>
<td>Foreign key</td><td>Not supported.</td></tr>
<td>Partitioned table</td><td>Not supported.</td></tr>
<td>Generated column</td><td>Not supported.</td></tr>
<td>Explicit DEFAULT expression</td><td>Not supported. For example, `CREATE TABLE t1(c1 FLOAT DEFAULT(RAND()))ENGINE=ROCKSDB` will fail, with the error `'Specited storage engine' is not supported for default value expressions` reported.</td></tr>
<td>Encrypted table</td><td>Not supported.</td></tr>
<tr> 
<td rowspan="3">Index</td>
<td>Spatial index</td><td>The spatial index and spatial data types such as `GEOMETRY` and `POINT` are not supported.</td></tr>
<tr> 
<td>Full-text index</td><td>Not supported.</td></tr>
<td>Multi-valued index</td><td>Not supported.</td></tr>
<tr>
<td rowspan="4">Replication</td>
<td>Group replication</td><td>Not supported.</td></tr>
<td>Binlog format</td><td>Only the `ROW` format is supported, while `STMT` and `MIXED` formats are not.</td></tr>
<td>Clone plugin</td><td>Not supported.</td></tr>
<td>Transportable tablespace</td><td>Not supported.</td></tr>
<tr>
<td rowspan="5">Transaction and lock</td>
<td>LOCK NOWAIT and SKIP LOCKED</td><td>Not supported.</td></tr>
<td>Gap lock</td><td>Not supported.</td></tr>
<td>Savepoint</td><td>Not supported.</td></tr>
<td>Partial LOB field update</td><td>Not supported.</td></tr>
<td>XA transaction</td><td>Not recommended.</td></tr>
</tbody></table>	

## Parameter Description
>?When creating a TencentDB for MySQL instance, you can select RocksDB as the default storage engine. You can also customize the parameter template to suit your needs by following the parameter descriptions below.

#### MySQL 5.7 parameter list

| Parameter | Restart Required | Default Value | Value Range/Valid Values | Description |
|---------|---------|---------|---------|---------|
| rocksdb_use_direct_io_for_flush_and_compaction | Yes | ON | ON/OFF | Whether to use DIO during compaction. |
| rocksdb_flush_log_at_trx_commit | No | 1 | 0/1/2 | Controls when to write logs to the disk.<br>It is similar to `innodb_flush_log_at_trx_commit` and indicates whether transactions need to be synced when being committed.<li>0: Transactions are not synced when being committed.<li>1: Transactions are synced when being committed.<li>2: Transactions are synced once every second.</li>  |
| rocksdb_lock_wait_timeout | No | 1 | 1–1073741824 | Lock wait timeout period in seconds. |
| rocksdb_deadlock_detect | No | ON | ON/OFF | Whether to enable deadlock detection. After it is enabled, all deadlock information will be recorded in `mysqld` error logs. |
| rocksdb_manual_wal_flush | Yes | ON | ON/OFF | If the total size of WAL files exceeds `rocksdb_max_total_wal_size`, RocksDB will forcibly flush the column family to the disk to ensure that the oldest WAL file can be deleted. |

#### MySQL 8.0 parameter list

| Parameter | Restart Required | Default Value | Value Range/Valid Values | Description |
|---------|---------|---------|---------|---------|
| rocksdb_flush_log_at_trx_commit | No | 1 | 0/1/2 | Controls when to write logs to the disk.<br>It is similar to `innodb_flush_log_at_trx_commit` and indicates whether transactions need to be synced when being committed.<li>0: Transactions are not synced when being committed.<li>1: Transactions are synced when being committed.<li>2: Transactions are synced once every second.</li>  |
| rocksdb_lock_wait_timeout | No | 1 | 1–1073741824 | Lock wait timeout period in seconds. |
| rocksdb_merge_buf_size | No | 524288(=512K) | 100–18446744073709551615 | Size of the merge-sort buffer used during secondary index creation. |
| rocksdb_merge_combine_read_size | No | 8388608 (=8M) | 524288(=512K)–18446744073709551615 | Size of the memory used by k-way merge during secondary index creation. |
| rocksdb_deadlock_detect | No | ON | ON/OFF | Whether to enable deadlock detection. |
| rocksdb_manual_wal_flush | Yes | ON | ON/OFF | If the total size of WAL files exceeds `rocksdb_max_total_wal_size`, RocksDB will forcibly flush the column family to the disk to ensure that the oldest WAL file can be deleted. |

## RocksDB Monitoring Metrics
RocksDB monitoring metrics are as listed below:

| Metric | Description |
|---------|---------|
| rocksdb_bytes_read | Data read from disk |
| rocksdb_bytes_written | Data written to disk |
| rocksdb_block_cache_bytes_read | Blocks read |
| rocksdb_block_cache_bytes_write | Blocks written |
| rocksdb_wal_log_capacity | Data written to WAL log |

