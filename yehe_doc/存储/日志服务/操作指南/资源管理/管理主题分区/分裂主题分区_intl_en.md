This document describes how to split topic partitions in the CLS console. CLS provides two operation modes: **auto-split** and **manual split**. In order to reduce the read/write restrictions due to traffic surges, we recommend you **[enable auto-split](#AutomaticDivision)**.



## Overview

When a log topic is created, an initial number of partitions is set, which can be modified subsequently through partition split or merge based on the actual needs. As a single topic partition limits write requests (up to 500 requests/sec) and write traffic (up to 5 MB/sec), if your service requests exceed the upper limit of a single partition, you can increase the throughput of the log topic by splitting the partition so as to avoid write failures.



## Directions


<span id="AutomaticDivision"></span>
### Auto-split

>? After the auto-split feature is enabled, if a topic partition keeps reaching the threshold of write requests or write traffic, CLS will automatically split it into a reasonable number of partitions (up to 50) based on the actual write conditions.
> If the number of partitions of a log topic has reached the set maximum value, CLS will no longer trigger auto-split, and the excessive part will be rejected with an [error code](https://intl.cloud.tencent.com/document/product/614/12402) returned.


1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Logset** to enter the logset management page.
3. Find the logset where you want to split topic partitions and click its ID/name to enter the logset information page.
4. In the **Log Topic** column, click the name of the log topic to enter its basic information page.
5. In the **Basic Info** column, click **Edit** as shown below:
6. In the pop-up dialog box, set **Partition Auto-Split** to <img src="https://main.qcloudimg.com/raw/9f9b4e34aa0b31639346223f9c853bad.png"/> and set the **Maximum Partitions** as shown below:
7. Click **OK** to complete partition auto-split.

### Manual split
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Logset** to enter the logset management page.
3. Find the logset where you want to split topic partitions and click its ID/name to enter the logset information page.
4. In the **Log Topic** column, click the name of the log topic to enter its basic information page.
5. In the **Topic Partition Management** column, find the target topic partition to be split and click **Edit** as shown below:
6. In the pop-up dialog box, select **Split** as the **Operation** and set the **Partition Quantity** as shown below:
<dx-alert infotype="explain" title=""> 
Each partition has a left-closed, right-open range. Even split is used by default.
</dx-alert>
7. Click **OK** to complete split.

