## Overview

In task details, you can view various information, such as sync task, sync configuration, structure initialization, data initialization, and monitoring data.

## Prerequisites
You have successfully created a data sync task and logged in to the [DTS console](https://console.cloud.tencent.com/dts/replication).

## Directions
- Method 1: in the [data sync](https://console.cloud.tencent.com/dts/replication) task list, select the target sync task and click its name.
- Method 2: in the [data sync](https://console.cloud.tencent.com/dts/replication) task list, select the target sync task and click **View** in the **Operation** column.

### Sync task page
It displays the information of the task, source database, and target database.
![](https://qcloudimg.tencent-cloud.cn/raw/1b9c5f80502aafacfb6abf214e248b29.png)

### Sync configuration page
It displays the sync task configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/37044c19f87ec1aaedc183de3398f36f.png)

### Structure initialization page
If you select **Structure Initialization** in the sync configuration, relevant information will be displayed on this page.

| Parameter   | Description                                             |
| ------ | ------------------------------------------------ |
| Object Name | Table name in the target database.                               |
| Source Database   | Name of the source database object, such as database and table.               |
| Target Database | Name of the target database object, such as database and table.           |
| Status   | Current status. If the task fails, the failure reason will be displayed.             |
| Operation   | Click **View Creation Statement** to view the creation syntax executed in the target database. |

![](https://qcloudimg.tencent-cloud.cn/raw/c6771f7eb82a16a24da4ef3d2b6055ad.png)

### Task initialization page
If you select **Data Initialization** in the sync configuration, relevant information will be displayed on this page.
>?If the task fails, you can click **View Failure Details** to troubleshoot.
>
![](https://qcloudimg.tencent-cloud.cn/raw/253e5bb2692158df8b5ce7f84c823e89.png)

### Monitoring data display
"-" will be displayed by default if no monitoring data is collected.
![](https://qcloudimg.tencent-cloud.cn/raw/1ed0cb1972cf91aa07b9c64a3c73f45c.png)

