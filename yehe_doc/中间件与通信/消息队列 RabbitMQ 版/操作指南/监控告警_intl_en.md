## Overview

TDMQ for RabbitMQ supports monitoring resources created under your account, including clusters, vhosts, queues, and exchanges. You can analyze the cluster usage based on the monitoring data and handle possible risks promptly. You can also set alarm rules for monitoring metrics, so that you can receive alarm messages when metrics are abnormal. This helps you deal with risks in time and ensure the stable operations of your system.



## Monitoring Metrics

The monitoring metrics supported by TDMQ for RabbitMQ are as follows:
<meta http-equiv="Content-Type" content="text/html;charset=utf-8">
<table>
    <thead>
    <tr>
        <th>Resource Type</th>
        <th>Monitoring Metric</th>
        <th>Unit</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td rowspan="7">Cluster</td>
        <td>Vhost quantity</td>
        <td>Count</td>
        <td>Total number of vhosts in the cluster within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ production speed</td>
        <td>Count/s</td>
        <td>The speed at which all clients in the cluster produce messages to exchanges within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ production throughput</td>
        <td>Bytes/s</td>
        <td>Throughput of all clients in the cluster producing messages to exchanges within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ delivery speed</td>
        <td>Count/s</td>
        <td>The speed at which all queues in the cluster deliver messages to the client within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ delivery throughput</td>
        <td>Bytes/s</td>
        <td>Throughput of all queues in the cluster delivering messages to the client within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ exchange quantity</td>
        <td>Count</td>
        <td>Total number of exchanges in the cluster within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ queue quantity</td>
        <td>Count</td>
        <td>Total number of queues in the cluster within the selected time range.</td>
    </tr>
    <tr>
        <td rowspan="2">Vhost</td>
        <td>RabbitMQ exchange quantity</td>
        <td>Count</td>
        <td>Total number of exchanges in all vhosts in the cluster within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ queue quantity</td>
        <td>Count</td>
        <td>Total number of queues in all vhosts in the cluster within the selected time range.</td>
    </tr>
    <tr>
        <td rowspan="9">Exchange</td>
        <td>RabbitMQ average production duration</td>
        <td>ms</td>
        <td>Average time taken by the client to produce messages to each exchange within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ P95 production duration</td>
        <td>ms</td>
        <td>95th percentile of the time taken by the client to produce messages to each exchange within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ P99 production duration</td>
        <td>ms</td>
        <td>99th percentile of the time taken by the client to produce messages to each exchange within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ P999 production duration</td>
        <td>ms</td>
        <td>99.9th percentile of the time taken by the client to produce messages to each exchange within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ maximum production duration</td>
        <td>ms</td>
        <td>Maximum time taken by the client to produce messages to each exchange within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ binding distribution speed</td>
        <td>Count/s</td>
        <td>The speed at which each exchange sends messages to the bound queue within the selected time range.</td>
    </tr>
    <tr>
        <td>Binding distribution throughput</td>
        <td>Bytes/s</td>
        <td>Throughput of each exchange sending messages to the bound queue within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ production speed</td>
        <td>Count/s</td>
        <td>The speed at which the client produces messages to each exchange within the selected time range.</td>
    </tr>
    <tr>
        <td>RabbitMQ production throughput</td>
        <td>Bytes/s</td>
        <td>Throughput of the client producing messages to each exchange within the selected time range.</td>
    </tr>
    <tr>
        <td rowspan="21">Queue</td>
        <td>Binding distribution production speed</td>
        <td>Count/s</td>
        <td>The speed at which each queue receives messages from the exchange within the selected time range.</td>
    </tr>
    <tr>
        <td>Binding distribution production throughput</td>
        <td>Bytes/s</td>
        <td>Throughput of each queue receiving messages from the exchange within the selected time range.</td>
    </tr>
    <tr>
        <td>Pull speed</td>
        <td>Count/s</td>
        <td>The speed at which the client pulls messages in the queue within the selected time range (the pull consumption mode refers to the `basicGet` command). </td>
    </tr>
    <tr>
        <td>Pull throughput</td>
        <td>Bytes/s</td>
        <td>Throughput of the client pulling messages in the queue within the selected time range (the pull consumption mode refers to the `basicGet` command). </td>
    </tr>
    <tr>
        <td>Acknowledgement speed</td>
        <td>Count/s</td>
        <td>The speed at which the client acknowledges the receipt of messages within the selected time frame.</td>
    </tr>
    <tr>
        <td>Negative acknowledgment speed</td>
        <td>Count/s</td>
        <td>The speed at which the client acknowledges no receipt of messages within the selected time frame.</td>
    </tr>
    <tr>
        <td>Redelivery speed</td>
        <td>Count/s</td>
        <td>The speed at which each queue in the cluster redelivers messages to the client when the client does not respond for a long time within the selected time range.</td>
    </tr>
    <tr>
        <td>Total messages</td>
        <td>Count</td>
        <td>Total number of messages received by each queue in the cluster at the current time.</td>
    </tr>
    <tr>
        <td>Total consumable messages</td>
        <td>Count</td>
        <td>Total number of unconsumed messages among messages received by each queue in the cluster at the current time.</td>
    </tr>
    <tr>
        <td>Delivered yet unacknowledged messages</td>
        <td>Count</td>
        <td>Total number of unacknowledged messages delivered by each queue in the cluster to the client at the current time.</td>
    </tr>
    <tr>
        <td>Average acknowledge duration</td>
        <td>ms</td>
        <td>Average time taken by the client to acknowledge queue messages within the selected time range.</td>
    </tr>
    <tr>
        <td>P95 acknowledgment duration</td>
        <td>ms</td>
        <td>95th percentile of the time taken by the client to acknowledge queue messages within the selected time range.</td>
    </tr>
    <tr>
        <td>P99 acknowledgment duration</td>
        <td>ms</td>
        <td>99th percentile of the time taken by the client to acknowledge queue messages within the selected time range.</td>
    </tr>
    <tr>
        <td>P999 acknowledgment duration</td>
        <td>ms</td>
        <td>99.9th percentile of the time taken by the client to acknowledge queue messages within the selected time range.</td>
    </tr>
    <tr>
        <td>Maximum acknowledgment duration</td>
        <td>ms</td>
        <td>Maximum time taken by the client to acknowledge queue messages within the selected time range.</td>
    </tr>
    <tr>
        <td>Consumers</td>
        <td>Count</td>
        <td>Number of clients connected to each queue in the cluster at the current time.</td>
    </tr>
    <tr>
        <td>Message storage usage</td>
        <td>Bytes</td>
        <td>Disk size used by messages in each queue in the cluster at the current time.</td>
    </tr>
    <tr>
        <td>Message heap size</td>
        <td>Bytes</td>
        <td>Size of unconsumed messages heaped in each queue in the cluster at the current time.</td>
    </tr>
    <tr>
        <td>Heaped messages</td>
        <td>Count</td>
        <td>Number of unconsumed messages heaped in each queue in the cluster at the current time.</td>
    </tr>
    <tr>
        <td>Delivery throughput</td>
        <td>Bytes/s</td>
        <td>Throughput of each queue in the cluster delivering messages to the client within the selected time range (the push consumption mode refers to the `basicConsume` command).</td>
    </tr>
    <tr>
        <td>Delivery speed</td>
        <td>Count/s</td>
        <td>The speed at which each queue in the cluster delivers messages to the client within the selected time range (the push consumption mode refers to the `basicConsume` command).</td>
    </tr>
    </tbody>
</table>

## Viewing Monitoring Data

1. Log in to the [TDMQ for RabbitMQ console](https://console.cloud.tencent.com/tdmq/rabbit-cluster).
2. Select **Cluster** on the left sidebar, select a region, and click the ID of the target cluster to enter the cluster details page.
3. At the top of the cluster details page, select the **Monitoring** tab to enter the monitoring page.
4. Select the target resource and set the time range to view the corresponding monitoring data.

| Icon | Description |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| ![img](https://main.qcloudimg.com/raw/9ba57bbd3b8ef3efc4f687d63d27a46d.png) | Click it to view the comparison of monitoring metric values at different granularities or on specified dates. |
| ![img](https://main.qcloudimg.com/raw/34bdbdbdabb7b5720bf17d78c636a4ad.png) | Click it to refresh and get the latest monitoring data. You can set to automatically refresh once every 30 seconds, 5 minutes, 30 minutes, or hour. |
| ![img](https://main.qcloudimg.com/raw/8f2bf7f4df9ddd959f0ecb69fdda8e4c.png) | Click it to copy the chart to a dashboard. For more information on dashboard, see [Overview](https://intl.cloud.tencent.com/document/product/248/38461). |
| ![img](https://main.qcloudimg.com/raw/af20129df7be46f33ab7d3598f6e9213.png) | Select it to display the legend information on the chart. |

![](https://qcloudimg.tencent-cloud.cn/raw/d58e0f6cc2d82ac89104bafaaee402ce.png)

## Configuring Alarm Rule

### Creating alarm rule

You can configure alarm rules for monitoring metrics. When a monitoring metric reaches the set alarm threshold, Cloud Monitor will notify you of exceptions in time via the configured notification channel.

1. On the [Monitoring](https://console.cloud.tencent.com/tdmq/rabbit-cluster-detail) page of the cluster, click the alarm icon below to enter the [CM console](https://console.cloud.tencent.com/monitor/policylist) and configure an alarm policy.
![](https://qcloudimg.tencent-cloud.cn/raw/2f1dcf53790cb34b0de4fd75be9a544b.png)
2. On the alarm configuration page, select a policy type and instance, and set the alarm rule and notification template.
   - **Policy Type**: Select **TDMQ/RabbitMQ**.
   - **Alarm Object**: Select the RabbitMQ resource for which to configure the alarm policy.
   - Trigger Condition: You can select **Select template** or **Configure manually**. The latter is selected by default. For more information on manual configuration, see the description below. For more information on how to create a template, see [Creating trigger condition template](#model).
   <dx-alert infotype="explain" title="">
 - Metric: For example, if you select 1 minute as the statistical period for the "average production duration" metric, then if the average production duration exceeds the threshold for N consecutive data points, an alarm will be triggered.
 - Alarm Frequency: For example, "Alarm once every 30 minutes" means that there will be only one alarm triggered every 30 minutes if a metric exceeds the threshold in several consecutive statistical periods. Another alarm will be triggered only if the metric exceeds the threshold again in the next 30 minutes.
   </dx-alert>
   - **Notification Template**: You can select an existing notification template or create one to set the alarm recipient objects and receiving channels.
3. Click **Complete**.
<dx-alert infotype="explain" title="">
For more information on alarms, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
</dx-alert>


[](id:model)
### Creating trigger condition template

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Trigger Condition Template** to enter the **Template** list page.
3. Click **Create** on the **Trigger Condition Template** page.
4. On the template creation page, configure the policy type.
   - **Policy Type**: Select **TDMQ/RabbitMQ**.
   - **Use preset trigger condition**: Select this option and the system recommended alarm policy will be displayed.
5. After confirming that everything is correct, click **Save**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/3bd7aa904ee8fc5bc9818388df354f2f.png)
6. Return to alarm policy creation page and click **Refresh**. The alarm policy template just configured will be displayed.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e67712512f4ccf5a4bccfbdd93485166.png)
