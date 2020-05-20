### How do I view the storage capacity usage of a TencentDB for MySQL instance?
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain), select **Diagnosis and Optimization** on the left sidebar, and select **Space Analysis** at the top. 
On the capacity analysis page, you can view the comparison between daily increases in the last week, available disk capacity, estimated number of available days, and disk capacity usage trends in the last week. In addition, you can view the capacity utilization and fragmentation details of each database table in your instance.
 ![](https://main.qcloudimg.com/raw/75a091b678a71f506f9abb5a76fe7a2b.png)

### How do I analyze the full SQL execution track of a TencentDB for MySQL instance?
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain), select **Diagnosis and Optimization** on the left sidebar, and select **Audit Log Analysis** at the top.
1. Click **Create Audit Task** in the top-right corner of the view, select a time period, and click **Confirm**.
2. Click **View SQL Analysis** in the task list to access the SQL analysis page.
![](https://main.qcloudimg.com/raw/60c636949f6bcbafe726256d2a08db5f.png)
3. On the SQL analysis page, you can display the view by SQL Type, Host, User, and SQL Code and specify a time period to expand the view and view data at specific time points.
 ![](https://main.qcloudimg.com/raw/67b3409d58404ba8de1059e0bf3aa79a.png)
4. Click the SQL template on the target row, and the SQL statement details will be displayed on the right.
 - On the analysis page, you can view and copy specific SQL statements and optimize them based on the provided optimization suggestion or description.
 - On the statistics page, you can view the statistical analysis and execution duration track of the specified types of SQL statements by Host, User, and SQL Code.
 
### How do I perform diagnosis or optimization by myself when a TencentDB for MySQL instance is faulty or has an exception?
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain), select **Diagnosis and Optimization** on the left sidebar, and select **Exception Diagnosis** at the top.
2. The "Diagnosis Prompt" column displays the diagnosis event history, including the health level, start time, diagnosis items, and duration. DBbrain performs health checks on the instance regularly.
 ![](https://main.qcloudimg.com/raw/8ef4f44b2bf18191a51588bca72f96b8.png)
3. You can click **View Details** or a diagnosis item in the "Diagnosis Prompt" to access the diagnosis details page. Click a diagnosis event in the view, and its details will be displayed below, including the event overview, symptom description, intelligent analysis, and expert suggestions. Based on the expert suggestions, you can perform optimization to solve the database exception and improve the instance performance.
 ![](https://main.qcloudimg.com/raw/bd74997165d561b84f4366a902e70d43.png)

### How can I receive the TencentDB for MySQL health report regularly?
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain), select **Diagnosis and Optimization** on the left sidebar, and select **Health Report** at the top. You can view health score trends and the problem overview for the specified time period. 
- Select the report time range and click **Create Health Report**. After the task is completed, you can view or download the health report for the specified time period.  
- Click **Regular Generation Settings** to configure the frequency for automatically generating health reports. 
 ![](https://main.qcloudimg.com/raw/c43247bfc06688bbea8a683fdb2a5014.png)

### How do I view and optimize MySQL slow logs?
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain), select **Diagnosis and Optimization** on the left sidebar, and select **Slow SQL Analysis** at the top. The "SQL Statistics" section displays the number of slow queries and the CPU utilization of the instance.
2. You can click or drag slow queries in "SQL Statistics", and the aggregated SQL template and execution information will be displayed below. Each column of data can be sorted in ascending or descending order. The duration distribution section on the right displays the distribution of the overall SQL statement execution duration for the selected time period.
 ![](https://main.qcloudimg.com/raw/66442e7012ad2baddc8efd8a68a1eae5.png)
3. Click an aggregated SQL template and the SQL optimization suggestions and statistics will be displayed on the right. You can rewrite the SQL statement or add appropriate indexes based on the optimization suggestion to improve the SQL statement execution efficiency and database performance.
 ![](https://main.qcloudimg.com/raw/0c5429de192d731e378bbfb020fdc928.png)
