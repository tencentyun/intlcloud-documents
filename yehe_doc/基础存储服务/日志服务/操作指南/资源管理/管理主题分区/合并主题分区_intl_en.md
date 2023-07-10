## Overview

This document describes how to merge topic partitions in the CLS console. By merging partitions in the adjacent range, the number of topic partitions can be reduced to avoid resource waste.

## Notes

- Each log topic has at least one partition. If you only have one partition, you cannot merge it.
- Only one object adjacent to the specified topic partition can be merged at a time.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Logset** to enter the logset management page.
3. Find the logset where you want to merge topic partitions and click its ID/name to enter the logset information page.
4. In the **Log Topic** column, click the name of the log topic to enter its basic information page.
5. In the **Topic Partition Management** column, find the target topic partition to be merged and click **Edit** as shown below:
6. In the pop-up dialog box, select **Merge** as the **Operation** and select the object to be merged as shown below:
7. Click **OK** to complete merge.

