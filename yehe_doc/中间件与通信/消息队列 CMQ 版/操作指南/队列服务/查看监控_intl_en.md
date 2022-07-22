## Overview

This document describes how to view monitoring data in the TDMQ for CMQ console.

## Directions

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Queue Service** on the left sidebar, select a **Region**, and click the ID of the target queue to enter the queue details page.
3. On the queue details page, select the **Monitoring** tab at the top and select a time range to view the monitoring data of the queue.
![](https://qcloudimg.tencent-cloud.cn/raw/d0926e1e95751885d8a0d475ec6b06e1.png)
#### Monitoring metric description
<table>
    <thead>
    <tr>
        <th>Monitoring Metric</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Heaped Messages</td>
        <td>`Activemessages`, which indicates the total number of messages that are in “Active” status in the queue in the selected time range. The metric value is approximate.</td>
    </tr>
    <tr>
        <td>Invisible Messages</td>
        <td>A message will be made invisible (in “Inactive” status) after being fetched by the consumer. It will become visible (in “Active” status) again if it is not consumed after the `VisibilityTimeout`.</td>
    </tr>
    <tr>
        <td>Production Speed (messages/sec)</td>
        <td>The number of messages produced by all producers in the queue per second in the selected time range.</td>
    </tr>
    <tr>
        <td>Consumption Speed (messages/sec)</td>
        <td>The number of messages consumed by all consumers in the queue per second in the selected time range.</td>
    </tr>
    <tr>
        <td>Production Traffic (Byte/sec)</td>
        <td>The size of messages produced by all producers in the queue per second in the selected time range.</td>
    </tr>
    <tr>
        <td>Consumption Traffic (Byte/sec)</td>
        <td>The size of messages consumed by all consumers in the queue per second in the selected time range.</td>
    </tr>
    <tr>
        <td>Total Message Size (Byte)</td>
        <td>The total size of all messages in the queue.</td>
    </tr>
    <tr>
        <td>Avg Message Size (Byte)</td>
        <td>The average size of all messages in the queue.</td>
    </tr>
    <tr>
        <td>Total Messages</td>
        <td>The total number of messages in the queue.</td>
    </tr>
    </tbody>
</table>


