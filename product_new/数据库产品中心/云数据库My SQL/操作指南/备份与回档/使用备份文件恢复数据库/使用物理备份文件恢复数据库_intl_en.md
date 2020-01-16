## Operation Scenario
The document describes how to restore a database on another server from a downloaded physical backup file.

## Directions
### Downloading a backup file
For more information on directions, see [Backup Download](https://intl.cloud.tencent.com/document/product/236/7274).

### Unpacking a backup file
1. Backup files are compressed with qpress and then packaged with xbstream (a packing/unpacking tool offered by Percona). Therefore, after a backup file is downloaded, it should be unpacked using xbstream first. The xbstream tool can be downloaded from the official website of Percona XtraBackup. Alternatively, you can directly download a binary package.
 - [Download from the official website of Percona XtraBackup and install](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/).
 Please select Percona XtraBackup 2.4.6 or higher. For more information on how to install the tool, see [Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI).
 - Binary package installation
The XtraBackup binary package appropriate for your OS can be downloaded [here](https://www.percona.com/downloads/Percona-XtraBackup-2.4/Percona-XtraBackup-2.4.13/binary/tarball/percona-xtrabackup-2.4.13-Linux-x86_64.libgcrypt145.tar.gz).
>Currently, XtraBackup is only supported on Linux but not available for Windows.
2. After XtraBackup is installed, run the xbstream command to unpack the backup file to the destination directory.
```
xbstream -x -C /data < ~/test.xb
```
The unpacking result is as shown below:
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

### Decompressing a backup file
Backup files are compressed with the quicklz algorithm, so they need to be decompressed first before use. After downloading the [qpress tool](http://www.quicklz.com/), you can extract qpress binary files by running the following command:
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
Then, decompress all `.qp` files in the destination directory by running the following qpress command:
```
xtrabackup --decompress --target-dir=/data
```
>
>- `xtrabackup --decompress` will call the qpress tool which should be installed before using the `--decompress` parameter.
>- The `--remove-original` options is supported only in Percona Xtrabackup v2.4.6 and higher.
>- `xtrabackup` won't delete the original files during decompression by default. If you want to delete them upon the completion of decompression, add the `--remove-original` parameter to the above command.
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

### Preparing a backup file
After a backup file is decompressed, you need to execute the "apply log" operation by running the following command.
```
xtrabackup --prepare  --target-dir=/data
```
If the execution result contains the following output, it means that the preparation succeeded.
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
	

### Modifying a configuration file
Given the existing version issues, the following parameters need to be commented out from the extracted file "backup-my.cnf".
- innodb_checksum_algorithm
- innodb_log_checksum_algorithm
- innodb_fast_checksum
- innodb_page_size 
- innodb_log_block_size
- redo_log_version 

![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

### Modifying file properties
Modify file properties and check whether files are owned by a TencentDB for MySQL user.
```
chown -R mysql:mysql /data
```
![](https://main.qcloudimg.com/raw/2c2bfcad8c8bdac9385e70d975bec56a.png)

### Starting the mysqld process and logging in for verification
1. Start the mysqld process.
```
mysqld_safe --defaults-file=/data/backup-my.cnf --user=mysql --datadir=/data &
```
2. Log in to the client for verification.
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

>
>- After restoration, the table "mysql.user" doesn't contain TencentDB users, which should be created.
>- The following SQL statements should be executed before creating a user:
```
delete from mysql.db where user<>'root' and char_length(user)>0;
delete from mysql.tables_priv where user<>'root' and char_length(user)>0;
flush privileges;
```
