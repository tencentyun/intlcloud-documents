### How do I recover accidentally deleted data in TencentDB for MySQL?
- Data can be recovered through rollback. TencentDB for MySQL allows you to roll back databases or tables to any time point within the backup period. For more information, please see [Data Rollback](https://intl.cloud.tencent.com/document/product/236/7276).
- XtraBackup can be used to restore MySQL physical backup files to CVM-based self-created databases. For more information, please see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910).
- XtraBackup can be used to restore MySQL logical backup files to CVM-based self-created databases. For more information, please see [Restoring Database from Logical Backup](https://intl.cloud.tencent.com/document/product/236/31909).

### How do I recover accidentally dropped databases or tables in TencentDB for MySQL?
Data can be recovered through rollback. TencentDB for MySQL allows you to roll back databases or tables to any time point within the backup period. For more information, please see [Data Rollback](https://intl.cloud.tencent.com/document/product/236/7276).
>?If the database or table to be rolled back has been dropped, you need to log in to the TencentDB instance and create a database or table with the same name as before first before performing rollback in the console.

### If I accidentally delete some data that hasn't been backed up when performing a stored procedure in TencentDB for MySQL, can I restore the data?
With the rollback feature in the console, you can restore the data to any point in time within the backup period.

### Will the current table data be overwritten during a rollback in TencentDB for MySQL?
A rollback operation will generate a new database or table in the original instance. Upon the completion of rollback, you can see both the new and original databases or tables. The new database or table after rollback are named "original database or table name_bak".

### How do I query the real-time rollback progress and log when a TencentDB for MySQL rollback operation is underway?
You can query rollback progress and log during rollback in real time. For more information, please see [Data Rollback](https://intl.cloud.tencent.com/document/product/236/7276).

