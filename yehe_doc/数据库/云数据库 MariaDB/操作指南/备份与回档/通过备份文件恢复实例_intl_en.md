
You can view historical data by using the rollback feature of TencentDB for MariaDB. To restore your database instance locally, you can do so by following the instructions below.

## Prerequisites
### Preparing a server
To restore the database instance locally, ensure that the basic configuration of the server meets the following requirements:
- CPU: 2 or more cores.
- Memory: 4 GB or above.
- Disk capacity: It must be greater than the used space of the database and leave enough temporary space for the system.
- Operating system: CentOS

### Preparing a database
>!The version of the local database must be the same as that of the TencentDB instance.
>
Take installation of MariaDB 10.0.10 as an example:
1. Add the yum source.
```
vi /etc/yum.repos.d/mariadb-10.0.10.repo):
# MariaDB 10.0 CentOS repository list - created 2016-05-30 02:16 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
# baseurl = http://yum.mariadb.org/10.0/centos7-amd64
baseurl = http://archive.mariadb.org/mariadb-10.0.10/yum/centos6-amd64/
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=0
```
2. Check whether the version of the MariaDB instance corresponding to the yum source is 10.0.10.
```
yum makecache
yum info MariaDB-server
```
- Install MariaDB-server.
```
yum install MariaDB-server
```
>?If the system prompts a conflict with a legacy version, you need to remove the previously installed package, such as`yum remove mariadb-libs`.

### Installing the auxiliary tool
1. Install the MariaDB client
```
yum install MariaDB-client
```
- Install the LZ4 decompression software. For more information, see [Decompressing Backups and Logs] (https://intl.cloud.tencent.com/document/product/237/2088). LZ4 is installed in the `mysqlagent/bin` directory by default. You can also install it in the `/usr/bin` directory and import it as an environment variable.
```
yum install -y lz4
percona-xtrabackup
yum install http://www.percona.com/downloads/percona-release/redhat/0.1-3/percona-release-0.1-3.noarch.rpm
yum install percona-xtrabackup
```

### Downloading a backup
In the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), click an instance ID to enter the instance management page, and get the backup download address on the **Backup and Restoration** tab.
Sample download command:
```
wget  --content-disposition 'http://1x.2xx.0.27:8083/2/noshard1/set_1464144850_587/1464552298xxxxxxxx'
```

## Restoring Databases from Backup Files (Unencrypted)
#### [1. Enter the cold backup file download directory and decompress the file with LZ4](id:mulu_jieya)
```
lz4 -d set_1464144850_587.1464552298.xtrabackup.lz4
```

#### [2. Decompress the file to a temporary directory `xtrabackuptmp` with xbstream](id:gongju_jieya)
```
mkdir xtrabackuptmp/
mv set_1464144850_587.1464552298.xtrabackup xtrabackuptmp/
xbstream -x < set_1464144850_587.1464552298.xtrabackup
```
After the decompression, the directories and files are as shown below:
![](https://main.qcloudimg.com/raw/6ad248ceef84e26eaf8ee40437c12d9e.png)

#### 3. Use `innobackupex` to apply logs
```
mkdir /root/dblogs_tmp
innobackupex --apply-log  --use-memory=1G --tmpdir='/root/dblogs_tmp/' /root/xtrabackuptmp/
```
After the operation succeeds, `completed OK!` will be displayed.
![](https://main.qcloudimg.com/raw/80a99e3a653a840655be806f92e5e434.png)

#### [4. Stop the database and clear data files](id:tingzhi_qingkong)
```
service mysql stop
```
Clear data files (in data directories, tablespace directories, and log directories):
```
mkdir /var/lib/mysql-backup
mv /var/lib/mysql/* /var/lib/mysql-backup
```

#### 5. Modify the database parameter file
Modify the database parameter file `(/etc/my.cnf.d/server.cnf)`. For specific parameter values, see parameters in the extracted `backup-my.cnf` file. **Do not directly replace the parameter file with `backup-my.cnf`.**
```
[mysqld]
skip-name-resolve
datadir=/var/lib/mysql
innodb_checksum_algorithm=innodb
innodb_log_checksum_algorithm=innodb
innodb_data_file_path=ibdata1:2G:autoextend
innodb_log_files_in_group=4
innodb_log_file_size=1073741824
innodb_page_size=4096
innodb_log_block_size=512
innodb_undo_tablespaces=0
```

#### 6. Use `innobackupex` to load the image
```
innobackupex --defaults-file=/etc/my.cnf --move-back /root/xtrabackuptmp/
```
After loading succeeds, `completed OK!` will be displayed.
![](https://main.qcloudimg.com/raw/f193ec9e3d4693e103038ca9a1f280e1.png)

#### 7. Start the database
```
chmod 777 -R /var/lib/mysql
service start mysql
```
If you fail to start the database, you need to check and fix the error, and then try again.

#### 8. Connect to the database to check data
After starting the database, you may need to connect to the database with the original account and password to view data.

## Restoring Databases from Backup Files (Encrypted)
TDE is only supported for Percona 5.7 in Hong Kong region and MySQL 8.0.24 , but it will be available to more kernel versions in the future. You can access **Data Security** > **Data Encryption** on the instance management page in the [TencentDB for MariaDB console] (https://console.cloud.tencent.com/mariadb)

After data encryption is enabled, the database instances can’t be restored from a backup file. It is recommended to restore them as instructed in [Rolling back Databases] (https://intl.cloud.tencent.com/document/product/237/8719). 
>?To use the data encryption feature, [submit a ticket] (https://console.cloud.tencent.com/workorder/category) to apply for it.
>
