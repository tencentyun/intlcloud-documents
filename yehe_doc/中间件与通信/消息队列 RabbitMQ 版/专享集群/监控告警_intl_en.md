## Overview

TDMQ for RabbitMQ exclusive cluster supports monitoring resources created under your account, including clusters and nodes. You can analyze the cluster usage based on the monitoring data and handle possible risks promptly. You can also set alarm rules for monitoring metrics to receive alarm messages when metrics are abnormal. This helps you deal with risks in time and ensure the stable operations of your system.

## Monitoring Metrics

TDMQ for RabbitMQ exclusive cluster supports the following monitoring metrics at **cluster** and **node** levels:


| Monitoring Metric | Unit | Description |
| ------------------ | ------- | ------------------------------------------------------------ |
| Connections           | -   | The number of currently open connections                                           |
| Channels           | -   | The number of currently open channels                                         |
| Queues           | -   | The number of currently available queues                                             |
| Consumers         | -   | The number of currently online consumers                                           |
| Heaped messages       | -   | The number of ready (heaped but not delivered) messages                              |
| Unacknowledged messages | -   | The number of delivered but not acknowledged messages                             |
| Message drop rate | Count/s | The rate of message drop caused by the lack of eligible routing conditions when messages are sent to the exchange in case of `mandatory=false` |
| Production acknowledgment rate | Count/s | The rate of acknowledgment packet return by the broker after the client successfully produces messages |
| Messages produced per second | Count/s | The rate of message production by the client |
| Consumption acknowledgment rate | Count/s | The rate of message acknowledgment by the consumer |
| Messages consumed per second | Count/s | The rate of message consumption per second, including values in case of `autoAck=false` and `autoAck=true` |
| Redelivery rate | Count/s | The rate of message redelivery to consumers in the channel |



## Viewing Monitoring Data

1. Log in to the [TDMQ for RabbitMQ console](https://console.cloud.tencent.com/tdmq/rabbit-cluster).
2. Select **Cluster** on the left sidebar, select a region, switch to the **Exclusive Cluster** tab, and click the ID of the target cluster to enter the cluster details page.
3. At the top of the cluster details page, select the **Monitoring** tab to enter the monitoring page.
4. Select the target resource and set the time range to view the corresponding monitoring data.

| Icon | Description |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| ![img](https://main.qcloudimg.com/raw/9ba57bbd3b8ef3efc4f687d63d27a46d.png) | Click it to view the comparison of monitoring metric values at different granularities or on specified dates. |
| ![img](https://main.qcloudimg.com/raw/34bdbdbdabb7b5720bf17d78c636a4ad.png) | Click it to refresh and get the latest monitoring data. You can set to automatically refresh once every 30 seconds, 5 minutes, 30 minutes, or hour. |
| ![img](https://main.qcloudimg.com/raw/8f2bf7f4df9ddd959f0ecb69fdda8e4c.png) | Click it to copy the chart to a dashboard. For more information on dashboard, see [Dashboard Overview](https://intl.cloud.tencent.com/document/product/248/38461). |
| ![img](https://main.qcloudimg.com/raw/af20129df7be46f33ab7d3598f6e9213.png) | Select it to display the legend information on the chart. |

![](https://qcloudimg.tencent-cloud.cn/raw/a44a98d3a9597093569aef198ad106b9.png)

## Configuring an Alarm Rule

### Creating an alarm rule

You can configure alarm rules for monitoring metrics. When a monitoring metric reaches the set alarm threshold, Cloud Monitor will notify you of exceptions in time via the configured notification channel.

1. On the [Monitoring](https://console.cloud.tencent.com/tdmq/rabbit-cluster-detail) page of the cluster, click the alarm icon below to enter the [CM console](https://console.cloud.tencent.com/monitor/policylist) and configure an alarm policy.
   ![](https://qcloudimg.tencent-cloud.cn/raw/4db136f8dc334d12aeacd62de71bd06d.png)

2. On the alarm configuration page, select a policy type and instance, and set the alarm rule and notification template.
   - **Policy Type**: Select **TDMQ/RabbitMQ**.
   - **Alarm Object**: Select the RabbitMQ resource for which to configure the alarm policy.
   - Trigger Condition: You can select **Select template** or **Configure manually**. The latter is selected by default. For more information on manual configuration, see the description below. For more information on how to create a template, see [Creating a trigger condition template](#model).
     <dx-alert infotype="explain" title="">

 - Metric: For example, if you select 1 minute as the statistical period for the "connections" metric, then if the average production duration exceeds the threshold for N consecutive data points, an alarm will be triggered.
 - Alarm Frequency: For example, "Alarm once every 30 minutes" means that there will be only one alarm triggered every 30 minutes if a metric exceeds the threshold in several consecutive statistical periods. Another alarm will be triggered only if the metric exceeds the threshold again in the next 30 minutes.
   </dx-alert>
   - **Notification Template**: You can select an existing notification template or create one to set the alarm recipient objects and receiving channels.

3. Click **Complete**.
   <dx-alert infotype="explain" title="">
   For more information on alarms, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
   </dx-alert>


[](id:model)

### Creating a trigger condition template

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Trigger Condition Template** to enter the **Template** list page.
3. Click **Create** on the **Trigger Condition Template** page.
4. On the template creation page, configure the policy type.
   - **Policy Type**: Select **TDMQ/RabbitMQ**.
   - **Use preset trigger condition**: Select this option and the system recommended alarm policy will be displayed.
5. After confirming that everything is correct, click **Save**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/07dcc7044fde9e78d9dd035f93d8304f.png)
6. Return to alarm policy creation page and click **Refresh**. The alarm policy template just configured will be displayed.
   ![](https://qcloudimg.tencent-cloud.cn/raw/a095c0b7ed7fbd9f89e048fc8517e329.png)
