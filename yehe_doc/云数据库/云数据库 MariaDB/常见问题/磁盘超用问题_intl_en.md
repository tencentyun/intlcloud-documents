
## Overview
Starting from August 3, 2020, TencentDB for MariaDB will lock instances with disk utilization of 150% or more to prevent data loss. Locked disks cannot be written to. Please arrange the storage space of your instance, and clean up or expand in advance the disks that are going to be overused.

#### Compositions of disk space
- Data space: the space which your data takes up.
- System file space: the space which system tablespace files, redolog, undolog, and temp files take up.
>?Tencent Cloud offers space for binlog free of charge, so binlog does not take up the disk space you have purchased.
 
## Causes of Disk Overuse
The following may cause disk overuse:
- Data has taken up too much space: as the business expands, new data is constantly inserted, resulting in data space growth.

- Temp files have taken up too much space: temp tables are generated when complex query statements with `order by` or `group by` and the `alter table` statements are executed. Small temp tables are stored in memory, while large temp tables in disks.
- System files have taken up too much space: during the database installation, some system files will be initialized to maintain normal operation. If transactions remain pending to be submitted for a long time and a large number of UPDATE, INSERT and DELETE operations are executed, the log recording transaction information may be oversized.

## Solution
If a disk is overused, we recommend that you identify the cause and troubleshoot the issue as follows:
- If it is caused by data taking up too much space, you can delete legacy tables no longer used in order to release space. You can also expand your instance disk specification in the [console](https://console.cloud.tencent.com/mariadb), and the instance can be read from and written to after the expansion is completed.

- If it is caused by temp files taking up too much space, you can optimize the `order by` or `group by` query statements for your application, and monitor and clear sessions and transactions that take a long time to execute, in order to reduce temp files.
- If it is caused by system files taking up too much space, it may be because there are queries existing for a long time and the ibdata1 file is oversized. You can monitor and clear sessions and transactions that take a long time to execute, in order to reduce system file redundancy.
