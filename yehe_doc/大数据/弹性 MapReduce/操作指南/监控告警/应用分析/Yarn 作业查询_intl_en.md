## Overview
You can view submitted jobs, memory and vCore consumption, and other information at the user granularity, and quickly check the queue, status, duration, and other metrics of YARN jobs in the EMR console. Comparison of historical tasks by job, job insight, task execution information, and other features are also available.
## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of a target cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, click **Cluster Services** and select **Operation** > **Job query** in the top-right corner of the YARN component to view job statistics and resource consumption trends, query job and task information, get insights into application execution results, and compare application monitoring data.
	i. Submitted jobs, view and distribution of memory and vCores consumed at the user granularity, and recent trends of relevant metrics.
	![](https://qcloudimg.tencent-cloud.cn/raw/d596d35d1fbdf65a7e17641706501230.png)
	![](https://qcloudimg.tencent-cloud.cn/raw/842f624a6781d9411c8718e85632912e.png)
	ii. Job filtering by user, application name, queue name, job type, duration, or relevant throughput metrics.
	iii. Resource consumption statistics by user, queue, or other metrics, helping check costs (also supported by API).
>! 
>- To use the new features of task information, application insight, and application comparison for applications of Spark type, you first need to check whether the Spark History version is supported by running `curl "http://localhost:10000/api/v1/applications" | json_pp`. If the returned result is in abnormal JSON format, the Spark History version is not supported. In this case, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for enabling such features.
>- In job query, ResourceManager data is collected once every 30s. The collection operation has negligible impact on cluster running.

3. In the job list, click **More** > **Application insight** to view detailed application insight items and related insight rules, results, and suggestions.
![](https://qcloudimg.tencent-cloud.cn/raw/66ffce9024b67645a9c2835d2f805356.png)
4. In the job list, click **More** > **Application comparison** to compare the business metrics between the current application and another application of the same type.
![](https://qcloudimg.tencent-cloud.cn/raw/2f46c07f11bd09bb2fb6286a7e141407.png)
>!  
>- Only applications of MAPREDUCE, Spark, or Tez type in the final status of SUCCEEDED can be compared.
>- Applications of the same type with the same name are filtered on the page by default. Only applications of the same type can be selected and filtered for comparison, and real-time data can be filtered and queried on the backend.

5. In the job list, click **More** > **Task information** to view the job task list, hosts comparison, and task execution logs.
![](https://qcloudimg.tencent-cloud.cn/raw/f8359cb38ead3c1d7b52e99a3144f4e4.png)
The feature support is as follows:
<table>
<thead>
<tr>
<th>Job Type</th>
<th>Task Information</th>
<th>Hosts Comparison</th>
<th>Task Log</th>
</tr>
</thead>
<tbody><tr>
<td>MAPREDUCE</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Spark</td>
<td>Supported</td>
<td>Not supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Tez</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Others</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
</tbody></table>


