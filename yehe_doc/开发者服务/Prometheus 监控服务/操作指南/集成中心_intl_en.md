 TMP integrates commonly used application, middleware, big data, and infrastructure databases. You only need to follow the instructions to monitor the corresponding components. It also provides out-of-the-box Grafana monitoring dashboards. The integration center covers three major monitoring scenarios of basic service monitoring, application layer monitoring, and TKE cluster monitoring, making it easier for you to connect and use.


## Supported Services
<table>
	<tr>
	<th>Service Type</th>
	<th>Service</th>
	<th>Monitoring Metric</th>
	</tr>
	<tr>
		<td rowspan="2">Big data</td>
		<td>Elasticsearch</td>
		<td>Including cluster/index/node monitoring</td>
	</tr>
    <tr>
	    <td>Flink</td>
		<td>Including cluster/job/task monitoring</td>
	</tr>
	<tr>
		<td rowspan="3">Application</td>
		<td>Go</td>
		<td>Including GC/heap/thread/Goroutine monitoring</td>
	</tr>
	<tr>
		<td>JVM</td>
		<td>Including heap/thread/GC/CPU/file monitoring</td>
	</tr>
	<tr>
		<td>Spring MVC</td>
		<td>Including HTTP API/exception/JVM monitoring</td>
	</tr>
	<tr>
		<td>Middleware</td>
		<td>Kafka</td>
		<td>Including broker/topic/consumer group monitoring</td>
	</tr>
	<tr>
		<td>Infrastructure</td>
		<td>Kubernetes</td>
		<td>Including API server/DNS/workload/network monitoring</td>
</tr>
	<tr>
		<td rowspan="4">Database</td>
		<td>TencentDB for MongoDB</td>
		<td>Including file count/read and write performance/network traffic monitoring</td>
</tr>
<tr>
		<td>TencentDB for MySQL</td>
		<td>Including network/connection count/slow query monitoring</td>
</tr>
<tr>
		<td>TencentDB for PostgreSQL</td>
		<td>Including CPU/memory/transaction/lock/read/write monitoring</td>
</tr>
<tr>
		<td>TencentDB for Redis</td>
		<td>Including memory utilization/connection count/command execution status monitoring</td>
</tr>
<tr>
		<td rowspan="4">Inspection</td>
		<td>Health inspection</td>
		<td>Blackbox can be used to regularly test the connectivity of the target service, helping you stay up to date with the service health and discover exceptions in time</td>
</tr>
</table>

## Directions
1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. In the instance list, select the corresponding TMP instance.
3. Enter the instance details page and click **Integration Center**.
4. Select the target service in the integration center. You can click **Connection Guide** to view the connection guide. After successful connection, you can monitor the corresponding service in real time. You can also click **Install/Upgrade** in **Dashboard Operation** to install or upgrade the Grafana dashboard for the service.
![](https://qcloudimg.tencent-cloud.cn/raw/a98c7d023b0f1fa586cdb681a63ea2c1.png)
