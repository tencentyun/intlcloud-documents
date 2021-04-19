## Overview

This document describes how to view the consumer group information of an instance in the CKafka console.

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, click the **Consumer Group** tab to view the consumer group information of the current CKafka instance.
![](https://main.qcloudimg.com/raw/9ba5455a279dc734c4120ae8eb6d2519.png)
	- On the consumer group list page, click **View consumer details** in the **Operation** column to view the information of consumers in the consumer group and the relationship between a consumer and the topic subscribed to by this consumer.
	- On the consumer group list page, click the small triangle on the left of the consumer group name to display the information of the topic subscribed to by this consumer group, including topic name, number of partitions, submitted offset position, maximum offset position, and number of unconsumed messages. Click **View partition details** in the **Operation** column to view offset consumption at the partition level.
 >?As the offset information is maintained on the consumer side, the offset position is subject to the way the consumer submits the offset. It is displayed asynchronously and does not necessarily represent real-time consumption conditions.
