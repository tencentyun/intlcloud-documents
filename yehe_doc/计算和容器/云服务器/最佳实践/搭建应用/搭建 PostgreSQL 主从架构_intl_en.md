## Overview

PostgreSQL is an open source relational database management system emphasizing scalability and standard compliance. PostgreSQL is ideal for enterprise-level complex online transaction processing (OLTP) systems. It supports NoSQL (JSON/XML/hstore) and Geographic Information System (GIS) data types. Featuring strong reliability and data integrity, PostgreSQL is a suitable for websites, location application systems, complex data object processing and other use cases.

This document describes how to build a PostgreSQL system on a CVM instance running CentOS 7.

## Software
This document uses the following software as an example to build PostgreSQL.
Linux: Linux operating system. This document uses CentOS 7.6 as an example.
PostgreSQL: Relational database management system. This document uses PostgreSQL 11.2 as an example.


## Prerequisites
- Two created CVM instances. One CVM instance works as the primary node and the other works as the secondary node.
For more information, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
- The security group rules for the two CVM instances have already been configured. Open the port 5432.
For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).

## Directions

### Configuring primary node

1. Log in to the primary CVM instance.
2. Run the following command to upgrade all packages, system versions and kernels.
```
yum update -y
```
3. Run the following command to install PostgreSQL storage repository.
```
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-6-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
4. Run the following command to install client package.
```
yum install postgresql11
```
5. Run the following command to install server package.
```
yum install postgresql11-server
```
6. Run the following command to initialize the database.
```
/usr/pgsql-11/bin/postgresql-11-setup initdb
```
7. Run the following command to start the service.
```
systemctl start postgresql-11
```
8. Run the following command to enable service autostart.
```
systemctl enable postgresql-11
```
9. Run the following command to switch to the `postgres` user.
```
su - postgres
```
10. Run the following command to enter the PostgreSQL terminal.
```
psql
```
11. Run the following command to set password for the `postgres` user.
```
ALTER USER postgres WITH PASSWORD 'Custom password';
```
12. Run the following command to create a database account (such as `postuser`) and set the password, login permission and backup permission.
```
create role account name login replication encrypted password 'Custom password';
```
For example, use the following command to create a database account naming `postuser` with the password `postuser`:
```
create role postuser login replication encrypted password 'postuser';
```
13. Run the following command to check if the account has been created.
```
SELECT usename from pg_user;
```
If the following result is returned, it indicates that the account has been successfully created.
```
usename  
 ----------
postgres
postuser
(2 rows)
```
14. Run the following command to check if the permission has been set.
```
SELECT rolname from pg_roles;
```
If the following result is returned, it indicates that the permission has been successfully set.
```
rolname  
 ----------
postgres
postuser
(2 rows)
```
15. Enter **\q** and press **Enter** to exit the PostgreSQL terminal.
16. Enter **exit** and press **Enter** to exit PostgreSQL.
17. Run the following command to open the `pg_hba.conf` file.
```
vim /var/lib/pgsql/11/data/pg_hba.conf
```
18. Press **i** to switch to edit mode. Add the following two lines to `IPv4 local connections`.
```
host    all             all             <IPv4 IP range of the secondary node’s VPC>          md5     #Enable the MD5 password encryption for connections in the IP ranges of the VPC
host    replication     database account        <IPv4 IP range of the secondary node’s VPC>        md5     ##Allow data synchronization from the `replication` database.
```
For example, if the database account is `postuser` and the IPv4 IP range of the secondary node’s VPC is `192.10.0.0/16`, add the following content to `IPv4 local connections`:
```
host    all             all             192.10.0.0/16          md5
host    replication     postuser        192.10.0.0/16          md5
```
19. Press **Esc** and enter **:wq** to save the file.
20. Run the following command to open the `postgresql.conf` file.
```
vim /var/lib/pgsql/11/data/postgresql.conf
```
21. Press **i** to enter edit mode, locate and modify the following parameters.
```
listen_addresses = 'xxx.xxx.xxx.xxx'   #The private IP addresses that are listened on.
max_connections = 100    #The maximum connections. The value of `max_connections` for the secondary node must be greater than that for the primary node
wal_level = hot_standby  #Enable hot standby mode.
synchronous_commit = on  #Enable synchronous replication
max_wal_senders = 32     #The maximum number of synchronization processes
wal_sender_timeout = 60s ##The timeout value for the streaming replication instance to send data.
```
22. Press **Esc** and enter **:wq** to save and close the file.
23. Run the following command to restart the service.
```
systemctl restart postgresql-11
```

### Configuring secondary node

1. Log in to the secondary CVM instance.
2. Run the following command to upgrade all packages, system versions and kernels.
```
yum update -y
```
3. Run the following command to install PostgreSQL storage repository.
```
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-6-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
4. Run the following command to install client package.
```
yum install postgresql11
```
5. Run the following command to install server package.
```
yum install postgresql11-server
```
6. Run the following command and use the pg_basebackup utility to create a backup directory:
```
pg_basebackup -D /var/lib/pgsql/11/data -h Private IP of primary node -p 5432 -U Database account -X stream -P
```
For example, if the private IP of the primary node is `192.10.123.321`, and the database account is `postuser`, run the following command:
```
pg_basebackup -D /var/lib/pgsql/11/data -h 192.10.123.321 -p 5432 -U postuser -X stream -P
```
Enter the password as prompted, and press **Enter**. If the following is returned, it indicates that the backup directory has been successfully created.
```
Password: 
24526/24526 kB (100%), 1/1 tablespace
```
7. Run the following command to copy configuration files of the primary node.
```
cp /usr/pgsql-11/share/recovery.conf.sample /var/lib/pgsql/11/data/recovery.conf
```
8. Run the following command to open the `recovery.conf` file.
```
vim /var/lib/pgsql/11/data/recovery.conf
```
9. Press **i** to switch to edit mode, locate and modify the following parameters:
```
standby_mode = on     #Declare the secondary node
primary_conninfo = ‘host=<Private IP of the primary node> port=5432 user=Database account password=Database password’ #Connection information of the primary node
recovery_target_timeline = ‘latest’ #Synchronize the latest data by using streaming replication
```
10. Press **Esc** and enter **:wq** to save the file.
11. Run the following command to open the `postgresql.conf` file.
```
vim /var/lib/pgsql/11/data/postgresql.conf
```
12. Press **i** to switch to edit mode, locate and modify the following parameters:
```
listen_addresses= 'xxx.xx.xx.xx'   #The private IP addresses that are listened on.
max_connections = 1000             #The maximum connections. The value of `max_connections` for the secondary node must be greater than that for the primary node
hot_standby = on                   #Enable hot standby mode
max_standby_streaming_delay = 30s  #The maximum delay for streaming replication
wal_receiver_status_interval = 1s  #The maximum interval for the secondary node to report its status to the primary node
hot_standby_feedback = on          #Enable the secondary node to report errors during replication.
```
13. Press **Esc** and enter **:wq** to save the file.
14. Run the following command to modify the group and owner of data directory:
```
chown -R postgres.postgres /var/lib/pgsql/11/data
```
15. Run the following command to start service.
```
systemctl start postgresql-11
```
16. Run the following command to enable service autostart.
```
systemctl enable postgresql-11
```

### Verifying deployment
Perform the following to verify the deployment.
1. Run the following command to check the `sender` process on the primary node:
```
ps aux |grep receiver
```
If the following is returned, it indicates that the `sender` process is available.
![](https://main.qcloudimg.com/raw/d25daabc3d32c58237dd20d871e6852a.png)
2. Run the following command to check the `receiver` process on the secondary node:
```
ps aux | grep receiver
```
If the following is returned, it indicates that the `receiver` process is available.
![](https://main.qcloudimg.com/raw/961283ed95a9640ba2121f5fafba2a7b.png)
3. On the primary node, run the following commands in sequence to check the secondary node status in the PostgreSQL terminal.
```
su - postgres
```
```
psql
```
```
select * from pg_stat_replication;
```
If the following is returned, it indicates that the secondary node status is available.
![](https://main.qcloudimg.com/raw/c85b5324929a4bffddd92c9dce906d56.png)
4. Verify that the secondary node synchronizes data with the primary node.
 1. On the primary node, run the following command to enter PostgreSQL terminal and create a database (such as `testdb`).
```
su - postgres
```
```
psql
```
```
create database testdb;
```
 2. On the secondary node, run the following commands in sequence to enter PostgreSQL terminal and check whether the secondary node is synchronized.
```
su - postgres
```
```
psql
```
```
"l",
```
If the following is returned, it indicates that the secondary node has been successfully synchronized.
![](https://main.qcloudimg.com/raw/2912a3d9892665469bff1768c76c7ae9.png)




