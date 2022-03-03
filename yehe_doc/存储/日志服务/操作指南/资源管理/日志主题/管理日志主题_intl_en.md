## Overview

This document describes how to add, delete, or update a log topic in the CLS console.

## Prerequisites

You have logged in to the [CLS console](https://console.cloud.tencent.com/cls).

## Directions
### Creating a log topic

1. Click **Log Topic** on the left sidebar.
2. On the log topic management page, select a region and click **Create Log Topic**.
3. In the pop-up window, enter the following information:
![](https://qcloudimg.tencent-cloud.cn/raw/a346c2b8a12e0955e6e250c918cd6513.png)
   - Log Topic Name: for example, enter `nginx`.
   > - Storage Class: `Real-time` by default. For more information about storage classes, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/614/42003).
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
After the log topic is created, you can click its ID/name on the **Log Topic** page to view its details.
![image-20210512121001919](https://main.qcloudimg.com/raw/3b708711d068dd04b6fdd8675be0bf79.png)
>?
>- You’re advised to select the same region as CVM or any other Tencent Cloud service from which you collect logs.
>- After the log topic is created, its region and logset cannot be modified.
>- Logs can be retained for 1 to 3600 days or permanently.
>

### Modifying log topic information

1. Click **Log Topic** on the left sidebar.
2 On the log topic management page, find the target log topic ID/name, and click **Edit**.
![image-20210512125731505](https://main.qcloudimg.com/raw/58b653915c64a9e931a4c05b5352516e.png)
3. In the pop-up window, modify the log topic name and the number of partitions by auto-split.
![](https://qcloudimg.tencent-cloud.cn/raw/f83dacbb7a8998301151a05757b04b5e.png)
4. Click **OK**.


### Deleting a log topic

1. Click **Log Topic** on the left sidebar.
2 On the log topic management page, find the target log topic ID/name, and click **Delete**.
![](https://main.qcloudimg.com/raw/80a3879a849e2baae3a1f481e78f0d42.png)
3. In the pop-up window, click **OK**.
<img src="https://main.qcloudimg.com/raw/c7ca5a6a30adc0340c14a4d733da8d4a.png" style="width: 65%" />
>! Once a log topic is deleted, you cannot recover its topic configuration and log data.
>
