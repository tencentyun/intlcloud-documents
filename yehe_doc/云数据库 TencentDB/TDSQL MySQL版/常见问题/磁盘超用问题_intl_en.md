## Overview
Starting from August 3, 2020, TDSQL for MySQL will lock instances with disk utilization of 150% or more to prevent data loss. Locked disks cannot be written to. Please organize your instance’s storage space, and clean up or expand in advance the disks that run the risk of being overused.

#### Disk space usage
- Data space: the space which your data takes up.
- System file space: the space which system tablespace files, redolog, undolog, and temp files take up.
>?Tencent Cloud offers space for binlog for free, therefore binlog does not take up any purchased disk space.
 
## Causes of Disk Overuse
The following may cause disk overuse:
- Too much data: as businesses expand, new data is constantly inserted, resulting in data space growth.

- Temp files too large: temp tables are generated when complex query statements with `order by` or `group by` and the `alter table` statements are executed. Small temp tables are stored in memory, while large temp tables in disks.
- System files too large: during the database installation, some system files will be initialized to maintain normal operation. If transactions are not submitted for an extended time and a large number of UPDATE, INSERT and DELETE operations are executed, the log recording transaction information may be too big.

## Solutions
If a disk is overused, we recommend that you identify the cause and troubleshoot the issue as follows:
- If the cause is data taking up too much space, you can delete legacy tables that are no longer in use to free up space. You can also expand your instance disk specification in the [console](https://console.cloud.tencent.com/dcdb); the instance can be read from and written to after the expansion is completed.

- If the cause is temp files taking up too much space, you can optimize the `order by` or `group by` query statements for your application, and monitor and clear sessions and transactions that take a long time to execute. These will reduce the number of temp files. 
- If the cause is system files taking up too much space, it may be due to existing extended queries and the ibdata1 file is oversized. You can monitor and clear sessions as well as transactions that take a long time to execute to reduce system file redundancy.
