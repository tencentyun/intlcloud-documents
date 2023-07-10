## Overview

CLS manages the log data stored on it in the form of log topics and logsets. A log topic is the basic unit for log data collection, storage, search, and analysis, and a logset is used to categorize log topics for easier management.

This document describes how to manage log topics in the console. We recommend you read [Log Topic and Logset](https://intl.cloud.tencent.com/document/product/614/32849) first to learn more about concepts and use cases.

## Prerequisites

You have logged in to the [CLS console](https://console.cloud.tencent.com/cls).

## Directions

### Creating a log topic

1. Click **Log Topic** on the left sidebar.
2. On the log topic management page, select a region and click **Create Log Topic**.
3. In the pop-up window, enter the following information:

   - Log Topic Name: For example, enter `nginx`.
   - Storage Class: STANDARD by default. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/614/42003).
   - Log Retention Period: 30 days by default. You can specify a log storage period, after which logs are automatically cleared. If LogListener is used, and a time field in the log content instead of the collection time is used as the logging time, the time specified by the time field will be used to determine whether a log expires.
   - Logset Operation:
      - Select an existing logset: select a target logset from the **Logset** drop-down list.
      - Create logset:
       Logset Name: for example, enter `cls_test`.
   - Log Topic Tag: set a tag for the current log topic to be created so that resources can be managed by category from different dimensions.
   - Advanced settings:
      - Partitions: Enter a positive integer. It defaults to `1`. For more information on topic partitions, see [Topic Partition](https://intl.cloud.tencent.com/document/product/614/33779).
      - Partition Auto-Split: Enabled by default.
      - Maximum Partitions: Enter an integer up to 50.
      - Logset Tag: this field is available only when **Logset Operation** is **Create logset**. You can set a tag for the logset to be created.
4. Click **OK**.
After the log topic is created, you can click its ID/name on the **Log Topic** page to view its details.

>?
>- You’re advised to select the same region as CVM or any other Tencent Cloud service from which you collect logs.
>- After the log topic is created, its region and logset cannot be modified.
>- Logs can be retained for 1 to 3600 days or permanently.


### Editing log topic

1. Click **Log Topic** on the left sidebar.
2. On the log topic management page, find the target log topic ID/name and click **Edit**.

3. In the pop-up window, modify the basic information of the log topic.

4. Click **OK**.


### Deleting a log topic

1. Click **Log Topic** on the left sidebar.
2 On the log topic management page, find the target log topic ID/name, and click **Delete**.

>? You can switch to different regions in the top-left corner of the page to delete log topics accordingly. To delete all log topics, we recommend you use an account with permissions of all resources; otherwise, some log topics may not be deleted as you don't have permissions to view them.
>
3. In the pop-up window, click **OK**.
>! Once a log topic is deleted, you cannot recover its topic configuration and log data. Proceed with caution.
>



