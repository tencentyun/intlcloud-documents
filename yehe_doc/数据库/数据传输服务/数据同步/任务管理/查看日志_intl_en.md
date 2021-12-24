
## Overview
During a sync task, you can view the sync task logs to know the task progress.

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), and you can view a task in the following two ways:
 - Method 1: on the **Data Sync** page, select the target sync task and click the task name.
 - Method 2: on the **Data Sync** page, select the target sync task and click **More** > **View** in the **Operation** column.
2. View the sync logs.
Switch the tab to view the task logs.
<img src="https://qcloudimg.tencent-cloud.cn/raw/405e65ba82ea1f729cbb8ecab2bd5a4c.png" style="zoom:67%;" />

## Task Status Description

| **Status**   | **Description**                                                     |
| ---------- | ------------------------------------------------------------ |
| Uninitialized   | The purchase has been completed, but no sync task has been configured.                               |
| Initialized   | The sync task has been configured.                                         |
| Checking     | The sync task is being checked.                                         |
| Verification passed   | The sync task passed the verification.                                           |
| Verification failed | The sync task failed the verification.                                         |
| Preparing   | The sync task is ready to start.                                           |
| Task running   | The sync task is running.                                             |
| Retryable error occurred | The sync task was interrupted during sync due to an exception. You can retry and resume the task in the console. |
| Stopping     | The sync task is being manually stopped during execution.     |
| Completed     | The task is stopped.                                               |
| Task failed   | The sync task failed.                                               |
| Deleting     | The task is being deleted. You can manually delete a task that is completed, failed, or no longer needed. |
| Deleted     | The task is deleted. Once deleted, it will no longer exist or occupy any resources.         |

