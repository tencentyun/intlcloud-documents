
This document describes how to restart an instance in the console.

## Scenario
Instance restart is a common maintenance method for TencentDB for SQL Server. It is similar to restarting a local database.

## Limits
- During the restart, the TencentDB for SQL Server instance cannot provide services. Therefore, make sure that an instance has stopped accepting business requests before restarting it. During the restart, if the business write volume is high, the restart may fail.
- Restarting an instance does not change its physical attributes, so the private IP and any data stored in the instance will remain unchanged.
- After the restart, reconnection to the database is needed. Make sure your business has a reconnection mechanism.
- Restart the instance during off-peak hours to ensure success and minimize the impact on your business.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select a region at the top, select one or multiple instances to be restarted, and click **Restart** at the top.
![](https://qcloudimg.tencent-cloud.cn/raw/98457bd89cf2d8b4c957516ec0487a58.png)
3. In the pop-up window, confirm the selected instances and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/37f483c9d7205dcb3fe8c2ab57130f4a.png)
4. Once the instance status changes from **Restarting** to **Running**, the restart is completed.

