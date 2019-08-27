## Scenario

The legacy TencentDB for Redis Cluster Edition instances (purchased before January 1, 2018) are on an older version and architecture, which may incur a stability risk. It is recommended that you upgrade them to the latest Redis Cluster Edition for better service stability.
The new edition comes with more flexible specification configuration, higher performance, and more comprehensive features. We will help you upgrade your legacy instances to Redis 2.8 Standard Edition or Redis 4.0 Cluster Edition from October 15, 2018 to January 30, 2019. For more information on the two new editions, see [Redis Standard Edition](https://intl.cloud.tencent.com/document/product/239/319591) and [Redis Cluster Edition](http://intl.cloud.tencent.com/document/product/239/18336).

> Hot migration from the legacy edition to a new edition is not supported. To avoid data loss in the migration process, writes to your Redis cluster need to be stopped once migration starts.
You can configure a security group to block all access requests or change the password to prohibit writes. You can check whether QPS is 0 on the monitoring page.

## Prerequisites
- You have purchased new Standard Edition or Cluster Edition instances.
>? If your existing data is less than 12 GB with incremental data of no more than 60 GB and QPS of no more than 40,000, Redis 2.8 Standard Edition is recommended; otherwise, Redis 4.0 Cluster Edition is your best choice. Redis 4.0 Cluster Edition does not support transactional commands, but other commands in it are completely compatible with the legacy edition. If you need transactional support, use Redis 2.8 Standard Edition.
- There is a CVM instance ready for data import, which needs to have sufficient disk capacity to accommodate the existing data.
- The data import tool crs-port has been installed. For more information on the tool usage and download address, see [here](https://intl.cloud.tencent.com/document/product/239/31940).

## Directions
1. Stop writes to the legacy Redis Cluster Edition instance.
2. Back up its data. The time backup takes depends on the amount of data. After backup is completed, an RDB file will be generated.
![](https://main.qcloudimg.com/raw/c4c2ce28b15f0e75c8fabe5c9cca69bf.png)
3. After backup is completed, you can view the backup file in the backup list. Click **Export** to generate an RDB file with a corresponding download link. Click the link to copy the private network download address and download the backup file on a private network CVM instance. Cross-AZ download is not supported.
4. Initialize the password of the newly purchased Redis 2.8 Standard Edition or Redis 4.0 Cluster Edition instance, which no longer supports the format of "instance ID:instance password". Instead, client access only requires the password. Use the crs-port tool to import the RDB file downloaded to the new instance.
```
crs-port restore -n 16 -i /data/dump.rdb -t 192.168.0.1:6379 -A passwd
```
5. After data import is completed, confirm whether the data is imported successfully in the console. You can view the actually used storage capacity in the configuration information on the instance details page.
6. To migrate your application to the new instance, simply replace the IP of the legacy instance in the code with the IP of the new instance.


