You can use the rollback feature of TencentDB for MariaDB to view historical data. To restore your database instance locally, restore the historical data by following the steps in this document.

## Prerequisites
### Preparing a server
If you need to restore the database instance locally, please ensure that the basic configuration of the server meets the following requirements:
- CPU: 2 or above cores.
- Memory: 4 GB or above.
- Disk capacity: it must exceed the database size plus the temporary capacity needed by the system.
- OS: CentOS.

### Preparing the database
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
>If the system prompts a conflict with a legacy version, you need to remove the previously installed package by running `yum remove mariadb-libs` for example.

### Installing the auxiliary tool
1. Install the MariaDB client.
```
yum install MariaDB-client
```
- Install the LZ4 decompression program. For more information, please see [Decompressing Backup and Log Files](https://intl.cloud.tencent.com/document/product/237/2088). LZ4 is installed in the `mysqlagent/bin` directory by default. You can also install it in the `/usr/bin` directory and import it as an environment variable.
```
yum install -y lz4
percona-xtrabackup
yum install http://www.percona.com/downloads/percona-release/redhat/0.1-3/percona-release-0.1-3.noarch.rpm
yum install percona-xtrabackup
```

### Downloading the backup
In the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql), click an instance name to enter the instance management page and get the backup download address on the **Backup and Restore** tab.
Sample of a download command:
```
wget  --content-disposition 'http://169.254.0.27:8083/2/noshard1/set_1464144850_587/1464552298xxxxxxxx'
```

## Restoring Database from Backup File (Unencrypted)
<span id = "mulu_jieya"></span>
#### 1. Enter the cold backup file download directory and decompress the file with LZ4
```
lz4 -d set_1464144850_587.1464552298.xtrabackup.lz4
```

<span id = "gongju_jieya"></span>
#### 2. Decompress the file with xbstream to the temporary directory `xtrabackuptmp`
```
mkdir xtrabackuptmp/
mv set_1464144850_587.1464552298.xtrabackup xtrabackuptmp/
xbstream -x < set_1464144850_587.1464552298.xtrabackup
```
After the decompression, the directories and files are as shown below:
![](https://main.qcloudimg.com/raw/6ad248ceef84e26eaf8ee40437c12d9e.png)

#### 3. Use innobackupex to apply logs
```
mkdir /root/dblogs_tmp
innobackupex --apply-log  --use-memory=1G --tmpdir='/root/dblogs_tmp/' /root/xtrabackuptmp/
```
After the operation succeeds, `completed OK!` will be displayed as shown below:
![](https://main.qcloudimg.com/raw/80a99e3a653a840655be806f92e5e434.png)

<span id = "tingzhi_qingkong"></span>
#### 4. Stop the database and clear data files
```
service mysql stop
```
Clear data files (in data directories, table space directories, and log directories):
```
mkdir /var/lib/mysql-backup
mv /var/lib/mysql/* /var/lib/mysql-backup
```

#### 5. Modify the database parameter file
Modify the database parameter file `(/etc/my.cnf.d/server.cnf)`. For specific parameter values, please see parameters in the extracted `backup-my.cnf` file. **Do not directly replace the parameter file with `backup-my.cnf`.**
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

#### 6. Use innobackupex to load the image
```
innobackupex --defaults-file=/etc/my.cnf --move-back /root/xtrabackuptmp/
```
After loading succeeds, `Complete OK!` will be displayed as shown below:
![](https://main.qcloudimg.com/raw/f193ec9e3d4693e103038ca9a1f280e1.png)

#### 7. Start the database
```
chmod 777 -R /var/lib/mysql
service start mysql
```
If the database fails to start, troubleshoot the error based on the error message and then try again.

#### 8. Connect to the database to view data
After starting the database, you may need to connect to the database with the original account and password to view data.

## Restoring Database from Backup File (Encrypted)
Transparent Data Encryption (TDE) is currently supported only in Percona 5.7. You can access it in TencentDB for MariaDB. Please download and install the critical tool needed by the restoration. Below is the encryption process:

#### 1. Decompress the backup file to the temporary directory
For more information, please see [Enter the cold backup file download directory and decompress the file with LZ4](#mulu_jieya) and [Decompress the file with xbstream to the temporary directory `xtrabackuptmp`](#gongju_jieya).

In this example, the backup file is decompressed to the temporary directory `./backup_dir`. **LZ4 is installed in the `mysqlagent/bin` directory by default. You can also install it in the `/usr/bin` directory and import it as an environment variable.**

#### 2. Get the data key plaintext
You can use an API of Key Management Service (KMS) for this step.
```
innobackupex --apply-log --rebuild-indexes  --use-memory=1G  --tmpdir=/tmp ./backup_dir/
```

#### 3. Prepare for data restoration
For more information, please see [Stop the database and clear data files](#tingzhi_qingkong).

#### 4. Get the data key plaintext
Before decrypting the data, you need to query the data key ciphertext in **Data Security** > **Data Encryption** on the instance management page in the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql). Then, you can use either of the following two schemes to decrypt the data key ciphertext to get the **data key plaintext**.
- Use a KMS API to get the data key plaintext on your own. For more information, please see the [KMS API documentation](https://intl.cloud.tencent.com/document/product/1030/32172).
- Use the Python script `./kms_tool.py` provided by Tencent Cloud to get the data key plaintext.
 - Parameter description:
    - --role: this parameter is in a fixed format. Enter `kmsTDSQLRole` here.
    - --secret_id, --secret_key: authorization information, which can be queried in [API Key Management](https://console.cloud.tencent.com/cam/capi) in **CAM**.
    - --region: region information, which can be queried in [KMS Common Parameters](https://intl.cloud.tencent.com/document/product/1030/32175).
    - --ciphertext: data key ciphertext.
![](https://main.qcloudimg.com/raw/c0b8552753c094fc6b0257c57e59872e.png)
 - Below is a demo:
```
python ./kms_tool.py --role="qcs::cam::uin/xxxxxxxxx:roleName/kmsTDSQLRole" 
--secret_id="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" --secret_key="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
--region="ap-hongkong" --ciphertext="CtFlCTPsA0+LilyvZ5V4nsEi6qSIA/KEhVeE8zQFIGfBwzXiMShQZIYYUt9KBWAUsHcfLQ0Z5feADH2D49/nOw==-k-fKVP3WIlGpg8m9LMW4jEkQ==-k-zudP3Tz4jxrvjs7zKkuKU+0V/gVVaNRRIIaRl/+83qCinaBgsLQbU5e1MpW4q/IJKpNXnb9N9/rO
5Es03fh7PU9n8Sjex6mnl+YKV1SMQog+RJ1E8bNmwx/22hhHb/1B5LGpwB8tbXKD3gL0tZwSJvV2QxSaUnONh5+6ssb2cQZI8MhcBBhGj9oXtbL6OC74PuDO1D/AsQ6qBLIqC2bTSA68s8Q="
```

#### 5. Generate the data key file again
After getting the data key plaintext, you can use either of the following two schemes to generate the data key file.
- Use an open-source TDE tool compatible with Percona to generate the file.
- Use the tool `./keyring_tool` provided by Tencent Cloud to generate the data key file. The basic command format of `./keyring_tool` is `./keyring_tool "[ciphertext]"  [File Path]`.
 ![](https://main.qcloudimg.com/raw/a23c3a8aa70281e3d0e0ec0c8aec1d6e.png)
 - Use double quotation marks to enclose the ciphertext of the data key string.
 - `keyring_tool`depends on `libboost_program_options.so.1.53.0`. If this lib does not exist in the system, you need to run `export LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH` first before using `keyring_tool`.
 
#### 6. Use the `./innobackupex` tool to apply the backup file
The figure below shows performing the `apply` operation on the backup file through `./innobackupex` till the end. During the operation, you need to use `--keyring-file-data=key_file` to specify the key by entering an absolute path.

xtrabackup mentioned in this document is the xtrabackup built in Tencent Cloud's proprietary TDSQL, which is stored in the `xtrabackup` directory in the TDSQL installation package directory by default.

Below is a demo of using this tool:
```
./innobackupex --apply-log  --use-memory=1G  --tmpdir=/tmp  --keyring-file-data=/data/home/test/key_file   ./backup/ 
```
![](https://main.qcloudimg.com/raw/97e34bfc2f7e44f6056bda395873e93e.png)

#### 7. Use the `./innobackupex` tool to copy the backup file to the data directory
The figure below shows moving the backup file with `./innobackupex`. You are recommended to use the permissions of the user who starts MySQL.
Below is a demo of using this tool:
```
./innobackupex --defaults-file='/data/home/seven/tdsqlinstall/percona-5.7.17/etc/my_8003.cnf' --move-back ./backup_dir/
```
![](https://main.qcloudimg.com/raw/32c59981a400f7e4bfc8c9096c476466.png)

#### 8. Use the `keyring_file` tool to configure the generated key file to MySQL
The figure below shows configuring the generated key file to MySQL. Please pay attention to the configuration in the red box. You are recommended to run `keyring_file` with the permissions of the user who starts MySQL.
![](https://main.qcloudimg.com/raw/2b4b6098a2f527902409fb3bac19fb61.png)

#### 9. Restart MySQL
The figure below shows the start script that comes with TDSQL. You can also use other schemes to start MySQL.
![](https://main.qcloudimg.com/raw/4c6cba9793eb01299b39c672b8bbab84.png)

#### 10. Access the encrypted table
After the encrypted backup is successfully restored, you can directly access the encrypted table. If the key is missing, the backup can still be restored, but the error message `can't find master key from keying, please check keyring plugin is loaded` will be displayed (for open-source MySQL or Percona, "Error" will be displayed) if you access the encrypted table.

