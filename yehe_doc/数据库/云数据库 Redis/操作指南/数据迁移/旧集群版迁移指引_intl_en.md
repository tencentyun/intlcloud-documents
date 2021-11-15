
## Overview
The legacy TencentDB for Redis Cluster Edition instances (purchased before January 1, 2018) are on an older version and architecture, which may pose a risk to instance stability. We recommend that you migrate their data to TencentDB for Redis 4.0 Memory Edition (standard or cluster architecture).
TencentDB for Redis 4.0 comes with more flexible configuration, higher performance, and more comprehensive features. This document describes how to migrate data from your legacy instances to TencentDB for Redis 4.0 Memory Edition instances ([standard](https://intl.cloud.tencent.com/document/product/239/31959) or [cluster](https://intl.cloud.tencent.com/document/product/239/18336) architecture).

>!To avoid data loss, you need to stop writing to your legacy instances before migrating their data to TencentDB for Redis Memory Edition instances (standard or cluster architecture), as hot migration is unsupported in this case.
You can configure a security group or reset the password to block all access requests. You can check QPS on the monitoring page: if it is zero, all access requests are blocked successfully.

## Prerequisites
- You have purchased TencentDB for Redis Memory Edition instances (standard or cluster architecture).
>?If your existing data is less than 12 GB with expected incremental data of no more than 60 GB and QPS of no more than 40,000, or you need to use transaction commands, TencentDB for Redis 4.0 Memory Edition (standard architecture) is recommended; otherwise, TencentDB for Redis 4.0 Memory Edition (cluster architecture) is your best choice. The cluster architecture is compatible with all commands of the legacy instances except that it does not support transaction commands.
- You have a CVM instance ready for data import, which needs to have sufficient disk capacity to accommodate the existing data.
- The data import tool, redis-port, has been installed. For more information on the tool usage and download address, see [Migration with redis-port](https://intl.cloud.tencent.com/document/product/239/31940).

## Directions
1. Stop writing to the legacy Redis Cluster Edition instance.
2. Back up its data in the TencentDB for Redis console. The time backup takes depends on the amount of data. After backup is completed, an RDB file will be generated.
3. After backup is completed, you can view the backup file in the backup list. Click **Export** to generate an RDB file with a download link, copy the link, and use it to download the backup file from the CVM instance over a private network. Cross-AZ download is unsupported.
4. Initialize the password of the newly purchased TencentDB for Redis 4.0 Memory Edition (standard or cluster architecture) instance, and use redis-port to import the RDB file to it.
```
./redis-restore dump.rdb -t 127.0.0.1:6379
```
5. After the data import is completed, check whether it is successful by viewing the memory usage in the **Specs Info** block on the instance details page.
6. Migrate your application to the new instance by replacing the IP of the legacy instance in the code with that of the new instance.

