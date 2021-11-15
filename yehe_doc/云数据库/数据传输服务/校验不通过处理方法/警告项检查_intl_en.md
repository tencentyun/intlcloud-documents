
## MySQL/TDSQL-C Check Details
You need to configure the following parameter as required; otherwise, the system will report warnings during verification, which will not affect the migration task progress but will affect the business. You need to assess and determine whether to modify the parameters.
- We recommend you set `max_allowed_packet` in the target database to a value greater than that in the source database. 
  - Impact on the business: if the `max_allowed_packet` parameter in the target database is smaller than that in the source database, it may cause failures in writing data to the target database and lead to full migration failures.  
  - Fix: change the value of the `max_allowed_packet` parameter in the target database to a value greater than that in the source database.

- We recommend you set `max_allowed_packet` in the target database to a value greater than 1 GB.
  - Impact on the business: if the value of `max_allowed_packet` is too large, more memory will be used, causing packet losses and inability to capture the SQL statements of large exception event packets. If its value is too small, program errors mat occur, causing backup failure and frequent sending/receiving of network packets, which compromises the system performance.
  - Fix: run the following command to modify the `max_allowed_packet` parameter:
```
set global max_allowed_packet = 1GB
```

- We recommend you use the same character set for the source and target databases.
  - Impact on the business: if the character sets of the source and target databases are different, there may be garbled characters.
  - Fix: run the following command to change the character sets of the source and target databases to the same one:
```
set character_set_server = 'utf8';
```

- We recommend you use a database with a specification above 2-core CPU and 4 GB memory.

- If you only perform full data migration, do not write new data into the source database during migration; otherwise, the data in the source and target databases will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.

- For data export with locks: you need to use `Flush Table With Read Lock` to temporarily lock tables in the source database, and the `MyISAM` table will be locked until the full data is exported. Currently, the lock wait timeout period is 60s, and if locks cannot be obtained before it elapses, the task will fail.

- For data export without locks: read locks will be added to tables without a primary key or non-null unique key.

## TDSQL for MySQL Check Details

You need to configure the following parameter as required; otherwise, the system will report warnings during verification, which will not affect the migration task progress but will affect the business. You need to assess and determine whether to modify the parameters.

- We recommend you set `max_allowed_packet` in the target database to a value greater than that in the source database. 
  - Impact on the business: if the `max_allowed_packet` parameter in the target database is smaller than that in the source database, it may cause failures in writing data to the target database and lead to full migration failures.  
  - Fix: change the value of the `max_allowed_packet` parameter in the target database to a value greater than that in the source database.

- We recommend you set `max_allowed_packet` in the target database to a value greater than 1 GB.
  - Impact on the business: if the value of `max_allowed_packet` is too large, more memory will be used, causing packet losses and inability to capture the SQL statements of large exception event packets. If its value is too small, program errors mat occur, causing backup failure and frequent sending/receiving of network packets, which compromises the system performance.
  - Fix: run the following command to modify the `max_allowed_packet` parameter:
```
set global max_allowed_packet = 1GB
```

- We recommend you use the same character set for the source and target databases.
  - Impact on the business: if the character sets of the source and target databases are different, there may be garbled characters.
  - Fix: run the following command to change the character sets of the source and target databases to the same one:
```
set character_set_server = 'utf8';
```

- We recommend you use a database with a specification above 2-core CPU and 4 GB memory.

- If you only perform full data migration, do not write new data into the source database during migration; otherwise, the data in the source and target databases will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.

- For data export with locks: you need to use `Flush Table With Read Lock` to temporarily lock tables in the source database, and the `MyISAM` table will be locked until the full data is exported. Currently, the lock wait timeout period is 60s, and if locks cannot be obtained before it elapses, the task will fail.

- For data export without locks: read locks will be added to tables without a primary key or non-null unique key.

- If the source database instance is a distributed database, you need to create sharded tables in the target database in advance; otherwise, the tables will become non-sharded tables after being migrated.

