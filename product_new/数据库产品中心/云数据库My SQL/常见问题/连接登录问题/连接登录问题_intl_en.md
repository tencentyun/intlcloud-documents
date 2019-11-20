### My CVM and TencentDB for MySQL instances are deployed in the same region, how to connect to MySQL?
In this case, please use the private network for access. For more information on the connection method, see [Accessing a MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130).

### My CVM and TencentDB for MySQL instances are deployed in different regions, how to connect to MySQL?
In this case, please use the public network for access. For more information on the connection method, see [Public Network Access](http://intl.cloud.tencent.com/document/product/236/9038).

### How to troubleshoot connection issues in TencentDB?
If a connection or login issue occurs on your TencentDB instance, use telnet first to verify the network and port connectivity of the instance and then log in to it via the command line in CVM:
>The instance account is "root" by default, and the password is the account password configured during instance initialization.
>
```
mysql -h [instance IP] -P[instance port] -uroot -p[instance password]
```
The following are common errors and solutions:
- If "ERROR 1045(28000):Access denied for user..." is displayed, check whether the instance account and password entered are correct. If you forgot the password, you can reset it as instructed [here](http://intl.cloud.tencent.com/document/product/236/1271). If the error persists after you enter the correct information again, check whether restrictions are imposed on the IP accessing your instance in "[TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb)" > "Instance" > "Account Management".
2. If "ERROR 1040(00000):Too many connections" is displayed, it means that the number of current connections to the instance exceeds the limit. Common reasons and solutions are as follows:
i. There are too many sleep threads. It is recommended to lower the values of wait_timeout and interactive_timeout in the console.
ii. Slow logs heaped up. The long_query_time parameter is 10s by default. It is recommended to change it to 1-2s and then observe slow logs.
iii. If there are few sleep threads and no slow logs heaped up, it is recommended to increase the value of the max_connections parameter in the console.
3. If "ERROR 2003 (HY000): Can't connect to MySQL server..." is displayed, check whether the instance IP and port entered are correct. If the error persists after you enter the correct information again, check the security group policies of the instance in the console to verify whether CVM has the permission to access TencentDB. For more information, see [TencentDB Security Group](https://intl.cloud.tencent.com/document/product/236/14470).
4. If the connectivity test fails during data migration, check whether the security policy allows the prompted migration proxy IP.
5. Check the init_connect parameter (if set), such as mysql>set global init_connect='insert into db_monitor.accesslog(thread_id,log_time,localname,matchname) values(connection_id(),now(),user(),current_user())';
This means that each connection to the database by each non-super-privileged user will insert an entry into the db_monitor.accesslog table. Once there are uncommitted transactions or relevant lock waits in the table, then "insert into db_monitor.accesslog" operations will be jammed, causing all connections by non-super-privileged users to be stuck and affecting the normal use of TencentDB. Therefore, please configure the init_connect parameter with caution.
