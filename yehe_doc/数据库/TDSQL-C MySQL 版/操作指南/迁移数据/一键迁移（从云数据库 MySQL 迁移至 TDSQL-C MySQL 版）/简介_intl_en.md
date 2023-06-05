This document describes how to perform the quick migration from TencentDB for MySQL to TDSQL-C for MySQL in the console.
## Background
TDSQL-C for MySQL is fully compatible with TencentDB for MySQL. It can deliver a high throughput of over one million QPS and a smart storage capacity up to the petabyte level, fully ensuring data security and reliability. TDSQL-C for MySQL also delivers better cost-effectiveness and performance in the same specifications.

Quick migration allows you to migrate full or incremental data in the console. which is suitable for migration from TencentDB for MySQL to TDSQL-C for MySQL. This feature can achieve smooth migration without downtime and retain original configurations such as original IP address, monitoring ,and parameters.
**Source Database**: TencentDB for MySQL
**Target Database**: TDSQL-C for MySQL
## Use Limits
- Quick migration is only supported from TencentDB for MySQL 5.7 or 8.0 in the single-node, two-node or three-node architecture to TDSQL-C for MySQL.
>? Quick migration is supported for all kernel minor versions. The cluster will automatically be upgraded to the latest kernel minor version when the migration succeeded.
- Currently, the quick migration is only supported for the source TencentDB for MySQL instance, and the migration of read-only instance and disaster recovery instance are in beta testing.

## Strengths
- All features are free of charge, and DTS is not required.
- No data loss in migration.
- Incremental migration is supported.
- Online migration is supported. When the connection address is switching from TencentDB for MySQL to TDSQL-C for MySQL, one momentary disconnection will occur.
- You can switch to TDSQL-C for MySQL without modifying any connection configuration in your application as the original connection address of the TencentDB for MySQL database will be retained after the migration.

[](id:QYDZB)
## Migration Specification Mapping Table
The mapping between the specifications of TencentDB for MySQL instance and the TDSQL-C for MySQL instance after migration is as follows:
>! Specification differences are marked in blue in the table.

| TencentDB for MySQL Single-Node Instance Specification | TencentDB for MySQL Two-Node Instance Specification | TencentDB for MySQL Three-Node Instance Specification | TDSQL-C for MySQL Instance Specification |
|---------|---------|---------|---------|
| 1-core 1000 MB MEM | 1-core 1000 MB MEM | 1-core 1000 MB MEM | 1-core 1 GB MEM |
| 1-core 2000 MB MEM | 1-core 2000 MB MEM | 1-core 2000 MB MEM | 1-core 2 GB MEM |
| 2-core 4000 MB MEM | 2-core 4000 MB MEM | 2-core 4000 MB MEM | 2-core 4 GB MEM |
| 2-core 8000 MB MEM | 2-core 16000 MB MEM | 2-core 16000 MB MEM | <font color="#0099FF">2-core 16 GB MEM |
| 4-core 8000 MB MEM | 4-core 8000 MB MEM | 4-core 8000 MB MEM | 4-core 8 GB MEM |
| 4-core 8000 MB MEM | 4-core 16000 MB MEM | 4-core 16000 MB MEM | 4-core 16 GB MEM |
|  | 4-core 24000 MB MEM | 4-core 24000 MB MEM | 4-core 24 GB MEM |
|  | 4-core 32000 MB MEM | 4-core 32000 MB MEM | 4-core 32 GB MEM |
|  | 8-core 16000 MB MEM | 8-core 16000 MB MEM | 8-core 16 GB MEM |
|  | 8-core 32000 MB MEM | 8-core 32000 MB MEM | 8-core 32 GB MEM |
|  | 8-core 48000 MB MEM | 8-core 48000 MB MEM | 8-core 48 GB MEM |
|  | 8-core 64000 MB MEM | 8-core 64000 MB MEM | 8-core 64 GB MEM |
|  | 12-core 48000 MB MEM | 12-core 48000 MB MEM | 12-core 48 GB MEM |
|  | 12-core 72000 MB MEM | 12-core 72000 MB MEM | 12-core 72 GB MEM |
|  | 12-core 96000 MB MEM | 12-core 96000 MB MEM | 12-core 96 GB MEM |
|  | 16-core 32000 MB MEM | 16-core 32000 MB MEM | <font color="#0099FF">16-core 64 GB MEM </font> |
|  | 16-core 64000 MB MEM | 16-core 64000 MB MEM | 16-core 64 GB MEM |
|  | 16-core 96000 MB MEM | 16-core 96000 MB MEM | 16-core 96 GB MEM |
|  | 16-core 128000 MB MEM | 16-core 128000 MB MEM | 16-core 128 GB MEM |
|  | 24-core 96000 MB MEM | 24-core 96000 MB MEM | 24-core 96 GB MEM |
|  | 24-core 128000 MB MEM | 24-core 128000 MB MEM | <font color="#0099FF">24-core 144 GB MEM </font>|
|  | 24-core 144000 MB MEM | 24-core 144000 MB MEM | 24-core 144 GB MEM |
|  | 24-core 192000 MB MEM | 24-core 192000 MB MEM | 24-core 192 GB MEM |
|  | 24-core 244000 MB MEM | 24-core 244000 MB MEM | <font color="#0099FF">32-core 256 GB MEM </font> |
|  | 24-core 256000 MB MEM | 24-core 256000 MB MEM | <font color="#0099FF">32-core 256 GB MEM </font> |
|  | 32-core 128000 MB MEM | 32-core 128000 MB MEM | 32-core 128 GB MEM |
|  | 32-core 192000 MB MEM | 32-core 192000 MB MEM | 32-core 192 GB MEM |
|  | 32-core 256000 MB MEM | 32-core 256000 MB MEM | 32-core 256 GB MEM |
|  | 48-core 192000 MB MEM | 48-core 192000 MB MEM | 48-core 192 GB MEM |
|  | 48-core 288000 MB MEM | 48-core 288000 MB MEM | 48-core 288 GB MEM |
|  | 48-core 384000 MB MEM | 48-core 384000 MB MEM | 48-core 384 GB MEM |
|  | 48-core 488000 MB MEM | 48-core 488000 MB MEM | 48-core 488 GB MEM |
|  | 64-core 256000 MB MEM | 64-core 256000 MB MEM | 64-core 256 GB MEM |
|  | 64-core 384000 MB MEM | 64-core 384000 MB MEM | 64-core 384 GB MEM |
|  | 64-core 512000 MB MEM | 64-core 512000 MB MEM | <font color="#0099FF">88-core 710 GB MEM </font>|
|  | 80-core 690000 MB MEM | 80-core 690000 MB MEM | <font color="#0099FF">88-core 710 GB MEM </font>|
|  | 90-core 720000 MB MEM | 90-core 720000 MB MEM | <font color="#0099FF">88-core 710 GB MEM </font>|

## Backup Policy
- As TDSQL-C for MySQL backup space is free of charge, you can use backup feature for free.
- TDSQL-C for MySQL does not support automatic logical backup and physical backup, but after the migration it will support the snapshot backup that features imperceptibility during backup and data restoration within seconds.
>?Snapshot backup period rules: Backup file is generated every 6-48 hours on a 24/7 uninterrupted basis, which has no impacts on the instance performance.
- TDSQL-C for MySQL allows you to set a retention period for the snapshot backup file, and you can roll back the instance data to any time point within this period.
