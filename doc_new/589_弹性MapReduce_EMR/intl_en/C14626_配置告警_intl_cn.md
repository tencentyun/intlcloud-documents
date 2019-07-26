## Application Scenario
Tencent Cloud Monitor provides a rich set of alarming services for EMR. You can create alarm policies for servers and cluster in the Cloud Monitor Console.

## Directions
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/policylist) and click **Create** on the **Alarm Policy** page in the left sidebar.
![](https://main.qcloudimg.com/raw/72a808c0b8066c398955593fd9e8d419.png)
2. Configure policy information and select **EMR policy**as the policy type.
EMR supports two types of alarm: Server Alarm and Cluster Alarms. Server Alarm includes both metric alarm and event alarm; Cluster Alarm includes only metric alarm.
 - Choose Server Alarm if you want to monitor the status of the hardware on each node, such as CPU utilization, memory usage, and pingability.
 - Choose Cluster Alarm If you want to monitor your cluster’s performance. The monitoring metrics include HDFS storage capacity, number of YARN application blocks and number of failures.

 ![](https://main.qcloudimg.com/raw/0af59225cdfc8a9f8b08b8ed12cdf250.png)


