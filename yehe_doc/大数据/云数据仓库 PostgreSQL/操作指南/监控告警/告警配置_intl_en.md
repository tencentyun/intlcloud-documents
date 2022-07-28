## Background
CDWPG provides a performance monitoring dashboard where you can observe the historical and current status of the operational metrics of each node in the cluster. It also offers the alarm notification feature to keep you informed of sensitive metrics that exceed thresholds, such as the node disk usage.

## Performance Monitoring
Log in to the [CDWPG console](https://console.cloud.tencent.com/snova) and click a cluster name in the cluster list to enter the cluster details page. On the **Performance Monitoring** tab, you can view cluster metrics. If there are multiple nodes, you can select the target node in **Node Dimension**.

Currently, CDWPG metrics include the number of connections, CPU utilization, memory utilization, inbound network throughput, outbound network throughput, write IOPS, read IOPS, disk utilization, read throughput, write throughput, read latency, and write latency.

## Alarm Access
CDWPG has three types of alarms, namely cluster monitoring, primary node monitoring, and compute node monitoring. These monitoring alarms are sent to users in three dimensions.

### Creating alarm policy
Log in to the [CM console](https://console.cloud.tencent.com/monitor/overview), select **Alarm Management > Alarm Configuration > Alarm Policy**, and click **Create** to create an alarm policy. When creating the alarm policy, you can select **CDWPG - cluster monitoring**, **CDWPG - master node monitoring**, or **CDWPG - compute node monitoring** as the **Policy Type**. This document takes compute node monitoring as an example.
1. Select **CDWPG - compute node monitoring` in the **Policy Type drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/90a86a431b8549d8bb8881570e874d49.png)
2. Set **Alarm Object** and select different groups of compute nodes in the drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/bb1c82be43f29ffa8501b15cb249a6ed.png)
3. Configure **Trigger Condition**, which can be **Select template** or **Configure manually**.
 - If you select **Select template**, you can click **Add Trigger Conditions** to configure an alarm threshold for each metric. Once a metric exceeds the threshold, the system will send you an alarm message. You can also click **Modify Template** to modify an existing template.
 - If you select **Configure manually**, you can add other metrics that you care about. Set thresholds for such metrics to configure their alarming thresholds and notification periods.
![](https://qcloudimg.tencent-cloud.cn/raw/8c3eca7d1c5caf91d4f77a43749451ab.png)
4. To configure **Notification Template**, click **Select template** and select an existing template, or click **Create template** to create a notification template.
![](https://qcloudimg.tencent-cloud.cn/raw/1ce8c8a437903770c69028679cbeb715.png)
When creating a notification template, set **Recipient** to the development and operations personnel who are interested in alarming or need to handle the alarms. You can choose to notify them by email, SMS, or WeChat.
![](https://qcloudimg.tencent-cloud.cn/raw/b92fcdfce05d88474377a40a6c1aefb2.png)
