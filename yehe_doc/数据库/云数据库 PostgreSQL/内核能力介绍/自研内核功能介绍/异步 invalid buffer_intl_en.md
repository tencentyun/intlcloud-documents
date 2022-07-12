## Background
The primary-standby replication logic of PostgreSQL will severely slow down data recovery from the standby database if there are many DDL statements in tables. To avoid this, TencentDB for PostgreSQL is specially optimized and modified.

## How It Works
PostgreSQL uses physical replication to implement primary-standby replication. After a log is synced to the standby node, the standby node will parse the WAL log to make the data consistent with that on the primary node. The standby node will perform the following operations when recovering a DROP statement:

1. Recover a system table, such as `pg_class`, `pg_attrbute`, and `pg_type`, which is equivalent to removing the table metadata.
2. Close the table file.
3. Traverse pages in the buffer and mark the found pages of the table as invalid, so subsequent processes can use them.
4. Send an async invalidation message to other backends to notify that the table has been deleted.
5. Delete the physical file of the table.

However, in the PostgreSQL kernel, the `DropRelFileNodesAllBuffers` function will be executed in step 3. It needs to traverse the entire `shard_buffer` to check whether the buffer has the data of the table to be deleted and mark corresponding pages as invalid. The default size of a page in PostgreSQL is 8 KB. If the size of `shard_buffer` is 16 GB for example, there will be 16 GB / 8 KB = 2 million pages. Therefore, every time a table is deleted, 2 million pages need to be checked one by one. If the table has indexes, 2 million pages will be checked one by one in each index.

From the perspective of business, when there are a high number of table changes and quick table deletions, as such operations can be executed concurrently on the primary database, the compromised performance is less obvious. However, as the PostgreSQL standby database recovers a table in a single thread, the primary-standby sync logs will be heaped, and data transfer will be delayed.

## Solution
When TencentDB for PostgreSQL recovers a dropped table, it writes the table information into a shared hash table. If a table file is deleted, it won't be physically deleted directly; instead, TencentDB for PostgreSQL will store the actual file deletion operation as an async action in the hash table.

After invalid buffer processing is completed, the table will be removed from the hash table. In this way, if a file fails to be opened during the process, it will be sufficient to check whether the file exists in the hash table. In addition, if the queue is traversed when a file is created and a file with the same name in the hash table is undergoing invalid buffer processing, just wait.
PostgreSQL stores each table filename as a UInt32 integer and adopts the principle of "global assignment and local storage", where all databases in an instance use the same counter to generate file numbers, and generated files are stored in the databases' respective directories. When the system assigns a filename, if the current database has a file with the same name, the system will try the next name until there is no conflict. The counter will reset after it reaches the maximum value.

After optimization, the primary-standby sync performance is improved by over 30,000 times in similar scenarios.
