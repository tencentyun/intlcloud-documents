## Downloading Backup in the Console for Restoration
### 1. Install PostgreSQL
In the CVM instance where data is to be restored, install PostgreSQL on the same version as that of the backup data. If PostgreSQL has already been installed, this step can be skipped.
>This document shows you how to install PostgreSQL 10 and restore data on a CentOS 7-based CVM instance.
>
1. Log in to a Linux-based CVM instance. For more information, please see [Getting Started with Linux CVM](https://intl.cloud.tencent.com/document/product/213/2936).
2. Install PostgreSQL. The yum repository method is used in this document. You can click [here](https://yum.postgresql.org/) to find the needed yum repository.
Run the following command to install PostgreSQL 10:
```
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
yum install postgresql10-server postgresql10-contrib postgresql10 postgresql10.x86_64
```
>The command for installing PostgreSQL 9.5 is as follows:
```
yum install https://yum.postgresql.org/9.5/redhat/rhel-7.6-x86_64/pgdg-centos95-9.5-3.noarch.rpm
yum install postgresql95-server postgresql95-contrib postgresql95
```
3. Run the following command to check the installation result:
```
rpm -aq| grep postgres
```
A message similar to the one below will be returned:
```
[root@i-87-575-VM vmuser]# rpm -aq| grep postgres
postgresql10-libs-10.11-2PGDG.rhel7.x86_64
postgresql10-server-10.11-2PGDG.rhel7.x86_64
postgresql10-contrib-10.11-2PGDG.rhel7.x86_64
postgresql10-10.11-2PGDG.rhel7.x86_64
```

### 2. Create a recovery directory as postgres user
Switch to the postgres user and create a recovery directory in the CVM instance
```
mkdir /var/lib/pgsql/10/recovery
```
`recovery` is an example directory name, which can be modified as needed. In the following examples, the directory names will be the same for one major version. For example, the directory will be `/var/lib/pgsql/10` for PostgreSQL 10.x and `/var/lib/pgsql/9.5` for PostgreSQL 9.5.x.
>The command for PostgreSQL 9.5 is as follows:
```
mkdir /var/lib/pgsql/9.5/recovery
```

### 3. Download the full backup file
1. Log in to the [TencentDB for PostgreSQL Console](https://console.cloud.tencent.com/pgsql), select the desired instance in the instance list, and click **Manage** in the "Operation" column to enter the management page.
2. On the **Backup Management** tab, select the backup version to be restored based on backup time and click **Download** in the "Operation" column.
3. Download the backup file from the provided VPC address or public network address.
>
>- If a VPC address is to be used, the TencentDB instance and CVM instance should be in the same VPC, and the backup needs to be downloaded to the `/var/lib/pgsql/10/recovery` directory.
>- If a public network address is to be used, the downloaded backup file needs to be uploaded to the `/var/lib/pgsql/10/recovery` directory in the CVM instance. For more information, please see [How to Copy Local Files to CVM Instances](https://intl.cloud.tencent.com/document/product/213/2761).
>
After upload, the following information will be displayed:
![](https://main.qcloudimg.com/raw/e450c3acbab7f0c18560accbe7085184.png)

### 4. Decompress the full backup file
Run the following command to decompress the full backup file:
```
cd /var/lib/pgsql/10/recovery
tar -xf 20191221010146.tar.gz
```
After decompression, the following information will be displayed:
![](https://main.qcloudimg.com/raw/c5849130653dbf20598fc2edc75703a2.png)

### 5. Remove unnecessary temporary files
Run the following command to remove unnecessary temporary files:
```
rm -rf backup_label
```

### 6. Modify the configuration file
1. Comment out the following options in the `postgresql.conf` configuration file by using # at the beginning of the line.
Comment all out if there are multiple such options.
```
shared_preload_libraries
local_preload_libraries
pg_stat_statements.max
pg_stat_statements.track
archive_mode
archive_command
synchronous_commit
synchronous_standby_names
```
2. Modify the `postgresql.conf` configuration file.
```
port = '5432'    ## Change the value of the `port` parameter to 5432
unix_socket_directories = '/var/run/postgresql/'  ## Change the value of `unix_socket_directories` to `/var/run/postgresql/`; this step can be skipped if the value is not set
```
3. Append configurations to the `postgresql.conf` configuration file, indicating that the strong sync mode will no longer be used.
```
synchronous_commit = local
synchronous_standby_names = ''
```

### 7. Modify folder permissions as root user
```
chmod 0700 /var/lib/pgsql/10/recovery
chown postgres:postgres /var/lib/pgsql/10/recovery -R
```
After modification, the following information will be displayed:
![](https://main.qcloudimg.com/raw/ad8fe68e68c55f9b3165cbd9744656a7.png)

### 8. Use the incremental backup file (optional)
If this step is skipped, the content of the database is that when the full backup was started.
Put the xlog files in the `/var/lib/pgsql/10/recovery/pg_wal` folder; if the downloaded backup does not contain the `pg_wal` directory, please modify `pg_xlog` to `pg_wal`, and PostgreSQL will automatically replay the xlog files.
For example, if a full backup is started at 12:00 and all xlog files between 12:00 and 13:00 are put in the `pg_wal` folder, then data can be restored to 13:00.
>For PostgreSQL 9.x, the folder is `/var/lib/pgsql/9.x/recovery/pg_xlog`.
>

1. On the **Backup Management** page in the console, get the xlog download address and download the incremental backup file (xlog).
After download, the following information will be displayed:
![](https://main.qcloudimg.com/raw/2f7bc19401dc01363de4df37d9624536.png)
2. Decompress the log to the `pg_wal` folder.
```
tar -xf 20170904010214_20170905010205.tar.gz
```
![](https://main.qcloudimg.com/raw/acd7311a8434305dc252e8fe4475c600.png)

### 9. Start PostgreSQL as postgres user
```
/usr/pgsql-10/bin/pg_ctl start -D /var/lib/pgsql/10/recovery
```
![](https://main.qcloudimg.com/raw/33f99c711355ecb9c400b80a27214e66.png)

### 10.	Log in to PostgreSQL
1. Log in to PostgreSQL.
```
export PGDATA=/var/lib/pgsql/10/recovery
psql
```
![](https://main.qcloudimg.com/raw/bcc5757ce2bca7246601e22d3714d3af.png)
2. Check whether the database is running.
```
/usr/pgsql-10/bin/pg_ctl status -D /var/lib/pgsql/10/recovery
```
If the prompt is "server is running", the database is running.
![](https://main.qcloudimg.com/raw/52466f7ac534d4d27863868a739a1647.png)

## Manually Exporting Data for Restoration
You can also manually export backup data and then restore it on CVM. This scheme is applicable to both Windows and Linux regardless of the file system where physical files reside.

1. Dump the data on CVM as shown below:
```
Command format: pg_dump -h <access IP> -U <accessing user> -f <full path to the backup file> -c -C <name of the exported database>
Example:
/usr/pgsql-10/bin/pg_dump -h 192.168.0.16 -U testroot -f backup.sql -c -C postgres
```
 - If no file format is specified, a text file will be exported by default, as shown below:
```
-- PostgreSQL database dump
--
-- Dumped from database version 9.5.4
-- Dumped by pg_dump version 9.5.19
SET statement_timeout = 0;
SET lock_timeout = 0;
SET client_encoding = 'UTF8';
SET standard_conforming_strings = on;
SELECT pg_catalog.set_config('search_path', '', false);
SET check_function_bodies = false;
SET xmloption = content;
SET client_min_messages = warning;
SET row_security = off;
```
 - If there is a massive amount of data, specify the file format as binary file by using `-Fc`.
2. Restore the data on CVM.
 - For text files, data can be restored by running the following SQL statement:
```
psql -U postgres <./backup.sql
```
>As there are extension like pg_stat_error, an error may occur, but that does not affect data import.
 - For binary files, data needs to be restored by using `pg_restore`.
