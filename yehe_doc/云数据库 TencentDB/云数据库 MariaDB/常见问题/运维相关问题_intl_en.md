### What should I do if some parameters I want to modify don't exist or cannot be modified in parameter settings?
The TencentDB Console supports most common database parameters and sets security thresholds for them. If a parameter to be modified does not exist or cannot be modified to a specific value, please submit a ticket for assistance and we will process it as soon as possible.

### I have purchased a CVM instance in East China (Shanghai Zone 2) and a TencentDB for MariaDB instance in Shanghai, and both of them are in the basic network. Why is the TencentDB for MariaDB instance unpingable on the CVM instance?
TencentDB disables ping by default.
You can use Telnet to check connectivity if needed.

### What can I do if Navicat MySQL 8.0.x of TencentDB for MariaDB has a connection error?
Please use the latest version for connection.

### What thread is `binlog dump` of TencentDB for MariaDB?
It is a normal master/slave sync thread, which is resident.

### What can I do if an error occurs when I use the multi-thread download tool Axel to download TencentDB for MariaDB backup or log files?
Due to operation strategies, multi-thread download is not supported. You can use the `wget --content-disposition` command for download.

### Why does the master/slave delay of TencentDB for MariaDB suddenly increase even to several minutes?
You can check whether you are running a very large SQL statement (e.g., batch insertion of a large amount of data). As the master needs to wait for response from the slave, the master/slave delay may seem long.

### What can I do if an error occurs when I run `SELECT INTO OUTFILE` or `./mysqldump` on a TencentDB for MariaDB instance to export files locally?
Files cannot be written to instance server directories.

### Why does an error similar to "READ ONLY" occur when I run `SELECT FOR UPDATE` on a TencentDB for MariaDB instance?
Some SQL statements do not support read/write separation. `SELECT FOR UPDATE` is a write operation and will cause an error.

### A large number of slow queries or performance problems occur shortly after I migrate data to TencentDB for MariaDB. How do I troubleshoot them?
You can enter the instance details page in the TencentDB for MariaDB Console and select "Performance Optimization" > "Slow Query Analysis" to specifically analyze the slow queries. 
Possible reasons include: 
- If connection failed, it may be because that a large number of slow queries previously affected the performance, and now TencentDB for MariaDB uses the thread pool mechanism to control the number of active threads, so the connection cannot be established. 
- Data was just migrated to the TencentDB for MariaDB instance and has not been fully cached to the memory; therefore, part of the data needs to be pulled from the disk with longer consumption time, leading to a drop in performance.

### How do I troubleshoot the `XA_RBTIMEOUT` error on a TencentDB for MariaDB instance?
It is possible that a large transaction has generated a super-large binlog. You are recommended to add an auto-increment field to the required tables.
![](https://main.qcloudimg.com/raw/126ef65cb6bbeb854ec0d9cca23e1ff7.png)

