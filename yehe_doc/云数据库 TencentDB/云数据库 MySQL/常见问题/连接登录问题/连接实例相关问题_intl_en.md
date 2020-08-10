### How do I connect to a TencentDB for MySQL instance?
You can connect to a TencentDB for MySQL instance in the following ways:
- **Private network connection**: a CVM instance can be used to connect to the private network address of a TencentDB instance. This method relies on the high-speed private network of Tencent Cloud and features low delay.
The two instances must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/zh/document/product/215/535) in the same region, or both in the classic network. 
- **Public network connection**: if you cannot access the private network, you can connect to your TencentDB for MySQL instance at its public network address. The public network address needs to be manually enabled. It can be viewed on the instance details page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and can be disabled if no longer needed.

For more information, please see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/zh/document/product/236/3130).

### How do I view the private/public network address?
Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click an instance name in the instance list to enter the instance details page, and view the private/public network address.

### How do I enable the public network address?
Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click an instance name in the instance list to enter the instance details page, and enable the public network address in "Public Network Address".

### What should I do if I have slow access over the public network?
We recommend you use the private network. This connection method uses the high-speed private network with a low delay. For more information, please see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/zh/document/product/236/3130).

### Can I use a CVM instance to connect to the private network address of a TencentDB for MySQL instance?
1. The following conditions must be met to use the private network connection:
The two instances must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/zh/document/product/215/535) in the same region, or both in the classic network. 
2. You can check whether they are in the same VPC or both in the classic network in the following ways:
 - You can log in to the [CVM Console](https://console.cloud.tencent.com/cvm/instance) and view the network information of a CVM instance in the instance list or on the instance details page.
 - You can log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and view the network information of an instance in the instance list or on the instance details page.

### What should I do if I can't use a CVM instance to connect to the private network address of a TencentDB for MySQL instance?
We recommend you use [One-Click Connectivity Checker](https://intl.cloud.tencent.com/zh/document/product/236/31927) to troubleshoot the problem first and then find the corresponding solution in [Common Problems] according to the check report.

### My CVM and TencentDB for MySQL instances are in different regions (such as Guangzhou and Shanghai, respectively). Can I use the private network for connection?
No.

### My CVM and TencentDB for MySQL instances are in different AZs (such as Shanghai Zone 2 and Shanghai Zone 1, respectively) in the same region. Can I use the private network for connection?
Even if the CVM and TencentDB for MySQL instances are in the same region, they may be in different VPCs.
- If they are in different AZs in the same VPC, they can interconnect over the private network.
- If they are in different VPCs (such as VPC1 and VPC2, respectively), they cannot interconnect over the private network.

### Can I use a CVM instance to connect to the private network address of a TencentDB for MySQL instance when they are under different accounts?
No, as one of the prerequisites is that the CVM and MySQL instances must be under the same account.

### My CVM and TencentDB for MySQL instances meet the conditions of interconnection over the private network (under the same account and in the same VPC), but they still cannot connect. What should I do?
You can troubleshoot the problem in the following ways:
- Check whether the configurations of the security groups are correct.
- Check whether the host configuration of the database account is correct.

<span id = "sytyzysjk"></span>
### The verification with telnet found that the network and port connectivity of the TencentDB instance was good, but an error was reported when I tried to log in to it on the command line in the CVM instance. What should I do?
- If "ERROR 1045(28000):Access denied for user..." is displayed, check whether the instance account and password entered are correct. If you forgot the password, you can [reset it](https://intl.cloud.tencent.com/zh/document/product/236/31901). If the error persists after you enter the correct information again, log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click an instance name to enter the instance management page, select **Database Management** > **Manage Account** to check whether restrictions are imposed on the IP connecting to your instance.

- The message "ERROR 1040(00000):Too many connections" indicates that the number of current connections to the TencentDB instance exceeds the limit. The common reasons and solutions are as follows:
i. There are too many sleeping threads. We recommend you lower the values of `wait_timeout` and `interactive_timeout` in the console.
ii. Slow queries heaped up. The `long_query_time` parameter is 10s by default. We recommend you change it to 1–2s and then observe slow query logs.
iii. If there are few sleeping threads and no slow queries heaped up, we recommend you increase the value of the `max_connections` parameter in the console.
- If "ERROR 2003 (HY000): Can't connect to MySQL server..." is displayed, check whether the instance IP and port entered are correct. If the error persists after you enter the correct information, check the security group policies of the instance in the console to verify whether the CVM instance has the permission to connect to the database.
- If the connectivity test fails during data migration, check whether the security policy allows the prompted migration proxy IP.
- Check the `init_connect` parameter (if set), such as `mysql>set global init_connect='insert into db_monitor.accesslog(thread_id,log_time,localname,matchname) values(connection_id(),now(),user(),current_user())';`.
This means that each connection to the database by each non-super-privileged user will insert an entry into the `db_monitor.accesslog` table. Once there are uncommitted transactions or relevant lock waits in the table, then `insert into db_monitor.accesslog` operations will be jammed, causing all connections by non-super-privileged users to be stuck and affecting the normal use of TencentDB. Therefore, please configure the `init_connect` parameter with caution.




