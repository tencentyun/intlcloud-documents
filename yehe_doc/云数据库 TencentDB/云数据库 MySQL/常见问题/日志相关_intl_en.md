### How do I view binlogs?
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click an instance ID/name to access the management page. On the **Backup and Restore** > **Log Backup List** tab, locate the desired binlog and click **Download** to view it.
![](https://main.qcloudimg.com/raw/b411a99afeae2858ae578696ad9d66af.png)

### Why does my instance have no binlog?
Probably because data is written slowly into the binlog, which, accordingly, has not been split yet. A non-split binlog will not be displayed in the TencentDB for MySQL console.

The procedure of displaying binlogs in the MySQL console is as follows:
1. When the binlog grows to 256 MB, it is split.
2. The split binlog is uploaded to COS.
3. The uploaded binlog is displayed in the MySQL console.
The whole procedure takes about three minutes.

You can log in to the database and run the `flush logs` command, and then check the binlog in the MySQL console three minutes later.

### How do I view the latest binlog?
Log in to the database and run the `flush logs` command, and then check the binlog in the TencentDB for MySQL console three minutes later.

### How do I back up binlogs? 
The binlog is automatically backed up every day. To set the log backup retention period, you can log in to the TencentDB for MySQL console and click an instance ID/name to access the management page. On the **Backup and Restore** > **Log Backup List** tab, click **Auto Backup Settings** and set the log backup retention period in the pop-up dialog box.

