# Restoring a Database Locally Using Physical Backup File
**If you want to use a physical backup file downloaded to the local computer to restore a database on other hosts, refer to this document**
#### 1. Downloading Backup File
For details on the steps, refer to [Download Instructions](https://intl.cloud.tencent.com/document/product/236/7358)
After the file is downloaded, the following information will be displayed:
![](https://mc.qcloudimg.com/static/img/d02b20501dd1c42a95f2b7a74c266b98/1.png)

#### 2. Decompressing Backup File
Decompress the backup file:
```
tar   xfv  backup.tgz
```
Query the file generated after the decompression. The directory files in blue are the databases where CDB resides in when the backup is generated.
![](https://main.qcloudimg.com/raw/60400fcbb47df35c77291c842c56c75e.png)

### 3. Modifying Configuration File
Due to version problems, please comment out
innodb_checksum_algorithm,
innodb_log_checksum_algorithm,
innodb_fast_checksum,
innodb_page_size,
innodb_log_block_size, and
redo_log_version in the decompressed file "backup-my.cnf", as shown below:
![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

#### 4. Modifying File Owner
Modify the file owner, and check whether the file belongs to a mysql user
```
chown -R mysql:mysql /home/mysql/backup/data
```
![](https://main.qcloudimg.com/raw/60400fcbb47df35c77291c842c56c75e.png)

#### 5. Starting mysql Process and Logging in for Verification
Start the mysql process, and verify whether it is successfully started
```
mysqld_safe --defaults-file=/home/mysql/backup/data/backup-my.cnf --user=mysql --datadir=/home/mysql/backup/data &
```
Log in to mysql for verification at the client
mysql  -uroot
![](https://mc.qcloudimg.com/static/img/346346626997b85385408ac728bf82ff/5.png)

Note:

* After the restoration, the table "mysql.user" does not contain the user created in the CDB, and you need to create one.
* Execute the following SQL before creating a new user:
```
delete from mysql.db where user<>'root' and char_length(user)>0;
delete from mysql.tables_priv where user<>'root' and char_length(user)>0;
flush privileges;
```






