## Overview

TDMQ for Pulsar allows you to monitor the topic resources created under your account, so that you can keep track of the status of your topics in real time and troubleshoot possible issues to ensure stable business operations.

This document describes how to view monitoring metrics and their descriptions in the TDMQ console.

## Directions

1. Log in to the [TDMQ for Pulsar console](https://console.intl.cloud.tencent.com/tdmq).
2. On the left sidebar, click **Topic Management** and select the region, cluster, and namespace.
3. In the topic list, find the target topic, click ![](https://qcloudimg.tencent-cloud.cn/raw/ac572a960433508f64f226e6ea218c10.png) in the **Monitoring** column, select the time range and granularity, and you can view the topic monitoring data.

**Monitoring information display**
![](https://qcloudimg.tencent-cloud.cn/raw/3d9feea91eb5c2e8c17251412c0d6642.png)

**Descriptions of monitoring metrics**
<table>
<tr>
<th>Metric</th>
<th>Description</th>
</tr>
<tr>
<td>Production Speed (Messages/Sec)	</td>
<td>Number of messages sent to the topic by producers per second in the selected time range.</td>
</tr>
<tr>
<td>Consumption Speed (Messages/Sec)	</td>
<td>Number of messages consumed by all consumers under the topic per second in the selected time range.</td>
</tr>
<tr>
<td>Production Traffic (Byte/sec)</td>
<td>Data size of messages sent to the topic by producers per second in the selected time range.</td>
</tr>
<tr>
<td>Consumption Traffic (Byte/sec)</td>
<td>Data size of messages consumed by all consumers under the topic per second in the selected time range.</td>
</tr>
<tr>
<td>Total Message Size (Byte)</td>
<td>Size of heaped messages.</td>
</tr>
<tr>
<td>Avg Message Size (Byte)</td>
<td>Average size of produced messages.</td>
</tr>
<tr>
<td>Total Messages</td>
<td>Total number of produced messages.</td>
</tr>
<tr>
<td>Producer Count</td>
<td>Number of producers producing messages to the topic.</td>
</tr>
<tr>
<td>Subscriber Count</td>
<td>Number of subscribers to the topic.</td>
</tr>
</table>


