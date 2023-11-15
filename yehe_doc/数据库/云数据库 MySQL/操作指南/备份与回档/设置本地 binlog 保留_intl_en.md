This document describes how to set the binlog retention period for a TencentDB for MySQL instance in the console.
>?
>- You cannot configure local binlog retention for single-node instances of cloud disk edition.
>- If there is a disaster recovery instance for the source instance, the local binlog retention period cannot be shorter than 120 hours. 

## Binlog Description
Binlog grows fast when a TencentDB for MySQL instance executes large transactions or lots of DML operations. Binlog is split every 256 MB and uploaded to COS. You can see the uploaded binlog files in the log list in the console.
![](https://main.qcloudimg.com/raw/bcf3d0d2ac291ccebbcfebea05fd11f1.png)

## Overview
Before being uploaded to COS, binlog files are stored on the instance disk (i.e., locally). You can set the local binlog retention period, control the maximum percentage of disk space binlog can take up, or expand disk space in the console. We recommend that you clear data no longer used to keep the disk utilization below 80%.
- MySQL's data sync is based on binlog. To ensure database restorability, stability, and high availability, binlog cannot be disabled in TencentDB for MySQL.
- The generated binlog files are automatically backed up to COS through the [automatic backup feature](https://intl.cloud.tencent.com/document/product/236/37796) provided by TencentDB for MySQL. The binlog files whose backups are already uploaded to COS will be cleared according the local binlog retention policy. To prevent exceptions, the binlog files in use cannot be cleared even they expire. Therefore, the local binlog clearing has a delay.
>?Rule for clearing expired binlog files:
>The local binlog files are checked once every 60 seconds. If a binlog file's start time or space usage does not meet the set retention rule, it will be added to the queue of to-be-deleted files. The binlog files in the queue will be sorted by time and deleted starting from the oldest file one by one until the queue is cleared.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** and click **Configure Local Binlog**.
3. In the pop-up window, specify the retention period and space utilization threshold and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/e5xL948_37.png)

## FAQs
#### Will database restoration be affected if the local binlog retention period is too short?
No, because the generated binlog files will be uploaded to COS through the automatic backup feature as soon as possible, and those not uploaded yet cannot be cleared. However, too short a retention period will affect the speed of rollback.

#### What is the default retention policy for local binlog?
By default, the local binlog retention period is 120 hours, and the maximum binlog space utilization is 30%. You can customize the retention period as needed. If there is a disaster recovery instance for the source instance, it cannot be shorter than 120 hours; otherwise, it can range from 72 to 168 hours.

#### Will binlog files take up the instance disk space?
Yes. Before the binlog files are uploaded to COS and cleared according to the retention policy, they will be stored on the instance disk.
