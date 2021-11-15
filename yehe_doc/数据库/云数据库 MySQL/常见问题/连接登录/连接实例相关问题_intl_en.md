### How do I connect to a TencentDB for MySQL instance?
You can connect to a TencentDB for MySQL instance in the following ways:
- **Private network connection**: a CVM instance can be used to connect to the private network address of a TencentDB instance. This method relies on the high-speed private network of Tencent Cloud and features low delay.
The two instances must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region, or both in the classic network. 
- **Public network connection**: if you cannot access the private network, you can connect to your TencentDB for MySQL instance at its public network address. The public network address needs to be manually enabled. It can be viewed on the instance details page in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and can be disabled if no longer needed.

For more information, please see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788).

### What should I do if the connection to TencentDB for MySQL failed?
#### Failure to connect to TencentDB for MySQL from CVM or local computer
1. Use the diagnosis tool to locate the causes
The TencentDB for MySQL console provides a [one-click connectivity check tool](https://intl.cloud.tencent.com/document/product/236/40333) to help you locate the causes of connection failures. Then, you can make changes according to the prompts and retry to connect to the instance.
2. Locate the causes by yourself
If you cannot locate the cause of the problem with the one-click connectivity check tool, you can try to locate the cause by yourself by referring to the failure causes as described in [Instance Connection Failure](https://intl.cloud.tencent.com/document/product/236/40333).

#### Failure to connect to TencentDB for MySQL from DMC
1. Confirm that the database account has authorized all IPs of DMC servers in the region. For more information on authorization, please see [Modifying Host Addresses with Access Permissions](https://intl.cloud.tencent.com/document/product/236/31903). You can also set **%** as the host address authorized by the database account to allow all IPs and only use security groups to control database access.
2. If you confirm that all needed IPs are authorized, then the cause may be incorrect password. Accordingly, you can enter the password again, [reset the password](https://intl.cloud.tencent.com/document/product/236/31901), or [create a temporary account with sufficient permissions](https://intl.cloud.tencent.com/document/product/236/31900).

For more information, please see [Instance Connection Failure](https://intl.cloud.tencent.com/document/product/236/40333).

### How do I view the private/public network addresses?
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list to enter the instance details page, and view the private/public network addresses.

### How do I enable the public network address?
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list to enter the instance details page, and enable the public network address in **Public Network Address**.

### What should I do if I have slow access over the public network?
We recommend you use the private network. This connection method uses the high-speed private network with a low delay. For more information, please see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788).

### Can I use a CVM instance to connect to the private network address of a TencentDB for MySQL instance?
1. The following conditions must be met before you can use private network access:
The two instances must be in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region, or both in the classic network. 
2. You can check whether they are in the same VPC or both in the classic network in the following ways:
 - You can log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance) and view the network information of a CVM instance in the instance list or on the instance details page.
 - You can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and view the network information of an instance in the instance list or on the instance details page.
For more information, please see [Viewing network type and VPC information](https://intl.cloud.tencent.com/document/product/236/40333#wllxvpdff).


### What should I do if I can't use a CVM instance to connect to the private network address of a TencentDB for MySQL instance?
We recommend you use the [one-click connectivity check tool](https://intl.cloud.tencent.com/document/product/236/31927) to troubleshoot the problem first and then find the corresponding solution in [Instance Connection Failure](https://intl.cloud.tencent.com/document/product/236/40333#wfljcjwt) according to the check report.

### My CVM and TencentDB for MySQL instances are in different regions (such as Guangzhou and Shanghai, respectively). Can I use the private network for connection?
No. For solutions, please see [CVM and MySQL in different regions and different VPCs](https://intl.cloud.tencent.com/document/product/236/40333#dywt).

### My CVM and TencentDB for MySQL instances are in different AZs (such as Shanghai Zone 2 and Shanghai Zone 1, respectively) in the same region. Can I use the private network for connection?
Even if the CVM and TencentDB for MySQL instances are in the same region, they may be in different VPCs.
- If they are in different AZs in the same VPC, they can interconnect over the private network.
- If they are in different VPCs (such as VPC1 and VPC2, respectively), they cannot interconnect over the private network. For solutions, please see [CVM and MySQL in the same region but different VPCs](https://intl.cloud.tencent.com/document/product/236/40333#cmvbt).

### Can I use a CVM instance to connect to a TencentDB for MySQL instance directly over the private network when they are under different accounts?
No. However, you can use [CCN](https://intl.cloud.tencent.com/document/product/1003) to implement cross-account connection over the private network.

### [The verification with telnet found that the network and port connectivity of the TencentDB instance was good, but an error was reported when I tried to log in to it on the command line in the CVM instance. What should I do?](id:sytyzysjk)
- If "ERROR 1045(28000):Access denied for user..." is displayed, check whether the instance account and password entered are correct. If you forgot the password, you can [reset it](https://intl.cloud.tencent.com/document/product/236/31901). If the error persists after you enter the correct information again, log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance name to enter the instance management page, select **Database Management** > **Manage Account** to check whether restrictions are imposed on the IP connecting to your instance.

- The message "ERROR 1040(00000):Too many connections" indicates that the number of current connections to the TencentDB instance exceeds the limit. The common reasons and solutions are as follows:
i. There are too many sleeping threads. We recommend you lower the values of `wait_timeout` and `interactive_timeout` in the console.
ii. Slow queries heaped up. The `long_query_time` parameter is 10s by default. We recommend you change it to 1–2s and then observe slow query logs.
iii. If there are few sleeping threads and no slow queries heaped up, we recommend you increase the value of the `max_connections` parameter in the console.
- If "ERROR 2003 (HY000): Can't connect to MySQL server..." is displayed, check whether the instance IP and port entered are correct. If the error persists after you enter the correct information, check the security group policies of the instance in the console to verify whether the CVM instance has the permission to connect to the database. For more information, please see [TencentDB Security Group Management](https://intl.cloud.tencent.com/document/product/236/14470).
- If the connectivity test fails during data migration, check whether the security policy allows the prompted migration proxy IP.
- Check the `init_connect` parameter (if set), such as `mysql>set global init_connect='insert into db_monitor.accesslog(thread_id,log_time,localname,matchname) values(connection_id(),now(),user(),current_user())';`.
This means that each connection to the database by each non-super-privileged user will insert an entry into the `db_monitor.accesslog` table. Once there are uncommitted transactions or relevant lock waits in the table, then `insert into db_monitor.accesslog` operations will be jammed, causing all connections by non-super-privileged users to be stuck and affecting the normal use of TencentDB. Therefore, please configure the `init_connect` parameter with caution.

