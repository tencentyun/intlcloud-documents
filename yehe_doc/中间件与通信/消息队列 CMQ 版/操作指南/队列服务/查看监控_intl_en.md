## Overview

This document describes how to view the details of a created queue in the TDMQ for CMQ console.

## Directions

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Queue Service** on the left sidebar, select the **region**, and click the ID of the target queue to enter the queue details page.
3. On the queue details page, select the **Monitoring** tab at the top and select a time range to view the monitoring data of the queue.

Description of monitoring metrics:

| Monitoring Metric | Description |
| -------------------- | ------------------------------------------------------------ |
| Production rate (messages/sec) | Number of messages produced by all producers under the **queue** per second in the selected time range |
| Consumption rate (messages/sec) | Number of messages consumed by all consumers under the **queue** per second in the selected time range |
| Production traffic (bytes/sec) | Data size of messages produced by all producers under the **queue** per second in the selected time range |
| Consumption traffic (bytes/sec) | Data size of messages consumed by all consumers under the **queue** per second in the selected time range |
| Total message size (in bytes) | Total data size of current messages |
| Average message size (in bytes) | Average data size of current messages |
| Total number of messages | Total number of current messages |
| Number of producers	 | Number of producers connected to the queue |
| Number of subscribers	 | Number of consumers connected to the queue |

![](https://main.qcloudimg.com/raw/aafd54c1328c3ad12f51b91504907af5.png)
