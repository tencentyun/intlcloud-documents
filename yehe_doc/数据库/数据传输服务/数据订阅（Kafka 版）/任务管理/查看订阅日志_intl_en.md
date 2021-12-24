
## Overview
During a subscription task, you can view its logs to know the task progress.

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration)and select **Data Subscription** on the left sidebar to enter the data subscription page.
   - Method 1: select the target subscription task and click its name.
   - Method 2: select the target subscription task and click **View Subscription Details** in the **Operation** column.
     ![](https://qcloudimg.tencent-cloud.cn/raw/1bf25aa341f6f7db0630c90a31e36669.png)
2. Switch between different tabs to view the task logs.
<img src="https://qcloudimg.tencent-cloud.cn/raw/865915e3ac57221c583c30ca249e81f9.png" style="zoom:67%;" />

## Task Status Description

| **Status**   | **Description**                         |
| ---------- | -------------------------------- |
| Not started     | The purchase has been completed, but no subscription task has been configured.   |
| Checking     | The subscription task is being checked.             |
| Verification passed   | The subscription task passed the verification.                                           |
| Verification failed | The subscription task failed the verification.                                         |
| Enabling     | The subscription task is ready to run.               |
| Task running   | The subscription task is running.                 |
| Stopping     | The subscription task is being stopped when a subscription object is reset. |
| Task error   | The subscription task is interrupted due to an error.     |

