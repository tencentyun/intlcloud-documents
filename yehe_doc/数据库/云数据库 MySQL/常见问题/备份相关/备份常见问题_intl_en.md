- **Backup capacity billing**
 -  [How is backup capacity billed?](#bfwt1)
 -  [How can I reduce the backup capacity cost?](#bfwt2)
- **Database backup**
 - [How do I configure automatic backup?](#bfwt3)
 - [Why can’t I initiate a manual backup task?](#bfwt13)
 - [Why can’t I logically back up and download by table?](#bfwt14)
 - [How do I back up data on my own?](#bfwt4)
 - [Can I download or restore backup files that exceed the retention period?](#bfwt11)
 - [Can I disable data and log backups?](#bfwt12)
 - [How do I cancel a backup task?](#bfwt9)
 - [Can I delete backups manually?](#bfwt8)
- **Backup and restoration**
 - [How do I download xbstream and qpress?](#bfwt16)
 - [Why can’t a downloaded backup file be unpacked/decompressed with tar?](#bfwt15)
 - [What should I do if the backup download is slow?](#bfwt10)
 - [Why does an error occur when I download data backup files?](#bfwt6)
 - [Can I restore the downloaded backups to another TencentDB for MySQL instance?](#bfwt7)
 - [How do I restore or migrate a basic single-node instance backup?](#bfwt5)


<span id = "bfwt1"></span>
### How is backup capacity billed?
TencentDB for MySQL offers a certain amount of backup capacity for free based on the region. The capacity is equivalent to the sum of the storage capacity of all two-node and three-node instances (including source instances) in the region.
For prices of backup capacity that exceeds the free tier, please see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).

<span id = "bfwt2"></span>
### How can I reduce the backup capacity cost?
- Delete manual backups that are no longer used (you can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID to access the instance’s management page, and delete manual backups on the **Backup and Restore** tab). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and retention period in the console, and the frequency should be at least twice a week).
>?The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backups and log backups (binlog). Rollback will be affected if you reduce the automatic backup frequency and retention period. Please select the parameters as needed.
>
- Reduce the retention period of data and log backups for non-core businesses (a 7-day retention period can meet the requirements of most scenarios).

| Business Scenario             | Recommended Backup Retention Period                                                 |
| -------------------- | ------------------------------------------------------------ |
| Core businesses             | 7-732 days                                              |
| Non-core and non-data businesses | 7 days                                                      |
| Archive businesses             | 7 days. We recommend that you manually back up data based on your business needs and delete the backups promptly after use |
| Testing businesses             | 7 days. We recommend that you manually back up data based on your business needs and delete the backups promptly after use |

<span id = "bfwt3"></span>
### How do I configure automatic backup?
You can configure it on the **Backup and Restore** tab in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/4df9e17b3d0d23d3e74f284e1e5efacd.png)

<span id = "bfwt4"></span>
### How do I back up data on my own?
TencentDB for MySQL instances are fully backed up on a daily basis by default. For more information, please see [Backing up Databases > Backup modes](https://intl.cloud.tencent.com/document/product/236/37796). You can also back up data by using the following methods:
- Use mysqldump.
- Use a third-party tool, such as Navicat Premium.
- [Log in to phpMyAdmin](https://intl.cloud.tencent.com/document/product/236/39352) and click **Export** on the navigation bar at the top.

<span id = "bfwt5"></span>
### How do I restore or migrate a basic single-node instance backup?
Basic single-node instances only support snapshot backups. For more information, please see [Offline Migration of Data > Data Migration via the Command Line Tool](https://intl.cloud.tencent.com/document/product/236/8464).

<span id = "bfwt6"></span>
### Why does an error occur when I download data backup files?
You can use the `wget -c 'backup file download address' -O custom filename.xb` command to download data backup files. Note that the download address should be placed inside a pair of single quotation marks (') to help the program identify it.

<span id = "bfwt7"></span>
### Can I restore the downloaded backups to another TencentDB for MySQL instance?
No. We recommend that you [use DTS to migrate a MySQL instance](https://intl.cloud.tencent.com/document/product/571/34103).

<span id = "bfwt8"></span>
### Can I delete backups manually?
- Automatic backups cannot be deleted manually. You can set the retention period for automatic backups, and the backups will be deleted automatically when they expire.
- Manual backups can be manually deleted from the backup list in the console. Manual backups can be retained permanently as long as they are not deleted.
 1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID to access the instance’s management page, and select the **Backup and Restore** tab.
 2. Click **Delete** in the **Operation** column in the backup list.

<span id = "bfwt9"></span>
### How do I cancel a backup task?
Backup tasks cannot be canceled.

<span id = "bfwt10"></span>
### What should I do if the backup download is slow?
We recommend that you copy the download address on the **Backup and Restore** tab in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), log in to a (Linux) CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for high-speed download over the private network.
>?`wget` command format: wget -c 'backup file download address' -O custom filename.xb

<span id = "bfwt11"></span>
### Can I download or restore backup files that exceed the retention period?
Expired backup sets will be deleted automatically and cannot be downloaded or restored.
- We recommend that you configure a backup retention period based on business needs or download the backup files locally via the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
- You can also manually back up instance data in the console. Manual backups will be retained permanently.
>?Manual backups will also take up the backup space. We recommend that you plan the usage of the backup space appropriately to reduce costs.

<span id = "bfwt12"></span>
### Can I disable data and log backups?
No. However, you can reduce the backup frequency and delete manual backups no longer used via the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) to lower the capacity usage.

<span id = "bfwt13"></span>
### Why can’t I initiate a manual backup task?
Please check the automatic backup time you configured. If the instance is performing the daily automatic backup task, you cannot initiate a manual backup task.

<span id = "bfwt14"></span>
### Why cannot I logically back up and download by tables?
After the [backup](https://intl.cloud.tencent.com/document/product/236/37796) feature was upgraded, both logical and physical backups adopted the new compression algorithm, making some download features currently unavailable. To perform logical backups by tables, you can log in to the TencentDB for MySQL console, click an instance ID to access the instance’s management page, click **Manual Backup** on the **Backup and Restore** tab, and select **Logical cold backup** > **Specify table** in the pop-up dialog box. You can also download the logical backup file from the backup list after the backup is completed.

<span id = "bfwt15"></span>
### Why can’t a downloaded backup file be unpacked/decompressed with tar?
Because backup files in the latest version adopt a new compression algorithm, they cannot be unpacked/decompressed using the tar tool. Instead, xbstream and qpress are required.
For more information about how to unpack/decompress backup files with xbstream and qpress, please see [Restoring Databases from Physical Backups](https://intl.cloud.tencent.com/document/product/236/31910) and [Restoring Databases from Logical Backups](https://intl.cloud.tencent.com/document/product/236/31909).

### [How do I download xbstream and qpress?](id:bfwt16)
- xbstream is a subprogram of Percona XtraBackup. To use it, you need to install Percona XtraBackup from binaries or `yum` repositories.
- Download qpress [here](http://www.quicklz.com/) and extract the qpress binary files by running the tar command.
For more information on XtraBackup and qpress installation, please see [Restoring Databases from Physical Backups](https://intl.cloud.tencent.com/document/product/236/31910).

