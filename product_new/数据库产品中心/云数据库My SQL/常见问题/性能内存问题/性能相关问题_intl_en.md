
### Why does TencentDB for MySQL crash during task execution?
This is normal because it goes into a status of Lock Wait as the result of concurrent operations.

### Why is Chinese data garbled in TencentDB for MySQL?
When storing data to TencentDB for MySQL, please log in to the [console](https://console.cloud.tencent.com/cdb) and enter the details page of the instance to view the default character set. When writing the program, set `character_set_client`, `character_set_results`, and `character_set_connection` to the same character sets in the instance; otherwise, garbled text will appear if the data to be stored contains Chinese characters.
For example, the default character set of the TencentDB instance is UTF8. When writing a program to connect to the instance, you need to execute the following statements before storing Chinese data:
```
SET NAMES 'utf8';
```

### What are the common reasons and solutions for issues where the maximum number of connections to TencentDB for MySQL is reached?
- There are too many sleep threads. It is recommended to lower the values of wait_timeout and interactive_timeout in the console.
- Slow logs heaped up. The long_query_time parameter is 10s by default. It is recommended to change it to 1-2s and then observe slow logs.
- If there are few sleep threads and no slow logs heaped up, it is recommended to increase the value of the max_connections parameter in the console.

### What are the common reasons and solutions for a high utilization of CPU by TencentDB for MySQL?
- Slow logs heaped up. Please check for slow logs and full table scans in the instance monitor, then conduct analysis and optimization by referring to slow logs (which can be downloaded in the console). If no slow logs are found and there are only full table scans in the monitor, change the value of long_query_time to 1-2s and then analyze slow logs after using TencentDB for MySQL for a while.
- If no slow logs heaped up, please check the memory utilization in the instance monitor. If it is much higher than the instance specification and the disk read/write count increases significantly, there is a bottleneck in the memory, and it is recommended to upgrade the memory.


