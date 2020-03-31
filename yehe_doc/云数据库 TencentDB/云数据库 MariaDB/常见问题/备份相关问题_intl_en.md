
### Does the backup feature of TencentDB for MariaDB support real-time backup?
Currently, real-time backup is not supported.

### How does TencentDB for MariaDB decompress a backup and restore it to a self-built instance?
For the detailed directions, please see [Restoring Instances from Backup Files](https://intl.cloud.tencent.com/document/product/237/4190?from_cn_redirect=1).

### What are the backup modes supported by TencentDB for MariaDB?
TencentDB supports full backup and incremental backup. For more information, please see 

### How do I decompress backup and log files of TencentDB for MariaDB?
Backup files and log files (binlog files) of TencentDB for MariaDB are compressed with LZ4 (Extremely Fast Compression algorithm). You can use LZ4 for decompression.
For decompression directions, please see [Decompressing Backup and Log Files](https://intl.cloud.tencent.com/document/product/237/2088).
