Memory is an important performance parameter for TencentDB for MySQL. It is common to see the memory utilization increase due to the presence of exceptional SQL statements and lack of database optimization. In severe cases, OOM can even occur and cause master/slave switchover, which compromises business stability and availability.

In MySQL, memory can be roughly divided into two parts: globally shared memory and session-level private memory. Shared memory is allocated upon the creation of an instance and shared by all connections. Private memory is used to allocate cache upon connection to the MySQL server. In some special SQL statements or field types, cache may be allocated to a single thread repeatedly. Therefore, all OOM exceptions are caused by the private memory of each connection. The composition of each part is as detailed below:

## Shared Memory
Run the following command to query how the shared memory in the sample is allocated:
```
show variables where variable_name in ('innodb_buffer_pool_size','innodb_log_buffer_size','innodb_additional_mem_pool_size','key_buffer_size','query_cache_size');
```

>innodb_additional_mem_pool_size is not supported in v5.7.

The following parameters are the query results of how the shared memory is allocated in an instance with 1,000 MB memory (below is the configuration of the test instance):
	1.  +---------------------------------+-----------+
	2.  | Variable_name                   | Value     |
	3.  +---------------------------------+-----------+
	4.  | innodb_additional_mem_pool_size | 8388608   |
	5.  | innodb_buffer_pool_size         | 524288000 |
	6.  | innodb_log_buffer_size          | 67108864  |
	7.  | key_buffer_size                 | 16777216  |
	9.  | query_cache_size                | 0         |
	10. +---------------------------------+-----------+
	11. 5 rows in set (0.01 sec)

**Parameter description**:
- **innodb_buffer_pool_size**
 It is the most important buffer area in InnoDB and also a major means to compensate physical data files through memory. For TencentDB for MySQL, it usually takes up 50-80% memory of an instance (1,000 MB*0.5=500 MB as shown in the above sample). This area mainly includes information such as data pages, index pages, undo pages, insert buffers, adaptive hash indexes, lock information, and data dictionaries. In SQL read/write operations, you should first manipulate buffer_pool rather than physical data files and then write back to data files through checkpoint or other mechanisms. This space can help improve database performance and accelerate SQL operations, but it may slow down failover.

- **innodb_log_buffer_size**
 It is mainly used to store redo logs and takes up 64 MB in TencentDB for MySQL. InnoDB will first write redo logs here and refresh them back to redo log files at a certain frequency. This space doesn't need to be large, because the buffer there is usually refreshed to redo logs at a relatively high frequency. Specifically, it will be refreshed for master thread (once every second), upon transactions committing, and when its available space is less than 1/2.

- **innodb_additional_mem_pool_size**
 It is mainly used to store some data structures within InnoDB and is uniformly set to 8 MB in TencentDB for MySQL. Generally, when applying for memory in buffer_pool, you also need to apply for space to store the object's structural information in additional memory. The size of this part is primarily dependent on the number of tables. The more tables, the larger the space should be.

- **key_buffer_size**
 It is an important buffer area of MyISAM tables and mainly used to store MyISAM table keys. It is uniformly set to 16 MB for all instances. Unlike InnoDB tables, MyISAM tables store index cache in key_buffer and data cache in the operating system memory. As TencentDB for MySQL uses MyISAM, this part should be allocated with a certain amount of space.

- **query_cache_size**
 It is used to cache query results to reduce the overhead of SQL parsing and execution. The caching feature of this part is disabled in TencentDB for MySQL. It is mainly suitable for application scenarios where there are more reads than writes, because it caches results based on the hash values of SQL statements and becomes invalid once table data changes.

## Private Memory
Run the following command to query how the session private memory in the sample is allocated:
```
show variables where variable_name in ('read_buffer_size','read_rnd_buffer_size','sort_buffer_size','join_buffer_size','binlog_cache_size','tmp_table_size');
```

The query result is displayed as follows (below is the configuration of the test instance):
		1.  +----------------------+-----------+
		2.  | Variable_name        | Value     |
		3. +----------------------+-----------+
		4.  | binlog_cache_size    | 32768     |
		5.  | join_buffer_size     | 262144    |
		6.  | read_buffer_size     | 262144    |
		7.  | read_rnd_buffer_size | 524288    |
		8.  | sort_buffer_size     | 524288    |
		9.  | tmp_table_size       | 209715200 |
		10.  +----------------------+-----------+
		11.  6 rows in set (0.00 sec)

**Parameter description:**

- **read_buffer_size**
	It stores the cache of sequential scans separately. When a thread scans data sequentially, it will first scan the buffer space to avoid causing more physical reads.

- **read_rnd_buffer_size**
	It stores the cache of random scans separately. When a thread scans data randomly, it will first scan the buffer space to avoid causing more physical reads.
	
- **sort_buffer_size**
	All the SQL statements that need to execute ORDER BY and GROUP BY will be allocated with sort_buffer to store the immediate results of the sorting operations. During sorting, if the storage size exceeds sort_buffer_size, a temporary table will be generated on the disk to complete the operation.

- **join_buffer_size**
	MySQL only supports the nested-loop join (NLJ) algorithm. The processing logic is to jointly search in one row of the driving table and the non-driving table, where the latter can be placed in join_buffer without having to access buffer_pool that has a concurrence protection mechanism.

- **binlog_cache_size**
	It is used to cache the thread's binlogs. Before a transaction is committed, its log will be stored in binlog_cache. After the transaction is committed, its binlog will be refreshed back to the binlog file on the disk for persistent storage.

- **tmp_table_size**
	Different from the above session-level buffer, this parameter can be modified in the console. It refers to the size of a temporary in-memory table. If the temporary table created by the thread exceeds the specified size, it will be converted to a MyISAM temporary table on the disk.
