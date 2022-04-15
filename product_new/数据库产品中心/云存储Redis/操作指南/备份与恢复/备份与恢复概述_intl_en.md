
## Overview

TencentDB for Redis supports data backup and restoration. The backend service can automatically back up the instance data on a regular basis at a juncture configured in the console. Manual backup can also be pe rformed at any time. The backup data is saved in RDB format corresponding to the Redis Engine Edition and stored in COS for high data reliability. TencentDB for Redis supports instance data restoration through rollback and clone, which implements data restoration and clone in specific scenarios.

## Data Backup

TencentDB for Redis supports automatic and manual backups. For automatic backups, the backup time window can be customized.

### Automatic Backup

The TencentDB backend service periodically backs up the data of the instance. The backup cycle can be viewed and configured in **Backup and Restoration** > **Auto Backup** in the console.
By default, a full data backup will be performed every day between 02:00 and 08:00 with the backup file stored in COS. You can view the daily backup files in **Backup and Restoration** in the TencentDB for Redis Console.
The backup list displays all backup files and their information of the instance. TencentDB for Redis provides two backup download addresses. The public network download address allows you to download the backup data wherever you can access the internet. The private network download address allows you to download over the Tencent Cloud private network, which does not support cross-region download though, i.e., you can only download the data in the region where you Redis instance resides.

### Manual Backup

In addition to automatic backup that is performed by the system backend regularly, you can manually back up your instance in the TencentDB for Redis Console to meet your diversified needs. Manual backup files are also displayed in the backup list in the console, which can be distinguished from automatic backup files by the backup type **Manual Backup** in the list.

## Data Restoration

TencentDB for Redis supports restoration of data based on backup files. There are two ways to do so: restoring to the original instance or restoring to a new instance through cloning.

### Restoring an Instance

The TencentDB for Redis 2.8 Standard Edition (Community), Standard Edition (CKV), and Cluster Edition (CKV) supports instance restoration, which clears the existing data on an instance and restores the specified backup data to it. The instance is inaccessible during the restoration. You can select a desired backup file for restoration in the backup list on the **Backup and Restoration** tab in the TencentDB for Redis Console.

### Cloning an Instance

TencentDB for Redis 4.0 Standard Edition (Community) and Cluster Edition (Community) supports instance clone, i.e., creating a complete instance based on a backup file. The data of the instance is the same as that in the backup file. You can use the clone feature to analyze previous data. You can also roll back an instance by swapping the IPs of the new instance and the original instance.

