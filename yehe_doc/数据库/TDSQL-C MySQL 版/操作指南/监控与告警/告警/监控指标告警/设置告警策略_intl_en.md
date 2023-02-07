This document describes how to create and manage an alarm policy in the console.

## Overview
You can create alarm policies to trigger alarms and send alarm notifications when the TDSQL-C for MySQL status changes. The created alarm policies can determine whether an alarm needs to be triggered according to the difference between the monitoring metric value and the given threshold at intervals.

When the alarm is triggered by a status change, you can promptly take the necessary preventative or corrective action. Alarm policies can therefore, if appropriately created, help you improve the robustness and reliability of your database. For more information on alarms, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).

To send an alarm for a specific status of TDSQL-C for MySQL, you need to create an alarm policy at first. An alarm policy is composed of three compulsory components, that is, the name, type and alarm triggering conditions. Each alarm policy is a set of alarm triggering conditions with the logical relationship "OR", that is, as long as one of the conditions is met, an alarm will be triggered. The alarm will be sent to all users associated with the alarm policy. Upon receiving the alarm, the user can view the alarm and take appropriate actions in time. After creating an alarm policy, you can change its name, remarks, or triggering conditions and edit its alarm objects.

## Directions
### Setting an alarm policy
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Find the target cluster in the cluster list and click the cluster ID to enter the cluster management page.
3. Select **Monitoring and Alarms** on the cluster management page and click **Configure Alarms** on the right.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/L8TD899_6.png)
4. Select **Alarm Configuration** > **Alarm Policy** on the left sidebar on the opened page and click **Create** in the alarm policy list.
5. On the policy creation page, configure the following parameters and click **Complete**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZQEV803_7.png)
<table>
<thead><tr><th width=10%>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Policy Name</td>
<td>Enter the policy name, which can contain up to 60 characters.</td></tr>
<tr>
<td>Remarks</td>
<td>Enter remarks for the policy, which can contain up to 100 characters.</td></tr>
<tr>
<td>Monitoring Type</td>
<td>Select **Tencent Cloud services**.</td></tr>
<tr>
<td>Policy Type</td>
<td>Select **TencentDB** >**TDSQL-C** > **MySQL**.</td></tr>
<tr>
<td>Alarm Object</td>
<td>Find the object instance to be associated with by selecting the region where the object is located or searching for the instance ID of the object.</td></tr>
<tr>
<td>Trigger Condition</td>
<td>Select a predefined template or manually configure the alarm trigger condition, which is a semantic condition composed of metric, comparison, threshold, statistical period, and duration. For example, if the metric is disk utilization, the comparison is &gt;, the threshold is 80%, the statistical period is 5 minutes, and the duration is two statistical periods, then the data on disk utilization of a database will be collected once every five minutes, and an alarm will be triggered if the disk utilization exceeds 80% for two consecutive times.</td></tr>
<tr>
<td>Configure Alarm Notification</td>
<td>Select a preset or custom notification template. Each alarm policy can be bound to three notification templates at most. For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/38922">Creating Notification Template</a>.</td></tr>
</tbody></table>


### Managing an alarm policy
1. In the [alarm policy](https://console.cloud.tencent.com/monitor/alarm2/policy) list, click the name of the target alarm policy to enter the alarm policy management page.
2. Select **Policy Details** on the alarm policy management page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8MeX001_8.png)
3. Select the configuration item to be modified as needed, such as policy name, remarks, trigger condition, and alarm object.
