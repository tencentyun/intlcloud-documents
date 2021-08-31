## Background
TDSQL for MySQL upgraded the monitoring items for server and component services on April 1, 2021 by replacing the legacy alarm policy type and modifying hundreds of monitoring and alarm metrics. You can configure alarm policies of the [TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/248/40012) type in the Cloud Monitor console.

The legacy TDSQL policy type was deactivated on July 29, 2021. You cannot configure new alarm policies in this type any more, and your previously configured TDSQL alarm polices will be gradually transferred to the new policy type.

**Comparison of the legacy and new alarm policy types:**

| Policy Type | Metric Coverage | Support and Maintenance |
| ------------- | ------------------------------------- | ----------------------- |
| Tencent Distributed SQL | 8 metrics | This policy type was deactivated on July 29, 2021 and cannot be configured subsequently. All legacy alarm policies will be transferred to the new policy type. |
| Cloud Database - TDSQL MySQL - Instance | 37 metrics | This policy type was released on April 1, 2021 with ongoing maintenance available. |

>!
>- The new TDSQL for MySQL policy type has covered all metrics of the legacy TDSQL policy type. For more information, please see [Comparison Table of New and Legacy Metrics](#jump).
> - For the new alarm policies, please see [New Metric Description](#jump2).

## Alarm Policy Migration
After the legacy TDSQL policy type is deactivated, the system will automatically transfer previously configured alarm policies to the new TDSQL for MySQL policy type on the backend.
>?Alarms may not be automatically transferred to the new alarm policy type by the system for certain instances or users. If this is the case for you, we will notify you through Message Center, email, or SMS. Then, please follow the manual transfer steps below to manually transfer the alarms.

#### Manual transfer steps
1. Sort out exiting alarm metrics and policies.
  1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/alarm2/policy), select **Alarm Configuration** > **Alarm Policy** on the left sidebar, and click **Advanced Filter**.
  2. On the pop-up page, select the alarm policy type corresponding to **Tencent Distributed SQL** in **Policy Type**, query alarm policies in this category, and download the previously configured alarm policies of the original **Tencent Distributed SQL** policy type.
![](https://main.qcloudimg.com/raw/9ed66978c7d097f2465573b497f8f686.png)
2. Configure new alarm policies.
  1. On the **[Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy)** page, click **Create**.
  2. On the **Create Alarm Policy** page, select **Cloud Database - TDSQL MySQL - Instance** for **Policy Type** and configure alarms according to the policies downloaded in step 1. For the alarm configuration method, please see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
3. Verify whether the TDSQL for MySQL alarm policies are enabled and can successfully trigger alarms.
Set a minimum trigger threshold in **Metric alarm** on the **Create Alarm Policy** page, choose to set a **recipient** or **recipient group**, and select the notification channel (email or SMS) to test a policy. For example, you can configure an alarm policy for the CPU utilization metric that triggers an alarm once per minute when the threshold is greater than or equal to 1% for one statistical period of one minute.
4. After the new policy type is verified, delete the alarm policies previously configured under the original TDSQL (legacy) policy type.
On the **[Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy)** page, filter alarm policies by the "Tencent Distributed SQL" policy type and delete the filtered policies according to the policy list downloaded in step 1.
If you encounter any issues during the transfer, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## [Comparison Table of New and Legacy Metrics](id:jump)
<table>
<thead><tr><th><strong>Legacy Policy Type</strong></th><th><strong>Metric/Event Alarm</strong></th><th><strong>Legacy Metric/Event Alarm Name</strong></th><th><strong>New Policy Type</strong></th><th><strong>New Metric/Event Alarm Name</strong></th></tr></thead>
<tbody><tr>
<td rowspan="14">Tencent Distributed SQL</td>
<td>Metric alarm</td><td>CPU utilization</td>
<td>Cloud Database - TDSQL MySQL - Instance</td><td>Maximum CPU utilization of source node</td></tr>
<tr>
<td>Metric alarm</td><td>Storage space utilization</td>
<td>Cloud Database - TDSQL MySQL - Instance</td><td>Maximum data disk utilization of source node</td></tr>
<tr>
<td>Metric alarm</td><td>Slow queries</td>
<td>Cloud Database - TDSQL MySQL - Instance</td><td>Total slow queries of source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Active connections</td>
<td>Cloud Database - TDSQL MySQL - Instance</td><td>Total active threads</td></tr>
<tr>
<td>Metric alarm</td><td>Cache hit rate</td>
<td>Cloud Database - TDSQL MySQL - Instance</td><td>Minimum cache hit rate of source node</td></tr>
<tr>
<td>Metric alarm</td><td>Database connections</td>
<td>Cloud Database - TDSQL MySQL - Instance</td><td>Total client connections</td></tr>
<tr>
<td>Metric alarm</td><td>Replica lag</td>
<td>Cloud Database - TDSQL MySQL - Instance</td><td>Secondary node delay</td></tr>
<tr>
<td>Metric alarm</td><td>Primary-Secondary switch</td>
<td>Cloud Database - TDSQL MySQL - Instance</td><td>Primary-Secondary switches</td></tr>
</tbody></table>

## [New Metric Description](id:jump2)
<table>
<thead><tr><th><strong>Policy Type</strong></th><th><strong>Metric/Event Alarm</strong></th><th><strong>Metric/Event Alarm Name</strong></th></tr></thead>
<tbody><tr>
<td rowspan="30">Cloud Database - TDSQL MySQL</td>
<td>Metric alarm</td><td>CPU utilization</td></tr>
<tr>
<td>Metric alarm</td><td>Total UPDATE requests of source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Total open connections</td></tr>
<tr>
<td>Metric alarm</td><td>Total maximum connections</td></tr>
<tr>
<td>Metric alarm</td><td>SQL Throughput</td></tr>
<tr>
<td>Metric alarm</td><td>SQL Error Throughput</td></tr>
<tr>
<td>Metric alarm</td><td>SQL Success Throughput</td></tr>
<tr>
<td>Metric alarm</td><td>Requests consuming less than 5 ms</td></tr>
<tr>
<td>Metric alarm</td><td>Requests consuming 5–20 ms</td></tr>
<tr>
<td>Metric alarm</td><td>Requests consuming 21–30 ms</td></tr>
<tr>
<td>Metric alarm</td><td>Requests consuming more than 30 ms</td></tr>
<tr>
<td>Metric alarm</td><td>Minimum remaining binlog disk space in all shards</td></tr>
<tr>
<td>Metric alarm</td><td>Total binlog disk space of source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Maximum database connection utilization</td></tr>
<tr>
<td>Metric alarm</td><td>Total available data disk space of source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Total DELETE requests of source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Maximum IO utilization of source node</td></tr>
<tr>
<td>Metric alarm</td><td>Total logical reads from InnoDB disk</td></tr>
<tr>
<td>Metric alarm</td><td>Total pages read into InnoDB buffer pool by read-ahead thread</td></tr>
<tr>
<td>Metric alarm</td><td>Total logical reads from InnoDB buffer pool</td></tr>
<tr>
<td>Metric alarm</td><td>Total rows deleted from InnoDB tables on source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Total rows inserted to InnoDB tables on source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Total rows read from InnoDB tables</td></tr>
<tr>
<td>Metric alarm</td><td>Total rows updated in InnoDB tables on source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Total INSERT requests of source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Total available cache of source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Total REPLACE_SELECT requests of source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Total REPLACE requests of source nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Total requests of source and replica nodes</td></tr>
<tr>
<td>Metric alarm</td><td>Total SELECT requests</td></tr>
</tbody></table>

