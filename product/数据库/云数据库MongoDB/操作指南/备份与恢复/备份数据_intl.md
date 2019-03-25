TencentDB for MongoDB supports daily automatic backup by default, and users can also manually back up their data.

### Automatic backup of instances

1. The instances are backed up automatically every day by default. The default policy for automatic backup is as follows: the backup is started between 01:00 and 02:00 every day, and 1 full backup and 6 incremental backups are conducted every 7 days.
2. You can change the automatic backup settings, as shown below.
	1. When there are frequent write, update and delete operations, the instance oplog may be overwritten. To ensure normal backup and rollback operations, you can schedule multiple backups per day.
	2. You can set the start time of backup. Note that when you schedule multiple backups per day, this start time is the start time of the first backup.
	3. You can also set up the backup exception alarm. When this option is set to "Yes", the system will send an event alarm to the alarm recipient when it finds that oplog is overwritten during backup. For specific alarm configuration, see the Cloud Monitor event alarms and settings in the product event list.
	![](https://main.qcloudimg.com/raw/97c3b30b015845c2de6fe8accca12cad.png)
3. The backup list is shown as below.
![](https://main.qcloudimg.com/raw/7c6a48c59d8f1a88f4bbc956351ca03f.png)

### Manual backup of instances
On the instance details page, click **Manual Backup** and enter remark information, and then submit the manual backup task to the backend management system.
![](https://main.qcloudimg.com/raw/b67a177016b10d3d27597d914e35f51d.png)

