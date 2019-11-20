### Will the current table data be overwritten during a rollback in TencentDB for MySQL?
A rollback operation will generate a new database or table in the original instance. Upon the completion of rollback, you can see both the new and original databases/tables. The new table after rollback is named "original table name_bak".

### How to recover accidentally deleted data in TencentDB for MySQL?
Data can be recovered through rollback. TencentDB for MySQL allows you to roll back to any point in time during a backup cycle. For more information, see [Data Rollback](http://intl.cloud.tencent.com/document/product/236/7276).

### If some data that is not backed up is accidentally deleted while TencentDB for MySQL is executing a storage operation, can the data be recovered?
With the rollback feature in the console, you can recover the data to any point in time within a backup cycle.

### How to query the real-time rollback progress and log when a TencentDB for MySQL rollback operation is in process?
To do so, see [Data Rollback](http://intl.cloud.tencent.com/document/product/236/7276).



