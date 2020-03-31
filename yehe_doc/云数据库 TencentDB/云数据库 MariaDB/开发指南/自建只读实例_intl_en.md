## 1. Overview
### 1.1. Overview
If you only need to implement [read/write separation](https://intl.cloud.tencent.com/document/product/237/35409), currently, all TencentDB for MariaDB slaves support read-only access. For more information, please see [Read/Write Separation](https://intl.cloud.tencent.com/document/product/237/35409).

However, you may still need extra read-only instances to implement more flexible control and construct more complex business systems. Therefore, TencentDB for MariaDB supports the scheme of **self-creating read-only instances based on CVM**.

### 1.2. Architecture of self-created read-only instance
As shown below, the self-created instance feature "syncing" data to one or more self-created instances by using master/slave sync or binlog sync of TProxy outside a TencentDB for MariaDB cluster. With this feature, you can install any software or perform any data operations on the CVM instances you have control over.

![](https://mc.qcloudimg.com/static/img/a347c4d64a22c6b3f08c115c9e51c490/image.png)

To ensure the performance and stability of the TencentDB for MariaDB cluster, only the **async** scheme is provided for self-created read-only instances, and the data sync delay will be increased when the cluster pressure is high so as to reduce performance loss of the master cluster. This means the data delay of your self-created read-only instances may vary from several seconds to several minutes. If you require low delay, you are recommended to use [read/write separation](https://intl.cloud.tencent.com/document/product/237/35409) of TencentDB for MariaDB.

## 2. Creation Scheme
### 2.1. Determining the MariaDB kernel version
Generally, you can view the MariaDB kernel version in the instance list or instance details. Currently, MariaDB 10.0.10 and 10.1.9 are supported (more versions will be supported in the future, but the basic scheme will stay unchanged).
 
### 2.2. Creating a CVM instance with appropriate specifications
Create a CVM instance based on your existing instance memory and disk capacity.
	
- **CVM configuration**: you are recommended to create a CVM instance whose configuration is around 20% higher than that of your TencentDB for MariaDB instance, with at least 50 GB more data disk capacity and 2 GiB more memory. If you need to install other software on the CVM instance, please increase the CVM configuration as appropriate.
- **Operating system**: CentOS 6 or 7 is recommended.
- **Data disk formatting**: the ext3 file system is required, and the disk needs to be mounted to the `/data` directory.
- **Installed MariaDB**: the same version as the TencentDB for MariaDB instance must be installed.

### 2.3. Example of installing MariaDB
Take CentOS as an example. Install MariaDB (`mariadb 10.0.10`) by following the steps below:
	
- 1. Configure and add the yum source file (`vi /etc/yum.repos.d/mariadb.repo`):

> The official yum source for v10.0.10 is as shown below:
	```
	# MariaDB 10.0 CentOS repository list - created 2016-05-30 02:16 UTC
	# http://downloads.mariadb.org/mariadb/repositories/
	[mariadb]
	name = MariaDB
	#baseurl = http://yum.mariadb.org/10.0/centos7-amd64
	baseurl = http://archive.mariadb.org/mariadb-10.0.10/yum/centos6-amd64/
	gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
	gpgcheck=0
	```
> The official yum source for v10.1.9 is as shown below:
	```
	# MariaDB 10.1 CentOS repository list - created 2016-05-30 02:16 UTC
	# http://downloads.mariadb.org/mariadb/repositories/
	[mariadb]
	name = MariaDB
	#baseurl = http://yum.mariadb.org/10.1/centos7-amd64
	baseurl = http://archive.mariadb.org/mariadb-10.1.9/yum/centos6-amd64/
	gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
	gpgcheck=0
	```

- 2. Check whether the MariaDB version corresponding to the yum source is correct.

```
	yum makecache
	yum info MariaDB-server
```

- 3. Install "MariaDB-server" and "MariaDB-client".


```
	yum install MariaDB-server MariaDB-client MariaDB-devel -y
	Note: if the system prompts a conflict with a legacy version, you need to remove the previously installed package by running `yum remove mariadb-libs` for example.
```

### 2.4. Installing mydumper

Download address: https://launchpad.net/mydumper
Compile and install: `yum install make cmake pcre-devel glib2-devel zlib-devel gcc-c++`
Decompress `mydumper-0.9.1.tar.gz` and enter the directory for installation:
	cmake . 
	make && make install
Run `mydumper –V` after the installation to view the version information.

### 2.5. Configuring and starting MariaDB on the CVM instance

Delete the file `/etc/my.cnf.d/enable_encryption.preset`:
	rm -f /etc/my.cnf.d/enable_encryption.preset
Create a directory:
	mkdir -p /data/dbdata/{data,tmpdir}
	mkdir -p /data/dblogs/relay
Modify the configuration file `/etc/my.cnf.d/server.cnf:`:
```
	[mysqld]
	character-set-server = utf8
	collation-server = utf8_general_ci
	innodb_page_size=16384
	lower_case_table_names=1
	server-id=10
	innodb_buffer_pool_size=2097152000
	skip-name-resolve
	datadir = /data/dbdata/data/
	relay-log = /data/dblogs/relay/relay.log
	log-error = /data/dblogs/mysqld.err
	tmpdir = /data/dbdata/tmpdir
```

>		Precautions:
			When configuring these parameters, you can run `show global variables like xxx` on the original instance to view its parameters for reference.
			Parameters such as `character-set-server`, `lower_case_table_names`, and `innodb_page_size` must be the same as those in the original TDSQL instance.
			The value of `innodb_buffer_pool_size` can be set based on the same parameter in TDSQL.
			The value of `server-id` must be different from that in the original TDSQL instance.
		Run `mysql_install_db` to install the database.
		Modify the file owner:
	chown -R mysql:mysql /data/dbdata/  /data/dblogs/
		Start MariaDB:
			service mysql start
		Change the root password and test login:
			mysqladmin -u root password 'root';
	mysql -uroot -proot -hlocalhost -P3306


### 2.6. Creating a database account for sync

If you want to sync data from the master, create a regular account; if from a slave, create a read-only account (you are recommended to sync from the slave to avoid affecting the master).
The permissions of the database account should be set to include at least the permissions of global `SELECT, REPLICATION SLAVE, REPLICATION CLIENT, RELOAD` operations. **(If you fail to configure the permissions in the console, or there is no desired permission, please submit a ticket to contact the customer service for assistance.)**

### 2.7. Exporting TDSQL data with mydumper

>Note: there will be a table lock in the first export. Please evaluate whether this is acceptable to your business. You are recommended to perform this operation during off-peak hours.
Use mydumper to export TDSQL data (add the database to be synced after `-B`):
	`mydumper -t 4 --host 10.66.183.239 --port 3306 --user=user --password=password001 --outputdir=./export_tdsql -B syncdb`
	Use myloader to import TDSQL data (add the database to be synced after `-B`):
`myloader --host localhost --port 3306 --user=root --password=root -d ./export_tdsql -o -B syncdb`


### 2.8. Establishing the master/slave sync relationship
View the metadata file information exported in step 7.
	`cat export_tdsql/metadata`
It should contain the binlog location and `gtid` information; otherwise, the master/slave sync relationship cannot be established.
	```
	SHOW MASTER STATUS:
	Log: binlog.000003
	Pos: 64233211
		GTID:0-2694363359-883267
Log in to the database of the CVM instance to configure the master and slave:
		Configure the database to be synced:
			set global replicate_do_db='syncdb';
		Set `gtid_slave_pos`:
	SET GLOBAL gtid_slave_pos = "0-2694363359-883267";
	Configure the master/slave relationship:
	CHANGE MASTER TO 	MASTER_HOST='10.66.183.239',MASTER_PORT=3306,MASTER_USER='user',MASTER_PASSWORD='password111',master_use_gtid=slave_pos;
	Start the slave:
	START SLAVE;
	View the slave status:
	show slave status\G
	```
If `Slave_IO_Running` and `Slave_SQL_Running` are in running status, the configuration is successful.

## 5. Considerations and Feature Limits

- Read-only instances deployed based on CVM here will not be included in a TencentDB for MariaDB cluster for management, which means that if a node in the cluster fails, the read-only instances deployed in this scheme will never be promoted to master instance. Therefore, this feature will not improve the system availability.

- You can mount multiple self-created read-only instances; however, you are recommended to keep the quantity no more than 4 for the sake of business performance.

- The self-created read-only instance feature is currently free of charge.

