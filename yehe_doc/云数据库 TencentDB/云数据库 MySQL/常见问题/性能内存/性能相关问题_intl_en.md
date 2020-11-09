### How do I view the storage space usage of a TencentDB for MySQL instance?
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain), select **Performance Optimization** on the left sidebar, select the target database at the top, and select **Space Analysis**. 
On the space analysis page, you can view the comparison between daily increases in the last week, remaining space, estimated available days, and disk capacity usage trends in the last week. In addition, you can view the capacity utilization and fragmentation details of each database table in your instance.

### How do I analyze the full SQL execution track of a TencentDB for MySQL instance?
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain), select **Performance Optimization** on the left sidebar, select the target database at the top, and select **Audit Log Analysis**.
1. Click **Create Analysis Task** in the top-right corner of the view, select a time period, and click **Confirm**.
2. Click **View SQL Analysis** in the task list to access the SQL analysis page.
3. On the SQL analysis page, you can display the view by "SQL Type", "Host", "User", or "SQL Code". You can specify a time period to expand the view and view data at specific time points.
4. Click the SQL template on the target row, and the SQL statement details will be displayed on the right.
 - On the analysis page, you can view and copy specific SQL statements and optimize them based on the provided optimization advice or description.
 - On the statistics page, you can view the statistical analysis and execution duration track of the specified types of SQL statements by "Host", "User", and "SQL Code".

### How do I conduct performance optimization by myself when a TencentDB for MySQL instance is faulty or has an exception?
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain), select **Performance Optimization** on the left sidebar, select the target database at the top, and select **Exception Diagnosis**.
2. The "Diagnosis Prompt" column displays the diagnosis event history, including the health level, start time, diagnosis item, and duration. DBbrain performs health checks on the instance regularly.
3. You can click **View Details** or a diagnosis item in the "Diagnosis Prompt" to access the diagnosis details page. Click a diagnosis event in the view, and its details will be displayed below, including the event overview, symptom description, intelligent analysis, and expert advice. Based on the expert advice, you can perform optimization to solve the database exception and improve the instance performance.

### How can I receive the TencentDB for MySQL health report regularly?
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain), select **Performance Optimization** on the left sidebar, select the target database at the top, and select **Health Report**. You can view health score trends and the problem overview for the specified time period. 
- Select the report time range and click **Create Health Report**. After the task is completed, you can view or download the health report for the specified time period.  
- Click **Regular Generation Settings** to configure the frequency for automatically generating health reports. 

### How do I view and optimize MySQL slow logs?
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain), select **Performance Optimization** on the left sidebar, select the target database at the top, and select **Slow SQL Analysis**. The "SQL Statistics" section displays the number of slow queries and the CPU utilization of the instance.
2. You can click or drag slow queries in "SQL Statistics", and the aggregated SQL template and execution information will be displayed below. Each column of data can be sorted in ascending or descending order. The consumed time distribution section on the right displays the distribution of the overall SQL statement execution duration for the selected time period.
3. Click an aggregated SQL template and the SQL optimization advice and statistics will be displayed on the right. You can rewrite the SQL statement or add appropriate indexes based on the optimization advice to improve the SQL statement execution efficiency and database performance.


### Why does TencentDB for MySQL crash during task execution?
This is normal because it goes into a status of Lock Wait as the result of concurrent operations.

### Why is Chinese data garbled in TencentDB for MySQL?
When storing data to TencentDB for MySQL, please log in to the [console](https://console.cloud.tencent.com/cdb) and enter the details page of the instance to view the default character set. When writing the program, set `character_set_client`, `character_set_results`, and `character_set_connection` to the same character sets in the instance; otherwise, garbled text will appear if the data to be stored contains Chinese characters.
For example, the default character set of the TencentDB instance is UTF-8. When writing a program to connect to the instance, you need to execute the following statements before storing Chinese data:
```
SET NAMES 'utf8';
```

### What are the common reasons and solutions for issues where the maximum number of connections to TencentDB for MySQL is reached?
- There are too many sleep threads. We recommend you lower the values of `wait_timeout` and `interactive_timeout` in the console.
- Slow queries heaped up. The `long_query_time` parameter is 10s by default. We recommend you change it to 1-2s and then observe slow query logs.
- If there are few sleeping threads and no slow queries heaped up, we recommend you increase the value of the `max_connections` parameter in the console.

### What are the common reasons and solutions for a high utilization of CPU by TencentDB for MySQL?
- Slow queries heaped up. Please check for slow queries and full-table scans in the instance monitor, and then conduct analysis and optimization by referring to slow query logs (which can be downloaded in the console). If no slow queries are found and there are only full-table scans in the monitor, we recommend you change the value of `long_query_time` to 1-2s and then analyze slow queries after using TencentDB for MySQL for a while.
- If no slow queries heaped up, please check the memory usage in the instance monitor. If it is much higher than the instance specification and the disk read/write count increases significantly, there is a bottleneck in the memory, and we recommend you upgrade the memory.

### Which monitoring metrics of the instance should I usually pay attention to?
CPU utilization, memory utilization, and disk space utilization. You can [configure alarms](https://intl.cloud.tencent.com/document/product/236/8457) as needed, and when you receive alarms, you can take corresponding measures to resolve them.
