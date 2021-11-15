
### How do I access a TencentDB for MySQL instance?
TencentDB for MySQL can be accessed in the following methods:

| Method     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Private network access | A CVM instance can be used to access the private network address of a TencentDB instance. This access method relies on the high-speed private network of Tencent Cloud and features low delay. <li>The two instances must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region or both must be in the classic network.|
| Public network access | If you cannot connect to the private network, you can access your TencentDB for MySQL instance at its public network address. <li>The public network address needs to be manually enabled. It can be viewed on the instance details page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and can be disabled if no longer needed.|

For more information, please see [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130).

### How do I query the private/public network address?
Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click an instance name in the instance list to enter the instance details page, and view the private/public network address.

### Can I use a CVM instance to access the private network address of a TencentDB for MySQL instance?
Yes. To do this, the two instances must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region or both must be in the classic network. For more information, please see [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130).
- You can log in to the [CVM Console](https://console.cloud.tencent.com/cvm/instance), and view the network information of a CVM instance in the instance list or on the instance details page.
- You can log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), and view the network information of a MySQL instance in the instance list or on the instance details page.

>?CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).

### Can I use a CVM instance to access the private network address of a TencentDB for MySQL instance when they are in different availability zones in the same region?
Yes. To do this, the two instances must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region or both must be in the classic network. For more information, please see [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130).
- You can log in to the [CVM Console](https://console.cloud.tencent.com/cvm/instance), and view the network information of a CVM instance in the instance list or on the instance details page.
- You can log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), and view the network information of a MySQL instance in the instance list or on the instance details page.

>?CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).

### Can I use a CVM instance to access the private network address of a TencentDB for MySQL instance when they are under the same account but in different regions?
No. However, CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).
You can also access your TencentDB for MySQL instance at its public network address. For more information, please see [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130).

### Can I use a CVM instance to access the private network address of a TencentDB for MySQL instance when they are in the same region but under different accounts?
No. However, CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).
You can also access your TencentDB for MySQL instance at its public network address. For more information, please see [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130).

### What should I do if I have slow access over the public network?
We recommend that you use a CVM instance to access the private network address of a TencentDB instance. This access method relies on the high-speed private network of Tencent Cloud and features low delay. The two instances must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region or both must be in the classic network. For more information, please see [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130).
>?CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).

### How do I access a TencentDB for MySQL instance when my CVM and TencentDB for MySQL instances are deployed in the same region?
If the CVM and TencentDB instances are under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region or both are in the classic network, we recommend that you use a CVM instance to access the private network address of a TencentDB instance. This access method relies on the high-speed private network of Tencent Cloud and features low delay. For more information, please see [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130).
>?CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).


### How do I access a TencentDB for MySQL instance when my CVM and TencentDB for MySQL instances are deployed in different regions?
In this case, use the public network for access. For more information on the connection method, please see **Appendix 1. Enabling Public Network Access** in [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130).

### How do I troubleshoot connection issues in TencentDB?
If a connection or login issue occurs on your TencentDB instance, use `telnet` first to verify the network and port connectivity of the instance and then log in to it via the command line in CVM:
>?The instance account is "root" by default, and the password is the account password configured during instance initialization.
>
```
mysql -h [TencentDB instance IP] -P[TencentDB instance port] -uroot -p[TencentDB instance password]
```
The following are common errors and solutions:
- If "ERROR 1045(28000):Access denied for user..." is displayed, check whether the instance account and password entered are correct. If you forgot the password, you can [reset it](https://intl.cloud.tencent.com/document/product/236/31901). If the error persists after you enter the correct information again, log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click an instance name to enter the instance details page, select **Database Management** > **Manage Account** to check whether restrictions are imposed on the IP accessing your instance.
2. The message "ERROR 1040(00000):Too many connections" indicates that the number of current connections to the TencentDB instance exceeds the limit. The common reasons and solutions are as follows:
i. There are too many sleeping threads. We recommend lowering the values of `wait_timeout` and `interactive_timeout` in the console.
ii. Slow query log has heaped up. The `long_query_time` parameter is 10s by default. We recommend changing it to 1-2s and then observe slow query logs.
iii. If there are few sleeping threads and no slow logs heaped up, we recommend increasing the value of the `max_connections` parameter in the console.
3. If "ERROR 2003 (HY000): Can't connect to MySQL server..." is displayed, check whether the instance IP and port entered are correct. If the error persists after you enter the correct information again, check the security group policies of the instance in the console to verify whether CVM has the permission to access TencentDB. For more information, see [TencentDB Security Group](https://intl.cloud.tencent.com/document/product/236/14470).
4. If the connectivity test fails during data migration, check whether the security policy allows the prompted migration proxy IP.
5. Check the `init_connect` parameter (if set), such as `mysql>set global init_connect='insert into db_monitor.accesslog(thread_id,log_time,localname,matchname) values(connection_id(),now(),user(),current_user())';`.
This means that each connection to the database by each non-super-privileged user will insert an entry into the db_monitor.accesslog table. Once there are uncommitted transactions or relevant lock waits in the table, then "insert into db_monitor.accesslog" operations will be jammed, causing all connections by non-super-privileged users to be stuck and affecting the normal use of TencentDB. Therefore, please configure the `init_connect` parameter with caution.
