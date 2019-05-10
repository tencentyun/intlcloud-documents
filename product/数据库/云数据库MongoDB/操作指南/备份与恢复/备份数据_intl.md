TencentDB for MongoDB by default automatically backs up on a daily basis, and you can also choose to back up data manually.

### Instance auto-backup

1. Your instance by default gets backed up automatically from 1 am to 2 am on a daily basis. Instances have 1 full backup and 6 incremental backups every 7 days.
2. You can follow instructions below to change the automatic backup settings.
	1. When you frequently write, update or delete data, the instance oplog may be overwritten. Therefore, you can schedule multiple backups every day to ensure normal backups and rollbacks.
	2. You can set the start time of the backup. Note that the start time means the start time of the first backup if there are multiple backups every day.
	3. You can also set up the exceptional backup alarm. With this alarm enabled, the system sends alarm notifications to the recipient for overwritten oplog during the backup. To configure the alarm, see Cloud Monitor Alarms and Settings in the product event list.
	![](https://main.qcloudimg.com/raw/97c3b30b015845c2de6fe8accca12cad.png)
3.  The following is a backup list.
![](https://main.qcloudimg.com/raw/7c6a48c59d8f1a88f4bbc956351ca03f.png)

### Instance manual backup
Click **Manual Backup** on the instance details page, enter remarks, and submit manual backup task to the backend management system.
![](https://main.qcloudimg.com/raw/b67a177016b10d3d27597d914e35f51d.png)


