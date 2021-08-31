This document describes how to terminate a TencentDB for Tendis instance in the console.

## Overview
Based on your business needs, you can return pay-as-you-go instances in the console in a self-service manner.
- After a pay-as-you-go instance is returned, it will be moved to the TencentDB recycle bin and retained there for 24 hours. During the retention period, the instance cannot be accessed but can be restored after startup.

When an instance is returned and its status has changed to **Isolated**, it will no longer generate fees.
>!
>- After the instance is terminated, its data cannot be recovered, and its backup files will also be terminated, so the data cannot be restored in the cloud. Please store your backup files safely elsewhere in advance.
>- When an instance is terminated, its IP address will be released.


## Directions
1. Log in to the [TencentDB for Tendis console](https://console.cloud.tencent.com/tendis). In the instance list, select a region at the top, locate the desired instance, and click **More** > **Terminate** in the **Operation** column.

>
![](https://main.qcloudimg.com/raw/17be53dac17e4c5dc2170627537d3ed4.png)
2. In the pop-up dialog box, confirm that everything is correct and click **Terminate**.
>!Note that all data will be cleared and cannot be recovered after termination.
>

