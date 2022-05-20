## Overview

This document describes how to view the details of a producer connected to a topic in the TDMQ for Pulsar console, so that you can stay up to date with the status of the connected producer and troubleshoot problems promptly.

## Directions

1. Log in to the [TDMQ for Pulsar console](https://console.intl.cloud.tencent.com/tdmq) and click **Topic Management** on the left sidebar.
2. On the **Topic Management** list page, click **View Producer** in the **Operation** column of the target topic to enter the producer list.
![](https://qcloudimg.tencent-cloud.cn/raw/9b83daa89ea1539262708571a28afbe1.png)

**Producer overview**
- Current Production TPS: Total number of messages produced by producers currently connected to the topic per second.
- Current Production Throughput: Size of messages produced by producers currently connected to the topic per second.
- Current Producers: Total number of producers currently connected to the topic (the listed items are combinations of producers and partitions; therefore, if there are multiple AZs, the number of producers displayed on the overview page will be less than the number of listed items).
- Current Message Storage Size: Total size of messages currently stored in the topic memory.

**Producer details**
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>Producer ID	</td>
<td>Producer ID.</td>
</tr>
<tr>
<td>Producer Name	</td>
<td>Message producer name.</td>
</tr>
<tr>
<td>Producer Address</td>
<td>Message producer address and port.</td>
</tr>
<tr>
<td>Client Version</td>
<td>Pulsar client version.</td>
</tr>
<tr>
<td>Message Production Rate (Messages/Sec)</td>
<td>Number of messages produced by producers to the topic per second.</td>
</tr>
<tr>
<td>Message Production Throughput (Mbps)</td>
<td>Size of messages produced by producers per second.</td>
</tr>
<tr>
<td>Avg Message Size (Bytes)</td>
<td>Average size of messages produced by producers to the topic.</td>
</tr>
</table>




