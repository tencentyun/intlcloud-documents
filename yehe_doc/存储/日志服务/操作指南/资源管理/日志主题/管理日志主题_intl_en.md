## Overview

This document describes how to add, delete, or update a log topic in the CLS console.

## Prerequisite

You have logged in to the [CLS console](https://console.cloud.tencent.com/cls).

## Directions
### Creating a log topic

1. Click **Log Topic** in the left sidebar.
2. On the log topic management page, select a region, click **Create Log Topic**.
3. In the pop-up window, enter the following information:
<img src="https://main.qcloudimg.com/raw/79b2a94628f6f42e68104ccefc09a052.png" style="width: 50%" /></br>
 - Log Topic Name: for example, enter `nginx`.
 - Storage Class: `Real-time` by default. For more information about storage classes, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/614/42003).
 - Log Retention Period: 30 days by default. You can specify a log storage period, after which logs are automatically cleared. If LogListener is used, and a time field in the log content instead of the collection time is used as the logging time, the time specified by the time field will be used to determine whether a log expires.
 - Logset Operation:
    - Select an existing logset: select a target logset from the **Logset** drop-down list.
    - Create logset:
    Logset Name: for example, enter `cls_test`.
 - Advanced Settings:
    - Partitions: enter a positive integer. It defaults to 1. For more information about topic partitions, see [Topic Partition](https://intl.cloud.tencent.com/document/product/614/33779).
    - Partition Auto-Split: enabled by default.
    - Maximum Partitions: enter an integer up to 50.
    - Log Topic Tag: set a tag for the current log topic to be created so that resources can be managed by category from different dimensions.
    - Logset Tag: this field is available only when **Logset Operation** is **Create logset**. You can set a tag for the logset to be created.
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

3. In the pop-up window, modify the log topic name and the number of partitions by auto-split.

4. Click **OK**.


### Deleting a log topic

1. Click **Log Topic** in the left sidebar.
2 On the log topic management page, find the target log topic ID/name, and click **Delete**.
![](https://main.qcloudimg.com/raw/8486812ce98ed7da7005be687ba230e4.png)
3. In the pop-up window, click **Confirm**.
<img src="https://main.qcloudimg.com/raw/1ac10a1f6f8ef2129bc189eebd5d88f1.png" style="width: 65%" />

>! Once a log topic is deleted, you cannot recover its topic configuration and log data.
>
