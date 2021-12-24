
## Overview
During a migration task, you can view the migration logs to know the task progress.

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), and you can view a task in the following two ways:
 - Method 1: on the **Data Migration** page, select the target migration task and click the task name.
 - Method 2: on the **Data Migration** page, select the target migration task and click **More** > **View** in the **Operation** column.
2. View the migration logs.
   Switch the tab to view the task logs.
![](https://qcloudimg.tencent-cloud.cn/raw/90fba5ec01e9c9312a270218f4f48d66.png)

## Task Status Description

| **Status**   | **Description**                                                     |
| ---------- | ------------------------------------------------------------ |
| Configured     | The migration task configuration has been completed.                                         |
| Checking     | The migration task is being checked.                                         |
| Verification passed   | The migration task passed the verification.                                           |
| Verification failed | The migration task failed the verification.                                         |
| Preparing   | The verification has been completed, and data migration is ready to start.                                 |
| Task running   | The migration task is running.                                           |
| Prepared   | Task running is basically completed and is ready to enter the completed status.                         |
| Task successful   | The migration task is successfully completed.                                           |
| Retryable error occurred | The migration task was interrupted during migration due to an exception. You can retry and resume the task in the console. |
| Task failed   | The migration task failed.                                               |
| Terminating     | The migration task is being manually terminated during execution.     |
| Completed     | During incremental migration, **Done** is manually clicked to move the task into the **Completed** status.         |
| Task error   | During migration, the task is interrupted due to an exception and cannot be continued.     |

