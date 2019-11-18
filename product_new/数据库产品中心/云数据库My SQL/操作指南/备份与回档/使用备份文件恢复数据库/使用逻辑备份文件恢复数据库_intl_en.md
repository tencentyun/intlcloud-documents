## Operation Scenario
The document describes how to restore a database on another server from a downloaded logical backup file.

## Directions
### Downloading a Backup File
For more information on directions, see [Backup Download](http://intl.cloud.tencent.com/document/product/236/7274).

### Unpacking/Decompressing a Backup File
Like a physical backup, a logical backup also needs to be compressed with qpress and then packaged with xbstream. For more information on how to use xbstream and qpress, see [Restoring a Database from a Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910).
- Unpack a backup file with xbstream.
```
xbstream -x < test_import_57_backup_20181114115236.xb
```
The unpacking result is as shown below:
![logic_extract.png](https://main.qcloudimg.com/raw/46b0241deeeb4bedf2e9a5c69094914d.png)
- Decompress a backup file with qpress.
```
qpress -d test_import_57_backup_20181114115236.sql.qp .
```
The decompressing result is as shown below:
![logic_decompress.png](https://main.qcloudimg.com/raw/35dd58d19c642f3e961b52dec744415a.png)

### Importing into Database
Import the files into the database by running the following command:
```
mysql -uroot -P3306 -h127.0.0.1 -p < test_import_57_backup_20181114115236.sql
```
