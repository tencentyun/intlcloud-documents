TencentDB for MongoDB is connected to the performance optimization feature of DBbrain. The feature monitors and diagnoses database instance exceptions in real time, automatically generates health reports, and gives expert optimization suggestions. This helps you stay on top of the running status of the current database, quickly locate and troubleshoot issues, and promptly optimize the database performance.

## Viewing performance optimization

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. On the left sidebar, select **Performance Optimization**.
3. At the top of the **Performance Optimization** page of **DBbrain**, select the target instance in the **Instance ID** drop-down list.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/0f8663ab9e4edf8eb32bf9594104d61b.png)
4. View and analyze the diagnosis data of the instance.
<table>
<thead><tr><th>Monitoring Type</th><th>Description</th></tr></thead>
<tbody><tr>
<td><a href="https://www.tencentcloud.com/document/product/1035/48621">Exception Diagnosis</a></td>
<td>Performs real-time performance monitoring and health inspections on the database and gives diagnosis prompts and optimization suggestions for failures.</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/1035/48620">Performance Trends</a></td>
<td>Monitors performance metrics of instances and Mongod nodes, such as resources, requests, and primary/secondary delay.</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/1035/48615">Real-Time Session</a></td>
<td>Collects the information of database client sessions in real time, such as the sources and number of sessions as well as the number of active sessions.</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/1035/48619">Slow SQL Analysis</a></td>
<td>Analyzes the number and duration of slow queries of instances and Mongod nodes in real time.</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/1035/48618">Space Analysis</a></td>
<td>Analyzes the database space utilization, including the sizes of data and logs, the daily increase in space utilization, and the estimated number of available days.</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/1035/48617">MongoStatus</a></td>
<td>Collects and analyzes the number of requests, updates, deletions, and connections as well as outbound/inbound traffic of the database.</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/1035/48616">MongoTop</a></td>
<td>Collects the top data of the database in terms of write operation, read operation, and total request duration.</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/1035/48614">SQL Throttling</a></td>
<td>Controls scenarios where excessive CPU resources are consumed due to high traffic. You can create SQL throttling tasks to control the number of access requests and SQL concurrency, thereby ensuring a high service availability.</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/1035/48613">Index Recommendation</a></td>
<td>Collects the real-time information of slow queries, automatically analyzes it, and recommends the optimal global index.</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36042">Health Report</a></td>
<td>Scores the instance health based on monitoring metrics and statistics.</td></tr>
</tbody></table>


