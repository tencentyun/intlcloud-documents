
This document describes how to set the binlog retention period for a TencentDB for MySQL instance in the console.

## Binlog Description
Binlog grows fast when a TencentDB for MySQL instance executes large transactions or lots of DML operations. Binlog is split every 256 MB and uploaded to COS. You can see the uploaded binlog files in the log list in the console.
![](https://main.qcloudimg.com/raw/bcf3d0d2ac291ccebbcfebea05fd11f1.png)

## Overview
Before being uploaded to COS, binlog files are stored on the instance disk (i.e., locally). You can set the local binlog retention period, control the maximum percentage of disk space binlog can take up, or expand disk space in the console. We recommend that you clear data no longer used to keep the disk utilization below 80%.
- MySQL’s data synchronization is based on binlog. To ensure database restorability, stability, and high availability, binlog cannot be disabled in TencentDB for MySQL.
- The generated binlog files are automatically backed up to COS via the [automatic backup feature](https://intl.cloud.tencent.com/document/product/236/37796) provided by TencentDB for MySQL. The binlog files whose backups are already uploaded to COS will be cleared according the local binlog retention policy. To prevent exceptions, the binlog files in use cannot be cleared even upon expiration. Therefore, the local binlog clearing has a delay.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID/name in the instance list, and access the instance management page.
2. On the **Backup and Restore** page, click **Configure Local Binlog**.
3. In the pop-up dialog box, specify the retention period and space utilization threshold, and click **OK**.


## FAQs
#### Will database restoration be affected if the local binlog retention period is too short?
No. Because the generated binlog files will be uploaded to COS via the automatic backup feature as soon as possible and those not uploaded yet cannot be cleared. However, the speed of rollback will be affected if the retention period is too short.

#### What is the default retention policy for local binlog?
By default, the local binlog retention period is 120 hours, the maximum binlog space utilization is 30%.

#### Will binlog files take up the instance disk space?
Yes. The binlog files are stored on the instance disk before they are uploaded to COS and cleared according to the retention policy.
