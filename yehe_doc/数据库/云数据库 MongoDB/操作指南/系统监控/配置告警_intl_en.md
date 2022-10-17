## Overview

You can configure alarm rules for monitoring metrics to prevent your system operations from being disrupted when these metrics reach a certain value. When monitoring data meets the configured conditions, the system can check it automatically and send alarm notifications to the admin. This allows you to stay on top of business exceptions and solve them quickly.

## Alarming and Monitoring Metrics

### Instance

<table width="100">
<thead>
<tr><th width="25%">Monitoring Metric</th><th width="5%">Unit</th><th width="45%">Description</th></tr>
</thead>
<tbody>
<tr>
<td>Write requests</td><td>-</td><td>Number of write requests received by the instance.</td></tr>
<tr>
<td>Read requests</td><td>-</td><td>Number of read requests received by the instance.</td></tr>
<tr>
<td>Update requests</td><td>-</td><td>Number of update requests received by the instance.</td></tr>
<tr>
<td>Deletion requests</td><td>-</td><td>Number of deletion requests received by the instance.</td></tr>
<tr>
<td>Count requests</td><td>-</td><td>Number of count requests received by the instance.</td></tr>
<tr><td>Aggregate requests</td><td>-</td><td>Number of aggregate requests received by the instance.</td></tr>
<tr>
<td>Successful requests</td><td>-</td><td>Number of requests received by the instance that are executed successfully.</td></tr>
<tr>
<td>Disk utilization</td><td>%</td><td>Proportion of the used disk capacity to the total capacity.</td></tr>
<tr>
<td>Requests consuming 10-50 ms</td><td>-</td><td>Number of requests with an execution time between 10 and 50 ms.</td></tr>
<tr>
<td>Requests consuming 50-100 ms</td><td>-</td><td>Number of requests with an execution time between 50 and 100 ms.</td></tr>
<tr>
<td>Requests consuming more than 100 ms</td><td>-</td><td>Number of requests with an execution time of more than 100 ms.</td></tr>
<tr>
<td>Connection utilization</td><td>%</td><td>Proportion of current connections to the maximum connections.</td></tr>
<tr>
<td>Requests per second</td><td>-</td><td>Number of requests received by the instance per second.</td></tr>
<tr>
<td>Command requests</td><td>-</td><td>Number of command requests received by the cluster other than INSERT, UPDATE, DELETE, and QUERY requests.</td></tr>
<tr>
<td>Connections</td><td>-</td><td>Number of TCP connections from cluster clients.</td></tr>     
</tbody></table>

### Node

<table width="100">
<thead>
<tr><th width="35%">Monitoring Metric</th><th width="5%">Unit</th><th width="60%">Description</th></tr>
</thead>
<tbody>
<tr>
<td>CPU utilization</td><td>%</td><td>CPU utilization of the node.</td></tr> 
<tr>
<td>Memory utilization</td><td>%</td><td>Memory utilization of the node.</td></tr>    
<tr>
<td>Network inbound traffic</td><td>Bytes</td><td>Number of bytes in the traffic inbound to the node.</td>   
<tr>
<td>Network outbound traffic</td><td>Bytes</td><td>Number of bytes in the traffic outbound from the node.</td></tr>
<tr>
<td>Read requests in queue</td><td>-</td><td>Number of read requests waiting in the queue.</td></tr>
<tr>
<td>Write requests in queue</td><td>-</td><td>Number of write requests waiting in the queue.</td></tr>
<tr>
<td>Connections</td><td>-</td><td>Number of client connections.</td></tr>
<tr>
<td>Node disk usage</td><td>MB</td><td>Used node disk capacity.</td></tr>
<tr>
<td>ActiveRead requests of WT engine</td><td>-</td><td>Number of active read requests.</td></tr>
<tr>
<td>ActiveWrite requests of WT engine</td><td>-</td><td>Number of active write requests.</td></tr>
<tr>
<td>Pieces of data deleted via TTL</td><td>-</td><td>Number of documents deleted through TTL.</td></tr>
<tr>
<td>TTL run times</td><td>-</td><td>Number of file deletions from the TTL collection performed by the backend process.</td></tr>
</tbody></table>

## Billing

- CM allows you to configure alarm policies to monitor the key metrics of instances and offers a free trial.
- Currently, only **alarm SMS messages and phone calls** are charged. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/248/18728).

## Prerequisites

- You have activated [CM](https://console.cloud.tencent.com/monitor/overview).
- The database instance is in **Running** status.
- You have collected the information of the recipients of alarm notifications, such as email address and phone number.

## Directions

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the row of the target instance, enter the **Create Policy** page of CM in any of the following ways:
   - Click ![img](https://qcloudimg.tencent-cloud.cn/raw/8e01de7cd5dd07c6d2626aaba4c2288c.png) in the **Monitoring/Status** column and click **Configure Alarms** in the top-right corner of the instance monitoring dashboard.
![](https://qcloudimg.tencent-cloud.cn/raw/22a4fbb65945da3376dbc7c1e1da97af.png)
   - Click the instance ID in blue to enter the **Instance Details** page. Then, select the **System Monitoring** tab and click **Configure Alarms**.
      ![](https://qcloudimg.tencent-cloud.cn/raw/ba96672dd2eca1482a6cbb7df4339fc5.png)
6. On the **Create Policy** page, configure the policy as shown below. For more information on the basic concepts of alarm policy, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
   ![](https://qcloudimg.tencent-cloud.cn/raw/3bc35419be4ecd93374b01bd6dd989ef.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Policy Name</td>
<td>Customize the alarm policy name for easier identification.</td></tr>
<tr>
<td>Remarks</td>
<td>Briefly describe the alarm policy for easier identification.</td></tr>
<tr>
<td>Monitoring Type</td>
<td>Select <strong>Cloud Product Monitoring</strong>.</td></tr>
<tr>
<td>Policy Type</td>
<td>Set <strong>Policy Type</strong> to <strong>TencentDB / MongoDB / instance</strong> or <strong>TencentDB / MongoDB / node</strong>.</td></tr>
<tr>
<td>Project</td>
<td>Specify a project for the alarm policy. You can quickly locate all alarm policies of a project in the alarm policy list.</td></tr>
<tr>
<td>Alarm Object</td>
<td><ul><li>Select <strong>Instance ID</strong> to bind the alarm policy to the specified database instance.</li><li>Select <strong>Instance Group</strong> to bind the alarm policy to the specified database instance group. For more information on how to create an instance group, see <a href="https://intl.cloud.tencent.com/document/product/248/35268">Instance Group</a>.</li><li>Select <strong>All Objects</strong> to bind the alarm policy to all instances on which the current account has permissions.</li><li>Select <strong>Tag</strong> to bind the alarm policy to all instances associated with the current tag key and value.</li></ul></td></tr>
<tr>
<td>Trigger Condition</td>
<td><ul><li>If you select <strong>Select template</strong>, you can select a template file from the drop-down list, and alarms will be reported based on the trigger conditions preset in the template. For specific configurations, see <a href="https://intl.cloud.tencent.com/document/product/248/38911">Configuring Trigger Condition Template</a>. If you select <strong>Configure manually</strong>, you need to configure the threshold for triggering an alarm for each metric in the <strong>Metric Alarm</strong> section below.</li>
<li><strong>Threshold Type</strong> in the <strong>Metric Alarm</strong> section: If you select **Static**, you can manually set a fixed threshold, and alarms will be triggered when the threshold is reached. If you select <strong>Dynamic</strong>, exceptions will be determined based on the dynamic threshold boundaries calculated by machine learning algorithms. </li>For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/38916">Creating Alarm Policy</a>.</ul></td>
</tr>
<tr>
<td>Alarm Notification</td>
<td>You can select a preset or custom notification template. Each alarm policy can be bound to three notification templates at most.</td>
</tr>
</tbody></table>
7. After confirming that the configuration is correct, click **Complete**. For more information on alarms, see [Tencent Cloud Documentation](https://intl.cloud.tencent.com/document/product//248/6126).

## Related APIs

| API | Description |
| :----------------------------------------------------------- | :----------------- |
| [CreateAlarmPolicy](https://intl.cloud.tencent.com/document/product/248/39326) | Creates CM alarm policy |

