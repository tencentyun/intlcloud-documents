This document describes how to split topic partitions in the CLS console. CLS provides two operation modes: **auto-split** and **manual split**. In order to reduce the read/write restrictions due to traffic surges, we recommend that you [**enable auto-split**](#AutomaticDivision).

## Overview

When a log topic is created, an initial number of partitions is set, which can be modified subsequently through partition split or merge based on the actual needs. As a single topic partition limits write requests (up to 500 requests/sec) and write traffic (up to 5 MB/sec), if your service requests exceed the upper limit of a single partition, you can increase the throughput of the log topic by splitting the partition so as to avoid write failures.

## Directions

### Auto-split[](id:AutomaticDivision)

>?
>- After the auto-split feature is enabled, CLS will automatically split a log topic into partitions (up to 50) when the write requests or write traffic exceed the capacity of the log topic.
>- If the number of partitions of a log topic has reached the set maximum value, CLS will no longer trigger auto-split, and the excessive partitions will be rejected with an [error code](https://intl.cloud.tencent.com/document/product/614/12402) returned.

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Log Topic** to enter the log topic list page.
3. Find the target log topic and click **Edit** in the **Operation** column.
4. In the pop-up window, set **Partition Auto-Split** to ![](https://qcloudimg.tencent-cloud.cn/raw/fb0f999622a0cc536bf0e3035b7c2777.png) and set the **Maximum Partitions** (we recommend that you set it to the maximum value `50`).
6. Click **OK**.

### Manual split

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Log Topic** to enter the log topic list page.
3. Find the target log topic and click its ID/name to enter the **Basic Info** page.
4. In the **Topic Partition Management** section, find the target topic partition and click **Edit**.
5. In the pop-up window, select **Split** as the **Operation** and set the **Partition Quantity** as shown below:
<dx-alert infotype="explain" title="">
Each partition has a left-closed-right-open range. Even split is used by default.
</dx-alert>

6. Click **OK**.

