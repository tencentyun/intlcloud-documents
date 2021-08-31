TencentDB for MariaDB supports full backup and incremental backup, and backups are compressed with LZ4. For more information on how to use LZ4, please see [Decompressing Backup and Log Files](https://intl.cloud.tencent.com/document/product/237/2088).

#### Full backup
You can set the start time and retention period for full backups. By default, the backup starts at 00:00–05:00 AM, during which the performance is relatively low. The retention period is 7 days by default (30 days for finance cloud).

#### Incremental backup
Incremental backup is implemented based on binlogs, which are generated in real time. The binlogs use a certain amount of disk capacity, and are periodically uploaded to the TencentDB backup system.
