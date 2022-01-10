## Overview

You can view the log details of a CKafka Pro Edition instance in the CKafka console, including consumer group broker logs and controller logs. This document describes how to view the log details in the console.

> ?This feature is only available for Pro Edition instances but not for Standard Edition instances.

**Log type**

| Log Type           | Event                                                         |
| ------------------ | ------------------------------------------------------------ |
| Consumer group broker log | <li>Heartbeat timeout of consumer group member</li><li>Rebalance exception</li><li>Commit of consumption progress by consumer group member</li><li>Consumer group rebalance</li> |
| Controller log     | <li>Leader switch</li><li>Cluster node connection</li><li>Cluster node disconnection</li> |

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, click **Log** at the top and select the log type to view log details.
	![](https://main.qcloudimg.com/raw/d2b0653fced0563093015983ebcb8151.png)
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Event Name</td>
<td>Event name.</td>
</tr>
<tr>
<td>Event Type</td>
<td>Events are divided into <strong>exception</strong> and <strong>status change</strong> based on their impact on the service.</td>
</tr>
<tr>
<td>Affected Object</td>
<td>Object affected by the event, such as a topic or consumer group.</td>
</tr>
<tr>
<td>Start Time</td>
<td>Time when the event started.</td>
</tr>
<tr>
<td>Operation</td>
<td>You can view the event details or configure an alarm policy.</td>
</tr>
</tbody></table>
4. Click **Details** in the **Operation** column to view the specific log.
	 ![](https://main.qcloudimg.com/raw/e448ba202830dddbfeb97b8982846621.png)
5. Click **Configure Alarm** in the **Operation** column to configure an alarm policy for a metric to which alarming has been enabled. For detailed directions, see [Configuring Alarm](https://intl.cloud.tencent.com/document/product/597/40976).

