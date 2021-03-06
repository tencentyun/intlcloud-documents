Tencent Cloud provides the Cloud Monitor service for all users by default; therefore, you do not need to manually activate it. Cloud Monitor will start collecting monitoring data only after a Tencent Cloud product is used.

## Getting Monitoring Data
### Obtaining method
The CKafka Console provides a dedicated tab for viewing monitoring data.
Monitoring data in the CKafka Console can be displayed by instance or topic. In the console, you can view monitoring data of CKafka instances and topics such as production traffic, consumption traffic, and number of retained messages. In addition, you can query the data within any custom time period. The specific steps are as follows:

1. Log in to the [CKafka Console](https://console.cloud.tencent.com/ckafka).
2. In the instance list, click **Configure Alarm** in the "Operation" column to enter the alarm configuration page. You must configure an alarm for an instance to prevent exceptions caused by traffic surges or exceeded specification threshold.
![](https://main.qcloudimg.com/raw/dc9f5683a22207babe37faca837503c5.png)
3. In the instance list, click the ID of the desired instance/topic to enter the instance details page.
4. At the top of the instance details page, click the **Monitoring of This Instance** tab to view monitoring data.


### Descriptions of CKafka monitoring metrics
Instance monitoring:

| Monitoring Metric | Description | 
|---------|---------|
| Production traffic in MB | Actual production traffic of the instance (excluding traffic generated by replicas), which is the total traffic in the selected time period. | 
| Consumption traffic in MB | Actual consumption traffic of the instance (excluding traffic generated by replicas), which is the total traffic in the selected time period. |
| Number of produced messages | Actual number of messages produced in the instance, which is the total number of messages in the selected time period. |
| Number of consumed messages | Actual number of messages consumed in the instance, which is the total number of messages in the selected time period. |
| Used disk capacity in MB | Total size of messages (including those produced by replicas) that actually use disk capacity, which is the latest value in the selected time period. |
| Number of persistent messages | Total number of actually stored messages (excluding those produced by replicas), which is the latest value in the selected time period. |
| Peak production bandwidth in MB/s | Peak traffic generated when the instance produces messages (excluding the traffic generated by replicas). |
| Peak consumption bandwidth in MB/s | Peak traffic generated when the instance consumes messages (there is no replica concept in consumption). |
| Disk utilization in % | Ratio of the currently used disk capacity to the total disk capacity of the instance in percentages. |
| Number of connections | Number of connections between client and server. |


Topic monitoring:

| Monitoring Metric | Description | 
|---------|---------|
| Production traffic in MB | Actual production traffic of the topic (excluding traffic generated by replicas), which is the total traffic in the selected time period. |
| Consumption traffic in MB | Actual consumption traffic of the topic (excluding traffic generated by replicas), which is the total traffic in the selected time period. |
| Number of produced messages | Actual number of messages produced in the topic, which is the total number of messages in the selected time period. |
| Number of consumed messages | Actual number of messages consumed in the topic, which is the total number of messages in the selected time period. |
| Used disk capacity in MB | Total size of messages in the topic (excluding those produced by replicas) that actually use disk capacity, which is the latest value in the selected time period. |
| Number of persistent messages | Total number of actually stored messages in the topic (excluding those produced by replicas), which is the latest value in the selected time period. |

Consumer group:

| Monitoring Metric | Description | 
|---------|---------|
| Current consumption offset | Current consumption offset of the consumer group. |
| Maximum offset of the current partition | Maximum offset of the current topic corresponding to the consumer group. |
| Number of unconsumed messages | Number of unconsumed messages in the consumer group. |

### CKafka monitoring API documentation
For more information on CKafka monitoring APIs, please see:
- Topic Monitoring
- Instance Monitoring
- Consumer Group Monitoring

## CKafka Alarm Policy
You can create an alarm to promptly remind yourself to take corresponding measures when the status of CKafka changes. The created alarm can determine whether an alarm notification should be sent based on the comparison between the monitored metric and the given threshold in the selected time period.
You can take appropriate precautionary or remedial measures in a timely manner when the alarm is triggered. Therefore, properly created alarms can help you improve the robustness and reliability of your applications. For more information on alarms, please see [Creating Alarms in Cloud Monitor](https://intl.cloud.tencent.com/document/product/248/38908).

## Monitoring and Alarm Policies Recommended for CKafka
For more information on metrics that may affect the business data stability, please see [CKafka Data Reliability Description](https://intl.cloud.tencent.com/document/product/597/31586).

Based on user feedback, it is recommended to configure monitoring and alarm policies in the following 3 dimensions (6 metrics in total) for CKafka, but you should configure them reasonably based on your actual business conditions.

**Instance monitoring**:

| Monitoring Metric | Description | 
|---------|---------|
| Peak production bandwidth in MB/s | Peak traffic generated when the instance produces messages (excluding the traffic generated by replicas). |
| Peak consumption bandwidth in MB/s | Peak traffic generated when the instance consumes messages (there is no replica concept in consumption). |
| Disk utilization in % | Ratio of the currently used disk capacity to the total disk capacity of the instance in percentages. |
| Number of connections | Number of connections between client and server. |

**Topic monitoring**:

| Monitoring Metric | Description | 
|---------|---------|
| Used disk capacity in MB | Total size of messages in the topic (excluding those produced by replicas) that actually use disk capacity, which is the latest value in the selected time period. |

**Consumer group**:

| Monitoring Metric | Description | 
|---------|---------|
| Number of unconsumed messages | Number of unconsumed messages in the consumer group. |
