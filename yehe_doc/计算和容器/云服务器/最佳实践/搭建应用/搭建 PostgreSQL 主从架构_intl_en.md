## Overview

PostgreSQL is an open source relational database management system emphasizing scalability and standard compliance. PostgreSQL is ideal for enterprise-level complex online transaction processing (OLTP) systems. It supports NoSQL (JSON/XML/hstore) and Geographic Information System (GIS) data types. Featuring strong reliability and data integrity, PostgreSQL is a suitable for websites, location application systems, complex data object processing and other use cases.

This document describes how to build a PostgreSQL system on a CVM instance running CentOS 7.

## Software
This document uses the following software as an example to build PostgreSQL.
- Linux: Linux operating system. This document uses CentOS 7.6 as an example.
- PostgreSQL: Relational database management system. This document uses PostgreSQL 12 as an example.


## Prerequisites
- Two created CVM instances. One CVM instance works as the primary node and the other works as the secondary node.
For more information, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
- Port 5432 is open in the security group of both the CVM instances.
For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).

## Directions

### Configuring primary node

1. Log in to the primary CVM instance.
2. Run the following command to upgrade all packages, system versions and kernels.
```
yum update -y
```
3. Run the following commands in sequence to install PostgreSQL.
This document uses PostgreSQL 12 as an example. You can choose other versions as needed.
```
wget --no-check-certificate https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
```
rpm -ivh pgdg-redhat-repo-latest.noarch.rpm
```
```
yum install postgresql12-server postgresql12-contrib -y
```
```
/usr/pgsql-12/bin/postgresql12-setup initdb
```
4. Run the following command to start the service.
```
systemctl start postgresql-12.service
```
5. Run the following command to enable the service at startup.
```
systemctl enable postgresql-12.service 
```
6. Run the following command to switch to the `postgres` user.
```
su - postgres
```
7. Run the following command to go to the PostgreSQL interactive terminal.
```
psql
```
8. Run the following command to set the password for the `postgres` user, and enhance its security.
```
ALTER USER postgres WITH PASSWORD 'Custom password';
```
9. Run the following command to create a database account and set the password, login permission and backup permission.
```
create role account name login replication encrypted password 'Custom password';
```
This document uses creating the database account `replica` and the password `123456` as an example. Run the following command:
```
create role replica login replication encrypted password '123456';
```
10. Run the following command to check whether the account has been created.
```
SELECT usename from pg_user;
```
If the following result is returned, it indicates that the account has been successfully created.
```
usename  
----------
postgres
replica
(2 rows)
```
11. Run the following command to check whether the permission has been created.
```
SELECT rolname from pg_roles;
```
If the following result is returned, it indicates that the account has been successfully created.
```
rolname      
-------------------
pg_signal_backend
postgres
replica
(3 rows)
```
12. Enter **\q** and press **Enter** to exit the PostgreSQL interactive terminal.
13. Enter **exit** and press **Enter** to exit PostgreSQL.
14. Run the following command to open the `pg_hba.conf` configuration file and add the `replica` user to the allowlist.
```
vim /var/lib/pgsql/12/data/pg_hba.conf
```
15. Press **i** to switch to the edit mode, and add the following two lines to the `IPv4 local connections` section:
```
host    all             all             <IPv4 IP range of the secondary node's VPC>          md5     #Enable the MD5 password encryption for connections in the IP ranges of the VPC
host    replication     replica         <IPv4 IP range of the secondary node's VPC>        md5     #Allow data synchronization from the `replication` database.
```
For example, if the database account is `replica` and the IPv4 IP range of the secondary node's VPC is `xx.xx.xx.xx/16`, add the following content to `IPv4 local connections`:
```
host    all             all             xx.xx.xx.xx/16         md5
host    replication     replica         xx.xx.xx.xx/16         md5
```
16. Press **Esc** and enter **:wq** to save and close the file.
17. Run the following command to open the `postgresql.conf` file.
```
vim /var/lib/pgsql/12/data/postgresql.conf
```
18. Press **i** to enter the edit mode, locate and replace the following parameters:
```
listen_addresses = '*'   #The private IP listened on
max_connections = 100    #The maximum connections. The value of `max_connections` for the secondary node must be greater than that for the primary node
wal_level = hot_standby  #Enable hot standby mode.
synchronous_commit = on  #Enable synchronous replication
max_wal_senders = 32     #The maximum number of synchronization processes
wal_sender_timeout = 60s ##The timeout value for the streaming replication instance to send data.
```
19. Press **Esc** and enter **:wq** to save the file.
20. Run the following command to restart the service.
```
systemctl restart postgresql-12.service
```

### Configuring secondary node

1. Log in to the secondary CVM instance.
2. Run the following command to upgrade all packages, system versions and kernels.
```
yum update -y
```
3. Run the following commands in sequence to install PostgreSQL.
```
wget --no-check-certificate https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
```
rpm -ivh pgdg-redhat-repo-latest.noarch.rpm
```
```
yum install postgresql12-server postgresql12-contrib -y
```
4. Run the following command and use the pg_basebackup utility to create a backup directory:
```
pg_basebackup -D /var/lib/pgsql/12/data -h Public IP of the primary node> -p 5432 -U replica -X stream -P
```
Enter the password as prompted, and press **Enter**. If the following is returned, it indicates that the backup directory has been successfully created.
```
Password: 
24526/24526 kB (100%), 1/1 tablespace
```
5. Run the following command to copy the configuration files of the primary node.
```
cp /usr/pgsql-12/share/recovery.conf.sample /var/lib/pgsql/121/data/recovery.conf
```
6. Run the following command to open the `recovery.conf` file.
```
vim /var/lib/pgsql/12/data/recovery.conf
```
7. Press **i** to switch to the edit mode, locate and replace the following parameters:
```
standby_mode = on     #Declare the secondary node
primary_conninfo = 'host=<Public IP of the primary node> port=5432 user=Database account password=Database password' #Connection information of the primary node
recovery_target_timeline = 'latest' #Sync the latest data by using streaming replication
```
8. Press **Esc** and enter **:wq** to save and close the file.
9. Run the following command to open the `postgresql.conf` file.
```
vim /var/lib/pgsql/12/data/postgresql.conf
```
10. Press **i** to switch to the edit mode, locate and replace the following parameters:
```
max_connections = 1000             #The maximum connections. The value of `max_connections` for the secondary node must be greater than that for the primary node
hot_standby = on                   #Enable hot standby mode
max_standby_streaming_delay = 30s  #The maximum delay for streaming replication
wal_receiver_status_interval = 1s  #The maximum interval for the secondary node to report its status to the primary node
hot_standby_feedback = on          #Enable the secondary node to report errors during replication.
```
11. Press **Esc** and enter **:wq** to save and close the file.
12. Run the following command to modify the group and owner of the data directory:
```
chown -R postgres.postgres /var/lib/pgsql/12/data
```
13. Run the following command to start the service.
```
systemctl start postgresql-12.service
```
14. Run the following command to enable the service at startup.
```
systemctl enable postgresql-12.service
```

### Verifying deployment
Perform the following to verify the deployment.
1. Run the following command to back up the directory from the node.
```
pg_basebackup -D /var/lib/pgsql/12/data -h <Public IP of the primary node> -p 5432 -U replica -X stream -P
```
Enter the database password and press **Enter**. If the following is returned, it indicates that the backup directory has been successfully created.
```
Password: 
24526/24526 kB (100%), 1/1 tablespace
```
2. Run the following command to check the `sender` process on the primary node:
```
ps aux |grep sender
```
![](https://qcloudimg.tencent-cloud.cn/raw/bc610cf837b18158a8d0ddd89d5d87ae.png)
3. Run the following command to check the `receiver` process on the secondary node:
```
ps aux |grep receiver
```
If the following is returned, it indicates that the `receiver` process is available.
![](https://qcloudimg.tencent-cloud.cn/raw/13c908ae7d83ff8d5099f2c488b40046.png)
4. On the primary node, run the following commands sequentially to check the status of the secondary node in the PostgreSQL interactive terminal.
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
![](https://qcloudimg.tencent-cloud.cn/raw/c38c6faf64af66188df0e944b335353a.png)

