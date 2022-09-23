## Issue
The source or target database connectivity test fails when you create a data migration, sync, or subscription task.

## Possible Causes
- If the Telnet test fails, the causes may be:
  - [The server where the source database resides has a security group or firewall configured.](#1)
  - [The source IP addresses are blocked in the source database.](#2)
  - [The source database port is not opened.](#3)
  - [There is a network conflict, such as IP range conflict or incorrect parameter configuration.](#4)
  - [After an access type is selected and the connectivity verification is passed, the access type is changed.](#7)
  
- If the Telnet test is passed, but the database connection fails, the causes may be:
  - [There is an account authorization problem.](#5)
  - [The account or password is incorrect.](#6)

## [Security Group or Firewall Configured in Network or Server of Source Database](id:1)
A security group is similar to a firewall. It is a group of network security settings for databases in the cloud.

Check as follows based on the actual conditions:
- If the source database is a self-built database, check whether the server where the source database resides is configured with firewall policies, and if so, disable the firewall.
  - Windows: Open Control Panel and find the Windows Defender Firewall and check whether firewall policies are configured.
  - Linux: Run the `iptables -L` command to check whether the server is configured with firewall policies.
  
- If the source database is a TencentDB database, check whether DTS IP range is blocked in the security group of the database, and if so, modify as follows:
When the connectivity test fails, the IP range that needs to be allowed for DTS will be displayed in the console as shown below:
1. Log in to the source database (with MySQL as an example) and click an instance ID in the instance list to enter the instance management page.
  2. On the instance management page, select the **Security Group** tab and check whether there are policies blocking the SNAT IP range of DTS.
  ![](https://qcloudimg.tencent-cloud.cn/raw/dad72032f72e3352fbf9da92ce91d6ac.png)
3. Set the DTS IP range policy to **Allow**.
  ![](https://qcloudimg.tencent-cloud.cn/raw/00ab6591945c4c7508e9a2400814ef90.png)

- If the source database is a third-party cloud database, check the security group settings.

## [Source IP Addresses Blocked in Source Database](id:2)
### Check method
#### MySQL
- On the server where the source database is deployed, use the database account and password entered in the data migration task to connect to the source database. If the database can be normally connected, the source IP address may be blocked in the source database.
- For self-built database, you need to check the `bind-address` configuration in the database. If it is not `0.0.0.0`, the IP is blocked.
- If the source database is MySQL, you can use the MySQL client to connect to it, run the following SQL statement, and check whether the list of authorized IP addresses contains the SNAT IP addresses of DTS in the output result.
When granting database permissions to users, the authorized IPs must include the SNAT IPs; otherwise, they may be blocked; for example:
```
root@10.0.0.0/8  // Authorize users to access through `10.0.0.0/8`, and other IPs will be blocked (incorrect configuration)
root@%           // Authorize users to access all IPs, which should include the SNAT IPs (correct configuration)
```
You can verify as follows:
```
select host,user,authentication_string,password_expired,account_locked from
mysql.user WHERE user='[\$Username]';   // `[\$Username]` is the database account entered in the data migration task
```

#### SQL Server
Check whether there is an endpoint or trigger that blocks the access source IP address in the source database.

#### PostgreSQL
- If the source database is a third-party cloud database, check whether the secure access policies in the source instance have restrictions. Check as follows according to the specific cloud vendor:
- If the source database is a self-built PostgreSQL database, enter the `data` directory in the `$PGDATA` directory, find the `pg_hba.conf` file, and check whether the file contains a `deny` policy or only allows access from certain IP addresses over the network.
```
# cat pg_hba.conf
local   replication     all                                     trust
host    replication     all             127.x.x.1/32            trust
host    replication     all             ::1/128                 trust
host    all             all             0.0.0.0/0               md5
host    all             all             172.x.x.0/20          md5
```

#### MongoDB/Redis
For self-built database, you need to check the `bind` configuration in the database. If it is not `0.0.0.0`, the IP is blocked.

### Fix
#### [MySQL](id:MySQL)
1. If the source database is MySQL, run the following SQL statement in it to authorize the user configured in the data migration task.
```
mysql> grant all privileges on . to '[\$UserName]'@'%';  // `[\$Username]` is the database account entered in the data migration task
mysql> flush privileges;
```
2. If the source database is a self-built database, you also need to check whether the `bind-address` configuration is abnormal, and if so, modify it as instructed below.
   2.1. Add the following content to the `/etc/my.cnf` file:
>?The default path of the `my.cnf` configuration file is `/etc/my.cnf`, subject to the actual conditions.
>
```
bind-address=0.0.0.0 # All IP addresses or specified addresses
```
   2.2. Restart the database.
```
service mysqld restart
```
   2.3. Check whether the configuration takes effect.
```
netstat -tln
```
3. Run the verification task again.

#### SQL Server
Disable the firewall or trigger.

#### PostgreSQL
1. Add an access policy allowing the DTS IP range to the `pg_hba.conf` file or temporarily open all IP ranges in the access policy during migration. For example, add the following line to the `pg_hba.conf` file:
```
host    all             all             0.0.0.0/0               md5
```
2. After the modification is completed, you can restart the database instance to make the configuration take effect:
```
pg_ctl -D $PGDATA restart
```
3. Run the verification task again.

#### MongoDB
Configure `bind-address` as instructed in [MySQL](#MySQL).

#### Redis

1. Disable the `bind` configuration in `redis.conf` or change it to `0.0.0.0`.
2. Restart the database to make the configuration take effect and execute the verification task again.

## [Closed Network Port](id:3)
Below are the default ports for common databases. You need to check whether they are opened, and if not, open them based on the actual conditions:

If the source database is SQL Server, you need to open the file sharing service port 445 at the same time.

- MySQL: 3306
- SQL Server: 1433
- PostgreSQL: 5432
- MongoDB: 27017
- Redis: 6379

## [Network Conflict](id:4)
If you select the [VPN/Direct Connect](https://intl.cloud.tencent.com/document/product/571/42651) or [CCN](https://intl.cloud.tencent.com/document/product/571/42650) access method, you can refer to the documentation for troubleshooting.

## [Migration Account Authorization](id:5)
Authorize the migration account again as instructed in the corresponding scenario in [Migration from MySQL to TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/571/42645) and [Sync from MySQL/MariaDB/Percona to TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/571/47344).

## [Incorrect Database Account or Password](id:6) 
Log in to the source database to check whether the account and password are correct.

## [Access Type Change](id:7)

For the same source and target databases, if an access type such as **Public Network** is selected and the connectivity verification is passed, you cannot switch to another access type such as **Direct Connect**; otherwise, an error will be reported during connectivity verification.

