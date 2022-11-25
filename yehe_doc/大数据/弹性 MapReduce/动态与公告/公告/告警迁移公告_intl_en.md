## Background
Elastic MapReduce upgraded its server and component service monitoring items on September 10, 2019. A new policy type "Elastic MapReduce" has been added, which covers hundreds of monitoring metrics. You can configure alarm policies under the **[Elastic MapReduce](https://intl.cloud.tencent.com/document/product/248/36845)** policy type in Cloud Monitor. **The original policy type "EMR" was deprecated at 23:00 on March 30, 2021, and all the configured "EMR" alarm policies were invalidated.** To add new alarm policies, configure under the "Elastic MapReduce" policy type.

 **Comparison of "EMR" and "Elastic MapReduce" policy types:**

| Policy Type | Metric Coverage | Support and Maintenance |
| ------------- | ---------------------------------------------- | --------------------------------------- |
| EMR | <li>Cluster alarming (12 metrics) </li> <li>Node alarming (8 metrics) </li> | It was deprecated at 23:00 on April 9, 2021 and no longer maintained. |
| Elastic MapReduce | <li>Server monitoring </li><li>Service monitoring </li> <li>Cluster monitoring</li>            | It was released on September 10, 2019 but is still maintained. |

>!The "Elastic MapReduce" policy type covers all the metrics of the "EMR" policy type. For details, see [Comparison of new and original metrics](#jump).

## Alarm policy transfer
After the "EMR" policy type was deprecated, the system automatically migrated existing alarm policies under the "EMR" policy type to the "Elastic MapReduce" policy type. See further notifications for specific rules and verification methods.

>! A few users might need to migrate them manually. 

**Steps for manual migration are as follows:**
1. Sort out exiting alarm metrics and policies.
Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview), select **Alarm Management** > **Alarm Configuration** > **Alarm Policy** on the left sidebar, click **Advanced Filter**, select any sub-type of the "EMR" policy type in **Policy Type**, search for related alarm policies, and download them. Repeat this step to download the alarm policies under other sub-types of the "EMR" policy type.
![](https://qcloudimg.tencent-cloud.cn/raw/2048487ec4974fea3d811517d7bcf375.png)
2. Configure alarm policies.
Click **Alarm Configuration** in the cluster list to go to the **Alarm Policy** page, click **Create**, select **Elastic MapReduce** in **Policy Type**, and configure an alarm policy according to one of the policies sorted out and downloaded in step 1. Repeat this step to configure other alarm policies. For more information on the configuration method, see [Alarm Configurations](https://intl.cloud.tencent.com/document/product/1026/31120).
3. Verify the new alarm policies.
Verify that the "Elastic MapReduce" alarm policies are activated and can successfully trigger alarms. Set trigger thresholds in **Metric Alarm**, set recipient groups or recipients, and select receiving channels (email, SMS, or WeChat) for verification. Take `memory zone percentage_SO` as an example: when the statistical period is five minutes, and the percentage is greater than or equal to 1% and lasts for five minutes, an alarm will be triggered once every five minutes.
4. Delete original alarm policies.
After verifying the new alarm policies, delete the original alarm policies configured under the "EMR" policy type. Select any sub-type of the "EMR" policy type in **Policy Type**, search for related alarm policies, and delete them. Repeat this step to delete the alarm policies under other sub-types of the "EMR" policy type.

If you encounter any issues during the transfer, [contact us](https://intl.cloud.tencent.com/contact-us) for assistance.

[](id:jump)
## Comparison of new and original metrics

<table>
<thead>
<tr>
<th><strong>Original Policy Type</strong></th>
<th><strong>Metric/Event Alarm</strong></th>
<th><strong>Original Metric/Event Name</strong></th>
<th><strong>New Policy Type</strong></th>
<th><strong>New Metric/Event Name</strong></th>
</tr>
</thead>
<tbody><tr>
<td rowspan="14">EMR-cluster alarm</td>
<td>Metric alarm</td>
<td>Used HDFS storage space</td>
<td>Elastic MapReduce-HDFS-overview</td>
<td>Cluster storage capacity_CapacityUsed</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>HDFS storage utilization</td>
<td>Elastic MapReduce-HDFS-overview</td>
<td>HDFS storage space utilization_capacityused</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>YARN app blocks</td>
<td>Elastic MapReduce-YARN-overview</td>
<td>Applications_pending</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Failed YARN apps</td>
<td>Elastic MapReduce-YARN-overview</td>
<td>Applications_failed</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Assigned cluster CPU cores</td>
<td>Elastic MapReduce-YARN-overview</td>
<td>Cores_allocatedVirtualCores</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Cluster CPU utilization</td>
<td>Elastic MapReduce-YARN-overview</td>
<td>CPU utilization_usageRatio</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Available cluster memory</td>
<td>Elastic MapReduce-YARN-overview</td>
<td>Memory_availableMB</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Cluster memory utilization</td>
<td>Elastic MapReduce-YARN-overview</td>
<td>Memory utilization_usageRatio</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Cluster container blocks</td>
<td>Elastic MapReduce-YARN-overview</td>
<td>Containers_containersPending</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>HBase requests</td>
<td>Elastic MapReduce-HBASE-overview</td>
<td>Total cluster requests_clusterRequests</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Time taken for HBase sync</td>
<td>No longer maintained</td>
<td>-</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>HBase sync log length</td>
<td>No longer maintained</td>
<td>-</td>
</tr>
<tr>
<td>Event alarm</td>
<td>Node monitoring heartbeat missing</td>
<td>Elastic MapReduce-server monitoring-network</td>
<td>Node monitoring heartbeat missing</td>
</tr>
<tr>
<td>Event alarm</td>
<td>Process restart</td>
<td>Elastic MapReduce-server monitoring-process</td>
<td>Process OOM</td>
</tr>
<tr>
<td rowspan="8">EMR-node alarm</td>
<td>Metric alarm</td>
<td>Disk utilization</td>
<td>Elastic MapReduce-server monitoring-disk</td>
<td>Disk capacity utilization_used_all</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Memory usage</td>
<td>Elastic MapReduce-server monitoring-memory</td>
<td>Memory usage_MemFree</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Server restart</td>
<td>No longer maintained</td>
<td>Server restart</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Memory utilization</td>
<td>Elastic MapReduce-server monitoring-memory</td>
<td>Memory utilization_used_percent</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>CPU usage</td>
<td>Elastic MapReduce-server monitoring-CPU</td>
<td>CPU utilization_idle</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Inbound packets over private networks</td>
<td>No longer maintained</td>
<td>-</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>Outbound packets over private networks</td>
<td>No longer maintained</td>
<td>-</td>
</tr>
<tr>
<td>Metric alarm</td>
<td>TCP connections</td>
<td>Elastic MapReduce-server monitoring-network</td>
<td>TCP connections</td>
</tr>
</tbody></table>