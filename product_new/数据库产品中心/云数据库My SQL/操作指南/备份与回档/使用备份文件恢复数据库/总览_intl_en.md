The TencentDB for MySQL backup system has gone live after transformation. In the new system, both physical and logical backups will be compressed and packaged. Specifically, a backup file is compressed with qpress first and then packed with xbstream offered by Percona. Backup files are in ```.xb``` format.
- The automatic backup feature only supports physical backup.
- Existing automatic logical backups will be switched to physical backups automatically. This will not affect your business access, but may have impact on your automatic backup habit. If you need logical backups, you can use the manual backup method in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) or [call the relevant API](http://intl.cloud.tencent.com/document/product/236/15844) to generate logical backups.

A database can be restored from a backup file as follows:
- For more information on restoration from a physical backup file, see [Restoring a Database from a Physical Backup](https://intl.cloud.tencent.com/document/product/236/33363).
- For more information on restoration from a logical backup file, see [Restoring a Database from a Logical Backup](https://intl.cloud.tencent.com/document/product/236/33364).
- For more information on restoration from a legacy physical backup file, see [Restoring a Database from a Physical Backup (Legacy)](http://intl.cloud.tencent.com/document/product/236/7944).

