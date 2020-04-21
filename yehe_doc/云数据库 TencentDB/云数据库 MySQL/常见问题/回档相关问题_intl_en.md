### How do I recover accidentally deleted data in TencentDB for MySQL?
- Data can be recovered through rollback. TencentDB for MySQL allows you to roll back databases or tables to any point in time during a backup cycle. For more information, please see [Data Rollback](https://intl.cloud.tencent.com/document/product/236/7276).
- XtraBackup can be used to restore MySQL physical backup files to CVM-based self-created databases. For more information, please see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910).
- XtraBackup can be used to restore MySQL logical backup files to CVM-based self-created databases. For more information, please see [Restoring Databases with Logical Backups](https://intl.cloud.tencent.com/document/product/236/31909).

### How do I recover accidentally dropped databases or tables in TencentDB for MySQL?
Data can be recovered through rollback. TencentDB for MySQL allows you to roll back databases or tables to any point in time during a backup cycle. For more information, please see [Data Rollback](https://intl.cloud.tencent.com/document/product/236/7276).

### If I accidentally delete some data that hasn't been backed up when performing a stored procedure in TencentDB for MySQL, can I restore the data?
With the rollback feature in the console, you can restore the data to any point in time within a backup cycle.

### Will the current table data be overwritten during a rollback in TencentDB for MySQL?
A rollback operation will generate a new database or table in the original instance. Upon the completion of rollback, you can see both the new and original databases/tables. The new database/table after rollback are named "original database/table name_bak".

### How do I query the real-time rollback progress and log when a TencentDB for MySQL rollback operation is underway?
You can query rollback progress and log during rollback in real time. For more information, please see [Data Rollback](https://intl.cloud.tencent.com/document/product/236/7276).

