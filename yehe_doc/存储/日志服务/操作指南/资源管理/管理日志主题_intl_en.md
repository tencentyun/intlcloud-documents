## Overview

This document describes how to add, delete, or update a log topic in the CLS console.

## Prerequisites

You have logged in to the [CLS console](https://console.cloud.tencent.com/cls).

## Directions
### Creating a log topic

1. Click **Log Topic** in the left sidebar.
2. On the log topic management page, select a region, click **Create Log Topic**.
3. In the pop-up, enter the following information:
<img src="https://main.qcloudimg.com/raw/79b2a94628f6f42e68104ccefc09a052.png" style="width: 50%" /></br>
 - Log Topic Name: for example, enter `nginx`.
 - Partitions: the default value is 1. For details about topic partitions, see [Topic Partition](https://intl.cloud.tencent.com/document/product/614/33779). 
 - Partition Auto-Split: enabled by default.
 - Maximum Partitions: you can specify the maximum number of partitions. The value is up to 50.
 - Logset Operation:
    - Select an existing logset: select a target logset from the drop-down list of the **Logset**. The log retention period is subject to the logset retention period.
    - Create logset:
      - Logset Name: for example, enter `cls_test`
      - Log Retention Period: the default value is 30
4. Click **OK**.
After a log topic is created, you can click its ID/name on the Log Topic page to view its details.
![image-20210512121001919](https://main.qcloudimg.com/raw/925a17d45f409d56b7f8d78da99bc1b1.png)

>?
>- You’re advised to select the same region as CVM or any other Tencent Cloud service from which you collect logs.
>- Once a logset is created, you cannot modify its region.
>- You can set to retain logs for 1-366 days. To retain logs for longer, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

### Modifying log topic information

1. Click **Log Topic** in the left sidebar.
2 On the log topic management page, find the target log topic ID/name, and click **Edit**.

3. In the pop-up, modify log topic name and the number of partitions by auto-split.

4. Click **OK**.


### Deleting a log topic

1. Click **Log Topic** in the left sidebar.
2 On the log topic management page, find the target log topic ID/name, and click **Delete**.
![](https://main.qcloudimg.com/raw/8486812ce98ed7da7005be687ba230e4.png)
3. In the pop-up, click **OK**.
<img src="https://main.qcloudimg.com/raw/1ac10a1f6f8ef2129bc189eebd5d88f1.png" style="width: 65%" />

>! Once a log topic is deleted, you cannot recover its topic configuration and log data.
>
